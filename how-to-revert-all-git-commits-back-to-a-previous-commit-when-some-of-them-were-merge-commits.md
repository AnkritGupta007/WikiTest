# Summary
Undoing work in **Git** can get messy. One technique you can use is to reset the *contents* from a commit from `master` that you want to revert everything back. The commands below can help you do that. Other Options like `git reset` or `git revert` are discussed in the [StackOverflow Answer](https://stackoverflow.com/questions/1463340/how-to-revert-multiple-git-commits/1470452#1470452) below.

```bash
# can do the below command in VS2017 GUI instead of command line
$ git checkout fix-RevertChanges 
# so this resets the CONTENT for the current folder (because of ".") 
$ git checkout -f {myCommitOnMasterToRewindBackTo} -- . 
# if any files that were added since {myCommitOnMasterToRewindBackTo} these need to be manually deleted
# can do the below command in VS2017 GUI instead of command line
$ git commit -a -m "Revert all changes since {myCommitOnMasterToRewindBackTo}" 
```
 
## Further Reading
- https://stackoverflow.com/questions/1463340/how-to-revert-multiple-git-commits/1470452#1470452
- https://git-scm.com/docs/git-checkout#git-checkout-emgitcheckoutemlttree-ishgt--ltpathspecgt82308203

## Tags
[[Git]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=GitTag)