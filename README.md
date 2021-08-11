# aksbicep

This is still a WIP.

An example to create an AKS cluster with secrets from Azure Key Vault with Bicep and GitHub actions.

Pre-requisites 

* Fork this repository so you can run GitHub Actions

* [Sign up for Azure, $200 free credit](https://cda.ms/2kz)

* Create an Azure Resource Group

* Follow the ["Generate deployment credentials"](https://cda.ms/2kx) and ["Configure the GitHub secrets"](https://cda.ms/2ky) of this guide

* [Create a Key Vault](https://cda.ms/2kB)

* [Store your two parameters as secrets.](https://cda.ms/2kC)

* Update `azuredeploy.parameters.json` with your vault details 

```
 "id": "/subscriptions/{subscriptionID}/resourceGroups/{resource group}/providers/Microsoft.KeyVault/vaults/{keyvault name}"
```

When you commit to the main branch, it will kick off a build.  You'll get an AKS cluster with a service principal.  The cluster will be given a randomized name, however you can add custom ones to the parameters file.

## With Azure CLI

You can execute the following command in the root of the directory with an autheticated Azure CLI.

This example creates a resource group then creates a deployment with ARM.

```
az login 

az group create -n <resource group name> -l <location>

az deployment group create  --name <deployment name>  --resource-group <resource group name> --template-file aks.bicep --parameters='@azuredeploy.parameters.json'
```

