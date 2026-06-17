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
