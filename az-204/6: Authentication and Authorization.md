# [Authentication and Authorization](https://learn.microsoft.com/en-us/training/paths/az-204-implement-authentication-authorization/)

### [Explore](https://learn.microsoft.com/en-us/training/modules/explore-microsoft-identity-platform/)
Microsoft Idenity platform implements OAuth 2.0 which allows applications to access resources on behalf of the user.
**Delegated permissions** are used when an application has a signed in user. Meaning the application *acts* as the user.
**App-only access persmissions** run without a signed in user and thus need administrator consent, probably tied to 
a service account of some sort.

The application object describes three aspects of an application: how the service can issue tokens in order to access
the application, resources that the application might need to access, and the actions that the application can take.

There are three types of service principals which define the acess policy:
- Application, is the local representation of an application object.
- Managed identity, represents a managed identity and can not be modified
- Legacy

Apps may have to handle Conditional Access when the permissions are not guaranteed. E.g. a user may have read or write 
permissions or not. **on-behalf-of** services sits in the middle of direct user application and the intended API. It forwards
the token from the user and responds with the challenge needed to be solved by the user.

### [MSAL](https://learn.microsoft.com/en-us/training/modules/implement-authentication-by-using-microsoft-authentication-library/)
MSAL.js handles authentication tokens, refreshes and caches to simplify authentication for an application.

Simple example in dotnet, using the builder:
```csharp
IPublicClientApplication app = PublicClientApplicationBuilder.Create(clientId).Build();
```

### [Shared Access Signature](https://learn.microsoft.com/en-us/training/modules/implement-shared-access-signatures/)
A shared access signature (SAS) is a URI that grants restricted access rights to Azure Storage resources. 
You can provide a shared access signature to clients that you want to grant delegate access to certain storage account resources.

Types of SAS:
- User delegation, uses Azure AD
- Service, uses a storage account key
- Account, same as service but can give access to a group of resources tied to the account

Seems like a homebaked version of JWT.

Commonly used to secure access to blob storage in applications.

### [Microsoft Graph](https://learn.microsoft.com/en-us/training/modules/microsoft-graph/)
GraphQl with integration to microsoft's cloud and 365, simple example app:
```csharp
var scopes = new[] { "User.Read" };

// Multi-tenant apps can use "common",
// single-tenant apps must use the tenant ID from the Azure portal
var tenantId = "common";

// Value from app registration
var clientId = "YOUR_CLIENT_ID";

// using Azure.Identity;
var options = new TokenCredentialOptions
{
    AuthorityHost = AzureAuthorityHosts.AzurePublicCloud
};

// Callback function that receives the user prompt
// Prompt contains the generated device code that you must
// enter during the auth process in the browser
Func<DeviceCodeInfo, CancellationToken, Task> callback = (code, cancellation) => {
    Console.WriteLine(code.Message);
    return Task.FromResult(0);
};

// https://learn.microsoft.com/dotnet/api/azure.identity.devicecodecredential
var deviceCodeCredential = new DeviceCodeCredential(
    callback, tenantId, clientId, options);

var graphClient = new GraphServiceClient(deviceCodeCredential, scopes);
```

Use the Authorization request header as a bearer token. Depending on your terms of use, don't store the data locally 
as this might violate Microsoft's terms of use.
