# Summary
To Read, Update and Delete ImageNow Documents and Meta data, we recommend using the CMU Nuget package [Perceptive Content Client](https://code.cmich.edu/IT-AppDevelopment/SharedLibraries/PerceptiveContentClient). You can explore features not yet implemented in this NuGet package but which are available at the [ImageNow Integration Server](https://imagingtest.cmich.edu/integrationserver/help/operations.html) and its RESTful API operations documented at [https://imagingtest.cmich.edu/integrationserver/help/operations.html](https://imagingtest.cmich.edu/integrationserver/help/operations.html).

## How to Extend Operations found in the ImageNow Integration Server to the NuGet Pacakge
### Background Info:
* Perceptive Content is CMU’s document management solution (electronic document repository).  The product has been owned by multiple companies (HP, Lexmark, Kofax, etc.; currently owned by Hyland).  It was originally called ImageNow, but was subsequently renamed.  “Perceptive Content” is the preferred name, but most in OIT refer to the system as “ImageNow”.
* Perceptive Content has two methods for importing documents in bulk.
   * Import Agent is a scheduled job that runs at periodic intervals and looks for documents in a folder (usually a shared folder).  Import Agent requires an index file that lists all documents in the folder and contains any metadata to attach to each of the documents.
   * Integration Server is a REST API that seems to mostly work (it generally returns 200/OK, but there is some question as to whether it actually does anything when it returns an OK).

* There are three Perceptive Content environments
 1. https://imagingdev.cmich.edu is the development sandbox used by the app support team to test patches and scripts.
 2. https://imagingtest.cmich.edu is the test system.  It is used by both the end users and by application developers.
 3. https://imaging.cmich.edu is the production system.
* Documentation on Integration Server is located at https://imagingtest.cmich.edu/integrationserver/help/operations.html.
* Business offices have workflows defined in Perceptive content and allow documents to be routed automatically.  Workflows are created by Perceptive Content administrators (usually Matt Norton or Tim Daugherty).
* A document in Perceptive Content has multiple parts.  The “document” is really just a container that holds metadata about the actual document it represents.  After a document is created, the binary content (.pdf, .doc, .docx, .png, .jpg, etc.) is added as a “page”.
   * The general rule is that all document images are converted to TIF images.  
   * Since a “page” contains the binary content of a real-world document, and a real-world document can have multiple real-world pages, a “document” can have multi-page “pages”.
     * The “conversion process” that converts documents to TIF images will also flatten them, so there is one page per “page”.
* A document requires two pieces of information to be created:  a “drawer” and a “document type”.  The drawer indicates the document location within Perceptive Content, and the document type corresponds to type defined by the business office.
* A document is distinguished by its “keys”, which include document type, drawer, a set of 5 fields (field1, field2, field3, field3, field5), so the combination of values must be unique or there will be a conflict.  
  * In response to a conflict, you may opt to generate an error, replace an existing document, or append to an existing document.
  * We generally ensure that at least one of the keys is unique to prevent conflicts.  A timestamp is often sufficient to guarantee uniqueness.
  * Field keys have a maximum length constraint (about 40 characters), so data may need to be truncated to prevent errors.
* Once a document is created, it can be put into a workflow.
* A document can have properties, which contain additional metadata about the document.
  * A property has an ID, a name, and a type.
  * A property type could also have a pre-defined listed of values.
* Perceptive Content auto-generates IDs, which are a combination of letters and numbers (e.g. 321Z2B9_055WD7Z810002F2).  The IDs are used to uniquely identify an object such as documents, workflows, and document properties.  Drawers do not have IDs, but instead are identified by name.

### Important things to know about the Integration Server API:
 * The API manages authentication through HTTP headers.  You provide username and password credentials, and the server will return a session hash.
 * Sessions can be started implicitly.  That is, as long as the credential headers are in place, a new session hash will be created automatically.
 * As long as a valid session hash is provided, Integration Server will continue to use it.  However, session hashes expire.
   * If the hash expires and the credential headers are in place, a new hash will automatically be generated.
   * If you don’t update the connector to use the new hash, Integration Server will continue to generate session hashes for every call performed.
   * There are a finite number of sessions available, so when an application does not manage its session hash, it can (and has) use up all available sessions.
     * Once sessions are used up, then we have to wait for an old one to expire.
   * A session hash should be closed when all processing is complete.
 * You’ll know best how to handle sessions.  Matt Bailey personally prefers to explicitly create a session and then remove the credentials headers to prevent new sessions from automatically being generated.  Session expiration can be detected when the API returns a 401/Unauthorized.
* The documentation page has this information in “Session Management” page under the “Getting Started” section.

### General steps for creating a document:
1.	Create a document (this should be treated as an atomic operation, if possible; if the second step can’t be completed, the first should be undone)
a.	Set up document keys and properties, and call the Document endpoint (if you need to add notes, you’ll need V3, otherwise V1 should be fine) [v1/document]
b.	Call the page endpoint for the document ID created in the previous step and add the file [v1/document/{id}/page]
2.	Call the WorkflowItem endpoint to add the document to the workflow [v1/workflowItem]
  * Object ID = document ID from previous step
  * Type = DOCUMENT
  * Priority = MEDIUM
  * Workflow queue ID = 321Z2B9_055WD7Z810002F2
### Note:  
* Document properties are set by property ID, not name.  The IDs used in the CommonApp import should be the same across environments (test, prod), but they could vary.  The Parchment import process just retrieves all properties from Perceptive Content initially and then looks up IDs based on the name.  However, you could treat the IDs as stable and just hardcode then.  Caveat emptor, YMMV, and all that.




## Current Projects Using This Tech
- [Agreements](https://code.cmich.edu/IT-AppDevelopment/CustomApplications/Agreements)

## Tags
[[ImageNow]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ImageNowTag)
[[PerceptiveClient]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PerceptiveClientTag)