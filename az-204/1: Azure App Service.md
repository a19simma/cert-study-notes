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
Overrides appsettings.json in aspnet and are passed in as environment variables in other cases.
Appsettings are generally bound to a specific deployment slot. Connection strings are generally not used except for aspnet apps. General settings configure the language stack, platform settings and tls as opposed to the appsettings.

You can mount storage to the custom containers or add virtual paths to the app root in windows apps.

Windows application logs can write to blob storage whereas containers can only be written to the filesystem, presumably to a mounted blob storage. However you must specifiy the retention preiod and quota, which seems strange. 

App services can use certificates ranging from managed in the service to uploading your own public one. The best way is probably saving one in the key vault and importing it. Using the managed certificate is not supported in the free tier. 

### [Scale](https://learn.microsoft.com/en-us/training/modules/scale-apps-app-service/)
Seems trivial. Uses application metrics to scale in and out, such as CPU, Memory or HTTP requests. Set an appropriate margin between scale in and out rules. Scaling in calculates metrics with the possibly removed instance to prevent constant scaling in and out.

### [Deployment Slots](https://learn.microsoft.com/en-us/training/modules/understand-app-service-deployment-slots/)
Deployment slots act as a staging environment which trafic is directed to when a swap is made. Kinda like red-green deployment. Facilitating testing, warm ups and rollbacks. The services in the slot restart with the new configurations of the slot it's being swapped into. E.g. staging applies production settings and restart before swapping to becoming the new production. 

You can route a percentage of the trafic to a certain deployment slot to do AB testing or canary deployment. The slot to use is pinned for the lifetime of a client session by a cookie in the http header `x-ms-routing-name`. This can also be done manually via a query parameter.
