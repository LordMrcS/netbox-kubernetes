# netbox-kubernetes
Kubernetes manifest resources for Netbox.  All images are pulled from docker hub. Netbox images pulled from https://hub.docker.com/r/netboxcommunity/netbox/

To get NetBox up and running:
```
$ git clone [this repo]
$ cd netbox-kubernetes
$ kubectl apply -k .
```

Glean that the pods are running, which nodes they are on, and what port it is using for NAT
```
$ kubectl get pods -o wide --sort-by="{.spec.nodeName}" -n netbox
NAME                       READY   STATUS    RESTARTS   AGE   IP               NODE            NOMINATED NODE   READINESS GATES
netbox-79f869bf96-tw9t4    1/1     Running   0          16m   10.244.138.139   192-168-93-27   <none>           <none>
nginx-5dcf99d9d-9gt9p      1/1     Running   0          16m   10.244.138.140   192-168-93-27   <none>           <none>
postgres-f4f7585dc-96cxx   1/1     Running   0          17m   10.244.57.138    192-168-93-28   <none>           <none>


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
