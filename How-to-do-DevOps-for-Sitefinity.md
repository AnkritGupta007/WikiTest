# How to do DevOps for Sitefinity
The CMU Public website is on the Sitefinity CRM platform and deployed and hosted on Azure.

## Technical Information
| Type       | Database(s)                           | URL                                    | Git Branch | UNC Deployment Path                                       |
| ---------- | ------------------------------------- | -------------------------------------- | ---------- | --------------------------------------------------------- |
| Test | server: dev-sqldb-cmich-sitefinity<br> - databases: all|site: https://dev-www.cmich.edu <br>admin: https://dev-www.cmich.edu/Sitefinity<br> static frontend: https://dev-web-cmich-edu-static-usnc.azurewebsites.net/ | master: https://dev.azure.com/CMUDevOps/_git/cmich-sitefinity | artifact: ['$(Build.ArtifactStagingDirectory)\\'](https://dev.azure.com/CMUDevOps/_git/cmich-sitefinity?path=%2FMaster.yml&version=GBmaster&line=67&lineEnd=68&lineStartColumn=1&lineEndColumn=1&lineStyle=plain&_a=contents)|
| Stage | server: test-sqldb-cmich-sitefinity<br> - databases: all|site: https://stage-www.cmich.edu <br>admin: https://stage-www.cmich.edu/Sitefinity| master: https://dev.azure.com/CMUDevOps/_git/cmich-sitefinity | artifact: ['$(Build.ArtifactStagingDirectory)\\'](https://dev.azure.com/CMUDevOps/_git/cmich-sitefinity?path=%2FMaster.yml&version=GBmaster&line=67&lineEnd=68&lineStartColumn=1&lineEndColumn=1&lineStyle=plain&_a=contents)|


