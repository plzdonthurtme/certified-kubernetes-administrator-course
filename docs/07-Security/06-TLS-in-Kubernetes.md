# TLS in Kubernetes
  - Take me to [Video Tutorial](https://kodekloud.com/topic/tls-in-kubernetes/)
  
In this section, we will take a look at TLS in kubernetes

Three types:
- Server certificates configured on the servers.
- Root certificate configured on the CA servers
- Client certificates configured on the clients.


| Type                      | Used By                       | Purpose                           | Example File               |
| ------------------------- | ----------------------------- | --------------------------------- | -------------------------- |
| **Server Certificate**    | API server, etcd, kubelet     | Proves server identity to clients | `apiserver.crt`            |
| **Root (CA) Certificate** | CA authority                  | Signs & verifies other certs      | `ca.crt`, `ca.key`         |
| **Client Certificate**    | kubectl, kubelet, controllers | Proves client identity to servers | `admin.crt`, `kubelet.crt` |


#### The two primary requirements are to have all the various services within the cluster to use server certificates and all clients to use client certificates to verify they are who they say they are.
- Server Certificates for Servers
- Client Certificates for Clients

  ![tls](../../images/tls.PNG)
  
#### Let's look at the different components within the k8s cluster and identify the various servers and clients and who talks to whom.

  ![certs](../../images/certs.PNG)
  
