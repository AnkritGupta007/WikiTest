## Background

CMU relies on SAP modules for its ERP (primarily HR and FI modules, with some CO, etc.) and SLCM functionality.  This data is the canonical source for the web applications, whether it is accessed in a live, cached, or synchronized method. Each method uses slightly different overall techniques:

*   Live Data (includes cached data): available via three separate technologies as currently implemented, all executing remote-enabled function modules (RFCs); SAP .NET Connector, SAP-hosted Web Services, ERP Connect from Theobold Software (see _ERPConnect in CMich API_ for a more complete discussion of CMU's use of ERPConnect).
*   Externally Synchronized: this data is retrieved/processed from BI endpoints or flat files exported by SAP using on-demand or scheduled programs. External processing of this data is usually performed with small applications, SQL Server Integration Services (SSIS) packages, or ad-hoc processing using suitable tools.

## Security Concerns

Security comes into play any time data is accessed in SAP.  The authentication is either from a named domain user or a SAP credential (where the username can be a C_* user – a console only, shared system account or can match the user's Global ID, typically, but often is used with a password that is separate from the user's Active Directory (AD) credential).

The exported files typically are found in <span style="text-decoration: underline;">\\sapdata\OIT$\</span> or some subdirectory thereof and access to this network resource uses the AD credential of the running program, service, or SSIS package.  When this is in a SSIS package the domain account the SQL Server Agent is running as is the account that must have provided access.

C_* users are commonly used where we don't need the specific action to be executed as a specific, named user in SAP (i.e. all users have same permissions, etc.) and where the end users don't have SAP credentials to authenticate.

Named SAP users are often prompted at run-time to provide their SAP username/password in order to prove identity for scenarios where interactions with SAP are done with the identity of the provided SAP account (along with the corresponding security permissions).  This is to allow for proper audit trails for administrative users (where the C_* users are assumed to be done by the owner — the student, faculty, or staff — of the user record in question).

## Interop Method Details

### .NET Connector

The .NET Connector employed by CMU is the original .NET Connector provided by SAP but for which support was never extended to Visual Studio 2005 or later.  It is an end-of-life product where the next version (released in 2011) was entirely different.  Therefore, no new development should introduce dependencies on the unsupported version of the .NET Connector.

This component works by employing a designer within Visual Studio 2003 that enables the user to connect to the SAP system (typically RS4) and view RFCs available on the system.  The desired RFCs are dropped on the design surface and there are options to tweak the manner in which the user interacts with the proxy objects generated by the WSDL that SAP utilizes in this environment.  These tweaks are all done in a haphazard fashion in the systems that we support so no direction will be provided here.

In order to enable us to continue to use this functionality (while not extending it) we have wrapped the use of this connector in a code library packaged as separate DLLs but all available in the CMichSapConnector solution within $/SAP Applications/ in Vault.  These are separated into separate projects based on the original applications that each supports.  The compiled library can be included with the applications that require the functionality.

Changes to any of these would be difficult and time consuming to set up due to the dependency on Visual Studio 2003 (which is not used for any development within the group) and it is recommended that any updates to these applications that require different interaction with RFCs break this dependency and migrate to our current platform for RFC interoperability.

### SAP Web Services

SAP Web Services allow for external applications to execute SAP RFCs.  These require additional setup to be done to execute properly.  To even get Web Service (WS) support in SAP requires a bit of setup with transaction SICF.  This has been done so it won't be covered here.

Also, the web service load balance listener installation/configuration will not be covered here, nevertheless, there is a web dispatcher that runs on SAP to help with load balancing the WS calls and if this is not running the web service calls will fail.  SAP may be up and available but if this is down then WS calls still fail.

Web Services must be configured in two places: SAP and Visual Studio Core API.

Configuration in SAP begins after the RFC has been created and has been enabled for remote execution.  This is typically done by the ABAP programmer.  You must also have a developer key installed on your SAP instance. Then, using transaction SE80, under the ZRPT Package, expand Service Definitions, right click on Service Definitions and select Create.

![img1](/uploads/0bb35ecdc8a148a691e0f310f948bef8/img1.png)You then need to provide a Service Definition, description, and Endpoint Type.

![img2](/uploads/955c3deb3ee7f4e16831cd5dc629ca58/img2.png)

The naming pattern is ZWs* where the name references what the WS call will do.  The Endpoint Type should be a Function Group in order to be more flexible for adding whatever RFCs need to be grouped together in this web service endpoint.  The function group may be appropriately selected if one exists uniquely to the RFC work being done.  If not, then we often use ZCMMD001 because it is simple (i.e. less to clean up/remove).  Mapping of Names should also be checked to assist with the proxy code generation later in Visual Studio.

![img3](/uploads/4eb4f83ca5546e1eca5ed470d5bfbef7/img3.png)

The next screen in the wizard allows you to add/remove functions to the web service… this is where the flexibility of using the group starts to come into play. You may add multiple functions. You can't remove all functions belonging to the root function group you selected, but you don't need to leave it active selected.  Only those selected will be used in the web service.
![img5](/uploads/a3b0885fc6d9bd4f97f120a0610ffefa/img5.png)

Because we don't have SSL configured properly on the SAP application servers, we must use the low security model, which isn't ideal.

![img6](/uploads/e923390762a1ee7ef3a28a31c2dba589/img6.png)

The next screen requires a package and transport request be created (another topic) in order to be able to be transported through the system, so this step is typically done with the transport request in DV4.  In RS4, you may use it as a Local Object.

![img6__1_](/uploads/d2d3889eab547e4540c02af300b56256/img6__1_.png)

It then needs to be activated upon completion.

![img7](/uploads/267e0ae0ab0689c9bd1a55fb8ef2e7fc/img7.png)

Only now is it ready to consume.

Then work needs to be done in Visual Studio (typically in the Core API) to add a web service reference to this.  You will need to provide SAP credentials to the system you point to.  The URL for the web service endpoint can be found under the WSDL tab of the service definition in SE80 (i.e. right side of window).

You will need to add additional references to the new service in the Core API in accordance with the established pattern (so the users of the Core API won't need to provide the C_* user and credentials, etc.).

Changing/refreshing of an existing definition is somewhat tricky to find.  Under the Internal View tab you can right click and choose "Modify Operations."  This will allow you to add/remove RFC functions from the web service endpoint or to update the operations to recognize changes made to the underlying RFC interfaces.  These need to be transported as well.

### ERPConnect

This is covered substantially in an external document: ERPConnect in CMich API.  That document also covers the use of ERP Builder (an internally built tool, very rough) that allows for the pointing of the tool to the RFC and it will extract the metadata for code generation to ease the setup of interacting with RFCs.

<h2>Tags</h2>
[[SAP]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SAPTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
