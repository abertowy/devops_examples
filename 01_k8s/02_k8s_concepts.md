# Core Concepts:

1. Cluster:  
    A set of machines (nodes) that run containerized applications and are managed by Kubernetes. It consists of a Control Plane and Worker Nodes. 

2. Control Plane:
    The components that manage the Kubernetes cluster's state and orchestrate activities like deploying applications, scaling, and updates. It includes the API Server, etcd, Scheduler, Controller Manager, and Cloud Controller Manager. AKA Master Node

3. Worker Node:
    The machines within the cluster that run the actual containerized applications. Each worker node contains the Kubelet (agent that communicates with the Control Plane), Kube-proxy (handles network proxying for Services), and Container Runtime (e.g., Docker, containerd).

4. Pod:
    The smallest deployable unit in Kubernetes. A Pod represents a single instance of a running process in the cluster and can contain one or more containers that share network and storage resources.

5. Deployment:
    An API object that manages a set of identical Pods, ensuring a desired number of replicas are running and facilitating rolling updates and rollbacks of applications.

6. Service:
    An abstract way to expose an application running on a set of Pods as a network service. Services provide stable network identities and load balancing for Pods. 

7. Namespace:
    A mechanism to divide cluster resources into isolated virtual clusters. Namespaces help organize resources and prevent naming conflicts in larger environments.

8. Ingress:
    An API object that manages external access to services within a cluster, typically HTTP. It can provide load balancing, SSL termination, and name-based virtual hosting. 

9. Persistent Volume (PV) & Persistent Volume Claim (PVC):
    PVs are pieces of storage in the cluster, while PVCs are requests for storage by users. This separation allows for abstracting storage details from application deployment.

10. ConfigMap & Secret:
    ConfigMaps store non-confidential configuration data in key-value pairs, while Secrets are used to store sensitive information like passwords and API keys securely.

11. Kubectl:
    The command-line tool used to interact with the Kubernetes API server and manage Kubernetes objects.

![Core components] (02_k8s_core_components.png)