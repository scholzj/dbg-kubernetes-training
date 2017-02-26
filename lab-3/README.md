# Lab 3: Multi-tier application

In this lab, we will deploy a multi-tier application which is using database with persistent storage. We will user Wordpress and MySQL.

## Deploy MySQL database

* Check the `mysql.config.yaml` file which describes the configuration map for the MySQL database

* Create the config map in Kubernetes cluster using using `kubectl`:
```
kubectl --namespace <NAMESPACE> create -f mysql.configmap.yaml
```

* Enter the passwords for the database root account and normal account in `passwords/root_password.txt` and `passwords/password.txt`. Make sure the password files don't contain any empty lines on the beginning or the end of the file.

* Generate a secret using the password files and `kubectl`:
```
kubectl --namespace <NAMESPACE> create secret generic mysql-secret --from-file=./passwords/root_password.txt --from-file=./passwords/password.txt
```

* Label the created secret with labels app=mysql, layer=db and project=wordpress:
```
kubectl --namespace <NAMESPACE> label secret mysql-secret app=mysql layer=db project=wordpress
```

* Use `kubectl` or Dashboard to verify that the configmap and secret were properly created.

* Check the file `mysql.pvc.yaml` which contains the PersistentVolumeClaim

* Create the volume claim in Kubernetes using `kubectl`:
```
kubectl --namespace <NAMESPACE> create -f mysql.pvc.yaml
```

* Use `kubectl` or Dashboard to verify that the volume claim has been created and that Kubernetes also automatically created the underlying Amazon EBS volume.

* Check the file `mysql.deployment.yaml` which contains the MySQL deployment. The different environment variables which are supported by the MySQL image can be found on [Docker Hub](https://hub.docker.com/_/mysql/).

* Deploy MySQL using `kubectl`:
```
kubectl --namespace <NAMESPACE> create -f mysql.deployment.yaml
```

* You can exec into the MySQL pod to verify that the database was properly created

* Check the file `mysql.service.yaml` which contains the MySQL service. Notice that the type of the service is ClusterIP and not load balancer. We do not want to expose MySQL to the outside and therefore we will not create Amazon AWS load balancer. We will expose it only to other Pods in our cluster using cluster IP address

* Create MySQL service using `kubectl`:
```
kubectl --namespace <NAMESPACE> create -f mysql.service.yaml
```

* Use `kubectl` or Dashboard check the MySQL Pods and service.

## Deploy Drupal

* Check the `drupal.config.yaml` file which describes the configuration map for the Drupal CMS

* Create the config map in Kubernetes cluster using using `kubectl`:
```
kubectl --namespace <NAMESPACE> create -f drupal.configmap.yaml
```

* Generate a secret using the password files and `kubectl`. This uses the same password file as used to MySQL:
```
kubectl --namespace <NAMESPACE> create secret generic drupal-secret --from-file=./passwords/password.txt
```

* Label the created secret with labels app=mysql, layer=db and project=wordpress:
```
kubectl --namespace <NAMESPACE> label secret drupal-secret app=drupal layer=backend project=wordpress
```

* Use `kubectl` or Dashboard to verify that the configmap and secret were properly created.

* Check the file `drupal.deployment.yaml` which contains the Drupal deployment. The different environment variables which are supported by the MySQL image can be found on [Docker Hub](https://hub.docker.com/_/drupal/).

* Deploy Drupal using `kubectl`:
```
kubectl --namespace <NAMESPACE> create -f drupal.deployment.yaml
```

* Check the file `mysql.service.yaml` which contains the MySQL service. Notice that the type of the service is ClusterIP and not load balancer. We do not want to expose MySQL to the outside and therefore we will not create Amazon AWS load balancer. We will expose it only to other Pods in our cluster using cluster IP address

* Create MySQL service using `kubectl`:
```
kubectl --namespace <NAMESPACE> create -f drupal.service.yaml
```

* Use `kubectl` or Dashboard check the MysQL Pods and service.

TODO: Deploy workdpress config map and secret
TODO: Deploy Wordpress
TODO: Create a loadbalaner service

## MySQL / Wordpress restarts

TODO: Kill the MySQL pod and see how kubernetes recreate it without loosing database
TODO: Kill the wordpress pod and see how it will be recreated

## Scale Wordpress

TODO: Scale wordpress to run in several instances
