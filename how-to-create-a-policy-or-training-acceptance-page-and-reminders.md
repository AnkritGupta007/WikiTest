Goal: Create a policy / required training page and reminder popup for a subset of users. We will use Information Security Training as an example.

Steps:
1. Go to 
test: https://resnetconnect.cmich.edu/policyacceptance/DocumentVersions.aspx
production: https://netconnect.cmich.edu/policyacceptance/DocumentView.aspx

2. In the Applications tab, add an application called InformationSecurityTraining with a short description.

3. In the Available Documents tab:
	- create a new document that represents or policy (or just a placeholder for a training)
	- add the current version of the document and give it a version number

4. In the Required Documents tab select our newly created application and newly created document and set the document lifecycle requested by the policy/training owners.

5. Unpack the [template.zip](/uploads/af648b604eae14d871784105b6512814/template.zip) file to your working folder and edit following lines in setup.ps1
	$ApplicationName = "InformationSecurityTraining";
	$year = "2017"
	$documentId = 12
	$content = 25
The values for the documentId and content can be found in the PolicyAcceptance database, tables Document (Id column) DocumentContent (Id column) by looking for the document title created at step 3. The sql server to connect to is it-webtestln (for the test environment).

6. Run the setup.ps1 powershell script and it will create a folder named after your application.
7. Place the created .js file in a new folder InformationSecurityTraining on cdn (\\\\it-prdcdn01\d$\Inetpub\wwwroot\cdn\js\Projects\)
8. Edit the InformationSecurityTraining Create Alerts.sql file to reflect the javascript location and the content of the alert popup for your policy/training. When selecting from ADBFeed.dbo.UserEmploymentData, a where clause can delimit the intended audience for this policy/training.
9. Go to
test: https://betaweb.cmich.edu/centrallink/pages/default.aspx
production: https://cmich.edu/centrallink/pages/default.aspx
and click on the top left settings wheel - which should be present if you have the appropriate permissions.
19. Click Add a page and edit the title and add the desired content. You need to make sure to insert a web part of type "Media and Content"/"Content Editor"/"Script Editor" at the end and edit it's snippet to:
	<script src="//cdn.cmich.edu/js/projects/internetsecurity/internetsecurity.js"></script>
	<div class="checkbox">
		<label>
			<input id="chkVerifyWatch" type="checkbox">I verify that I have completed the internet security training video.
		</label>
	</div>
	<div class="form-group">
		<button class="btn btn-default" id="btnSubmitVerfication">Submit</button>
	</div>
Make sure you edit the src to point to your .js file in cdn.
20. Use the sql code created at step 6 to add popup alerts for the desired audience.

Done!

## Tags
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[Training]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=TrainingTag)
