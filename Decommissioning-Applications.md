# Taking Applications Offline
1. Make best effort to replace or remove any references to the application being decommissioned.
1. Check the databases in the web.config and determine if any of the databases can/need to be decommissioned 
1. Take a backup (.zip) of the application from the production server and place in the share: `\\cab\appdev$\backups\decommissioned\apps`
1. Setup `app_offline.htm` using the provided template
1. Edit the README so 
   - the title reads `Application Name (DECOMMISSIONED - [Service or Incident Ticket Number](link to service request or incident) - DO NOT UPDATE)`
     - e.g., **Student Orientation (DECOMMISSIONED - [3939903](https://cmich.teamdynamix.com/TDNext/Apps/393/Tickets/TicketDet?TicketID=3939903) - DO NOT UPDATE)**
1. Archive the site in GitLab (Ask a team lead to do this since they will have the required elevated level of permissions)
1. Create a ticket to decommission the application (and if necessary any database) and send it to `IT_APPLICATIONS` that includes:
   - Description: `Please take {appName} offline on {appDeleteDate} and begin decommissioning {db} database(s). Please allow for 30 days before deleting the database.`
     - Where {appDeleteDate} is the date **6** months from today
     - Where {appName) is the name of the application 
     - Where {db} is the name of any database(s) that need to be decommissioned
   - List of servers the database resides on if possible
   - List all known instances of the application (dev,stg,prd)

## When Moving or Migrating an Application
If you are moving or migrating an app, *rather than decommissioning* it, [RedirectWithTicket](https://code.cmich.edu/IT-AppDevelopment/Playground/RedirectWithTicket) allows for a phased approach to make for smoother user experience and still catches referrer links that need to be updated to the new URL.

## Template for `app_offline.htm`
```html
<html>
<head>
    <link rel="icon" type="image/png" href="https://cdn.cmich.edu/media/img/sp2013/favicon.png">
    <meta name="viewport" id="metaViewport" content="width=device-width, initial-scale=1.0">
    <title>Application Offline</title>
    <link rel="stylesheet" href="https://cdn.cmich.edu/bootstrap/3.3.2/css/bootstrap.min.css">
    <link rel="stylesheet" type="text/css" href="https://cdn.cmich.edu/css/fonts/fonts.css">
    <link rel="stylesheet" type="text/css" href="https://cdn.cmich.edu/fonts/cmichIcons/cmich_icons.css">
    <style>
        html {
            background-color: #6a0032;
        }
        body {
            background-color: #fafafa;
            font-family: "Oxygen", sans-serif;
            margin: 0;
        }
        .oxygen {
            font-family: "Oxygen", sans-serif;
        }
        .roboto {
            font-family: "Roboto Slab", serif;
        }
        .header {
            background-color: #6a0032;
            border-bottom: 3px solid #d7a404;
            height: 75px;
            position: relative;
            width: 100%;
        }
        .cmichAppBanner_headerWordmark {
            float: left;
            height: 60px;
            margin-top: 10px;
            width: 122px;
        }
        .pageContent {
            padding-top: 5vh;
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
        }
    </style>
</head>

<body>
    <header class="header" role="banner">
        <div class="container-fluid cmichAppBanner">
            <div class="row">
                <div class="col-lg-12">
                    <div class="cmichAppBanner_topBar">
                        <a class="cmichAppBanner_headerWordmark" href="https://www.cmich.edu">
                            <img src="https://cdn.cmich.edu/media/img/applicationTemplate/cmuwordmark.png" title="CMU Wordmark" alt="CMU Wordmark">
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </header>
    <section role="main" class="container pageContent">
        <div class="row">
            <div class="col-md-12">
                <!--Content will go here-->
                <h1 class="pageTitle">Application Offline</h1>
                <p>
                    The application hosted at <b><script>document.write(window.location);</script></b> has been moved or discontinued.
                </p>
                <p>
                    If you have found this page please <a href="https://cmich.teamdynamix.com/TDClient/664/Portal/Requests/ServiceDet?ID=14955">Submit a ticket</a>, contact the help desk at <b>(989) 774-3662</b>, or <b><a href="http://helpdesk.remotesupport.cmich.edu/api/start_session.ns?popup=1&c2cjs=1&id=0&issue_menu=1">Chat Live!</a></b>
                </p>
                <p>
                    Please be prepared to provide:
                    <ul>
                        <li>A screenshot of this error</li>
                        <li>The steps that you took to reach this page</li>
                    </ul>
                </p>
                <p>
                    <a href="https://www.cmich.edu/office_provost/OIT/help/help_desk/Pages/default.aspx">Click here or more information about the help desk hours.</a>
                </p>
                <p>
                    <b>Referrer:</b><script>document.write(" "+ document.referrer || " None");</script>
                </p>
            </div>
        </div>
    </section>
</body>
</html>
```

<!-- :white_check_mark: Complete, :clock10: In Progress, :date: Holding, :thinking: TBD -->


## Tags
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[SDLC]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SDLCTag)