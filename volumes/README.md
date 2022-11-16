PV --> It's a piece of storage(hostPath,nfs,ebs,azurefile,azuredisk) in k8s cluster. PV exists independently from 
from pod life cycle whihc is consuming.

Persistent Volumes are provisioned in two ways, Statically or Dynamically.

1) Static Volumes (Manual Provisionging)
    As a k8's Administrator will create a PV manullay so that pv's can be avilable for PODS which requires.
	Create a PVC so that PVC will be attached PV. We can use PVC with PODS to get an access to PV. 
	
2) Dynamic Volumes (Dynamic Provisioning)
     It's possible to have k8's provsion(Create) volumes(PV) as required. Provided we have configured storageClass.
	 So when we create PVC if PV is not available Storage Class will Create PV dynamically.
   

PVC
If pod requires access to storage(PV),it will get an access using PVC. PVC will be attached to PV.



PersistentVolume – the low level representation of a storage volume.
PersistentVolumeClaim – the binding between a Pod and PersistentVolume.
Pod – a running container that will consume a PersistentVolume.
StorageClass – allows for dynamic provisioning of PersistentVolumes.


PV Will have Access Modes

ReadWriteOnce – the volume can be mounted as read-write by a single node
ReadOnlyMany – the volume can be mounted read-only by many nodes
ReadWriteMany – the volume can be mounted as read-write by many nodes

In the CLI, the access modes are abbreviated to:

RWO - ReadWriteOnce
ROX - ReadOnlyMany
RWX - ReadWriteMany


Claim Policies

A Persistent Volume can have several different claim policies associated with it including

Retain – When the claim is deleted, the volume remains.
Recycle – When the claim is deleted the volume remains but in a state where the data can be manually recovered.
Delete – The persistent volume is deleted when the claim is deleted.
The claim policy (associated at the PV and not the PVC) is responsible for what happens to the data on when the claim has been deleted.


Commands

kubectl get pv
kubectl get pvc
kubectl get storageclass
kubectl describe pvc <pvcName>
kubectl describe pv <pvName>
