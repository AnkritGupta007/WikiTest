# Summary
This documents explain the details of how to build and run a CMich Web App based on the [Enterprise Angular 2 Template](https://code.cmich.edu/IT-AppDevelopment/Templates/Enterpise-ActiveDirectory-Angular2).

## Requirments to run locally


### Node and NPM
* Must have recent version of Node.js installed (to test, run CMD `node -v`)
   * (https://nodejs.org/en/) - we strongly recommend *LTS Version: 10.x.x* 
* When installing fresh, make sure to install the Windows Build tools. If upgrading from an earlier version, you may also need to run `npm install --global --production windows-build-tools`
* To build and run project
  * Restore NuGet Packages on Solution
  * In Web.Ui project, open command prompt 
    * Type `npm install` (This will build your node_modules folder and get all your dependencies and typings)
      * You can ignore the audit package vulnerabilities. Unnecessary upgrades could break your build.
    * Type `npm run dist` (This pull all the files needed for distribution, including goodies like font awesome icons)
	* Type `npm run serve` (This will compile Angular code.  Use instead of ng serve as it moves code to web project)
  * At this point, you should be able to build and debug project
  * To start up Jest for TDD, again open command prompt in Web.Ui and type `npm run testify` (use instead of ng test, as it adds in code coverage and sets source maps to false for easier to understand errors)
  * To build for production, open command prompt in Angular project and type `npm run dist:prod`

### Typescript for Visual Studio
* To build and run project in Visual Studio 2017 you must install [Visual Studio 2017 Extension TS SDK Compiler](https://www.microsoft.com/en-us/download/details.aspx?id=55258)
     * [TypeScript 2.3.3 — May 22, 2017](http://download.microsoft.com/download/7/0/A/70A6AC0E-8934-4396-A43E-445059F430EA/2.3.3-TS-release-dev14update3-20170519.1/TypeScript_SDK.exe)
     * Restart Visual Studio

# Angular CLI
* You can add new components and services programmatically with Angular CLI.  Open command prompt in .Angular project and type....
	* To generate service `ng generate service services/YourServiceName`
	* To generate component `ng generate component components/YourComponentName`
	* This will generate .ts and .spec.ts files for you in both cases.  For components, it will also generate html and css files.
	* Full docs at : https://cli.angular.io/
    * Best practices (i.e., Style Guide): https://angular.io/guide/styleguide

# Practical Step by Step Guide for Getting Started
In this example we will be renaming the template to be an app called **AdminRegistration**.
We will then get it functional, and finally save it back to a gitlab repo (to get you on the right path to [commit early and commit often](http://www.databasically.com/2011/03/14/git-commit-early-commit-often/)

## Confirm Node Version
* In command prompt `node -v`
* If below `v6.0.0` install more recent version of Node.js (https://nodejs.org/en/) - we recommend *LTS Version: 8.11.3*
* Run `npm rebuild node-sass --force -g` to rebind node-sass to the new version (if you have issues see [further reading](https://stackoverflow.com/a/46857429/3018212))

## Clone and Setup Clean, Functional Project
* From the command prompt in your desired directory`git clone https://code.cmich.edu/IT-AppDevelopment/SharePoint/Misc/Cmich.SP.Repfinder.git`
* Rename directory *Enterpise-ActiveDirectory-Angular2* to *AdminRegistration*
* In *AdminRegistration* rename *Enterprise.Security.ActiveDirectory.sln* to *AdminRegistration.sln*
* Delete *.git* directory
* Back in the command prompt `git init`
* Change directory `cd Web.Ui`
* Restore all npm packages `npm install`
* Run `npm run dist` to put copies of font awesome icons and other static content in place
* Run the Angular hot-reload server `npm run serve` to watch for .ts file changes and auto transcompile them to .Net friendly places
  * It is up and ready to use when you see `chunk <vendor> ... [initial] [rendered]` show up 
  * If this ever gives you issues, or you need to stop and restart this server, use <kbd>Ctrl</kbd> + <kbd>C</kbd> then <kbd>Enter</kbd> (repeat until `Terminate batch job (Y/N)?` appears, and enter `Y`) 
* Double click your *.sln* to open the solution in Visual Studio 2017
* Open the `.gitlab-ci.yml` file and change *Enterprise.Security.ActiveDirectory.sln* to *AdminRegistration.sln*
* Click :arrow_forward: **Google Chrome** to debug and confirm that the site is functional 
  * Note: the *documentation* route won't be there (401 error), but you can run `npm run doc` to populate it. It contains more comprehensive documentation about the tech stack and pre-built components that are included.

## Add to GitLab as a New Repo
* We are now going to [add a new project](https://code.cmich.edu/projects/new) on GitLab
* Then after you have your new url (e.g., https://code.cmich.edu/IT-AppDevelopment/CustomApplications/AdminRegistration.git), use Visual Studio 2017 :arrow_up: **Add to Source Control** (on the bottom right)
* Select *GIT* > *Publish Git Repo* (under *Push to Remote Repository*) > paste your above url > *Publish*
* See if your pipeline has failed for your repo on GitLab (e.g., https://code.cmich.edu/IT-AppDevelopment/CustomApplications/AdminRegistration/pipelines) and make the necessary changes
  * Contact the maintainer of this template if you have issues

## Tags
[[Angular]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=AngularTag)
