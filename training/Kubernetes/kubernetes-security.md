# Kubernetes Security & Workload Isolation Playbook

## 1. How would you isolate workloads in a Kubernetes environment?
### WHY to isolate workloads
This is a general practice to separate workloads, security wise if one workload is compromised the other workload can work as per its requirement without getting affected, if there is an incident it is easier for troubleshooting.

### Isolation Strategies
*   Use separate namespaces per workload to logically isolate resources. (consider one namespace as a folder and all the information regarding that particular workload is present in that namespace. Like these, there can be many namespace)
*   Enforce Kubernetes Network Policies to control pod-to-pod communication between namespaces, ensuring pods in one workload’s namespace cannot communicate with another workload’s pods unless explicitly allowed.
*   Use RBAC (Role-Based Access Control) to restrict user and service account permissions within each namespace.
*   Consider node-level isolation using separate node pools or node selectors/taints so workload’ pods run on dedicated nodes.

---

## 2. How do labels help in isolation? Are they enough?
*   Labels help organize and select resources for Network Policies and RBAC rules.
*   Labels alone don’t enforce security. They are metadata used by policies and controllers.
*   Actual enforcement requires Network Policies and RBAC, which use labels to scope their rules.
*   For example, a Network Policy might allow ingress only from pods with a certain label in the same namespace.

---

## 3. How do you enforce network-level isolation between workloads?
*   Apply Kubernetes Network Policies to define allowed ingress and egress for pods and namespaces.
*   Use a CNI plugin that supports Network Policies (e.g., Calico) to set up all the networking for pod to pod communication. 
*   Define policies that deny all traffic by default, then explicitly allow only necessary communication.
*   Optionally use separate node pools for stronger isolation at the node level.

---

## 4. How do you limit blast radius if a container is compromised?
### Blast radius
Blast radius defines the amount of harm an attacker can do if something is compromised in your system.

### Mitigation Steps
*   Use Pod Security Policies to restrict capabilities (e.g., no privileged containers)
*   Enforce resource quotas and limits to prevent resource exhaustion.
*   Implement network policies to prevent lateral movement.
*   Use runtime security tools like Falco (it is used to detect and alert abnormal behavior and potential security threats in real time)
*   Rotate secrets regularly and use short-lived tokens for pod identities.
*   Monitor audit logs for unusual access patterns.

---

## 5. How would you secure secrets used by pods?
*   Store secrets in a dedicated secrets store that enables strong encryption, centralised management and automated rotation. 
*   Avoid hardcoding secrets in pod specs or images.
*   Use Kubernetes RBAC to restrict access to secrets.
*   Rotate secrets frequently.

---

## 6. What is your approach to securing container images?
*   Use minimal base images and scan them for vulnerabilities 
*   Sign images 
*   Pull images only from trusted registries.
*   Enforce image policies to allow only signed/trusted images.
*   Keep images up to date with patches.

---

## 7. How do you monitor and audit Kubernetes clusters?
*   Enable audit logging in Kubernetes API Server.
*   Use prometheus + Grafana for metrics monitoring and alerting.
*   Use Falco - Enable runtime security tools to detect anomalies.

---

## 8. How do you protect Kubernetes API access?
*   Use RBAC to restrict user and service account permissions.
*   Enable API Server authentication
*   Restrict access to API Server with IP whitelisting or VPN.
*   Enable audit logs for API calls.
*   Use MFA for users with elevated privileges.
*   Rotate tokens and certificates regularly.

---

## 9. What tools and best practices would you use to secure a production Kubernetes environment?
*   Use Infrastructure as Code tools (Terraform) with security scanning (tfsec).
*   Enforce Network Policies.
*   Use image scanning.
*   Implement CI/CD securely (integration test suite, PR validation)
*   Use runtime security tools like Falco.
*   Continuously auditing and rotate credentials.
