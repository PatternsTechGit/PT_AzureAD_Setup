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
Previously we have

In this exercise we will


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


## Step No. 2:

## Step No. 3:

## Step No. 4:

## Step No. 5:

## Step No. 6:

## Step No. 7:
