Namespace
   │
   ├── Pod
   │
   ├── ReplicaSet
   │      │
   │      └── Pods
   │
   ├── Deployment
   │      │
   │      └── ReplicaSet
   │             │
   │             └── Pods
   │
   ├── DaemonSet
   │      └── Pod on each node
   │
   ├── StatefulSet
   │      ├── Pod
   │      └── PVC
   │
   ├── Job
   │
   └── CronJob

Networking
   ├── ClusterIP
   ├── NodePort
   ├── LoadBalancer
   └── Ingress

Configuration
   ├── ConfigMap
   └── Secret

Storage
   ├── StorageClass
   ├── PVC
   └── PV

Security
   ├── ServiceAccount
   ├── Role
   ├── RoleBinding
   ├── ClusterRole
   └── ClusterRoleBinding

Scaling
   ├── HPA
   └── PDB

Scheduling
   ├── Labels
   ├── NodeSelector
   ├── Affinity
   ├── Taints/Tolerations
   └── PriorityClass

Advanced
   ├── NetworkPolicy
   ├── InitContainer
   ├── Sidecar
   ├── Probes
   └── Lifecycle

Pre-Requisities:

aws --version
kubectl version --client

##How to connect to  EKS cluster
aws eks update-kubeconfig \
  --region us-east-1 \
  --name <cluster-name>

Verify the cluster set-up using:

kubectl config current-context
kubectl get nodes
kubectl get nodes -o wide
kubectl cluster-info 
kubectl api-resources #list all the apis

AWS
 │
 └── EKS Cluster
       │
       ├── Control Plane
       │
       └── Worker Nodes
             │
             └── Kubernetes Resources

##how to create namespace ## Namespaces provide logical isolation inside a Kubernetes cluster.
1.To create it via command line using kubectl use below command 
   kubectl create ns <your-namespace-name>
2.To create via the yaml file,use namespace.yaml and run below command
   kubectl apply -f namespace.yaml 


##How to create a pod

A Pod is the smallest deployable unit in Kubernetes. A Pod normally contains one application container, although it can contain multiple tightly coupled containers.

1.We can create a pod using kubectl pod command but not recommended
2.The ideal way to create a pod is using pod manifest that is pod.yaml using command
    kubectl apply -f pod.yaml -n <your-namespace-name>
    kubectl get pods -n k8s-demo
    kubectl get pods -o wide -n k8s-demo
    kubectl describe pod nginx-pod -n k8s-demo
    kubectl logs nginx-pod -n k8s-demo
    kubectl exec -it nginx-pod -n k8s-demo -- /bin/bash 
    kubectl delete pod nginx-pod -n k8s-demo


##commands for replicaset.yaml
    kubectl get rs -n k8s-demo
    kubectl get pods -n k8s-demo 

    ##Deployment

    Why Deployment?

ReplicaSet handles replicas, but Deployment gives us:

Rolling updates
Rollbacks
Version management
ReplicaSet management

--------------------------------------

Module 1 — Kubernetes/EKS Foundation
EKS architecture
Control plane vs worker nodes
AWS CLI
kubeconfig
kubectl
Namespace
Pod
Module 2 — Workload Management
ReplicaSet
Deployment
Rolling update
Rollback
DaemonSet
StatefulSet
Job
CronJob
Module 3 — Networking
Pod networking
Service
ClusterIP
NodePort
LoadBalancer
Ingress
AWS Load Balancer Controller
DNS
Module 4 — Configuration
ConfigMap
Secret
Environment variables
Volume-mounted configuration
Module 5 — Storage
Storage concepts
StorageClass
PersistentVolume
PersistentVolumeClaim
EBS CSI
StatefulSet + PVC
Module 6 — Security
ServiceAccount
Role
RoleBinding
ClusterRole
ClusterRoleBinding
kubectl auth can-i
EKS IAM integration
Module 7 — Scheduling
Labels
NodeSelector
Node Affinity
Taints
Tolerations
PriorityClass
Module 8 — Reliability & Scaling
Requests
Limits
HPA
PDB
Probes
Rolling deployments
Module 9 — Advanced Kubernetes
NetworkPolicy
InitContainers
Sidecars
Lifecycle hooks
Graceful termination
Pod security concepts

##The Most Important kubectl Commands

Cluster:

kubectl cluster-info
kubectl get nodes
kubectl get nodes -o wide
kubectl get namespaces
kubectl api-resources

Resources:

kubectl get pods
kubectl get deployment
kubectl get rs
kubectl get daemonset
kubectl get statefulset
kubectl get svc
kubectl get ingress
kubectl get configmap
kubectl get secret
kubectl get pvc
kubectl get pv
kubectl get jobs
kubectl get cronjobs

All Resources:

kubectl get all -n k8s-demo

YAML:

kubectl apply -f file.yaml
kubectl delete -f file.yaml
kubectl get pod <pod> -o yaml

Debugging:

kubectl describe pod <pod>
kubectl logs <pod>
kubectl logs <pod> -c <container>
kubectl exec -it <pod> -- /bin/sh

Watch:

kubectl get pods -w

Labels:

kubectl get pods --show-labels
kubectl get pods -l app=nginx

Scheduling:

kubectl get nodes --show-labels
kubectl describe node <node>

Events:

kubectl get events \
  -n k8s-demo \
  --sort-by='.lastTimestamp'

