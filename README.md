# Azure AD Setup for Authentication
The [Azure portal](https://portal.azure.com/#allservices) is a web-based, unified console that provides an alternative to command-line tools. With the Azure portal, we can manage your Azure subscription using a graphical user interface (GUI). We can build, manage, and monitor everything from simple web apps to complex cloud deployments.

## What is Azure Active Directory (AD)
Azure Active Directory (Azure AD) is a Microsoft's multi-tenant, cloud-based directory and identity management service. This service helps to access external resources, such as Microsoft 365, the Azure portal, and thousands of other SaaS applications.

### Azure AD Tenant
A tenant represents an organization / group of people. It's a dedicated instance of Azure AD that an organization or app developer receives at the beginning of a relationship with Microsoft. Each tenant has its own representation of work and school identities, consumer identities.
An app registration inside your tenant can allow authentications only from accounts within your tenant or all tenants.

### Azure AD B2C
[Azure Active Directory B2C](https://docs.microsoft.com/en-us/azure/active-directory-b2c/) provides business-to-customer identity as a service. Your customers use their preferred social, enterprise, or local account identities to get single sign-on access to your applications and APIs.

![image](https://user-images.githubusercontent.com/100778209/167414618-e6588a6a-eada-4e06-b638-31bd06757f4c.png)

Azure AD B2C is a separate service from Azure Active Directory (Azure AD). It is built on the same technology as Azure AD but for a different purpose. It allows businesses to build customer facing applications, and then allow anyone to sign up into those applications with no restrictions on user account.

### Azure AD B2B
[Azure Active Directory B2B](https://docs.microsoft.com/en-us/azure/active-directory/external-identities/what-is-b2b) is a feature within External Identities that lets you invite guest users to collaborate with your organization. With B2B collaboration, you can securely share your company's applications and services with guest users from any other organization, while maintaining control over your own corporate data.

![image](https://user-images.githubusercontent.com/100778209/167415199-4b9110b8-8c7b-4355-9e71-30b08eed8469.png)

Developers can use Azure AD business-to-business APIs to customize the invitation process or write applications like self-service sign-up portals.
## About this exercise
Previously we have developed
- RESTful Web API using .NET 6
- Client Application using Angular

In this exercise we will configure the Azure Active Dicrectory Tenant to use with our applications.

## Step No. 1: App Registration
Login to the [Azure Portal](https://portal.azure.com/) using the credentials.
![1  main page](https://user-images.githubusercontent.com/100778209/167418192-470dfc0a-ef6e-4104-83e9-8d0a9e203709.jpg)

Select the Azure Active Directory link from the available options.
![2  Azure AD](https://user-images.githubusercontent.com/100778209/167418431-4f7f9f2f-c9fd-40e6-9eac-10c143cdb5bc.jpg)

From the menu select Add -> App Registration
![3  Add App Registration](https://user-images.githubusercontent.com/100778209/167418594-4e64c97f-3aec-412e-983d-6395c5e7d33b.jpg)

Enter the details (User facing display name and redirect URI in case of SPA i.e., the angular application ) 
![1  App Registration](https://user-images.githubusercontent.com/100778209/167419015-66d4372b-c47f-44b6-b94c-a5516d7250bd.jpg)

Similarly, for the API just the user facing display name is required
![2  Api Registration](https://user-images.githubusercontent.com/100778209/167419108-16f6b2e8-a2be-488d-988b-ae87aeafd46d.jpg)

Finally, the registered apps in the active directory listings;
![3  Registrered Apps](https://user-images.githubusercontent.com/100778209/167419336-9bb49245-b1b3-43d2-bf05-5c4a41be1aeb.jpg)


## Step No. 2: Application Role(s) Registration
Click the "App Registrations" from the main menu of Azure Active Directory.

Since, our API will implement the authorization for the roles at endpoints. So, select the BBBankAPI from the applications we have already registered. 

Select the **App Roles** from the navigation menu (left side bar)

![1  App roles](https://user-images.githubusercontent.com/100778209/167421556-85769a60-53eb-4644-bde1-bfc0fa221bb3.jpg)

Click **Create App Role** button to create a new **App Role**.

Enter all the required details as in case of **Account Holder** following settings are entered.
![2  Create App role](https://user-images.githubusercontent.com/100778209/167422769-ff2e0518-7732-4420-8569-38cd94196061.jpg)

Similarly create another App role **Bank Manager** for this application (BBBankAPI)

## Step No.3: Assing Role(s) to User(s)
Go to **Enterprise Applications** from Active Directory AD sidebar menu
Select the BBBankAPI from the application listing as we have roles in this application
Click the **Users and Groups** from the left menu bar

Then **select user** and then select **app role** from the list
![image](https://user-images.githubusercontent.com/100778209/167428713-d1f97a80-5138-4e35-bb0d-0025c49a9754.png)

After assigning role to a user we get the result
![image](https://user-images.githubusercontent.com/100778209/167429404-8e5b3ed5-42d8-4d11-a23e-d6765d4c30a4.png)

## Step No. 4: Expose the API (BBBankAPI)
Click on the **Expose API** from left side bar.

Create a new scope by clicking on **Add a Scope**
![2  Add a scope](https://user-images.githubusercontent.com/100778209/167425146-07ca1642-b6a7-4ded-8f8b-583c73e6d8ac.jpg)

Add a client application to the scope for the API to grant access
![image](https://user-images.githubusercontent.com/100778209/167425654-aaa1fc90-6671-41a4-bb18-1a5818ee7388.png)

## Step No. 5: Grant Permissions to UI (BBBank UI)
Go to App Registrations and select the BBBankUI
Select the **API Permissions** from the sidebar menu.
Click **Add a Permission**
Select the API by clicking the **My API** tab
![image](https://user-images.githubusercontent.com/100778209/167426913-b1206129-fef7-4c19-b565-aaa8da2ac1d0.png)

Select the **BBBankAPI** from the listing
Grant the permission as under
![image](https://user-images.githubusercontent.com/100778209/167427137-4bf5047a-80fe-46d5-bad3-aff3a3021d8c.png)

Finally **Grant Admin Consent** and click **Ok**
![3  Grant Admin consent](https://user-images.githubusercontent.com/100778209/167427464-e321f8d3-0f47-47d2-baa7-38a410261267.jpg)

## Step No. 5: Token Configurations
Select the **App Registrations** from the Active Directory main menu
Select **BBBankUI** Application
Select **Token Configuration** from the left menu bar
Click on the **Add Optional Cliam** and select **Access Token**

![image](https://user-images.githubusercontent.com/100778209/167430278-b38901b9-0508-4e19-998f-54fcef57dfa1.png)

From this list we have to select the claims which will be available in our **access token**.
