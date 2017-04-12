# Getting Started with Kubernates on macOS  

## What is Kubernetes?

Kubernetes is an open source system for automating deployment, scaling, and management of containerized applications. 
It is a project created to manage a cluster of Linux containers as a single system, managing and running Docker 
container across multiple hosts, offering co-location of containers, service discovery, and replication control. 

Kubernetes serves two purposes: It scales and starts containers across multiple Docker hosts, balancing the containers 
across them. It also adds a higher level API to define how containers are logically grouped, allowing defining pools of 
containers, loading balancing, and affinity. Kubernetes is defined by states, not processes. It builds upon 15 years of 
experience of running production workload at Google, combined with the best of breed ideas and practices from the community 
and it groups containers that make up an application into logical units for easy management and discovery.

Kubernetes is considered more production ready and has its own concepts of pods which makes it a bit more complex than
 Docker Swarm while on the other hand, Swarm is more Docker native, using cmd similar to the regular Docker CLI commands.
 
[Source](http://www.zymr.com/docker-vs-kubernetes/)

## Main concepts

### Pods

A Pod is the basic building block of Kubernetes–the smallest and simplest unit in the Kubernetes object model that you create or deploy. A Pod represents a running process on your cluster.

### Deployments

A Deployment provides declarative updates for Pods and Replica Sets. You only need to describe the desired state in a Deployment object, and the Deployment controller will change the actual state to the desired state at a controlled rate for you.

### Services

A Kubernetes Service is an abstraction which defines a logical set of Pods and a policy by which to access them - sometimes called a micro-service.
 
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