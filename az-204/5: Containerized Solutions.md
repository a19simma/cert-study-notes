# [Containerized Solutions](https://learn.microsoft.com/en-us/training/paths/az-204-implement-iaas-solutions/)

### [Manage](https://learn.microsoft.com/en-us/training/modules/publish-container-image-to-azure-container-registry/)
Azure Container Registry is a private docker repository. It has Basic, Standard and Premium tier depending on the usage
requirements. ACR Tasks allows you to automate container building and pushing based on source code changes, base image, 
or time based schedules.

Docker example file:
```docker
# Use the .NET 6 runtime as a base image
FROM mcr.microsoft.com/dotnet/runtime:6.0

# Set the working directory to /app
WORKDIR /app

# Copy the contents of the published app to the container's /app directory
COPY bin/Release/net6.0/publish/ .

# Expose port 80 to the outside world
EXPOSE 80

# Set the command to run when the container starts
CMD ["dotnet", "MyApp.dll"]
```

Create a resource group and registry:

```bash
az group create --name az204-acr-rg --location <myLocation>

az acr create --resource-group az204-acr-rg --name <myContainerRegistry> --sku Basic

az acr build --image sample/hello-world:v1  \
    --registry <myContainerRegistry> \
    --file Dockerfile .

az acr repository list --name <myContainerRegistry> --output table
```

### [Run](https://learn.microsoft.com/en-us/training/modules/create-run-container-images-azure-container-instances/)
Azure Container Instances is the simplest way to run a single container, exposed to the internet with a FQDN.
A container group is a collection of containers, schedules on the same host like a pod. 

Create a container:
```bash
az container create --resource-group az204-aci-rg 
    --name mycontainer 
    --image mcr.microsoft.com/azuredocs/aci-helloworld 
    --ports 80 
    --dns-name-label $DNS_NAME_LABEL --location <myLocation>
```

### [Container Apps](https://learn.microsoft.com/en-us/training/modules/implement-azure-container-apps/)
Container apps run on AKS but you do not have to manage a cluster. You can create resources the same way you would in a 
k8s cluster, scale based on any KEDA scaler etc. 

```bash
az extension add --name containerapp --upgrade

az provider register --namespace Microsoft.App

az provider register --namespace Microsoft.OperationalInsights

myRG=az204-appcont-rg
myLocation=<location>
myAppContEnv=az204-env-$RANDOM

az group create \
    --name $myRG \
    --location $myLocation

az containerapp env create \
    --name $myAppContEnv \
    --resource-group $myRG \
    --location $myLocation

az containerapp create \
    --name my-container-app \
    --resource-group $myRG \
    --environment $myAppContEnv \
    --image mcr.microsoft.com/azuredocs/containerapps-helloworld:latest \
    --target-port 80 \
    --ingress 'external' \
    --query properties.configuration.ingress.fqdn
```
The last command returns a link to the external ingress.

```bash
az group delete --name $myRG
```
Container apps only run linux images.
