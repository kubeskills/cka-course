# WEEK 7 - CKA Book Course

Access the Book Here: [AcingTheCKA.com](https://acingthecka.com)

[WEEK 7 - Meeting Recording](https://community.kubeskills.com/c/meetings/volumes-persistentvolumes-persistentvolumeclaims-storage-class-chapter-7-review)

## Chapter 7 Overview
- Creating a volume in Kubernetes
- Persistent volume claims and storage classes
- Using storage with applications in Kubernetes

## CHAPTER 7 CHALLENGE

- [https://community.kubeskills.com/c/welcome-to-the-cka/chapter-7-challenge-simulate-data-catastrophe](https://community.kubeskills.com/c/welcome-to-the-cka/chapter-7-challenge-simulate-data-catastrophe)

## LINKS

- [Volumes - K8s docs](https://kubernetes.io/docs/concepts/storage/volumes/)
- [Persistent Volumes - K8s docs](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
- [Persistent Volume Claims - K8s Docs](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)
- [Storage Classes - k8s Docs](https://kubernetes.io/docs/concepts/storage/storage-classes/)
- [How to use a PV inside of a pod - K8s Docs](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)
- [Use NFS volumes for pods - Killercoda Lab](https://killercoda.com/chadmcrowell/course/ckad/nfs-vol)
- [More PV and PVC YAML - github link](https://github.com/chadmcrowell/k8s/blob/main/manifests/pvc.yml)

## FAQ

#### What are Kubernetes volumes and why are they necessary?
Kubernetes volumes provide persistent storage for applications running in pods. Unlike containers themselves, which are ephemeral and lose their data upon restart, volumes allow data to be preserved even when pods are terminated or rescheduled. This persistence is crucial for stateful applications that require ongoing access to their data.

#### What is the difference between a volume and a persistent volume?
A volume is a directory within a pod that can store data. While volumes can be used for temporary storage, they lack persistence and their data is lost upon pod termination. Persistent volumes (PVs), on the other hand, offer durable storage that exists independently of individual pods. PVs represent the underlying storage infrastructure, such as network file systems (NFS) or cloud-based block storage.

#### What is a persistent volume claim (PVC)?
A persistent volume claim (PVC) is a request for storage resources by a pod. It acts as a "claim" on an available persistent volume (PV). The PVC specifies the desired storage size, access modes, and other characteristics, but it doesn't directly interact with the underlying storage infrastructure.

#### How do storage classes relate to PVs and PVCs?
Storage classes enable administrators to define different tiers of storage with specific properties, such as performance characteristics or backup policies. When a PVC is created with a storage class specified, Kubernetes automatically provisions a PV matching the storage class requirements. This simplifies storage management and allows for dynamic provisioning of volumes.

#### What are the different types of volumes available in Kubernetes?
Kubernetes offers various volume types, including:

- EmptyDir: Provides temporary, non-persistent storage within a pod. Data is lost when the pod is deleted.
HostPath: Mounts a directory from the host node into the pod. Useful for temporary storage or sharing data between the pod and the host.
- NFS: Mounts an NFS share into the pod, providing persistent storage from an external NFS server.

#### What are volume modes and what are they used for?
Volume modes define how a volume is exposed to a pod. The two available modes are:

- Filesystem: The volume is presented as a directory with a standard file system, allowing applications to interact with it using typical file operations.
- Block: The volume is exposed as a raw block device, granting applications direct access to the storage without any filesystem abstraction.

#### What are access modes in the context of Kubernetes volumes?
Access modes determine how a volume can be mounted and accessed by pods. The three common access modes are:

- ReadWriteOnce (RWO): The volume can be mounted by only one pod at a time in read-write mode.
- ReadOnlyMany (ROX): The volume can be mounted by multiple pods simultaneously, but only in read-only mode.
- ReadWriteMany (RWX): The volume can be mounted by multiple pods concurrently in read-write mode.
- What are reclaim policies for persistent volumes and how do they work?
- Reclaim policies dictate what happens to a PV when it's no longer needed by a PVC. The available policies are:

- Retain: The data on the PV is preserved after the PVC is released, allowing for manual handling.
- Recycle: The PV is "scrubbed" by deleting existing data, preparing it for reuse by another PVC.
- Delete: The PV and its associated storage are permanently deleted when the PVC is released.