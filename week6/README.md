# WEEK 6 - CKA Book Course

Access the Book Here: [AcingTheCKA.com](https://acingthecka.com)

[WEEK 6 - Meeting Recording](https://community.kubeskills.com/c/meetings/dns-services-ingress-and-more-chapter-6-review)

## Chapter 6 Overview
- How nodes communicate via CNI and the different CNIs available
- How Pod-to-Pod communication happens
- Types of Services in Kubernetes and when they are used
- Assigning IP addresses to Pods
- Communication via DNS and how to use CoreDNS
- Using Ingress and Ingress controllers

## CHAPTER 6 CHALLENGE

- [https://community.kubeskills.com/c/welcome-to-the-cka/using-network-policies-to-restrict-traffic-from-frontend-to-backend](https://community.kubeskills.com/c/welcome-to-the-cka/using-network-policies-to-restrict-traffic-from-frontend-to-backend)

## LINKS

- [Create Ingress Resource - Killercoda Lab](https://killercoda.com/chadmcrowell/course/cka/create-ingress)
- [Modify Cluster DNS - Killercoda Lab](https://killercoda.com/chadmcrowell/course/cka/modify-cluster-dns)
- [CKA Cluster Setup](https://github.com/chadmcrowell/cka-exercises)
- [Static Pods - K8s Docs](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/)
- [Nginx Ingress controller YAML](https://raw.githubusercontent.com/chadmcrowell/acing-the-cka-exam/main/ch_06/nginx-ingress-controller.yaml)
- [Ingress resource YAML](https://raw.githubusercontent.com/chadmcrowell/acing-the-cka-exam/main/ch_06/hello-ingress.yaml)
- [Ingress - K8s Docs](https://kubernetes.io/docs/concepts/services-networking/ingress/)
- [Metal LB - LoadBalancer for KIND](https://raw.githubusercontent.com/chadmcrowell/acing-the-cka-exam/main/ch_06/metallb-native.yaml)
- [Connect App Services - K8s Docs](https://kubernetes.io/docs/tutorials/services/connect-applications-service/)
- [Network Policies - K8s Docs](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
- [Labeling Pods - K8s Docs](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_label/)
- [Network Policy Visualizer](https://editor.networkpolicy.io/)

## Kubernetes Services & Networking FAQ
1. What is CoreDNS and why is it important in Kubernetes?
CoreDNS is the default DNS service in Kubernetes. It's essential for several reasons:
- Pod-to-Pod Communication: CoreDNS translates service names to IP addresses, enabling pods to communicate with each other within the cluster.
- Service Discovery: It allows applications to find and connect to services by their names, abstracting the underlying IP addresses.
- Ingress Resolution: CoreDNS helps resolve external domain names to the correct internal services, facilitating communication between external clients and applications inside the cluster.
- Troubleshooting: Understanding CoreDNS configurations can be crucial when troubleshooting connectivity issues within a cluster.

2. How do I change the default IP address range for Services in Kubernetes?
Changing the service cluster IP range requires modifying the API server's configuration:
- Access the API server's YAML file: This file is typically located at `/etc/kubernetes/manifests/kube-apiserver.yaml.`
- Modify the `--service-cluster-ip-range` flag: Change the value to the desired new IP range.
- Restart the API server: The API server will restart with the new IP range applied. Be aware that this will cause temporary disruption to cluster access.
- Update CoreDNS Service IP: Edit the `kube-dns` service in the `kube-system` namespace to reflect the new IP range.
- Update kubelet Configuration: Change the cluster DNS IP in both the local kubelet config file (`/var/lib/kubelet/config.yaml`) and the `kubelet-config` ConfigMap.
- Restart kubelet: Use systemctl daemon-reload followed by systemctl restart kubelet to apply the changes.
- Verify Changes: Deploy a test pod and check the `/etc/resolv.conf` file to ensure it uses the updated DNS server IP.

3. What is the difference between an Ingress resource and an Ingress Controller?
- **Ingress Resource:** It's a Kubernetes object that defines rules for routing external traffic to services within the cluster. It acts like a high-level traffic routing configuration.
- **Ingress Controller:** This is a specialized pod that implements the rules defined by Ingress resources. It manages the actual traffic routing, load balancing, and other ingress-related functions.
- **Key Points:** An Ingress resource alone won't function; it needs an Ingress Controller to process and apply the rules.
You usually don't need to install an Ingress Controller during the CKA exam, as one is typically provided.

4. What are the different types of Kubernetes Services, and when would you use each?
Kubernetes offers three types of services:
- **ClusterIP:** This is the default type. It exposes a service internally within the cluster using an internal IP address. Useful for communication between pods within the cluster.
- **NodePort:** Exposes a service on a static port on each node in the cluster. Traffic sent to this port is forwarded to the service. Primarily used for giving external access to a service, especially during development or debugging.
- **LoadBalancer:** This type utilizes a cloud provider's load balancer to expose the service externally. It provides a stable external IP address for accessing the service. Ideal for production deployments where external access with load balancing is needed.

5. How do Endpoints relate to Services in Kubernetes?
Endpoints represent the actual backend pods that a service routes traffic to. They provide the mapping between a service name and the IP addresses and ports of the pods that implement the service.
- When you create a service, Kubernetes automatically creates a corresponding Endpoints object.
- As pods are created or deleted, the Endpoints object is updated to reflect the current set of backend pods.
- Services use the Endpoints object to direct traffic to the appropriate pods.

6. What is a Container Network Interface (CNI), and why is it needed?
The Container Network Interface (CNI) manages the networking for pods in Kubernetes. It is responsible for:
- IP Address Allocation: Assigning IP addresses to pods.
- Network Connectivity: Establishing network connections between pods, even across different nodes.
- Network Isolation: Providing network isolation between pods and the host system.
- Without a CNI, pods wouldn't be able to communicate with each other or the outside world. Examples of CNIs include Calico, Flannel, and Weave Net.

7. What are Network Policies, and how can you use them to restrict pod communication?
Network Policies are Kubernetes resources that define how pods are allowed to communicate with each other and with external networks. They provide a way to control network traffic at the pod level.
- **Deny-All by Default:** A common security practice is to implement a "deny-all" Network Policy, blocking all traffic by default.
- **Allow Specific Traffic:** You then create more specific policies to allow communication between designated pods or groups of pods.
- **Label-Based Selection:** Network Policies use labels to select pods that the rules should apply to.

8. How can I test Pod-to-Pod communication within a Kubernetes cluster?
- Deploy Test Pods: Create pods with the necessary tools (e.g., mysql client, curl) to send and receive traffic.
- Use `kubectl exec`: Get a shell into one of the test pods using the kubectl exec command.
- Execute Network Commands: From within the pod, use commands like curl, ping, or mysql to try and connect to other pods within the cluster.
- Observe Results: Based on the results, you can determine whether communication is successful and diagnose any connectivity problems.