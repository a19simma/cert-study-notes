# [Azure App Service](https://learn.microsoft.com/en-us/training/paths/create-azure-app-service-web-apps/)

### [Explore](https://learn.microsoft.com/en-us/training/modules/introduction-to-azure-app-service/)
App service is a hosting method which features a full integrated framework as the runtime.
But there is support for custom linux containers. 

- Shared Compute: Free and Shared
- Dedicated Compute: Basic, Standard, PremiumV1-3
- Isolated: IsolatedV1-2

Deployment slots allow you to do red-green deployment to staging before swapping prod.

The builtin authentication and authorization acts as middleware, processing requests before they arrive at your service. Submitting the auth token from a provider which is then validated by the built in auth and returns its new authentication token which is used to provide authorization to the service. There is a Token store in the management page of the service.

The network features of App services are behind a managed network. You need to specify network proxy services to handle inbound and outbound calls. **App-assigned address** and **Hybrid Connections** are examples of this.

### [Configure](https://learn.microsoft.com/en-us/training/modules/configure-web-app-settings/)
Overrides appsettings.json in aspnet.


