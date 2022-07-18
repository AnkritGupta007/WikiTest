# Summary
Nobody likes merge conflicts, and even more so when you have them between protected branches (e.g., master => testing). Below are the git steps that can fix this. Note that this can also be done entirely through Visual Studio by making sure you do not to fast-forward merging.


> We Recommend using the [In Visual Studio 2017](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-resolve-merge-conflicts-in-testing-or-higher-branches#in-visual-studio-2017) method

## In Visual Studio 2017 
### (Using branches *left* => *right*, where *left* might be *master* and *right* might be *testing* in a real world example)
1. Go to Team Explorer > Branches
2. Expand remotes/origin and right-click *right* > *New Local Branch From*
3. Enter new branch name (e.g., fixing-merge-conflicts) **check "Checkout branch"**
4. Right-click fixing-merge-conflicts > *Merge From...* > Merge from branch: *origin/left* , **uncheck the "Commit changes after merging" to avoid fast-forward merging**
5. Click ":warning: Conflicts: #" and resolve each conflict, selecting or typing the desired resulting code
6. In Team Explorer click the *Commit Merge* button
7. Enter a commit message and click *Commit All*
8. You now need to click *Sync* (which will bring you to the *synchronization sub menu*) and then *Push*
9. In [Gitlab](https://code.cmich.edu) merge *fixing-merge-conflicts* into *master*, and so on up the chain until you have merged *left* into *right* and there is no longer a conflict.


## In Git command line 
(STEPS NEED VERIFICATION)
### (Using branches *left* => *right*, where *left* might be *master* and *right* might be *testing* in a real world example)

1. `git checkout -b fixing-merge-conflicts --no-track origin/right`
  - Creates new branch *fixing-merge-conflicts* from *origin/right*
2. `git merge --no-ff origin/left`
3. `git mergetool` 
4. `git add .` 
5. `git commit -m "fixed it message"` 
6. `git push` 
7. In [Gitlab](https://code.cmich.edu) merge *fixing-merge-conflicts* into *master*, and so on up the chain until you have merged *left* into *right* and there is no longer a conflict.

## Tags
[[VisualStudio]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=VisualStudioTag)
[[Git]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=GitTag)
