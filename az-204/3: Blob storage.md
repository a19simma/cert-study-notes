# [Blob Storage](https://learn.microsoft.com/en-us/training/paths/develop-solutions-that-use-blob-storage/)

### [Explore](https://learn.microsoft.com/en-us/training/modules/explore-azure-blob-storage/)
Blob storage is optimized for storing massive amounts of *unstructured* data. The data is accessed over HTTP/HTTPS.
Standrad tier uses HDD and Premium SSDs. Hot, Cool and Archive Access Tiers affect the retrieval latency and cost. 
The storage is cheapest per storage unit in the archive tier, but retrieving the data is comparably expensive and can
take hours. 

Types of blobs:
- Block, used for inidividual data like text and binary files.
- Append, optimized for append actions like logging.
- Page, used for random access like a VHD for VMs.

Access can be granted with Azure AD and RBAC is supported for storage. Encryption can use MS managed keys or your own.
Customer provided keys can provide more granular control of data access as it includes the encryption key with every
request as opposed to Customer Managed keys which encrypt the entire storage account.

Storage can be used to host static websites by enabling it in the options.

### [Manage](https://learn.microsoft.com/en-us/training/modules/manage-azure-blob-storage-lifecycle/)
Lifecycle management allows you to set policies to transition data blobs between access tiers. E.g. go from Hot to Archive
after 30 days to decrease costs. Perhaps to clean up and remove old data which is not needed anymore.

Example of ruleset:
```json
"rules": [
    {
      "name": "ruleFoo",
      "enabled": true,
      "type": "Lifecycle",
      "definition": {
        "filters": {
          "blobTypes": [ "blockBlob" ],
          "prefixMatch": [ "container1/foo" ]
        },
        "actions": {
          "baseBlob": {
            "tierToCool": { "daysAfterModificationGreaterThan": 30 },
            "tierToArchive": { "daysAfterModificationGreaterThan": 90 },
            "delete": { "daysAfterModificationGreaterThan": 2555 }
          },
          "snapshot": {
            "delete": { "daysAfterCreationGreaterThan": 90 }
          }
        }
      }
    }
  ]
```
To read a data blob in the archive tier you must first rehydrate it from the offline storage state by moving it into cool
or hot. The recommended way of doing this is by making a copy into an online tier blob. Changing an offline tier to online
may immediately trigger lifecycle policies to archive it again as it does not change the last modified date.

### [Working With](https://learn.microsoft.com/en-us/training/modules/work-azure-blob-storage/)
Using the csharp SDK this seems pretty straightforward: 
```csharp
using Azure.Identity;
using Azure.Storage.Blobs;

public BlobServiceClient GetBlobServiceClient(string accountName)
{
    BlobServiceClient client = new(
        new Uri($"https://{accountName}.blob.core.windows.net"),
        new DefaultAzureCredential());

    return client;
}
```
This object then contains helper methods to interact with policies, containers and blobs. These things can also be
done using the AZ cli or simple REST methods.
