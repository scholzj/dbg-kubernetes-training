# Demo 10: Config Maps

* Show the YAML file with Config Map
* Create the config map in Kubernetes `kubectl --namespace schojak create -f configmap.yaml`
* Show the directory with the config files
* Create a config map from the directory using `kubectl --namespace schojak create configmap file-based --from-file=config/`
* Show how to use the config map in deployment
* Redeploy kuard to show the `kubectl --namespace schojak apply -f deployment.yaml`
* Show the env. variables in kuard as well as the files
