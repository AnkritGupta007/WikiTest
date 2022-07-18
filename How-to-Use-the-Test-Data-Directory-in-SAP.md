# Using the Test Data (Variants) Directory in SAP

When troubleshooting web applications that call SAP RFCs it is sometimes necessary to execute the RFCs directly in SAP. To share your findings with others, it can be helpful to save your test parameters using the Test Data (Variant) Directory. This allows others can execute the RFC with the same values you are using. This brief article describes how to access, execute, delete, and save items in the Test Data Directory.

## Working with the Test Data Directory

1. After logging into SAP with your [SAP-specific password](https://cmich.teamdynamix.com/TDClient/664/Portal/KB/ArticleDet?ID=20255), call the **SE37** transaction to access the _Function Builder_ screen.

   ![image](uploads/191133a578de5a8af51f53c4d9574f9b/image.png)

1. Within the _Function Builder_ screen, enter the name of the Function Module and click the **Test/Execute** (![image](uploads/1fc3f72bde530b9e016cc92e0a233473/image.png)) button. Note, using wildcards (\*) will search for all function modules that match the given text.

   ![image](uploads/78826fd85b5d2dd6942cefe1882d8bbf/image.png)

1. You should now see the _Test Function Module_ screen. From here, you can click the **Test data directory** button to access the _Test Data Directory_ screen.

   ![image](uploads/fea64a960d73d28d396809b7dc7d943f/image.png)

1. You should now see the _Test Data Directory_ screen. Clicking **Regression test**(![image](uploads/1fc3f72bde530b9e016cc92e0a233473/image.png)) will immediately execute the function module with the test parameters. Clicking **Delete**  (![image](uploads/952496d8eff7acf3a2f85b41236dc408/image.png)) will delete the selected test. **Double-clicking** on a test or selecting a test and clicking the **Get test data** (![image](uploads/01518785739b625dbc7f00c160471a40/image.png)) button [F2] will take you back to the _Test Function Module_ screen with the test parameters already entered in case you want to review or modify them before executing.

   ![image](uploads/791e9d4de886f866bd663e8fd33262a5/image.png)

## Saving a Test (Variant) in the Test Data Directory

1. Enter the **Import parameters** and **Tables** test values on the _Test Function Module_ screen. Then click the **Save data record** (![image](uploads/9003f9ed9d6dae405be1c7beba7a4a11/image.png)) button.

   ![image](uploads/5d2cd344d3e2e1e8559eb0c98319849a/image.png)

1. Provide a name for the test in the **Comments** field and click the **Save** button. Others will be able to use this name to find and execute your test.

   ![image](uploads/830e350f2658c3e6394f0e8590a86000/image.png)

1. The new test should now appear in the _Test Data Directory_ list of tests.

   ![image](uploads/26e2232d6d6cc13e526e3fb66cdc1058/image.png)

## Tags
[[SAP]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SAPTag)