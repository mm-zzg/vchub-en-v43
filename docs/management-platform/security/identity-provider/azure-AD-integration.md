# Azure AD integration with MFA

The VC Hub  identity provider is compatible with Azure AD, enabling seamless integration. By leveraging Azure AD's multi-factor authentication (MFA) capability, the identity provider can extend MFA support to the VC Hub thereby enhancing security indirectly.

1. Open the Azure portal from Url: [ https://portal.azure.com/]( https://portal.azure.com/) , then open the Microsoft Entra ID.

    ![alt text](10.png)

2. Click the menu itme "App registration" in the left panel, then click the "+ New registration" icon.

    ![alt text](11.png)

3. Click the "Authentication" menu item in the left panel,  then fill the VC Hub login url and logout url into the "Web Redirect URIs" panel.

    ![alt text](12.png)

4. Click the menu item "Token configuration",  add the optional claim.

    ![alt text](13.png)

5. Click the menu item "Certificates & secrets", and a pair of client id and client secret.

    ![alt text](14.png)

6.  Copy the client id and client secret. 

    ![alt text](15.png)

7. Click the menu item "Overview" from the left panel, then click the "Endpoints" icon and copy the "OpenID Connect metadata document" Url

    ![alt text](16.png)

8. Back to the root path of "Microsoft Entra ID",  then click the "Users" menu item 

    ![alt text](17.png)

9. Click the "Per-user MFA" icon, 

    ![alt text](18.png)

10. Select the users and click the "Enable MFA" button, then MFA is enabled for the selected users. 

    ![alt text](19.png)

11. Navigate to VC Hub identity provider page, then create a new provider with the client id, client secret and openId onnecct meta docuemnt Url

    ![alt text](20.png)

12. Click the "Login Test" of the AzureAD provider, then current page is  navigated to Microsoft login page.

    ![alt text](21.png)

    ![alt text](22.png)

13. Enter the personal user account or domain account, then login page shows the random number used to verify the user account.

    ![alt text](23.png)

14. Enter the number into the Microsoft Authenticator on the mobile phone, then login request is auhenticated.

    ![alt text](24.png)



  

