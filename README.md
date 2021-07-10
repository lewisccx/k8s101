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

### minikube service
assign external IP to a service
 minikube service [serviceName]
e.g. minikube service express-service

## kubectl CLI
for configuring the minikube cluster

## MiniKube CLI
for start/deleting the cluster

### see version
kubectl version

### Practice
deployment & Service in 1 file

### see all current services
kubectl get all

### see master node status in minikube
kubectl get nodes

### see master processes status in minikube
minikube status
kubectl get po -A

### see pod 
kubectl get pod
kubectl describe pod [podName]
*monitor mode*
kubectl get pod --watch
### create pod
kubectl create deployment NAME --image=image [--dry-run] [options]


### see services
kubectl get services
kubectl describe service [serviceName]

service endpoint should be same as your pod IP

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

### see all components in a deployment
kubectl get all | grep [appName]

### get into shell of pod
kubectl exec -it [podName] bash
exit

### delete pod using yaml file
kubectl delete -f nginx-deployment.yaml

### delete service using yaml file
kubectl delete -f nginx-service.yaml

## Secret yaml file
convert string to base64
echo -n 'your string' | base64

### create secret first before deployment
kubectl apply -f mongodb-secret.yaml
kubectl get secret

## '---' 3 dashes is yaml document separator

## What is a K8s namespace
virtual cluster inside k8s cluster
by default, 4 namespaces are given
kubectl get namespace

why use namespace
1. group resources in namespace
2. many teams, same application (accidentally deployed app with same name, override other team)
3. avoid re-deployment of share services
4. access and resource limits on Namespaces level

e.g of resource cannot be shared in namespace
1. Configmap
2. secret

e.g of resource can be shared in namespace
1. service

e.g of resource cannot be created  in namespace
1. volumn
2. node

### create namespace
kubectl create namespace [namespaceName]
or create namespace with configuration file
kubectl get namespace 

### create a component in a namespace
kubectl apply -f [file name] --namespace=[your namespace name]

or define namespace: [your namespace name] in yaml file

## change active namepace
by default, k8s show component from default namespace
if each team want to show component from different namespace

## for ingress controller, minikube setup only
0. start minikube dashboard
   minikube dashboard

1. minikube addons enable ingress

2. verify ingress controller has installed, 
   kubectl get pod -n kube-system
3. create ingress rule
   kubectl get ns
   kubectl get all -n kubernetes-dashboard
   

