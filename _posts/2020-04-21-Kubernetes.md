- What is Kubernetes
- Why Kubernetes is Popular?
- Understanding Kubernetes Architecture
- How does Kubernetes work?
- How to configure Kubernetes Cluster in Google Cloud
- Role of Docker in Kubernetes
- How to deploy Hello World Rest API Image in Kubernetes Cluster
- Tools/Plugins used in Kubernetes
- Kubernetes Commands

### What is Kubernetes?

As per Kubernetes documentation, ``Kubernetes (also known as k8s or "kube")`` is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapid growing ecosystem. Kubernetes services, support, and tools are widely available.

In simple words, you can cluster together groups of hosts running Linux containers, and Kubernetes helps you easily and efficiently manage those clusters.

### Why is Kubernetes so Popular?

More than just enabling a containerized application to scale, Kubernetes has release-management features that enable ``updates with near-zero downtime``, ``version rollback``, and ``clusters that can 'self-heal'`` when there is a problem. ``Load Balancing``, ``Auto-Scaling`` and ``SSL`` can easily be implemented. Plugins like Helm, has revolutionized the world of server management by making multi-node data stores like Redis and MongoDB incredibly easy to deploy.

And also using Kubernetes for solutions that are already containerized can drastically reduce development time spent on operations and deployment. However, the effort of migration existing brown-field applications or legacy solution to be container-based so that Kubernetes can be used may be a viable solution.

### Understanding Kubernetes Architecture

Kubernetes Architecture has the following main components:

 - Master Node(s)
 - Worker/Slave Node(s)
 - Distributed Key-Value Store(etcd)
 
 ![Kubernetes Architecture](../images/kubernetesarchitecture.jpg)
 
#### Master Node(s)

It will perform all administrative tasks like responsible and managing the Kubernetes cluster. There can be more than one master node in the cluster to check for fault tolerance. If we have more than one master node which makes system in a High Availablity mode, in which one of them will be the main node which we perform all the tasks.
It consists of 4 components:
   1. API Server
   2. Scheduler
   3. Controller Manager
   4. Etcd

#### Worker Node(s)

It acts like a physical server or you can say a VM which runs the applications using Pods (a pod scheduling unit) which is controlled by the master node. On a physical server (worker/slave node), pods are scheuduled. In order to access the application from the external world, we will connect to work nodes.

It consists of the following components:
1. Container runtime
2. Kubelet
3. Kube-proxy
4. Pods

#### Distributed Key-Value Store(Etcd)

etcd is written in the Go programming language. It is a distributed key-value store which stores the cluster state, it can be part of the Kubernetes master or, it can be configured externally. Along with storing the cluster state, it is also used to store configuration details such as subnets, ConfigMaps, Secrets, etc.
 
 
 
 
