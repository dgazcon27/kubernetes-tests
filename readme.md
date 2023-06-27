
# [Kubernetes] Deploying a NodeJS app in Minikube (Local development)


## Appendix

A brief description of what this project does and who it's for

This blog will walk you through the steps of how to deploy a NodeJS application in MiniKube. We will be using a local docker image without relying on a Docker registry.

At this stage, I’m assuming you have a general idea of what Kubernetes is. If not https://kubernetes.io/ is a great place to start.

Before starting the tutorial, make sure you have the following installed on your machine (Assuming Docker and Node are pre-installed)

minikube: https://minikube.sigs.k8s.io/docs/start/
— Minikube is a tool to learn and develop Kubernetes locally

kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl/
— Kubectl is a command-line tool that allows you to control the Kubernetes cluster.

Note: Read more on Kubernetes components https://kubernetes.io/docs/concepts/overview/components/
## Installation

build docker image locally. Inside of node-app folder run

```bash
$docker build -t starwars-node .
$docker images
#you will see starwars-node image
```
Run a container with the image built previously

```bash
$docker run -d -p 3000:3000 starwars-node
$docker ps
#you will see the container running
```
## Kubernetes

Up to this point, we have been doing stuff that supports the main content.
From this point onward let’s work with minikube and kubectl .

First, we need to start the Kubernetes cluster. We can do this by running.

```bash
minikube start
```
Load image from local Docker to VM Docker running in minikube

```bash
eval $(minikube docker-env)

docker build -t starwars-node .
# Additionally you can check to see if starwars-node Docker image is in minikube by
minikube ssh
docker@minikube:~$ docker images
# You should see starward-node docker image
```
### Deployment app in Kubernetes

First we have to set enviroment variables that we will use in deployment

Navigate to ms_deployments folder and run

```bash
kubectl apply -f envs.yaml
```
We already had env variables loaded, next we are going to deploy with

```bash
kubectl apply -f sw_deploy.yaml
```
Now we have two pods running. Now what?

Service
Now we need to connect to these pods. Each pod has an associated IP address, but if we attempt to use these IPs to connect, it will become unmanageable when the number of Worker machines and prods increases. Here is where the concept of Service comes. It is an abstraction to access Pods without relying on lower-level details like IP addresses.

Note: Read https://kubernetes.io/docs/concepts/services-networking/service/ to learn more on Service

Now run the following commands,
```bash
kubectl apply -f sw-service.yaml
# service/sw-service created
kubectl get service
# Observe that sw-service created
minikube service sw-service --url
# http://<external_service_ip>:31000
```

Now run curl http://<external_service_ip>:31000 and see that you can get your favorite Star Wars character. This means we have successfully deployed the NodeJS application in the Kubernetes cluster. Yeyyy!