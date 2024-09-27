# WEEK 2 - CKA Book Course

Access the Book Here: [AcingTheCKA.com](https://acingthecka.com)

[WEEK 2 - Meeting Recording](https://community.kubeskills.com/c/meetings/kubernetes-cluster-etcd-chapter-2-review)

## Chapter 2 Overview
- Control plane and worker node components in a multinode cluster
- Upgrading control plane components with kubeadm
- Investigating Pod and node networking
- Backing up and restoring etcd
- Taints and tolerations

## Links
- [Applying the 80/20 Rule to Kubernetes - KubeSkills Blog](https://blog.kubeskills.com/applying-the-8020-rule-to-kubernetes)
- [Installing Kubeadm, Kubelet, and Kubectl - K8s Docs](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#installing-kubeadm-kubelet-and-kubectl)
- [Cluster Architecture - K8s Docs](https://kubernetes.io/docs/concepts/architecture/)
- [Using `crictl` on Kubernetes nodes - K8s Docs](https://kubernetes.io/docs/tasks/debug/debug-cluster/crictl/)
- [Upgrading control Plane node - K8s Docs](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/#upgrading-control-plane-nodes)
- [Cloud Controller Manager - K8s Docs](https://kubernetes.io/docs/concepts/architecture/#cloud-controller-manager)
- [Controller Manager - K8s Docs](https://kubernetes.io/docs/concepts/architecture/#kube-controller-manager)

## Synopsis
In robotics and automation, a control loop is a non-terminating loop that regulates the state of a system. Here is one example of a control loop: a thermostat in a room. When you set the temperature, that's telling the thermostat about your desired state. The actual room temperature is the current state. The thermostat acts to bring the current state closer to the desired state, by turning equipment on or off. In Kubernetes, controllers are control loops that watch the state of your cluster, then make or request changes where needed. Each controller tries to move the current cluster state closer to the desired state. [source](https://kubernetes.io/docs/concepts/architecture/controller/)

`etcdctl` is the primary command-line client for interacting with etcd over a network. It is used for day-to-day operations such as managing keys and values, administering the cluster, checking health, and more. [source](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

**Kubelet:** An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod. The kubelet takes a set of PodSpecs that are provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy. The kubelet doesn't manage containers which were not created by Kubernetes. [source](https://kubernetes.io/docs/concepts/architecture/#kubelet)



![Diagram - Control Plane and Worker Node](<k8s-control-plane-and-worker-node-diagram (1).png>)