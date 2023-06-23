
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