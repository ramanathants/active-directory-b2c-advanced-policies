This sample demonstrate one approach to create a just in time migration policy.
NOTE: This advanced b2c policy is relatively complex, not a great place to begin learning.  Complete the labs -available elsewhere in this repo before tackling JIT.

The user is migrated from an Azure SQL data store (userprofileapi.azurewebsites.net) into a the b2c tenant (casalaolab2c.onmicrosoft.com) as part of what appears to the user to be a normal signin journey.The userid and password provided by the user during the login session is used in a  REST API call to an azure app (Visual studio project included as Contoso.B2C.WebApi) which reads and writes to the SQL Data store. This web app also creates users in the directory (casalaola.onmicrosoft.com),mapping existing claims to new directory, in effect migrating the user just in time without disruption.

General steps to repro experience:

1. Configure the advanced policies complete with its trustframework in the advanced tenant.
1a. B2C_1A_Demo_Base - you will need to update the app credentials to read/write from your directory - search for STS.
1b. B2C_1A_Demo_SungupOrSignin

2. Open the project (Contoso.B2C.WebApi).  The file packages.7z has the specific binaries/ package versions I used, you would place these contents in the packages directory of the VS project (if needed).

3. Create the Azure sql database (or use existing store) -note the structure of the DB is important.  You must create a table (see CreateB2CTable under Models folder)  (Microsoft SQL Server Management Studio 2016 was used to edit the database and create demo users)

4. Update web.config  in the project to include credentials to access database [NOTE: The sample project uses the EntityFramework to control the database - when you publish the project make sure that Visual Studio does not overwrite your webconfig settings, you have to disable this wizard]

5. Update web.config to include the app-based credentials to give the web app access to the user store via Graph

6. Review powerpoint included to review the meaning of "status"

7. Create a few users to be migrated . see Excel for sample8. Invoke policy B2C_1A_Demo_SignuporSignin to test.9. Login one of the demo users and they should migrate to the b2c tenant
