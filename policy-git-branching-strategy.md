# Summary
To ensure a standardized way of using git across the application development team. There are two main Strategies, [Master-Testing-Prod](policy-git-branching-strategy#master-testing-prod-branching-strategy) (recommended for consistency) and [Master-Tag](policy-git-branching-strategy#master-tag-branching-strategy) (no longer in use at CMU) and a few naming conventions to keep in mind. Also remember to always do peer code reviews.

## Naming Convention
* feature-BranchName – used for new features or changes to existing features
* fix-BranchName – code fixes made to the master branch
* hotfix-BranchName – code fixes made directly to the production branch during emergency situations

## Code Reviews
* Best industry practice is to have at least one other engineer reviewing code before it goes into production
    * Example: [Google](https://www.quora.com/What-is-Googles-internal-code-review-policy-process)
* Mandatory Code reviews will happen when code is merged into the **Master** branch.  This will be enforced by Gitlab.
* Optional code reviews can happen at any point in the branching process.  

## Master-Testing-Prod Branching Strategy
*  **Master** is the production ready branch that **has not** had official UAT signoff.
* Feature and fix branches are created off and merged back into **Master**
* Code reviews happen on merge requests from a feature or fix branch into **Master**.  Additional code reviews may happen when merging into **UAT** or **Production** branches.
* Merging from Master to Testing requires no additional signoff, though you should check the merge request diff for any other changes being merged along with yours before actually merging.
* Typical (standard) workflow - The **Master** branch is merged into the **Testing** branch and, upon signoff from the ticket requester, the **Testing** branch is merged **Staging**. **Staging** is then merged into the **Production** branch once a [Change Calendar ticket](how-to-request-a-change-calendar-deployment) is approved, during the deployment window (4 AM - 7 AM Thursday mornings).
* (Optional) Unstable/Nightly builds/branches can be used for projects that need them for faster user feedback.  Unstable/Nightly builds/branches must still be merged into the **Master** branch and push through the standard workflow.
* Further reading with diagrams - [CMU GitLab Flow](https://resapps.cmich.edu/gitlabflow)

![Master-Testing-Prod Branching Strategy](https://code.cmich.edu/IT-AppDevelopment/Playground/git-flows/raw/master/img/current.png)

## Master-Tag Branching Strategy
*  **Master** is the production ready branch that **has** had official UAT signoff.  **Tagged** commits on master are deployed to production. 
* Feature and fix branches are created off **Master**, while *Hot fixes* (ticket work outside the agile teams work) should pull from the most recent **tagged** commit on master.
* Code from features should be merged into **Testing** for user sign off. After user sign off, the code from the feature can be commited to master, or to a **UserApprovedBundle** branch.
* Code reviews happen as code is pushed from a feature or fix branch into **Master**.  Additional code reviews may happen when merging into **UAT** or **Production** branches.
* Typical (standard) workflow - The **Feature** branch is merged into the **Testing** branch and, upon signoff, the **Feature** branch is merged into the **Master** branch. Merging into master auto-deploys to the *staging* environment. From *staging* users can do a brief confirmation check. Tagging the branch **v1.2.3** with a correct version number causes it to deploy to *production*
* Further reading with diagrams - [CMU GitLab Flow](https://resapps.cmich.edu/gitlabflow)

![Master-Tag Branching Strategy](https://code.cmich.edu/IT-AppDevelopment/Playground/git-flows/raw/master/img/proposed.png)

## Tags
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[Git]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=GitTag)