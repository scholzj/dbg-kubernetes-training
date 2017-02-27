# Demo 11: Secrets

* Show the YAML file with Secret
* Create the secret in Kubernetes `kubectl --namespace schojak create -f secret.yaml`
* Show the directory with the config files
* Create a secret from the directors using `kubectl --namespace schojak create secret generic file-based --from-file=certificates/`
* Show how to use the secret in deployment
* Redeploy kuard to show the `kubectl --namespace schojak apply -f deployment.yaml`
* Show the env. variables in kuard as well ad the files
