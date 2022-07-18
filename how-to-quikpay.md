1.  Requesting a new QuikPay payment site
    * Before any development is done against QuikPay a request must be made to Student Account Services and University Billing (SASUB). It is recommended that the end user department work with SASUB to determine the details of how payments will be processed into SAP and reconciled against campus systems. Developers should for the most part not need to be a part of these conversations except for the rare occasion that the application posts data to SAP for purposes of reconciling automatically. 
    * SASUB will provide the developer with four important pieces of information. 
       * OrderType - Unique identifier that allows SASUB to limit payments down to a single entity 
       * OrderDescription - Secondary unique identifier that is usually specific to a project or application 
       * OrderNumber - An identifier that is used to uniquely identify payments in a particular system. If SASUB does not specify a specific convention, the developer should just send along a unique identifier for the application. e.g. The SQL identity for the submission. 
       * Payer - Determines what QuikPay application a user will end up with when paying. If there isn't a decision to use a specific payer, most applications will use the "General" payer

1.  Setting up a test QuikPay Redirect
    * For testing purposes developers willl need to setup redirect URLs in order to process responses from QuikPay. It is important to note that these URLs are **case sensitive**. The developer will need to mark their local computer as a safe redirect location and the location on the test server.
       * Go to the website [https://uatquikpayasp.com/cmich/root/administrator.do](https://uatquikpayasp.com/cmich/root/administrator.do) and login with the following (both case sensitive)  
       *   Username: ITWEBTECH
       *   Password: test1234  
       *   Select "Configuration" from the navigation on the left
       *   Select "Allowed Redirects" from the expanded "Configuration" navigation
       *   Enter the **case sensitive** url into the box and select "Add"
    * Please remove any unused redirects, so we can maintain a current list of redirects
1.  Requesting a production QuikPay Redirect
1.  Developing Against QuikPay

## Tags
[[QuikPay]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=QuikPayTag)