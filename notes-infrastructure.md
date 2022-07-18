# Notes on Infrastructure
Mostly tables below showing the servers we commonly do work on for application development.

## Databases

| Listener | Server(s) | Environment | Notes |
| ----- | ----- | ----- | ----- |
| - | IT-Db2k12Dev01 | Development | Summer 2022 - Transitioning to IT-SQL17-T-Db1 | 
| IT-WebTestln | IT-Db2K12Test01(?)<br>IT-Db2K12Test02 | Testing | Summer 2022 - Transitioning to IT-SQL17-S-WebL |
| IT-WebDb | IT-Db2K12-01<br>IT-Db2K12-02 | Production | Summer 2022 - Transitioning to IT-SQL17-P-WebL |
| - | IT-SQL17-T-Db1 | Testing | |
| IT-SQL17-S-OCL<br>IT-SQL17-S-WebL |  IT-SQL17-S-DB1 | Staging | |
| IT-SQL17-P-OCL<br>IT-SQL17-P-WebL | IT-SQL17-P-DB1  | Production | |
| oc-sql2012\WWW | OC-SQL2012 (now gone?) | Production | Summer 2021 - Moved to IT-SQL17-P-OCL |
| oc-sql2012 | OC-SQL2012 (now gone?) | Production | Summer 2021 - Moved to IT-SQL17-P-OCL |

### Limited Access for `AuthDB`
| IP Address | Server | Environment | Access |
| ----- | ----- | ----- | -----|
| 10.209.15.70 | DBMain-Dev | Testing | via `IT-CheckWeb` |
| 10.209.15.71 | DBMain | Production | ask for help from `IT_INFO_SECURITY_VALIDATIONS` team |

## Web Servers

### Application - OIT
| Server | Application Type | IP Address | URL | Environment | Has Internet Access |
| ----- | ----- | ----- | ----- | ----- | ----- | 
| it-resweb01 | Web | 141.209.19.13 | https://resapps.cmich.edu | Development/Testing | true |
| it-stgweb01 | Web | 141.209.19.12 | https://stgapps.cmich.edu | Testing/Staging (SAP) | true |
| it-prdweb01 | Web | 141.209.19.69 | https://apps.cmich.edu | Production | true |
| it-prdweb02 | Web | 141.209.19.70 | https://apps.cmich.edu | Production | true |
| it-prdweb03 | Web | 35.33.110.15 | https://apps.cmich.edu | Production | true |

### Application - OIT Legacy
| Server | Application Type | IP Address | Environment |
| ----- | ----- | ----- | ----- |
| it-devweb1 | Web | 141.209.19.64 | Development |
| it-prodweb1 | Web | 141.209.19.253 | Production |

### Application - Former Global Campus
| Server | Application Type | IP Address | URL | Environment |
| -----  | -----            | -----      | ----| -----       | 
| oc-vm-iis8 | Web | 141.209.127.96 | https://globalapp.cmich.edu | Development/Testing/Production |
| oc-miscel2 | Web | 141.209.127.35 | ? | Development/Testing/Production |

### GitLab CI Runners
| Server | Application Type | IP Address | URL | Environment |
| ----- | ----- | ----- | ----- | ----- | 
| it-gitlab-ci1 | Runner| 141.209.15.111 | ? | Testing |
| OC-SP2013 | Runner| 141.209.127.46 | ? | Development |

### NuGet
| Server | Full path | IP Address | Environment |
| ----- | ----- |  ----- | ----- | 
|it-sdlc-p-dts1 | `it-sdlc-p-dts1\d$\inetpub\nuget.cmich.edu`|10.209.19.185|Prod/beta/alpha|

### Middleware API
| Server | Application Type | IP Address | URL | Environment |
| ----- | ----- | ----- | ----- | ----- | 
| it-web-t-midw1 | API | 141.209.19.81 | https://test-*.apps.cmich.edu | Testing |
| it-web-s-midw1 | API | 141.209.19.84 | https://stage-*.apps.cmich.edu | Staging (App Support) |
| it-web-p-midw1 | API | 141.209.19.88 | https://*.apps.cmich.edu | Production |
| it-web-p-midw2 | API | 141.209.19.89 | https://*.apps.cmich.edu | Production |
| it-web-p-midw3 | API | 35.33.110.16 | https://*.apps.cmich.edu | Production |

### Services, Processes and Schedule Tasks
| Server | Application Type | IP Address | URL | Environment |
| ----- | ----- | ----- | ----- | ----- | 
| it-tstproc01 | Services, Processes and Schedule Tasks| 141.209.8.65 | ? | Testing |
| it-prdproc01 | Services, Processes and Schedule Tasks| 141.209.15.77 | ? | Production|


## SharePoint

| Server | IP Address | URL | Environment |
| ----- | ----- | ----- | ----- |
| oc-sp2013 | 141.209.127.46 | ? | Development |
| it-sp13-d-app1 | 141.209.19.23 | ? | Development |
| it-sp13-d-app2 | 141.209.19.24 | ? | Development |
| it-sp13-d-app3 | 141.209.19.25 | ? | Development |
| it-res13web1 | 141.209.19.90 | https://betaweb.cmich.edu | Testing |
| it-res13web2 | 141.209.19.91 | https://betaweb.cmich.edu | Testing |
| it-res13app1 | 141.209.19.92 | https://betaweb.cmich.edu | Testing |
| it-res13app2 | 141.209.19.93 | https://betaweb.cmich.edu | Testing |
| sp-stgweb01 | 35.33.110.10 | https://stgweb.cmich.edu | Staging (App Support) |
| sp-stgweb02 | 35.33.110.11 | https://stgweb.cmich.edu | Staging (App Support) |
| sp-stgapp01 | 35.33.110.12 | https://stgweb.cmich.edu | Staging (App Support) |
| sp-stgapp02 | 35.33.110.13 | https://stgweb.cmich.edu | Staging (App Support) |
| sp-prdweb01 | 10.209.17.16 | https://www.cmich.edu | Production |
| sp-prdweb02 | 10.209.17.17 | https://www.cmich.edu | Production |
| sp-prdweb03 | 10.209.17.18 | https://www.cmich.edu | Production |
| sp-prdweb04 | 10.209.17.19 | https://www.cmich.edu | Production |
| sp-prdapp01 | 10.209.17.20 | https://www.cmich.edu | Production |
| sp-prdapp02 | 10.209.17.21 | https://www.cmich.edu | Production |
| sp-prdapp03 | 10.209.17.22 | https://www.cmich.edu | Production |

## Tags
[[Infrastructure]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=InfrastructureTag)
[[Database]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DatabaseTag)