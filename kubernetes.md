# Introduction

**Cloud-Native** is everything that is built on the cloud. A cloud-native application means the application is fully deployed on the cloud.

**Kubernetes** (also known as **K8s**) is an open-source system for automating the deployment, scaling, and management of containerized applications. 
* It is a cloud-native platform for containerized applications.
* It enables you to manage containerized applications with cloud-native features.
* It works in both public and private clouds.

### Key Tools
* **`kubeadm`**: A tool that simplifies the process of setting up a Kubernetes cluster.
* **Calico**: Used to set up Kubernetes networking.

---

# Kubernetes Resources

**Resources** are objects of a certain type in the Kubernetes API (Application Program Interface). We interact with the cluster by creating and modifying these objects. Anything created by the Kubernetes API is a resource.

### Pods
* **Pod**: The most basic resource in Kubernetes.
* It represents a group of one or more containers.
* The application runs inside the pod.

### Resource Types
Objects and resources have a specific resource type. **Pods**, **Deployments**, and **Services** are all different resource types. 
* Each resource type specifies different functionality in Kubernetes.
* Each individual pod is an object.

### Configuration & Deployment
You can create a Kubernetes configuration file to define a resource type (e.g., `my-pod.yml`, where you define a `pod` resource type).

* `kubectl apply -f my-pod.yml` — This command will apply the configuration defined in the Kubernetes cluster.
* `kubectl get pods` — This command will show the pods that are spun up. This creates a pod object.

---

# Resources for Managing Pods

Kubernetes has a variety of resource types dedicated to **pod management**:

* **ReplicaSet**: It ensures that a given number of pod replicas are running at any specified time. Pod creation is done with the help of a template, and pods can also be destroyed through it.
* **Deployment**: It can be used for scaling applications by declaring the minimum and maximum replicas. It uses a `RollingUpdate` deployment strategy for zero-downtime updates to the workload. This means that when a deployment is updated, the new pods replace the older ones one by one, rather than all at once. Deployment is used to manage stateless applications (Applications are running inside a pod. This pod has a specific configuration maintained. For a stateful application, the pod inside which this application is running has a configuration maintained and if this pod fails, the new pod that is spun up has the same configuration as the previous pod. But for stateless application, the pod configuration is not maintained hence if this pod is gone and if another pod needs to spin up, that new pod will not have a similar configuration as the old one). Deployment automatically creates replica set. 

# Kubernetes Resource Management & Architecture

## Pod Verification Commands
```bash
# Get all active deployments in the namespace
kubectl get deployment

# Get all replica sets to see pod scaling status
kubectl get replicaset

# Get all pods to see individual running instances
kubectl get pods
```

---

## Workload Resources

* **StatefulSet**: Used for managing stateful applications. It maintains a sticky identity and strict ordering for each pod (keeping the same pod name and network hostname) even if they are re-created on a different node. While a **Deployment** creates random pod names upon re-creation, a **StatefulSet** guarantees the new pod keeps the exact same name and sequence order. A **Headless Service** must be created alongside a StatefulSet to manage its network identity.
* **DaemonSet**: Ensures that a replica copy of a specific pod runs on every node in the cluster. It dynamically provisions replicas on new nodes as they join the cluster. Filter criteria (such as node selectors or affinities) can be applied to restrict execution to specific subsets of nodes.
* **Job**: Reliably executes a discrete, containerised task to its successful completion.
* **CronJob**: Runs jobs repeatedly according to a specified temporal schedule (e.g., executing a routine application task inside a pod every minute).

---

## Kubernetes Architecture

* **Data Plane / Nodes**: The underlying worker machines that host pods and actively run container workloads.
* **Control Plane**: The orchestration layer consisting of a collection of core components that manage node states, pod scheduling, and the overall cluster lifecycle.

![Alt text](<kubernetes_architecture.png>)
