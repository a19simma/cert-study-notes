# [CosmosDB](https://learn.microsoft.com/en-us/training/paths/az-204-develop-solutions-that-use-azure-cosmos-db/)

### [Explore](https://learn.microsoft.com/en-us/training/modules/explore-azure-cosmos-db/)
Cosmos is a multi-master distributed database. Containers for databases can be dedicated with an SLA backing
or shared throughput mode which shares the databases' configured throughput between all the shared containers.
A container supports multiple different paradigms, such as collection, table and graph in the same database.

Conistency levels are key to replication and performance of the data base: ![consistency level](https://learn.microsoft.com/en-us/training/wwl-azure/explore-azure-cosmos-db/media/five-consistency-levels.png)
The consistency levels from Strong, which guarantees the user to always read the latest committed item,
to come level of latency by a specified amount. To Eventual, which *eventually* reaches consistency.

The NoSQL API is the native option for Cosmos, but it also implements protocols such as postgres and cassandra.
Costs in Cosmos are calculated by RUs *request units*, which are resource metrics from Memory, CPU and IOPS usage for the given operation.

### [Work](https://learn.microsoft.com/en-us/training/modules/work-with-cosmos-db/)
You can write User Defined Functions and store procedures in Javascript. Cosmos provides a feed of changes,
like a normal database operations log. These changes can for example trigger an azure functions when an item is created.
