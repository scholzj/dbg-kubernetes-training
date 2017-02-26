# Demo 8: Pods and Labels

* Deploy pod:
```
kubectl --namespace schojak create -f pod.yaml
```
* Show running pod using `kubectl --namespace schojak get pods`
* Show pod details `kubectl --namespace schojak describe pod nginx`
* Show listing pods by labels `kubectl --namespace schojak get pods -l app=nginx` versus `kubectl --namespace schojak get pods -l app=somethingelse`
* Show how to add labels `kubectl --namespace schojak label pod nginx something=something`
* Show how to remove labels `kubectl --namespace schojak label pod nginx something-`
* Show `kubectl` port forwarding
```
kubectl --namespace schojak port-forward nginx 5000:80
```
* Open [http://localhost:5000](http://localhost:5000) from the browser to show the running nginx server
* Show Nginx logs using `kubectl`
```
kubectl --namespace schojak logs nginx
```
* Exec into the container
```
kubectl --namespace schojak exec -ti nginx bash
```
* Explain what happens when the process inside the container is killed (Container is restarted)
* Delete the pod and show that it is not recreated
