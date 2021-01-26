# netbox-kubernetes
Kubernetes manifest resources for Netbox using local filesystems on 2 nodes (adjust the replicas and PV's for more or less nodeS).  all images are pulled from docker hub. Netbox images pulled from https://hub.docker.com/r/ninech/netbox/

To get NetBox up and running:
!! Ensure that you modify the nodeAffinity.required.nodeSelectorTerms.matchExpressions.values with the hostnames of your K8s nodes !!
```
$ git clone [this repo]
$ cd netbox-kubernetes
$ mkdir /netbox/data  ## On All Nodes
$ kubectl apply -f netbox-namespace.yaml
$ kubectl apply -f storageclass.yaml -n netbox ## Ensure you have changed the hostnames in the 'values' field in this yaml file first
$ kubectl patch storageclass netbox -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
$ kubectl apply -f postgres-all.yaml --namespace netbox
$ kubectl apply -f netbox-all.yaml --namespace netbox
$ kubectl apply -f nginx-all.yaml --namespace netbox
```

Glean that the pods are running
```
$ kubectl get pods -n netbox
$ kubetl get services -n netbox -o wide
[jlunde@192-168-93-28 netbox-kubernetes]$ kk get services -n netbox -o wide
NAME       TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE     SELECTOR
netbox     ClusterIP   10.96.130.122    <none>        8001/TCP       8m51s   app=netbox
nginx      NodePort    10.111.111.198   <none>        80:30969/TCP   8m44s   frontend=nginx
postgres   ClusterIP   None             <none>        5432/TCP       8m57s   backend=postgres
```

In my example output above, I can access the netbox instance on my node IP address and port of 30969. Port and IP will vary based on deployment. Default credentials:

* Username: **admin**
* Password: **admin**


## Dependencies
https://hub.docker.com/r/ninech/netbox/
