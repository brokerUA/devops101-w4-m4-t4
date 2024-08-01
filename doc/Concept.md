# Concept. Comparative Analysis of Tools for Deploying Kubernetes Clusters: minikube, kind, k3d

## Introduction

This document provides a comparative analysis of three tools for deploying Kubernetes clusters in a local environment: **minikube**, **kind**, and **k3d**. The goal is to determine the optimal tool for the startup "AsciiArtify", which plans to develop a software product for converting images to ASCII art using Machine Learning. The tools are evaluated based on various criteria, such as supported operating systems, automation capabilities, additional features, ease of use, deployment speed, stability, documentation, and community support.

## Characteristics

| Characteristic             | minikube                       | kind                            | k3d                             |
|----------------------------|--------------------------------|---------------------------------|---------------------------------|
| Supported OS               | Windows, macOS, Linux          | Windows, macOS, Linux           | Windows, macOS, Linux           |
| Architectures              | x86-64, ARM                    | x86-64, ARM                     | x86-64                          |
| Automation                 | Yes                            | Yes                             | Yes                             |
| Monitoring                 | Not built-in                   | Not built-in                    | Not built-in                    |
| Cluster Management         | Yes                            | Yes                             | Yes                             |
| Uses Docker                | Yes                            | Yes                             | Yes                             |
| Podman Alternative         | Yes                            | No                              | No                              |

## Advantages and Disadvantages

### minikube

**Advantages:**
- Easy to use for beginners.
- Supports various drivers (Docker, VirtualBox, KVM, Hyper-V).
- Quick to deploy.

**Disadvantages:**
- Limited scalability.
- Uses additional resources for virtual machines.
- Potential performance issues on low-end machines.

### kind

**Advantages:**
- Easy to set up and use.
- High deployment speed.
- Uses Docker containers, reducing system load.

**Disadvantages:**
- Does not support alternative container platforms like Podman.
- Less beginner-friendly compared to minikube.

### k3d

**Advantages:**
- Fast deployment of clusters in Docker containers.
- Easy to set up.
- Supports Rancher Kubernetes Engine (RKE).

**Disadvantages:**
- Limited to x86-64 architecture.
- Does not support alternative container platforms like Podman.
- Potential issues with application integration due to Docker container limitations.

## Demonstration

### Recommended Tool: k3d

#### Example of Deploying a "Hello World" Application on Kubernetes

![Demo GIF](https://raw.githubusercontent.com/brokerUA/devops101-w4-m4-t4/main/doc/resoures/concept_01__demo.gif)

1. Install k3d:
    ```sh
    curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash
    ```

2. Create a cluster:
    ```sh
    k3d cluster create mycluster
    ```

3. Check the status of the cluster:
    ```sh
    kubectl get nodes
    ```

4. Create and deploy the "Hello World" application:
    ```sh
    kubectl create deployment hello-node --image=k8s.gcr.io/echoserver:1.4
    kubectl expose deployment hello-node --type=LoadBalancer --port=8080
    ```

5. **Port Forwarding**:

    ```sh
    kubectl port-forward service/hello-node 8080:8080
    ```

    This command will forward the port `8080` of the `hello-node` service to your local machine's port `8080`. Then, you can access the application by navigating to `http://localhost:8080` in your web browser or by using `curl`:

6. **Testing with curl**:

    ```sh
    curl http://localhost:8080
    ```

    You should receive a response similar to the following:
    ```sh
    Hostname: hello-node-xxxx
    ```


## Conclusions

- **minikube** is suitable for beginners and for quick deployment and testing but has limited scalability and potential performance issues on low-end machines.
- **kind** is an efficient and fast tool for deploying clusters in Docker containers but does not support alternative containerization platforms like Podman.
- **k3d** offers fast and easy deployment of clusters using Rancher Kubernetes Engine (RKE) and is well-suited for the PoC of the "AsciiArtify" startup due to its speed and ease of setup.

Based on the comparative analysis, it is recommended to use **k3d** for deploying a local Kubernetes cluster for the PoC of the "AsciiArtify" startup.

