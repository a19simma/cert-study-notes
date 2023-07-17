# [Implement secure Azure solutions](https://learn.microsoft.com/en-us/training/paths/az-204-implement-secure-cloud-solutions/)

### [Implement Azure Key Vault](https://learn.microsoft.com/en-us/training/paths/az-204-implement-secure-cloud-solutions/)
Common use cases for AKV are:
- Secret management, tokens, passwords etc.
- Key management, encryption keys.
- Certificate Management, SSL/TLS certs. Includes renewal.

Supports access logs for auditing. Use standard Azure AD to authenticate and set permissions with RBAC.

Use managed identities in azure for automatic rotation of the service principle client secret.

- Use separate key vaults: Recommended using a vault per application per environment (Development, Pre-Production and Production). This pattern helps you not share secrets across environments and also reduces the threat if there is a breach.

- Control access to your vault: Key Vault data is sensitive and business critical, you need to secure access to your key vaults by allowing only authorized applications and users.

- Backup: Create regular back ups of your vault on update/delete/create of objects within a Vault.

- Logging: Be sure to turn on logging and alerts.

- Recovery options: Turn on soft-delete and purge protection if you want to guard against force deletion of the secret.

```bash
az group create --name az204-vault-rg --location $myLocation
az keyvault create --name $myKeyVault --resource-group az204-vault-rg --location $myLocation
az keyvault secret set --vault-name $myKeyVault --name "ExamplePassword" --value "hVFkk965BuUv"
az keyvault secret show --name "ExamplePassword" --vault-name $myKeyVault
```

### [Implement managed identities](https://learn.microsoft.com/en-us/training/modules/implement-managed-identities/)
System-assigned identities are tied to the azure service instance like a container, it is created and removed in tandem 
with the service's lifecycle.

User-assigned identities are a standalone azure resource. The identity can then be assigned to one or more azure service
instances.

Retrieving an app-only access token to access resources:
```csharp
// Create a secret client using the DefaultAzureCredential
var client = new SecretClient(new Uri("https://myvault.vault.azure.net/"), new DefaultAzureCredential());
```

### [Implement App Configuration](https://learn.microsoft.com/en-us/training/modules/implement-azure-app-configuration/)
Simple key value store. Also supports feature flags and lifecycle management/refreshes of those feature flags. Changing
state of the flag in azure allows management without redeploying.


