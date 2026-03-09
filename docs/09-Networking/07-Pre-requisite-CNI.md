# Pre-requisite CNI

  - Take me to [Lecture](https://kodekloud.com/topic/prerequsite-cni/)

In this section, we will take a look at **Pre-requisite Container Network Interface(CNI)**


![net-7](../../images/net7.PNG)

What a CNI runtime must fulfill:
- Container Runtime must create network namespace 
- Identify the network the container must attach to 
- Container Runtime to invoke Network Plugin (bridge) when container is ADDed 
- Container Runtime to invoke Network Plugin (bridge) when container is DELeted 
- JSON format of the Network Configuration 

Plugin side:
- Must support command line arguments ADD/DEL/CHECK 
- Must support parameters container id, network ns, etc. 
- Must manage IP Address assignment to PODs 
- Must return results in a specific format


## Third Party Network Plugin Providers

- [Weave](https://www.weave.works/docs/net/latest/kubernetes/kube-addon/#-installation)
- [Calico](https://docs.projectcalico.org/getting-started/kubernetes/quickstart)
- [Flannel](https://github.com/coreos/flannel/blob/master/Documentation/kubernetes.md)
- [Cilium](https://github.com/cilium/cilium)


## To view the CNI Network Plugins

- CNI comes with the set of supported network plugins. 

```
$ ls /opt/cni/bin/
bridge  dhcp  flannel  host-device  host-local  ipvlan  loopback  macvlan  portmap  ptp  sample  tuning  vlan
```

Note: Docker uses s Container Network Model (CNM). To integrate, do 
```
$ docker run --network=none nginx
$ bridge add <interface> /var/run/netns/<interface>
```


#### References Docs

- https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/


