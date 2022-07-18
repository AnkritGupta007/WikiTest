# How to Make a Tag ( *Only applies to CMich NuGet packaged items, like the Core API*)
A *Tag* is used to easily identify the commits linked to each release (See for example https://code.cmich.edu/App-Shared-Libraries/Visual-Captcha/commits/v1.0.0 where it shows the commits for that version of the app.)

1. Next we will add a *Tag* linked to the commit that includes the changes just prior to their merge into *master*
1. Go to the **Commits** or **Network** section of your project in GitLab, whichever you feel more comfortable with to identify the proper commit
1. Find the last commit (hopefully on a feature or fix branch) before the merge to master
1. Click the node for that commit to link to that commit 
![network-find-commit](/uploads/d33a43fdd0c2075fa566c956f27032e3/network-find-commit.png)
1. Click *Copy to clipboard* icon to copy the hash code for that commit  
![copy-commit-to-clipboard](/uploads/c94c3c97a1130e41b1a63d8c40aa0106/copy-commit-to-clipboard.png)
1. Go to the **Tags** section of your project in GitLab
1. Click the *New Tag* button on the top right
1. Enter a *Tag name* in the format `v{Major}.{Minor}.{Bug}` (note the **v** at the beginning). So for example, `v2.0.3`
1. In the *Create from* field, paste the hash code from your clipboard
1. Click *Create Tag* button, and your all done