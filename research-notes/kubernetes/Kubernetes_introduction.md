### Architecture of Kubernetes

#### Overview

![image-20210129160003815](https://i.loli.net/2021/01/30/JeFvkAZXbxiIEVg.png)

Kubernetes uses client-server architecture and Master is the key component used to communicate with client side (UI/CLI) and Service side (Node).

#### Master

![image-20210129160244673](https://i.loli.net/2021/01/30/meuBwrU6QDLbJi7.png)

There are 4 components in Master:

- API Server: All components in Kubernetes use API server to communicate and corporate.
- Controller: Manage and controll clusters. 
- Scheduler: Schedule resources.
- etcd: A ditributed storage system which stores metadata that needed by API server.

#### Node

![image-20210129160504275](https://i.loli.net/2021/01/30/qE9LRnmu5wJMQeF.png)

Node will not directly communicate with users. All messages are transfered by **Master** between users and nodes.

##### Pod

Pod is the minimum deployment and resource unit in kubernetes. It contains several containers, define how each containers work, and provides runtime environment.

There are several containers in one **pod**, each pod runs in **Kubelet**. Kubelet uses API server to receive request and run it within the **container runtime**.

**Storage Plugin** and **Network Plugin** are used to defind the pod policy of stroage and network. They are usually written by developers. 

![image-20210129161711063](https://i.loli.net/2021/01/30/oELK1JzkFeO4ftB.png)

In the picture above, users use UI/CLI to send a Pod to Kubernetes to deploy. This request will first be sent to API server, API server will write this request into etcd and Scheduler will get the request through **watch**. Then scheduler schedules the request based on the memory status and send a report to API server. After receiving the report from scheduler, API server will also write this report into etcd and Kubelet gets the report through watch and uses container runtime to deploy the pod.

