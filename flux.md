# Flux setup on AKS

## Register providers

```
az provider register --namespace Microsoft.Kubernetes
az provider register --namespace Microsoft.ContainerService
az provider register --namespace Microsoft.KubernetesConfiguration
```

## Enable k8s extensions

```
az extension add -n k8s-configuration
az extension add -n k8s-extension
```

## Add flux configuration for the cluster

```
az k8s-configuration flux create \
   --name cluster-config \
   --cluster-name ol-flux \
   --namespace default \
   --resource-group flux-demo \
   -u https://arashms.visualstudio.com/java-demo/_git/java-demo \
   --https-user username \
   --https-key pass \
   --scope cluster \
   --cluster-type managedClusters \
   --branch master \
   --kustomization name=cluster-config prune=true path=manifests/overlays/watch-all-namespaces
```

```
az k8s-configuration flux create \
-g flux-demo \
-c ol-flux \
-n apps-config \
--namespace apps \
-t managedClusters \
--scope cluster \
-u https://arashms.visualstudio.com/java-demo/_git/java-demo \
--https-user username \
--https-key pass \
--branch master  \
--kustomization name=apps path=./open-liberty-on-aks/javaee-app-simple-cluster/src/main/aks/test prune=true
```