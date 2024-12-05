# CosmoCloud Deploy

This is a Helm chart for deploying a sample application to a Kubernetes cluster.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Kubernetes Prerequisites](#kubernetes-prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)


## Introduction

This Helm chart deploys a sample application consisting of a frontend, backend, and Redis service to a Kubernetes cluster.

## Prerequisites

- Kubernetes cluster [ You can use minikube ]
- Helm installed on your machine
- Docker installed on your machine (for building images)
- Create a account on [DockerHub](https://hub.docker.com/)
- Basic knowledge of Docker and Kubernetes concepts, including:
  - Docker: containerization, images
  - Kubernetes: pods, services, deployments, and configmaps

## Kubernetes Prerequisites

- Familiarity with Kubernetes networking concepts, including:
  -ClusterIP: a virtual IP address that allows access to a service within the cluster

  # Sample YAML for ClusterIP
```
   apiVersion: v1
  kind: Service
  metadata:
    name: cluster-svc
    labels:
        env: demo
  spec:
    ports:
      - port: 80
    selector:
        env: demo
```
- NodePort: a port that allows access to a service from outside the cluster

  # Sample YAML for Nodeport
```
  apiVersion: v1
  kind: Service
  metadata:
    name: nodeport-svc
    labels:
        env: demo
  spec:
    type: NodePort
    ports:

    - nodePort: 30001
      port: 80
      targetPort: 80
    selector:
      env: demo
```
- Knowledge of how to create a ConfigMap in Kubernetes, including:
  - Creating a ConfigMap from a file or literal value
  - Using a ConfigMap to store application configuration data

## Installation

1. Clone this repository to your machine.
2. Run `helm install testapp .` to install the chart.
3. Verify that the deployments are deployed with `kubectl get deployments`.
4. Verify that the pods are running with `kubectl get pods`.

## Usage

1. To access the applcation: Run the command `minikube service frontend-svc` or `kubectl port-forward svc/frontend-svc 5175:5175` then access the frontend service by visiting `http://localhost:5175` in your web browser.
2. If the frontend service does not work, try accessing the backend service by running `minikube service backend-svc` and following the instructions to access the service.
3. Use the `kubectl port-forward` command to forward traffic to the backend service.


## Troubleshooting

- Check the pod logs with `kubectl logs <pod-name>`.
- Check the service status with `kubectl get svc <service-name>`.
- Check the Helm release status with `helm status testapp`.
