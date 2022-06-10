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
## Previously
We have developed
- RESTful Web API using .NET 6
- Client Application using Angular

## In this exercise
 We will configure the Azure Active Directory Tenant to use with our applications. For this we will
 - Register our Angular UI and .Net API we before
 - Register application roles
 - Assign roles to the users
 - Expose our API
 - Grant permissions to UI
 - Token Configuration

## Step 1: App Registration
- Login to the [Azure Portal](https://portal.azure.com/) using the credentials.
![1  main page](https://user-images.githubusercontent.com/100778209/167418192-470dfc0a-ef6e-4104-83e9-8d0a9e203709.jpg)

- Search and select **Azure Active Directory** link from the available options.
![](/images/1.jpg)

- Select **Add** and click **App Registration**
![3  Add App Registration](https://user-images.githubusercontent.com/100778209/167418594-4e64c97f-3aec-412e-983d-6395c5e7d33b.jpg)

- Here our you add the following details:
    - Enter a **display Name** for your application. In our case it is  BBBank_UI. Users of your application might see the display name when they use the app, for example during sign-in. You can change the display name at any time and multiple app registrations can share the same name. The app registration's automatically generated Application (client) ID, not its display name, uniquely identifies your app within the identity platform.
    - We will choose **Accounts in this organizational directory only**	Select this option if you're building an application for use only by users (or guests) in your tenant.
    - It is our single page application (SPA) made in angular so we will select the desired option and add URI of local host http://localhost:4200/
![1  App Registration](https://user-images.githubusercontent.com/100778209/167419015-66d4372b-c47f-44b6-b94c-a5516d7250bd.jpg)

- Similarly, for the API, just add user facing display name (BBBank_API) and select the tenant option. Leave the displace name. 
![2  Api Registration](https://user-images.githubusercontent.com/100778209/167419108-16f6b2e8-a2be-488d-988b-ae87aeafd46d.jpg)

-Finally, the registered apps in the active directory listings.
![3  Registered Apps](https://user-images.githubusercontent.com/100778209/167419336-9bb49245-b1b3-43d2-bf05-5c4a41be1aeb.jpg)


## Step 2: Application Role(s) Registration
Now we have assign the roles of our Apps we created. For this click the **App Registrations** from the left hand menu of Azure Active Directory.

Since, our API will implement the authorization for the roles at endpoints. So, select the BBBankAPI from the applications we have already registered. 

- Select the **App Roles** from the navigation menu (left side bar)
![1  App roles](https://user-images.githubusercontent.com/100778209/167421556-85769a60-53eb-4644-bde1-bfc0fa221bb3.jpg)

- Click **Create App Role** button to create a new **App Role**.

- Enter all the required details as as following:
    - **Display name**: Display name for the app role that appears in the admin consent and app assignment experiences. This value may contain spaces. In our case we are assigning it as **Account Holder**
    - **Allowed member types:**	Specifies whether this app role can be assigned to users, applications, or both.
    - **Value:**	Specifies the value of the roles claim that the application should expect in the token. The value should exactly match the string referenced in the application's code. The value cannot contain spaces.
    - **Description:**	A more detailed description of the app role displayed during admin app assignment and consent experiences.
    - **Do you want to enable this app role?**	Specifies whether the app role is enabled. To delete an app role, deselect this checkbox and apply the change before attempting the delete operation.
    - Select **Apply** to save your changes.
![2  Create App role](https://user-images.githubusercontent.com/100778209/167422769-ff2e0518-7732-4420-8569-38cd94196061.jpg)

- Similarly create another App role **Bank Manager** for this application (BBBankAPI)

## Step 3: Assign Role(s) to User(s)
- Go to **Enterprise Applications** from Active Directory AD sidebar menu.

- Select the *BBBankAPI* from the application listing as we have roles in this application
- Click the **Users and Groups** from the left menu bar

- Here select **Add User/Group** and add User and its role.
![image](https://user-images.githubusercontent.com/100778209/167428713-d1f97a80-5138-4e35-bb0d-0025c49a9754.png)
- Then **select user** and add User from your organization to whom you want to assign a role.
- Now select **app role** from the list and assign that user a role we created before. 
- After assigning role to a user we get the result
![image](https://user-images.githubusercontent.com/100778209/167429404-8e5b3ed5-42d8-4d11-a23e-d6765d4c30a4.png)

## Step 4: Expose the API (BBBankAPI)
We have registered our API now we will expose it to client apps by adding an example **scope**. By registering your web API and exposing it through scopes, you can provide permissions-based access to its resources to authorized users and client apps that access your API.

- For this select the API (BBBank_API) we registered before.
- Click on the **Expose API** from left side bar.

- Create a new scope by clicking on **Add a Scope**
- Next, specify the scope's attributes in the Add a scope pane. For this walk-through, you can use the example values or specify your own.
    - **Scope name**. A common scope naming convention is resource.operation.constraint.
    - At the moment, we will use the default options for remaining sections
![2  Add a scope](https://user-images.githubusercontent.com/100778209/167425146-07ca1642-b6a7-4ded-8f8b-583c73e6d8ac.jpg)

- Now **add a client application to the scope** for the API to grant access
- Here you have to to provide your Client ID (*BBBank_UI*) and check scope you created.
- Click **Add application** to save the changes
![image](https://user-images.githubusercontent.com/100778209/167425654-aaa1fc90-6671-41a4-bb18-1a5818ee7388.png)

## Step 5: Grant Permissions to UI (BBBank UI)
Now we grant a client app access to our own web API.

This diagram shows how the two app registrations relate to one another. In this section, you add permissions to the client app's registration.
![](/images/2.jpg)

- Go to App Registrations and select the BBBankUI
- Select the **API Permissions** from the sidebar menu.
- Click **Add a Permission**
Select the API by clicking the **My API** tab
![image](https://user-images.githubusercontent.com/100778209/167426913-b1206129-fef7-4c19-b565-aaa8da2ac1d0.png)

- Select the **BBBankAPI** from the listing and grant the permission, we created before. 
![image](https://user-images.githubusercontent.com/100778209/167427137-4bf5047a-80fe-46d5-bad3-aff3a3021d8c.png)

- Finally **Grant Admin Consent** and click **Ok**
![3  Grant Admin consent](https://user-images.githubusercontent.com/100778209/167427464-e321f8d3-0f47-47d2-baa7-38a410261267.jpg)

## Step 6: Token Configurations
Application developers can use optional claims in their Azure AD applications to specify which claims they want in tokens sent to their application.

You can use optional claims to:

- Select additional claims to include in tokens for your application.
- Change the behavior of certain claims that the Microsoft identity platform returns in tokens.
- Add and access custom claims for your application.

To add claims: 
- Select the **App Registrations** from the Active Directory main menu
- Select **BBBankUI** Application
- Select **Token Configuration** from the left menu bar
- Click on the **Add Optional Claim** and select **Access Token**

![image](https://user-images.githubusercontent.com/100778209/167430278-b38901b9-0508-4e19-998f-54fcef57dfa1.png)

- From this list we have to select the claims which will be available in our **access token**.

-------------------

### Now we have all the necessary Setup for our Apps in Azure Active Directory. In next lab we will configure all our Apps according to this Azure AD. 
