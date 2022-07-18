# Summary

This document provides step-by-step instructions for changing your GitLab credentials in Windows.  Sometimes you will encounter the following error when attempting to clone a repository or otherwise connect to the GitLab server.

```
Git failed with a fatal error.
Authentication failed for 'https://code.cmich.edu/IT-AppDevelopment/CustomApplications/<repository_name>.git/'
```

## Prerequisites

This document assumes that you are using the Git Credential Manager for Windows, which stores your credentials in the Windows Credential Manager.  If you are not using the Git Credential Manager for Windows, you will need to [search for instructions](http://lmgtfy.com/?q=git+change+credentials+-%22git+credential+manager%22) on how to change your credentials.

## Procedure

Click the Start button or press the Windows key on the keyboard.  Type "control", and select Control Panel from the results list.

1.  If your control panel window is arranged by category, click User Accounts, then select Windows Credentials.  Otherwise, click Credential Manager, then select Windows Credentials.
1.  Update each entry for `code.cmich.edu` with your new password.  You should have the following three entries (see example screenshot below):
    - `git:https://[global ID]@code.cmich.edu`
    - `git:https://[global ID]@code.cmich.edu/`
    - `git:https://code.cmich.edu`

<figure>
<img src="https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/uploads/e9d8433a9e8bfda74c9314619b248736/git-credentials.png" alt="Example of Git credentials in the Windows Credential Manager" />
<figcaption>Figure 1.  Example of Git credentials in the Windows Credential Manager</figcaption>
</figure>

## Tags
[[Git]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=GitTag)
