# Lab 2: My first application

In this lab, we will deploy our first application and expose it using Amazon AWS Elastic Load Balancer. We will use open source blogging platform Ghost as an example in this lab.

## Namespace

* Create your own namespace
```
kubectl create namespace <NAMESPACE>
```
for example:
```
kubectl create namespace schojak
```
Save namespace into environmental variable, as we are going to use it quite often. This way we make sure, you are always working in your own, isolated namespace. For example
```
export namespace=schojak
```
Check, if the variable is set correctly:
```
echo $namespace
```

* List the deployments, pods:
```
kubectl --namespace $namespace get deployments
kubectl --namespace $namespace get pods
```

* List all namespaces in the cluster
```
kubectl get namespaces
```

## Deploy your first application

* Check the `deployment.yaml` file which describes the deployment

* Deploy Ghost using `kubectl`:
```
kubectl --namespace $namespace create -f deployment.yaml
```

* Check the deployment and the pods
```
kubectl --namespace $namespace get deployments
kubectl --namespace $namespace describe deployment ghost-deployment
kubectl --namespace $namespace get pods
kubectl --namespace $namespace describe pod <POD_NAME>
```

* Use lables to filter through the running pods:
```
kubectl --namespace $namespace get pods -l project=microblogging
kubectl --namespace $namespace get pods -l project=macroblogging
```

* Use `kubectl` to expose the port of your application to your local computer
```
kubectl --namespace $namespace port-forward <POD_NAME> 5000:2368
```

* Open the address http://localhost:5000 in your browser

## Expose your application

* Check the `service.yaml` file which describes the service

* Create service using `kubectl`:
```
kubectl --namespace $namespace create -f service.yaml
```

* Check the service
```
kubectl --namespace $namespace get service
```

* Check the service description to find out the hostname of your application
```
kubectl --namespace $namespace describe service ghost-service
```

* Open the address from your browser (the DNS propagation might take some time)

## Monitoring of your application

* To check the logs of the application, you can either go to the Kubernetes Dashboard or `kubectl`:
```
kubectl --namespace $namespace logs <POD_NAME>
```

* You can also connect into the running container using `kubectl`:
```
kubectl --namespace $namespace exec -ti <POD_NAME> bash
```
