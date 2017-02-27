# Demo 17: Autoscaling

* Shoud the YAML file
* Apply changes to the kuard Deployment `kubectl --namespace schojak apply -f deployment.yaml`
* Add the autoscaler `kubectl --namespace schojak apply -f hpa.yaml`
* Show the HPA in Dashboard and show the results

* Start Ubuntu container `kubectl run --namespace=schojak --rm -ti --image ubuntu bash`
* Install Apache performance test `apt-get update && apt-get install -y apache2-utils`
* Run performance test `ab -v 2 -n 1000000 -c 100 http://ac038685efceb11e699720aba288c0c9-663655579.eu-west-1.elb.amazonaws.com/`
* Show how it scales
