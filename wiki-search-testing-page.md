# Testing examples for Wiki Search
Original ticket was https://cmich.teamdynamix.com/TDNext/Apps/393/Tickets/TicketDet.aspx?TicketID=3812229
These test searches ***do*** work on **GitLab Enterprise Edition 13.0.0-pre db62b608419** . Eric Johnson has a working example of this in his [private repo](https://gitlab.com/DogCentralGroup6/DogCentral/-/wikis/home)
As of **GitLab Enterprise Edition 12.10.3-ee** and **GitLab Enterprise Edition 13.0.4-ee** the searches were still broken.

But in **GitLab Enterprise Edition 13.2.3-ee** they all work 👍!

## Tag searches
[[app.authServices]](https://code.cmich.edu/search?group_id=&project_id=365&repository_ref=master&scope=wiki_blobs&search=authServices) **Does work** `object.propertyCamelCase`

[[app.authI =authInterceptor]](https://code.cmich.edu/search?group_id=&project_id=365&repository_ref=master&scope=wiki_blobs&search=authInterceptor) **Does NOT work** `=camelCase`

[[authProvider]](https://code.cmich.edu/search?group_id=&project_id=365&repository_ref=master&scope=wiki_blobs&search=authProvider) **Does NOT work** `camelCase`

[[AuthService]](https://code.cmich.edu/search?group_id=&project_id=365&repository_ref=master&scope=wiki_blobs&search=AuthService) **Does work** `PascalCase`

[[Infrastructure]](https://code.cmich.edu/search?group_id=&project_id=365&repository_ref=master&scope=wiki_blobs&search=taggedWithInfrastructure) **Does NOT work** `taggedWithInfrastructure` (real world case)

## ConnectionString searches
Goal: find any occurrence of `Database=EventsCalendar` or `Initial Catalog=EventsCalendar` in any file (not just configs).

[`EventsCalendar extension:config`](https://code.cmich.edu/search?group_id=&project_id=&repository_ref=&scope=blobs&search=EventsCalendar+extension%3Aconfig&snippets=false) returns results including:
```
<add name="EventsCalendarDAL" connectionString="Server=IT-WebDB;Initial Catalog=EventsCalendar;
```

[`=EventsCalendar extension:config`](https://code.cmich.edu/search?group_id=&project_id=&repository_ref=&scope=blobs&search=%3DEventsCalendar+extension%3Aconfig&snippets=false) zero results

[`\=EventsCalendar extension:config`](https://code.cmich.edu/search?group_id=&project_id=&repository_ref=&scope=blobs&search=%5C%3DEventsCalendar+extension%3Aconfig&snippets=false) zero results

[`"=EventsCalendar" extension:config`](https://code.cmich.edu/search?group_id=&project_id=&repository_ref=&scope=blobs&search=%22%3DEventsCalendar+extension%3Aconfig&snippets=false) zero results