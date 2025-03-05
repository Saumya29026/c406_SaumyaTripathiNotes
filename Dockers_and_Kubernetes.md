# Dockers and Kubernetes Notes

---

## Introduction to Docker
Docker is a platform for developing, shipping, and running applications in containers. Containers allow you to package an application with all its dependencies into a standardized unit.

### Key Concepts:
- **Container**: A lightweight, standalone, and executable package that includes everything needed to run a piece of software.
- **Image**: A read-only template used to create containers.
- **Dockerfile**: A text file that contains instructions for building a Docker image.

---

## Docker Commands
Here are some commonly used Docker commands:

- `docker build -t <image_name> .`: Build a Docker image from a Dockerfile.
- `docker run <image_name>`: Run a container from an image.
- `docker ps`: List running containers.
- `docker stop <container_id>`: Stop a running container.

---

## Basic Commands
- docker build -t <image_name> .: Build a Docker image from a Dockerfile.
- docker run <image_name>: Run a container from an image.
- docker ps: List running containers.
- docker stop <container_id>: Stop a running container.

## Advanced Commands
- docker logs <container_id>: View logs from a container.
- docker exec -it <container_id> /bin/bash: Access a running container's shell.
- docker push <image_name>: Push an image to Docker Hub.
- docker pull <image_name>: Pull an image from Docker Hub.
- docker network ls: List all Docker networks.
- docker volume ls: List all Docker volumes


---

# Introduction to Kubernetes
Kubernetes (K8s) is an open-source platform for automating the deployment, scaling, and management of containerized applications.

## Why Use Kubernetes?
- Scalability: Automatically scale applications based on demand.
- High Availability: Ensure applications are always running.
- Self-Healing: Automatically restart failed containers.

##Kubernetes Concepts
1. Pod
A Pod is the smallest deployable unit in Kubernetes. It can contain one or more containers.

2. Node
A Node is a physical or virtual machine that runs containers. There are two types:
- Worker Node: Runs the application workloads.
- Master Node: Manages the cluster.

3. Cluster
A Cluster is a set of nodes that run containerized applications.

4. Deployment
A Deployment defines how an application should be deployed and updated.

5. Service
A Service provides a stable IP address and DNS name for accessing Pods.

## Kubernetes Basic Commands
- kubectl get pods: List all pods in the current namespace.
- kubectl apply -f <config_file>: Apply a configuration file to create or update resources.
- kubectl delete pod <pod_name>: Delete a pod.
- kubectl logs <pod_name>: View logs from a pod.

##Advanced Commands
- kubectl scale deployment <deployment_name> --replicas=3: Scale a deployment to 3 replicas.
- kubectl describe pod <pod_name>: Get detailed information about a pod.
- kubectl expose deployment <deployment_name> --type=LoadBalancer --port=80: Expose a deployment as a service.

## Docker vs Kubernetes
| Feature                | Docker                          | Kubernetes                      |
|------------------------|---------------------------------|---------------------------------|
| **Purpose**            | Containerization                | Container orchestration         |
| **Scaling**            | Manual                          | Automatic                       |
| **Networking**         | Basic                           | Advanced                        |
| **Self-Healing**       | No                              | Yes                             |
| **Use Case**           | Single-host applications        | Multi-host, large-scale systems |
