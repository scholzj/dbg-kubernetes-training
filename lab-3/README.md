# Lab 3: Multi-tier application

In this lab, we will deploy a multi-tier application which is using database with persistent storage. We will user Etherpad and MySQL.  

Before you start, make sure, that you got `$namespace` set correctly in your environmental variable.
```
echo $namespace
```

## Deploy MySQL database

* Check the `mysql.configmap.yaml` file which describes the configuration map for the MySQL database

* Create the config map in Kubernetes cluster using using `kubectl`:
```
kubectl --namespace $namespace create -f mysql.configmap.yaml
```

* Enter the passwords for the database root account and normal account in `passwords/root_password.txt` and `passwords/password.txt`. Make sure the password files don't contain any empty lines on the beginning or the end of the file.

* Generate a secret using the password files and `kubectl`:
```
kubectl --namespace $namespace create secret generic mysql-secret --from-file=./passwords/root_password.txt --from-file=./passwords/password.txt
```

* Label the created secret with labels app=mysql, layer=db and project=etherpad:
```
kubectl --namespace $namespace label secret mysql-secret app=mysql layer=db project=etherpad
```

* Use `kubectl` or Dashboard to verify that the configmap and secret were properly created.

* Check the file `mysql.pvc.yaml` which contains the PersistentVolumeClaim

* Create the volume claim in Kubernetes using `kubectl`:
```
kubectl --namespace $namespace create -f mysql.pvc.yaml
```

* Use `kubectl` or Dashboard to verify that the volume claim has been created and that Kubernetes also automatically created the underlying Amazon EBS volume.

* Check the file `mysql.deployment.yaml` which contains the MySQL deployment. The different environment variables which are supported by the MySQL image can be found on [Docker Hub](https://hub.docker.com/_/mysql/).

* Deploy MySQL using `kubectl`:
```
kubectl --namespace $namespace create -f mysql.deployment.yaml
```

* You can exec into the MySQL pod to verify that the database was properly created

* Check the file `mysql.service.yaml` which contains the MySQL service. Notice that the type of the service is ClusterIP and not load balancer. We do not want to expose MySQL to the outside and therefore we will not create Amazon AWS load balancer. We will expose it only to other Pods in our cluster using cluster IP address

* Create MySQL service using `kubectl`:
```
kubectl --namespace $namespace create -f mysql.service.yaml
```

* Use `kubectl` or Dashboard check the MySQL Pods and service.

## Deploy Etherpad

* Check the `etherpad.config.yaml` file which describes the configuration map for the Etherpad

* Create the config map in Kubernetes cluster using using `kubectl`:
```
kubectl --namespace $namespace create -f etherpad.configmap.yaml
```

* Enter the password for the Etherpad admin account in `passwords/etherpad_password.txt`. Make sure the password files don't contain any empty lines on the beginning or the end of the file.

* Generate a secret using the password files and `kubectl`. This uses the same password file as used to MySQL:
```
kubectl --namespace $namespace create secret generic etherpad-secret --from-file=./passwords/etherpad_password.txt --from-file=./passwords/password.txt
```

* Label the created secret with labels app=mysql, layer=db and project=etherpad:
```
kubectl --namespace $namespace label secret etherpad-secret app=etherpad layer=backend project=etherpad
```

* Use `kubectl` or Dashboard to verify that the configmap and secret were properly created.

* Check the file `etherpad.deployment.yaml` which contains the Etherpad deployment. The different environment variables which are supported by the Ethepad image can be found on [Docker Hub](https://hub.docker.com/r/tvelocity/etherpad-lite/).

* Deploy Etherpad using `kubectl`:
```
kubectl --namespace $namespace create -f etherpad.deployment.yaml
```

* Check the file `etherpad.service.yaml` which contains the Etherpad service. Unlike the MySQL service, this service has type LoadBalancer and creates Amazon AWS load balancer.

* Create Etherpad service using `kubectl`:
```
kubectl --namespace $namespace create -f etherpad.service.yaml
```

* Find the hostname for the Etherpad application from the service and open it from the browser (the DNS propagation might take some time).

## MySQL / Etherpad restarts

* The Etherpad application is stateless. You can try to delete the Etherpad pod using `kubectl` or Dashboard. New one will be automatically started by Kubernetes deployment and all your notebooks should be still present.

* The MySQL application is stateful, backed by the persisitent volume. You can try to delete the Etherpad pod using `kubectl` or Dashboard. New one will be automatically started by Kubernetes deployment and all your notebooks should be still present, as recovered from disk.
