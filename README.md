# netbox-kubernetes
Kubernetes manifest resources for Netbox.  all images are pulled from docker hub. Netbox images pulled from https://hub.docker.com/r/ninech/netbox/


## Quickstart on Minikube

To get NetBox up and running:

```
$ git clone 
$ cd netbox-kubernetes
$ mkdir /netbox/data  ## On All Nodes
$ kubectl apply -f netbox-namespace.yaml
$ kubectl apply -f storageclass.yaml --n netbox
$ kubectl apply -f persistant_volume -n netbox
$ kubectl apply -f postgres-all.yaml --namespace netbox
$ kubectl apply -f netbox-all.yaml --namespace netbox
$ kubectl apply -f nginx-all.yaml --namespace netbox
```

At the moment you can access the application using follwing command. 
```
$ kubectl get pods -n netbox
```

Default credentials:

* Username: **admin**
* Password: **admin**


## Dependencies
https://hub.docker.com/r/ninech/netbox/
