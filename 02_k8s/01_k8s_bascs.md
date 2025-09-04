# Kubernetes (k8s)
  
**Kubernetes** (`K8s`) is an open-source container **orchestration** system that **automates** the **deployment**, **scaling**, and **management** of containerized applications. It helps manage applications across clusters of machines, providing automated service discovery, load balancing, resource allocation, and health checks to ensure applications remain available and performant.  
  
- Automates Deployment:  
    It automates the process of deploying applications and their components into containers. 
- Manages Scaling:  
    It can automatically scale applications up or down based on demand and resource availability. 
- Provides Load Balancing:  
    It distributes network traffic across multiple instances of an application to prevent overloading. 
- Enables Self-Healing:  
    Kubernetes can monitor the health of containers and restart or replace them if they fail. 
- Facilitates Portability:  
    It allows applications to run consistently across different environments, from development machines to cloud platforms. 
  
How it works
------------
- Containers:  
    Applications are packaged into containers, which bundle the application's code, dependencies, and configuration. 
- Pods:  
    Kubernetes groups one or more containers into a single unit called a Pod. 
- Proxy / config:
    access to Pod from outside  
- Worker Node:
    WN runs the containers of your app. Nodes are your machines / virtual instances  
- Clusters:  
    A Kubernetes cluster consists of multiple machines, or nodes, where these Pods run. 
- Orchestration:  
    Kubernetes orchestrates the entire system using an open-source API, making it possible to manage large numbers of containers and servers
  
Key features
------------
- Service Discovery and Load Balancing:  
    Kubernetes gives Pods unique IP addresses and helps manage their accessibility through a single DNS name. 
- Storage Orchestration:  
    It can automatically mount storage systems that the application needs. 
- Resource Management:  
    It keeps track of resource allocation and scales based on compute utilization. 
- Environmental Consistency:  
    It ensures applications run the same way in development, testing, and production environments. 
  
Why use Kubernetes?
-------------------
- Operational Efficiency:  
    Automates many tedious operational tasks, saving time and effort for developers and operators. 
- Increased Reliability:  
    Features like self-healing and scaling help keep applications running smoothly. 
- Flexibility:  
    Works across a variety of infrastructure options, including public clouds, private clouds, and on-premises servers. 
  
What is needed
----------------
- Kubernetes configuration (i.e. desired architecture - number of running containers, how many instances, how it should scale up, etc)
- Pass it to some Provider (specific Setup or Tool)
- Cloud Provider or Remote Machine: configuration will be applied
  
K8s is like Docker-Compose for multiple machines  
  
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: users-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: users
  template:
    metadata:
      labels:
        app: nginx
  spec:
    containers:
      - name: users
        image: my-repo/users-application
```
