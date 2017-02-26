# Demo 9: Deployments

* Create deployment `kubectl --namespace schojak create -f deployment.yaml`
* Show the running pod using `kubectl --namespace schojak get pods -l app=kuard`
* Scale the replica from command line `kubectl --namespace schojak scale deployment/kuard --replicas 3`
* Show that 3 replicas are running using `kubectl --namespace schojak get pods -l app=kuard`
* Show how to configure replicas in YAML and how to do it in Dashboard
* Delete the pods and show that a new ones are started by the deployment:
```
kubectl --namespace schojak get pods -l app=kuard --watch
kubectl --namespace schojak delete pods -l app=kuard
```
* Show rolling update
  * Scale the deployment to 10 replica `kubectl --namespace schojak scale deployment/kuard --replicas 10`
  * Update the image version `kubectl --namespace schojak set image deployment/kuard kuard=gcr.io/kuar-demo/kuard-amd64:3`
  * Watch the rollout `kubectl --namespace schojak rollout status deployment/kuard --watch`
* Do update which will fail `kubectl --namespace schojak set image deployment/kuard kuard=gcr.io/kuar-demo/kuard-amd64:4`
  * Watch the rollout `kubectl --namespace schojak rollout status deployment/kuard --watch`
  * Check the revision history `kubectl --namespace schojak rollout history deployment/kuard`
  * Rollback to previous revision `kubectl --namespace schojak rollout undo deployment/kuard --to-revision 4`
* Scale down the deployment `kubectl --namespace schojak scale deployment/kuard --replicas 3`
