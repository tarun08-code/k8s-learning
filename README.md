# k8s-learning

notes

day 1 
---

### **1. Why Kubernetes is Essential**
*   **The Market Reality:** While many focus on CI/CD pipelines, **Kubernetes (K8s)** is the "key player" in the DevOps job market. It is considered the future of DevOps.
*   **Career Path:**
    *   Knowing only CI/CD and basic DevOps tools might land you a "Release Engineer" role.
    *   To have a long-term career ("marathon") and become a key player, **Kubernetes is mandatory**.
*   **Microservices:** The industry has shifted toward microservices over the last 6–7 years. Kubernetes is the standard for managing these at scale.

---

### **2. Prerequisites**
*   **Docker/Containers:** You must have a strong understanding of containers before starting K8s.
*   **What to Review:**
    *   Difference between Containers and Virtual Machines (VMs).
    *   Namespace and Network isolation.
    *   Why containers are lightweight.
    *   Security, multi-stage builds, and lifecycle management.
*   *Note:* If you haven't watched the previous videos (Day 24–29) covering Docker, go back and watch them first.

---

### **3. The Core Question: Docker vs. Kubernetes**
*   **Docker:** A **Container Platform**. It handles the lifecycle of containers on a single host.
*   **Kubernetes:** A **Container Orchestration Platform**. It manages containers across multiple hosts (clusters).

#### **The 4 Major Problems with Docker (Single Host)**
Abhishek outlines four specific limitations of running containers on a single Docker host:

| Problem | Description | The Consequence |
| :--- | :--- | :--- |
| **1. Single Host Nature** | Docker runs on one machine. If one container consumes too much RAM/CPU, it can crash other containers on the same host. | Resource contention; one bad app kills others. |
| **2. No Auto-Healing** | If a container crashes, it stays down until a human manually restarts it. | **Downtime.** In production with thousands of containers, manual monitoring is impossible. |
| **3. No Auto-Scaling** | If traffic spikes (e.g., a movie release on Netflix), you cannot automatically add more container instances. | Application slows down or crashes under load. |
| **4. Lack of Enterprise Features** | Docker is minimalistic. It lacks built-in firewalls, advanced load balancing, API gateways, and security policies required for production. | Not "Enterprise Ready" for large-scale production environments. |

---

### **4. How Kubernetes Solves These Problems**
Kubernetes addresses each limitation through a **Cluster Architecture** (Master Node + Worker Nodes).

*   **Solution to Single Host:**
    *   K8s uses a **Cluster** (group of nodes).
    *   If a container on one node causes issues, K8s can reschedule workloads to a healthy node.
*   **Solution to Auto-Scaling:**
    *   Uses **ReplicaSets** and **Deployments** (defined in YAML files).
    *   Supports **HPA (Horizontal Pod Autoscaler)**: Automatically increases container count when CPU/Memory usage hits a threshold (e.g., 80%).
*   **Solution to Auto-Healing:**
    *   The **API Server** constantly monitors the cluster.
    *   If a container (Pod) dies, K8s immediately spins up a new one to replace it, often before the user notices.
*   **Solution to Enterprise Support:**
    *   Built on Google's internal tool **Borg**.
    *   Designed for production with support for Load Balancers, Firewalls, and API Gateways.
    *   Extensible via **Custom Resource Definitions (CRDs)** and **Ingress Controllers** (e.g., Nginx) to add advanced features like advanced load balancing.

---

### **5. Key Takeaways for Beginners**
*   **K8s is Easy:** Don't be intimidated. Understanding the "Why" (the 4 problems above) is the first 5% of learning.
*   **Production Reality:** Docker alone is rarely used in enterprise production; Kubernetes is the standard.
*   **Community Support:** Backed by the **CNCF** (Cloud Native Computing Foundation), ensuring constant evolution and new tools (like Prometheus, Podman).
*   **Next Steps:** The course will move on to:
    *   Kubernetes Architecture.
    *   Pods, Deployments, Services, and Ingress Controllers.

> **Quote from Transcript:** *"Kubernetes is the future of DevOps... if you want to do a marathon journey in DevOps, Kubernetes is the future."*

day 2 
-------------------------------------------------------------------------------------------------
☸️ Kubernetes Architecture — Simple Notes
Big Picture: Control Plane vs Data Plane

Think of Kubernetes as a company.

🧠 Control Plane (Master Node)

The brain of Kubernetes. It makes decisions and manages the entire cluster.

💪 Data Plane (Worker Nodes)

The workers that actually run your applications (pods).

Worker Node (Data Plane)

Every worker node needs 3 main components:

Component	What it Does	Easy Way to Remember
Kubelet	Watches pods and makes sure they are running. If a pod crashes, it reports and restarts it.	👷 Site Foreman
Kube Proxy	Handles networking and load balancing between pods.	🚦 Traffic Police
Container Runtime	Actually runs containers. Examples: containerd, CRI-O, Docker.	🚗 Engine
Quick Memory Trick

Kubelet → Watches Pods
Kube Proxy → Handles Traffic
Container Runtime → Runs Containers

Control Plane (Master Node)

This is where all cluster decisions happen.

Component	What it Does	Easy Way to Remember
API Server	Entry point of Kubernetes. Receives all requests and commands.	🛎 Receptionist
Scheduler	Decides which worker node should run a pod.	📋 Manager
etcd	Stores all cluster information and configuration.	🗄 Filing Cabinet
Controller Manager	Ensures desired state is maintained.	👀 Supervisor
Cloud Controller Manager (CCM)	Connects Kubernetes with AWS, Azure, GCP, etc.	🌐 Translator
How Everything Works Together
Example: Creating a Pod

1️⃣ User sends request → API Server

2️⃣ Scheduler selects the best worker node

3️⃣ Controller Manager checks if desired state is maintained

4️⃣ Kubelet on the selected worker node receives instructions

5️⃣ Container Runtime starts the container

6️⃣ Kube Proxy gives networking and traffic access

Why Kubernetes is Powerful
Auto-Healing

If a pod crashes:

Kubelet detects it
Controller Manager notices desired state is broken
New pod gets created automatically
Auto-Scaling

Kubernetes can increase or decrease pods based on load.

Load Balancing

Kube Proxy distributes incoming traffic across multiple pods.

Super Short Interview Revision
Worker Node Components
Kubelet → Manages pods
Kube Proxy → Networking & Load Balancing
Container Runtime → Runs containers
Control Plane Components
API Server → Entry point
Scheduler → Chooses node
etcd → Stores cluster data
Controller Manager → Maintains desired state
CCM → Cloud integration
Fun Fact 🎉

K8s = Kubernetes

The "8" represents the 8 letters between K and S.

K + (ubernete) + S = K8s

One-Line Summary
API Server receives requests → Scheduler picks node → Controller Manager ensures desired state → Kubelet starts pod via Container Runtime → Kube Proxy handles traffic. 🚀

day 3 

insatall minikube 

day 4 / day 32
--------------------------------------------------------------------------------------------

### Local vs Production Kubernetes

**For Learning/Development:**

* Minikube
* k3s
* kind
* MicroK8s

❌ Not production-ready because they lack HA, scalability, and enterprise support.

---

### Production Kubernetes Options

* Vanilla Kubernetes
* OpenShift
* Rancher
* VMware Tanzu
* Amazon EKS
* Azure AKS
* Google GKE

**Managed Services (EKS, AKS, GKE):**

* Cloud provider manages control plane
* Easier maintenance and support

**Self-Managed:**

* Team manages everything
* More control, lower cost

---

### kops (Kubernetes Operations)

A tool used to:

* Create clusters
* Upgrade clusters
* Configure clusters
* Delete clusters

Commonly used for managing self-managed Kubernetes clusters on AWS.

---

### kops Cluster Setup Steps

1. Install:

   * Python 3
   * AWS CLI
   * kubectl
   * kops

2. Configure AWS IAM permissions:

   * EC2
   * S3
   * IAM
   * VPC

3. Create an S3 bucket to store cluster state.

4. Configure domain:

   * Production → Route 53 + custom domain
   * Testing → `.k8s.local`

5. Create cluster using `kops create cluster`.

---

### Quick Revision

✅ Local: Minikube, k3s, kind, MicroK8s
✅ Production: OpenShift, Rancher, Tanzu, EKS, AKS, GKE
✅ kops = Kubernetes cluster lifecycle management on AWS
✅ S3 stores cluster state
✅ Route 53 manages DNS
✅ Managed = Cloud handles control plane
✅ Self-managed = Team handles everything 🚀


day 5 / 33
--------------------------------------------------------------------------------------------

Day 33 — First App Deployment in K8s
Pod = smallest unit in K8s

Wrapper around container(s). You deploy Pods, not containers directly.
Gets a Cluster IP. Usually 1 container per pod (multi-container = sidecar/init pattern).

Tools:

kubectl → CLI to talk to cluster
minikube → local single-node cluster for learning

pod.yaml structure:

yamlapiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80

Key commands:

bashkubectl create -f pod.yaml
kubectl get pods / kubectl get pods -o wide
kubectl describe pod <name>   # debug
kubectl logs <name>            # app logs
kubectl delete pod <name>
minikube ssh → curl <pod-ip>  # access app

Limitation: Plain pods have no auto-healing or auto-scaling → use Deployments instead (next topic).

day 6 / 34
------------------------------------------------------------------------------------------
Hierarchy:
Deployment → ReplicaSet → Pod → Container
Container vs Pod vs Deployment:

Container → runtime instance (docker run)
Pod → K8s wrapper around container, defined in YAML
Deployment → manages pods via ReplicaSet, adds auto-heal + auto-scale

Why not just Pods?

If you delete a pod → it stays deleted. No recovery.
Deployment fixes this → ReplicaSet watches desired state and recreates pods instantly.

deployment.yaml key fields:
yamlkind: Deployment
spec:
  replicas: 3
  selector: ...
  template: ... # pod definition goes here
Key behaviors:

Set replicas: 3 → always 3 pods running
Delete a pod → ReplicaSet auto-creates a replacement
Update replicas in YAML → scales up/down instantly

Rule: Never create bare Pods in production. Always use Deployments.
Interview answers:

Pod vs Deployment → Pod has no self-healing; Deployment does via ReplicaSet
Deployment vs ReplicaSet → Deployment handles lifecycle (updates, rollbacks); ReplicaSet just maintains pod count





