# Getting Started with Kubernates on macOS  

## What is Kubernetes?

Kubernetes serves two purposes: It scales and starts containers across multiple Docker hosts, balancing the containers 
across them. It also adds a higher level API to define how containers are logically grouped, allowing defining pools of 
containers, loading balancing, and affinity. Kubernetes is defined by states, not processes.

[Source](http://www.zymr.com/docker-vs-kubernetes/)

## Main concepts

### Pods

A Pod represents a running process on your cluster.

### Services

A Service defines a logical set of Pods and a policy by which to access them.

### Deployments
 
A Deployment provides declarative updates for Pods. You only need to describe the desired state in a Deployment object, and the Deployment controller will change the actual state to the desired state for you.

[Learn more](https://kubernetes.io/docs/concepts/)

## Prerequisites

[Minikube](https://github.com/kubernetes/minikube) is the recommended method to create a single node Kubernetes cluster locally for purposes of development and testing. 

Installing Minikube (along with Docker and VirtualBox) via Homebrew:

```bash
brew update && brew install kubectl && brew cask install docker minikube virtualbox
```

Verifying:

```bash
docker --version                
docker-compose --version        
docker-machine --version        
minikube version                
kubectl version --client
```

Starting Minikube:

```bash
minikube start
```

Great! Minikube started a virtual machine for you, and a Kubernetes cluster is now running in that VM.

Setting Docker environment variables:

```bash
eval $(minikube docker-env)
```

[Learn more](https://gist.github.com/kevin-smets/b91a34cea662d0c523968472a81788f7)

## 1. Building Docker image

```bash
docker build -t hello-node:v1 .
```

## 2. Creating or updating configuration

```bash
kubectl apply -f service.yaml 
```

## 3. Accessing service

```bash
curl $(minikube service hello-node --url)
```

## 4. Accessing Minikube dashboard

```bash
minikube dashboard
```

## Cleanup

Deleting deployment and service:

```bash
kubectl delete service,deployment hello-node
```

Stopping Minikube:

```bash
minikube stop
```

To be continued...