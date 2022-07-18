# Summary
If you need to access a remote drive or folder (e.g., `\\imagenow-dev\d$\docs\pages`) with your elevated Privileges admin account (e.g., `it-globa1id`) in Windows Explore you can do this by give your normal global ID local NTLM rights, at least until your machine is rebooted.

## Steps
- <kbd>Windows</kbd> then `Run` > enter the **shared base** drive or folder (e.g., `\\imagenow-dev\d$`) and hit <kbd>Enter</kbd>
- Windows Security Modal will pop-up. Enter your it-globa1id credentials.

![image](/uploads/6c64ae10a0a9470fb9e609a80b6bd1ae/image.png)

- You should now have access with Windows Explorer!


- To verify your access is in place until you restart your computer <kbd>Windows</kbd> then `CMD` > `net use`

```
C:\> net use
New connections will be remembered.
 
Status       Local     Remote                    Network
 
-------------------------------------------------------------------------------
OK           U:        \\Udrive\johns7ed$        Microsoft Windows Network
OK                     \\imagenow-dev\d$         Microsoft Windows Network
The command completed successfully.

```
- Similarly you can run `C:\> wmic netuse get remotepath, Username /value` to see the directories you can access, and as whom you can asses them. 

## Tags
[[Remote]](https://code.cmich.edu/search?utf8=%E2%9C%93&project_id=365&scope=wiki_blobs&search=RemoteTag)