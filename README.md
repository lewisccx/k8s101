## Pod  <  Node
### Pod
e.g. abtraction of container, an app in a container, 1 app per pod
### Worker Node
e.g. virtual machine

3 proccess must be installed in a Node
1. container runtime e.g. docker
2. Kubelet, assign resource to a pod
3. Kube Proxy, forward the requests

### Master Node
 
4 processes in a master node
1. API server, cluster gateway, gatekeeper for authentication
    1. UI
    2. API
    3. CLI: kubectl
2. etcd, key-value Store, cluster brain, store cluster state information
3. Scheduler, place a new pod
4. Controller manager, detect cluster state changes, e.g. pod dies
### Service
internal service: internal facing, DB app
external service: public facing, web app
stand-alone permanent IP address attached to Pod
load balancer

### Ingress
forwarding request from service internally in a Node

### ConfigMap
external configuration of application

### Secret
used to store secret data
base64 encoded 

### Volumes
persistent

### StatefulSet
challenging to set up
for stateful app, DB app

## K8s
replicate everything, node , pod
DB apps are often hosted outside of K8s cluster

## minikube
Master process and worker process run in a Node
for testing local cluster setup
docker preinstalled

## kubectl CLI
for configuring the minikube cluster

## MiniKube CLI
for start/deleting the cluster

### see version
kubectl version

### see master node status in minikube
kubectl get nodes

### see master processes status in minikube
minikube status
kubectl get po -A

### see pod 
kubectl get pod
kubectl describe pod [podName]
### create pod
kubectl create deployment NAME --image=image [--dry-run] [options]
e.g. 

### see services
kubectl get services
kubectl describe service [serviceName]

### create deployment
kubectl create deployment [deploymentName] --image=[imageName]
touch [configfile.yaml]
kubectl apply -f [configfile.yaml]
kubectl delete -f [configfile.yaml]

### see all deployment
kubectl get deployment
*get updated config of yaml file with status spec*
kubectl get deployment [deploymentName] -o yaml > [outputFileName]
 kubectl get deployment nginx-deployment -o yaml > nginx-deployment-result.yaml
###  see replicaset
*managing the replica of a pod*
kubectl get replicaset

### edit deployment
kubectl edit deployment [deploymentName]

### delete deployment
kubectl delete deployment [deploymentName]

### see pod's log
kubectl logs [podName]

### get into shell of pod
kubectl exec -it [podName] bash
exit

### delete pod using yaml file
kubectl delete -f nginx-deployment.yaml

### delete service using yaml file
kubectl delete -f nginx-service.yaml