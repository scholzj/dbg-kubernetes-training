# Demo 7: Namespaces

* Create a namespace using `kubectl`:
```
kubectl create namespace schojak
```
* List the namespaces:
```
kubectl get namespaces
```
* List pods from the new namespace
```
kubectl --namespace schojak get pods
```
* List pods from the `kube-system` namespace
```
kubectl --namespace kube-system get pods
```
* Show how to create namespace from YAML file
```
kubectl create -f namespace.yaml
```
* Show how to work with namespaces in Dashboard
* Show how to delete the namespace
```
kubectl delete namespace schojak2
```
