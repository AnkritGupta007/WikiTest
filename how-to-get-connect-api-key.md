# API Keys for Connects
This page is used to detail how to get an API key for the various "Connect" middleware applications (ITSMConnect, SLCMConnect, etc.)

## Local machines 
If you only need an API key for your local machine, **you can edit the table of API keys in the respective application's database**. There is usually a table called "ApiKey" on the test server. The process of adding an APIKey to this table will vary depending on the application. For example, ITSMConnect has a stored procedure called "GenerateApiKeys" that will generate an API key when executed. 

### ITSM Example for generating API keys:
1. Log into IT-Webtestln
2. Find the "Test-ITSMConnect" database
3. Find dbo.GenerateApiKeys under Programmability/Stored Procedures
4. Run this procedure (**Note:** The IPADDRESSCSV is a comma separated list of multiple IP addresses, without spaces. Any spaces will be included in the IP address and caused it to not be recognized).
   - APP: Name of the web application or the developer who's machine this is generated for.
   - IPADDRESSCSV: The IP address of the workstation or machine that will be sending this key. (**Note:** The IPADDRESSCSV is a comma separated list of multiple IP addresses, without spaces. Any spaces will be included in the IP address and caused it to not be recognized).
   - NOTE: Human readable note describing this API key and its purpose.

Each application should have authorization information in their readme detailing how it works. 
Below is what appears on the ITSMConnect readme for authorization:
___
The ITSM Connect sandbox API allows for two modes of authentication: API key and Cmich authentication. When using API key authorization, the Authorization header value will have the format Apikey [key], where Apikey specifies the authorization mode and [key] is replaced by your assigned key.

If using Cmich authentication, the Authorization header value will have the format Basic [globalId:password], where Basic is the authorization mode and [globalId:password] is replaced by your Global ID and password, separated by a colon and converted to a Base64 string. For example, the Global ID "testr1t" and password "mysupersecretpassword" are combined as testr1t:mysupersecretpassword, which converts to the Base64 string dGVzdHIxdDpteXN1cGVyc2VjcmV0cGFzc3dvcmQ=, and results in an Authorization header value of Basic dGVzdHIxdDpteXN1cGVyc2VjcmV0cGFzc3dvcmQ=.
___

Unlike the sandbox API, the production API only accepts a pre-assigned API key for authorization. In either case, an API key is assigned to an IP address, so authorization will fail if attempting to use an API key on a machine to which it is not assigned.

## Setting up API Keys for any Other Environment or Outside Parties
If you need an APIKey for a production/staging environment, or if a third party developer needs an API key, a ticket would need to be created. The ticket must include who specifically needs access and the business need for that access.

## Tags
[[Development]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DevelopmentTag)
