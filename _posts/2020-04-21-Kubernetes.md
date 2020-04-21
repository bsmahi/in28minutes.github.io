- What is Kubernetes
- Why Kubernetes is Popular?
- Understanding Kubernetes Architecture
- Role of Docker in Kubernetes
- How to configure Kubernetes Cluster in Google Cloud
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

### Role of Docker in Kubernetes

Docker plays a pivotal role in Kubernetes architecture. It can be used as a container runtime that Kubernetes orchestrates. When Kubernetes schedules a pod to a node, the kubelet on that node will instruct Docker to launch the specified containers.

The kubelet then continuously collects the status of those containers from Docker and aggregates that information in the master. Docker pulls containers onto that node and starts and stops those containers.

Using Kubernetes with Docker is that an automated system asks Docker to do those things instead of the admin doing so manually on all nodes for all containers.

### How to configure Kubernetes Cluster in Google Cloud


Let's start with creating a Google Cloud Account

### Creating A Google Cloud Free Trial Account

Make sure that you're logged into your Google account and go to the website [cloud.google.com](cloud.google.com). 

![image info](../images/02-getting-started-with-kuberbetes-and-gke-step02-002.png)

Click the button ```Get Started For Free```. 

Choose your country, read the ```Terms of Services```, and agree to them. 

![image info](../images/02-getting-started-with-kuberbetes-and-gke-step02-003.png)

At the time of writing this, Google free trial account gives you ```$300``` credit, as well as free access to a number of Google services for about 12 months. 

> Google does not auto charge you after the free trial ends. 

Click ```Continue```. 

You will be asked a lot of details. Follow the screens and enter the requested details.
- Choose your account type
- Enter your tax information
- Enter your address information
- Choose your payment method and card details (Go through the card verification process which can change based on the country you are in)
![image info](../images/02-getting-started-with-kuberbetes-and-gke-step02-004.png)
![image info](../images/02-getting-started-with-kuberbetes-and-gke-step02-005.png)
![image info](../images/02-getting-started-with-kuberbetes-and-gke-step02-006.png)
![image info](../images/02-getting-started-with-kuberbetes-and-gke-step02-007.png)
![image info](../images/02-getting-started-with-kuberbetes-and-gke-step02-008.png)

After entering all the details, click```Start My Free Trial``` button. 

And at the end of it, you should land up on a screen like this. 

![image info](../images/02-getting-started-with-kuberbetes-and-gke-step02-009.png)

 
 
 
