ARMOAuth
========
This demonstrates OAuth workflow where users grant access to their ARM (Azure Resource Management) to third party site.

Instructions
============
1. Clone this repository to your local drive.
2. Open `ARMOAuth.sln` with VS 2012+ and compile.
3. Before runnin the project, you need to create AAD application and adjust AAD related settings described below.

Create AAD application
======================
1. Goto [Azure Portal](https://manage.windowsazure.com/) and create AAD Application.  You may create an application on existing AAD directory or a new directory altogether.
2. Select `Add an application my organization is developing`
3. Enter any name for application name.
4. Select `WEB APPLICATION AND/OR WEB API`
5. Enter `https://localhost:44300/` as `SIGN ON URL` 
6. Enter `https://<tenant-name>/` as `APP ID URL`.  This is required in order to enable `APPLICATION IS MULTI-TENANT`.  The value should be in form of `https://<mytenant>.onmicrosoft.com/`.  You can find this information on the address URL of the portal above (look for path with @<mytenant>.onmicrosoft.com).
7. Once created, click `CONFIGURE` tab
8. Select YES for `APPLICATION IS MULTI-TENANT` and save.
10. On `Permission to other applications`, add `Windows Azure Management API` and check `Access Azure Service Management` for `Delegated Permissions` and save.
11. On `Keys` section, create a client secret and give it 2 years expiration.   You must save the `key` value somewhere since Portal will not display this again.

Test with localhost
===================
2. Open `ARMOAuth.sln` with VS 2012+.
2. Copy `CLIENT ID` of your AAD application and paste it in [this line](https://github.com/suwatch/ARMOAuth/blob/master/Modules/ARMOAuthModule.cs#L26).
3. Copy `key` (client secret) and paste it in [this line](https://github.com/suwatch/ARMOAuth/blob/master/Modules/ARMOAuthModule.cs#L31).
4. Build and run the project.
5. On browser, it should redirect to login page.
6. Enter AAD account and password.  
  Note: try account that is not in the same directly as the application.  
  Note: currently this does not work with MSA account.
7. You should be prompt with OAuth allow/deny page, do accept it.

Test ARM apis
=============
1. `https://localhost:44300/token` - show current token details.
2. `https://localhost:44300/tenants` - show all tenants (AAD directory) user belongs to.
3. `https://localhost:44300/tenants/<tenant-id>` - to switch tenant.
4. `https://localhost:44300/subscriptions` - list subscriptions.
5. `https://localhost:44300/subscriptions/<sub-id>/resourceGroups` - list resourceGroups for a subscription.
6. `https://localhost:44300/subscriptions/<sub-id>/resourceGroups/<resource>/providers/Microsoft.Web/sites` - list sites.
7. and so on.. 

Test with Azure Websites
========================
1. Simply click below button.<br/>
   [![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/).
  - Enter the Site Name or use the auto-generated one.
  - Enter `CLIENT ID` as AADClientID settings.
  - Enter `key` as AADClientSecret settings.
  - Click Next and Deploy
2. Go back to the AAD application on Azure Portal and add the site https url (such as https://<sitename>.azurewebsites.net) as the reply URL for AAD application.
3. Simply browse to your site
  
Any issue, do let me know.
