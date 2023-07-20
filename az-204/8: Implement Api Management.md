# [Api Management](https://learn.microsoft.com/en-us/training/paths/az-204-implement-api-management/)

### [Explore](https://learn.microsoft.com/en-us/training/modules/explore-api-management/)
APIs are grouped under products in azure. Subscribe to the product to access the API.
The management is made up of the Gateway, Management Plane and the Dev Portal.

- The API gateway is the endpoint that:
  - Accepts API calls and routes them to appropriate backends
  - Verifies API keys and other credentials presented with requests
  - Enforces usage quotas and rate limits
  - Transforms requests and responses specified in policy statements
  - Caches responses to improve response latency and minimize the load on backend services
  - Emits logs, metrics, and traces for monitoring, reporting, and troubleshooting

- The management plane is the administrative interface where you set up your API program. Use it to:
  - Provision and configure API Management service settings
  - Define or import API schema
  - Package APIs into products
  - Set up policies like quotas or transformations on the APIs
  - Get insights from analytics9
  - Manage users

- The Developer portal is an automatically generated, fully customizable website with the documentation of your APIs. Using the developer portal, developers can:
  - Read API documentation
  - Call an API via the interactive console
  - Create an account and subscribe to get API keys
  - Access analytics on their own usage
  - Download API definitions
  - Manage API keys

Api Management exists in a Managed and Self-hosted variation.

[Policies](https://learn.microsoft.com/en-us/training/modules/explore-api-management/5-create-advanced-policies) 
contain too many examples and syntax. Check the link. 


