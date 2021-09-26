# Add AKS Admin Group IDs using Azure Policy

This guide covers the approach to add `AdminGroupIDs` to AKS clusters using Azure Custom Policy. This requires `ManagedAAD` feature enabled on AKS clsuters.

## Setup Environment Defaults

```sh
SUBSCRIPTION_ID=<my-subsscription-id>
RESOURCE_GROUP=<my-aks-rg>
LOCATION=eastus2
CLUSTER_NAME=<my-aks-cluster>
```

## Create AKS Admin Group

```sh
az ad group create \
    --display-name ${CLUSTER_NAME}-admin-group \
    --mail-nickname ${CLUSTER_NAME}-admin \
    --description "Administrator group for managing AKS cluster"

ADMIN_GROUP_OBJECT_ID=$(az ad group show --group ${CLUSTER_NAME}-admin-group --query objectId -o tsv)
```

## Create AKS Cluster with Managed AAD

```sh
az group create \
    --name $RESOURCE_GROUP \
    --location $LOCATION
az aks create \
    --resource-group $RESOURCE_GROUP \
    --name $CLUSTER_NAME \
    --enable-managed-identity \
    --enable-aad \
    --network-plugin azure \
    --kubernetes-version 1.21.2
```