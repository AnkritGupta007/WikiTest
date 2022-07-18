# Summary
This wiki page will explain a fix to get around the `Filename too long` error, which involves adding a permanent `robocopy node_clobber node_modules` and a one-time change of  `GIT_CLEAN_FLAGS: none`. We are investigating a preventative solution for this problem for the future.


## Problem description: 
When working on a project making use of NPM, an error similar to the following might be encountered when pushing a commit with test scripts enabled to gitlab:
```console
Running with gitlab-runner 11.10.1 (1f513601)
  on it-gitlab-ci1 41a54163
Using Shell executor...
Running on IT-GITLAB-CI1...
Reinitialized existing Git repository in D:/Multi-Runner-PRD/builds/41a54163/0/IT-AppDevelopment/Templates/WebApi-Angular-Application-Template/.git/
Fetching changes...
From https://code.cmich.edu/IT-AppDevelopment/Templates/WebApi-Angular-Application-Template
   b885ef9..fd69f9f  fix-3828557 -> origin/fix-3828557
Checking out fd69f9f2 as fix-3828557...
warning: Could not stat path 'Web.Ui/node_modules/.staging/@angular/material-396ac2a0/schematics/address-form/files/__path__/__name@dasherize@if-flat__/__name@dasherize__.component.spec.ts': Filename too long
warning: Could not stat path 'Web.Ui/node_modules/.staging/@angular/material-396ac2a0/schematics/dashboard/files/__path__/__name@dasherize@if-flat__/__name@dasherize__.component.__styleext__': Filename too long
ERROR: Job failed: exit status 1
```
This is caused by the `node_modules` directory caching too long of a filename. While the _exact_ fix will differ depending on what stages are included in your `gitlab-ci.yml` file, the general step-by-step instructions for  the fix are as follows:
1.  In whatever script runs `npm install`, replace the npm-related code in the standard script with a before_script similar to the following:
    ```yml
    before_script:
      # before_script handles Client-Side UI concerns
      - 'echo off'
      - 'call "%VS140COMNTOOLS%\vsvars32.bat"' # we added this in because it was part of the global script
      - cd .\Web.Ui
      - echo 'Clobbering Node Modules directory...'
      - mkdir node_clobber
      - powershell -noprofile -command "&{ $tries=0; do { $tries++; robocopy node_clobber node_modules /s /mir /r:2; if ($lastexitcode -le 1) { exit 0; } } While ($lastexitcode -le 2 -and $tries -lt 10); exit $lastexitcode;}"
      - rmdir node_clobber
      - rmdir node_modules
      - echo 'Restoring NPM Packages'
      - where git.exe
      - call npm install --force
      - call npm run dist
      - cd ..\
    ```
    This clobbers the broken node_modules directory and restores it correctly, fixing the broken state. (Any lines in your global before script that the stage in question uses also need to be copied in, as this script will *override* that script rather than add to it. In this case That's the `- 'call "%VS140COMNTOOLS%\vsvars32.bat"'` line, which isn't used to fix the state in question but *is* used in the script tag not shown.)
2.  Add the following line to your variables, generally at the very top of the YAML script: `GIT_CLEAN_FLAGS: none`. This turns off the broken git clean operation, allowing the pipeline to reach the script you just created and fix the broken state; without this line the build will fail before the script to fix it has a chance to run.
3.  Commit this change and push it to Gitlab, so it can fix the broken environment in question. An example commit that fixed the problem can be seen in IT-AppDevelopment/Templates/WebApi-Angular-Application-Template@c2ea06d1 for reference.
4.  Remove the `GIT_CLEAN_FLAGS: none` line now that the problem is fixed. (Keep the node_clobber script; it might add a bit of extra time to the build, but it's necessary to keep the problem from recurring.) Commit the change and push it to the remote repository again.
5.  That's it! Other issues may pop up related to the clobbering of node_modules, depending on the stages configured for the project in question; adding or removing a cache may help keep the environment in the correct state, but attempting to exhaustively document all possible configurations and fixes to each is well outside of the scope of this page. Please add any new issues and fixes as they occur.

## Tags
[[Git]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=GitTag)