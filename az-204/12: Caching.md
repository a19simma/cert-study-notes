# [Caching](https://learn.microsoft.com/en-us/training/paths/az-204-integrate-caching-content-delivery-within-solutions/)

### [Redis](https://learn.microsoft.com/en-us/training/modules/develop-for-azure-cache-for-redis/)
Both OSS Redis and Redis Enterprise. 

Key Scenarios for using Redis Cache:
- Data Cache instead of querying a database
- Content Cache for static content on a website
- Session Store used for user data in active sessions
- Job and Message queues can be implemented in Redis
- Transactions, like sagas are statemachines for distributed wordloads.

Service Tiers:
- Basic
- Standard, OSS Redis with replication. Lowest cost prod
- Premium, OSS Redis on VMs
- Enterprise, Redis Enterprise

Always place the cache in the same region as the application. Uses access keys for authentication.

Redis ConnectionString:
`[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False`

Create a redis instace in Azure:
```bash
redisName=az204redis$RANDOM
az redis create --location <myLocation> \
    --resource-group az204-redis-rg \
    --name $redisName \
    --sku Basic --vm-size c0
```

```csharp
using (var cache = ConnectionMultiplexer.Connect(connectionString))
{
    IDatabase db = cache.GetDatabase();

    // Snippet below executes a PING to test the server connection
    var result = await db.ExecuteAsync("ping");
    Console.WriteLine($"PING = {result.Type} : {result}");

    // Call StringSetAsync on the IDatabase object to set the key "test:key" to the value "100"
    bool setValue = await db.StringSetAsync("test:key", "100");
    Console.WriteLine($"SET: {setValue}");

    // StringGetAsync retrieves the value for the "test" key
    string getValue = await db.StringGetAsync("test:key");
    Console.WriteLine($"GET: {getValue}");
}
```

### [CDN](https://learn.microsoft.com/en-us/training/modules/develop-for-storage-cdns/)
Managed content cache for the edge. Freshness of cached content is evaluated based on the pre-defined
constant time to live. Upon which the content is requested again from the origin server. The Cache-Control
header contained in the HTTP response from origin server determines the TTL duration.

Manually purge a caching endpoint:
```bash
az cdn endpoint purge \
    --content-paths '/css/*' '/js/app.js' \
    --name ContosoEndpoint \
    --profile-name DemoProfile \
    --resource-group ExampleGroup
```
