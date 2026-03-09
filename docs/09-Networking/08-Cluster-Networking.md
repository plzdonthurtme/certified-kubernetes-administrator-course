# Pre-requisite Cluster Networking

  - Take me to [Lecture](https://kodekloud.com/topic/cluster-networking/)


In this section, we will take a look at **Pre-requisite of the Cluster Networking**

- Set the unique hostname.
- Get the IP addr of the system (master and worker node).
- Check the Ports on master and worker.
  - kube-api:6443 (m)
  - kubelet:10250 (m&w)
  - kube-scheduler:10259 (m)
  - kube-controller-manger:10257 (m)
  - services:30000-32767(w)
  - etcd:2379 (m to listen to etcd server)
  - etcd:23780 (m for clients)

## IP and Hostname

- To view the hostname

```
$ hostname 
```

- To view the IP addr of the system

```
$ ip a -o wide
```

To view the IP addr of the system

```
$ ip a -o wide
```


## Set the hostname

```
$ hostnamectl set-hostname <host-name>

$ exec bash
```

## View the Listening Ports of the system

```
$ netstat -nltp
```

## View the Established Ports to a specific service

```
# netstat -pan | grep -i <service> | grep -i <port> | wc -l
$ netstat -pan | grep -i etcd | grep -i 2379 | wc -l
```

If you would to grep and count the number of connections according to service or ports:
```
controlplane ~ ➜  netstat -pan | grep ESTABLISHED | awk '{print $7}' | cut -d/ -f2 | sort | uniq -c | sort -nr
     76 kube-apiserver
     62 etcd
      2 kube-scheduler
      2 kube-controlle
      1 ttyd
      1 kube-proxy
      1 kubelet
      1 flanneld

controlplane ~ ➜  netstat -tan | grep ESTABLISHED | awk '{print $4}' | awk -F: '{print $NF}' | sort | uniq -c | sort -nr
     62 2379
     13 6443
      1 8080
      1 54190
      1 54172
      1 54164
...
``
Note: 2379 is the port of ETCD to which all control plane components connect to. 2380 is only for etcd peer-to-peer connectivity. When you have multiple controlplane nodes. 

## Address Resolution Protocol (ARP) 

```
$ arp
$ route
```
arp command is used to display and modify the Address Resolution Protocol (ARP) cache. Route command is used to view and manipulate the IP routing table, allowing users to add, delete, or modify routes for network traffic.

## IP forwarding settings

```
$ cat /proc/sys/net/ipv4/ip_forward
```
check if IP is listed in ip forwarding settings.

## find bridge

```
$ ip a show type bridge 
```



#### References Docs

- https://kubernetes.io/docs/reference/networking/ports-and-protocols/
- https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#check-required-ports
- https://kubernetes.io/docs/concepts/cluster-administration/networking/
- https://kubernetes.io/docs/concepts/cluster-administration/addons/
- https://kubernetes.io/docs/concepts/cluster-administration/networking/#how-to-implement-the-kubernetes-networking-model

