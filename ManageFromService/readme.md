# UWP Add Ons - Troubleshooting: Managing Entitlements from a Service

The documentation for managing entitlements from a service can be found here: [Manage product entitlements from a service - Windows UWP applications](https://docs.microsoft.com/en-us/windows/uwp/monetize/view-and-grant-products-from-a-service).

Use this document to help troubleshoot issues with using the Microsoft Store collection and Microsoft Store purchase REST APIs.

## Quick Checklist:  
## Preparing your UWP app: 
1. If this is a Win32 app, make sure your are initializing the [StoreContext Class (Windows.Services.Store)](https://docs.microsoft.com/en-us/uwp/api/windows.services.store.storecontext) following the documentation here: [Using the StoreContext class with the Desktop Bridge](https://docs.microsoft.com/en-us/windows/uwp/monetize/in-app-purchases-and-trials#using-the-storecontext-class-with-the-desktop-bridge).  
2. Associate your UWP app with the Store. In Visual Studio, right click your project. Select Store | Associate the App with the Store. Select your app from the list or reserve a new app name. You will access this app in the 'Preparing Partner Center' section below.

## Registering an Azure Active Directory Application:  
1.  Complete App Registration with **Azure Active Directory** using your Azure account at http://portal.azure.com.  
    a. Capture the **Application (client) ID**  
    b. Capture the **Directory (tenant) ID**  
    c. Capture the **Client Secret**.

## Preparing Partner Center:
1. In [Partner Center](https://dev.windows.com) (Services > Product collections and purchases) associate your UWP application with the AAD Application **Application (client) ID**.  Note: Per the docs, this can take up to 16 hours to go into effect.

## Get the AAD Token, Collection API token, Purchase API tokens

1. Use the following Postman requests to get the AAD token, Collection API token and Purchase API token: https://documenter.getpostman.com/view/3167620/S1TSafQk.  To use the Postman requests you’ll need to update the variables to match your environment. Note that after a successful return if the AAS access token, it is automatically saved for use in the Authorization header of the Collection or Purchase API requests. 
4. Validate the returned tokens with: https://jwt.io/  
5. Get a fresh AAD bearer token to get a fresh Collection API token using Postman. See the main docs here for additional details: [Manage product entitlements from a service - Windows UWP applications](https://docs.microsoft.com/en-us/windows/uwp/monetize/view-and-grant-products-from-a-service).


## From your UWP app, get the Microsoft Store ID key

1. Get the Collection API token in the step above and pass it to the ```serviceTicket``` parameter of [StoreContext.GetCustomerCollectionsIdAsync(String, String) Method (Windows.Services.Store)](https://docs.microsoft.com/en-us/uwp/api/windows.services.store.storecontext.getcustomercollectionsidasync)      
2. For the REST Purchase API use the Purchase API token received in the step above and pass it to the ```serviceTicket``` parameter of [StoreContext.GetCustomerPurchaseIdAsync(String, String) Method (Windows.Services.Store)](https://docs.microsoft.com/en-us/uwp/api/windows.services.store.storecontext.GetCustomerPurchaseIdAsync)  
3. Note: If these APIs return an empty string, review the above checkpoints. Note that the app registration may not be in effect yet given the 16 hour SLA. 



  