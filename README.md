# aiwrepository
Azure Immersion Workshop 진행을 위한 실습 코드


**[소스 코드]**
아래 Azure-Sample 코드를 활용하였습니다. 

https://github.com/Azure-Samples/containerize-and-deploy-Java-app-to-Azure.git

**[실습 준비]**
1. Azure 계정에 Login 합니다.
2. Azure CLI Open
3. 변수를 저장합니다.
```
AZ_RESOURCE_GROUP={리소스그룹명}
AZ_CONTAINER_REGISTRY={ACR리소스명}
AZ_KUBERNETES_CLUSTER={AKS리소스명}
AZ_LOCATION=koreacentral
AZ_KUBERNETES_CLUSTER_DNS_PREFIX={PREFIX명}
```
4. 리소스 그룹을 생성합니다.
```
az group create \
    --name $AZ_RESOURCE_GROUP \
    --location $AZ_LOCATION \
    | jq
```
5. Azure Container Registry를 생성합니다.
```
az acr create \
    --resource-group $AZ_RESOURCE_GROUP \
    --name $AZ_CONTAINER_REGISTRY \
    --sku Basic \
    | jq
```

```
az configure \
    --defaults acr=$AZ_CONTAINER_REGISTRY
```

```
az acr login -n $AZ_CONTAINER_REGISTRY
```
6. Azure Kubernetes Service를 생성합니다. 
```
"az aks create \
    --resource-group $AZ_RESOURCE_GROUP \
    --name $AZ_KUBERNETES_CLUSTER \
    --attach-acr $AZ_CONTAINER_REGISTRY \
    --dns-name-prefix=$AZ_KUBERNETES_CLUSTER_DNS_PREFIX \
    --generate-ssh-keys \
    | jq"
```
