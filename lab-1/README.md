# Lab 1: Accessing Kubernetes cluster

* Download `kubectl` utility for [Windows](https://storage.googleapis.com/kubernetes-release/release/v1.5.3/bin/windows/amd64/kubectl.exe), [Linux](https://storage.googleapis.com/kubernetes-release/release/v1.5.3/bin/linux/amd64/kubectl) or [MacOs](https://storage.googleapis.com/kubernetes-release/release/v1.5.3/bin/darwin/amd64/kubectl)
* Add it to the path
* On Linux and MacOS, make it executable
* Make sure you can use kubectl by running `kubectl help` from your command line

## Configure cluster

Use the configuration details provided by your trainer to configure the cluster access. Cluster hostname, username and password should be provided.

* Add `cluster` named `trainingcluster` to `kubectl` configuration:
```
kubectl config set-cluster trainingcluster --insecure-skip-tls-verify=true --server=<CLUSTER_HOSTNAME>
```

* Add `credentials` named `traininguser` to `kubectl` configuration:
```
kubectl config set-credentials traininguser --username <CLUSTER_USER> --password <CLUSTER_PASSWORD>
```

* Create `context` names `trainingcontext` using the `cluster` and `credentials` to `kubectl` configuration:
```
kubectl config set-context trainingcontext --cluster=trainingcluster --user=traininguser
```

* Instruct `kubectl`:
```
kubectl config use-context trainingcontext
```

## First steps with kubectl

* Check the cluster details:
```
kubectl cluster-info
```

* List cluster nodes:
```
kubectl get nodes
```

* Get details about one of the cluster nodes:
```
kubectl describe node <NODE_NAME>
```
for example:
```
kubectl describe node ip-172-35-106-33.eu-west-1.compute.internal
```

## Use proxy and access the dashboard

* Start the proxy to the Kubernetes cluster
```
kubectl proxy
```

* Open browser and go to `http://127.0.0.1:8001/ui`

* Checkout the Kubernetes Dashboard

## Use proxy and access the dashboard

* Start the proxy to the Kubernetes cluster
```
kubectl proxy
```

* Use your browser or `curl` and explore the APIs. Try for example following URLs:
** `http://127.0.0.1:8001/healthz`
** `http://127.0.0.1:8001/api/v1`
** `http://127.0.0.1:8001/apis`
