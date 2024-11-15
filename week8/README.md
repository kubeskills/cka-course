# WEEK 8 - CKA Book Course

Access the Book Here: [AcingTheCKA.com](https://acingthecka.com)

[WEEK 8 - Meeting Recording](https://community.kubeskills.com/c/meetings/troubleshooting-all-the-things-chapter-8-review)

## Chapter 8 Overview
- Creating a volume in Kubernetes
- Persistent volume claims and storage classes
- Using storage with applications in Kubernetes

## CHAPTER 8 CHALLENGE

- [https://community.kubeskills.com/c/welcome-to-the-cka/troubleshooting-a-go-application-in-kubernetes](https://community.kubeskills.com/c/welcome-to-the-cka/troubleshooting-a-go-application-in-kubernetes)

## LINKS

- [Init containers - k8s docs](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)
- [Verbosity of API server logs - K8s discuss](https://discuss.kubernetes.io/t/api-sever-logs/17309)
- [Debugging nodes with crictl - K8s Docs](https://kubernetes.io/docs/tasks/debug/debug-cluster/crictl/)
- [Monitor node health - K8s Docs](https://kubernetes.io/docs/tasks/debug/debug-cluster/monitor-node-health/)
- [Troubleshoot kubectl access - K8s docs](https://kubernetes.io/docs/tasks/debug/debug-cluster/troubleshoot-kubectl/)
- [Kubectl debug - K8s Docs](https://kubernetes.io/docs/tasks/debug/debug-cluster/kubectl-node-debug/)

## FAQ

1. What are the main types of logs in Kubernetes and how do they help with troubleshooting?
Kubernetes primarily uses two types of logs: pod logs and event logs. Pod logs offer insights into the processes within a container, captured via standard output and standard error. They are essential for pinpointing issues within the application itself. Event logs, accessible using kubectl events, provide a chronological record of actions and events within the cluster, such as API interactions, scheduling decisions, and component statuses. These logs help trace back the root cause of problems and understand the sequence of events leading to an issue.

2. My pod is stuck in a "CrashLoopBackOff" state. How do I find out what's wrong?
A "CrashLoopBackOff" status indicates the container within the pod is repeatedly crashing and restarting. To troubleshoot, start by examining the pod logs using kubectl logs <pod-name>. The logs should contain error messages or stack traces that hint at the cause of the crash. If logs are unavailable or insufficient, use kubectl describe pod <pod-name> to view events related to the pod. These events may reveal issues with image pulling, resource limits, or configuration errors that prevent the pod from starting successfully.

3. How can I access logs from a specific container in a multi-container pod?
When dealing with pods containing multiple containers, you can target a specific container's logs using the -c flag with kubectl logs. For instance, kubectl logs <pod-name> -c <container-name> retrieves logs only from the specified container. This is particularly useful in scenarios where you need to isolate issues within a specific component of the application running inside the pod.

4. I suspect a node is experiencing resource pressure. How do I confirm and investigate this?
Resource pressure on a node usually manifests as high CPU or memory utilization, potentially impacting pod performance and stability. To investigate, use kubectl describe node <node-name> to check for conditions like "MemoryPressure" or "DiskPressure." Additionally, kubectl top nodes (requires the Metrics Server to be installed) provides real-time CPU and memory usage statistics for each node, enabling quick identification of resource-hungry nodes. If a particular node shows excessive resource consumption, investigate the pods running on that node using kubectl top pods --all-namespaces to identify potential culprits.

5. My application can't resolve internal service names. What steps should I take to troubleshoot?
Inability to resolve service names points towards DNS resolution problems within the cluster. First, ensure that the CoreDNS pods are running in the kube-system namespace using kubectl get pods -n kube-system. Next, get a shell into a pod in the affected namespace using kubectl exec -it <pod-name> -- sh. From within the pod, use nslookup <service-name> to test name resolution. If resolution fails, check CoreDNS logs for errors. You might also want to verify the DNS configuration within your pods and ensure it points to the correct ClusterDNS service.

6. How do I troubleshoot a service that doesn't seem to be routing traffic to any pods?
When a service fails to route traffic, it's often due to a mismatch between the service selector and pod labels. Use kubectl describe service <service-name> to inspect the service selector. Then, verify that pods belonging to the target application have matching labels using kubectl get pods -l <selector-key>=<selector-value>. Ensure the labels in the service definition align with the labels of the pods meant to receive traffic.

7. I'm unable to connect to the Kubernetes cluster. What are the initial troubleshooting steps?

Start by verifying the following:

kubeconfig accessibility: Ensure your kubeconfig file is located in the ~/.kube directory and has the correct permissions.
IP address and port accuracy: Confirm the control plane IP address and port specified in your kubeconfig match the actual cluster configuration.
Certificate validity: Verify that the certificates in your kubeconfig are valid and correspond to the certificates on the control plane.
API server status: Check if the API server pod is running in the kube-system namespace using kubectl get pods -n kube-system. If not, investigate the API server logs for errors.
8. The kubectl command is reporting "did you specify the right host or port?" What could be wrong?
This error message typically indicates a problem with the connection to the Kubernetes API server. Double-check the following:

API server availability: Ensure the API server pod is running and healthy.
Network connectivity: Verify that your network allows communication between your client machine and the API server's IP address and port.
Firewall rules: Check if any firewall rules are blocking traffic to the API server.
DNS resolution: If you're using a hostname to connect to the API server, confirm that it resolves to the correct IP address.