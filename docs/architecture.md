# Architecture - Kubernetes MongoDB + Mongo Express

## Overview

This project demonstrates the deployment of a MongoDB database and Mongo Express administration UI on a Kubernetes cluster using Minikube.

The project showcases fundamental Kubernetes concepts including:

* Deployments
* Pods
* Services
* ConfigMaps
* Secrets
* Service Discovery

## Architecture Diagram

```text
+------------------+
|      Browser     |
+------------------+
          |
          v
+-----------------------+
| Mongo Express Service |
| (LoadBalancer)        |
+-----------------------+
          |
          v
+-----------------------+
| Mongo Express Pod     |
+-----------------------+
          |
          v
+-----------------------+
| MongoDB Service       |
| (ClusterIP)           |
+-----------------------+
          |
          v
+-----------------------+
| MongoDB Pod           |
+-----------------------+
```

## Components

### MongoDB Deployment

MongoDB is deployed using a Kubernetes Deployment resource.

Responsibilities:

* Creates MongoDB Pod
* Maintains desired state
* Restarts Pod if it fails

Container Image:

```text
mongo
```

Port:

```text
27017
```

---

### MongoDB Service

A ClusterIP service exposes MongoDB internally within the Kubernetes cluster.

Service Name:

```text
mongodb-service
```

Port:

```text
27017
```

Purpose:

* Provides stable network endpoint
* Enables service discovery
* Allows Mongo Express to connect without knowing Pod IP

---

### Secret

Sensitive credentials are stored in a Kubernetes Secret.

Stored Values:

* MongoDB Root Username
* MongoDB Root Password

Purpose:

* Prevent hardcoding credentials
* Secure injection into containers

Used By:

* MongoDB Deployment
* Mongo Express Deployment

---

### ConfigMap

Application configuration is stored in a ConfigMap.

Stored Values:

```text
database_url = mongodb-service
```

Purpose:

* Store non-sensitive configuration
* Decouple configuration from application code

---

### Mongo Express Deployment

Mongo Express provides a web-based interface for MongoDB administration.

Responsibilities:

* Connect to MongoDB
* Display databases and collections
* Manage documents

Container Image:

```text
mongo-express
```

Port:

```text
8081
```

---

### Mongo Express Service

A LoadBalancer service exposes Mongo Express outside the cluster.

Service Name:

```text
mongo-express-service
```

Port:

```text
8081
```

In Minikube:

```bash
minikube service mongo-express-service
```

creates a temporary tunnel to access the application.

---

## Request Flow

### User Access

1. User opens Mongo Express URL.
2. Request reaches Mongo Express Service.
3. Service forwards traffic to Mongo Express Pod.
4. Mongo Express reads MongoDB connection details.
5. Mongo Express connects to MongoDB Service.
6. MongoDB Service routes traffic to MongoDB Pod.
7. MongoDB returns data.
8. Mongo Express displays data in the browser.

## Kubernetes Concepts Demonstrated

### Pods

Smallest deployable unit in Kubernetes.

Used:

* MongoDB Pod
* Mongo Express Pod

### Deployments

Provide:

* Pod lifecycle management
* Self-healing
* Scaling

### Services

Provide:

* Stable networking
* Service discovery
* Load balancing

### ConfigMaps

Used for:

* Application configuration
* Environment-specific settings

### Secrets

Used for:

* Database credentials
* Sensitive application data

## Learning Outcomes

By completing this project, the following Kubernetes concepts are demonstrated:

* Kubernetes Architecture
* Deployments
* Pods
* Services
* ConfigMaps
* Secrets
* Internal Service Communication
* Environment Variables
* Service Discovery
* Minikube Networking

## Future Improvements

* Persistent Volumes (PV)
* Persistent Volume Claims (PVC)
* Ingress Controller
* Helm Charts
* StatefulSets
* Monitoring with Prometheus and Grafana
* Deployment on AWS EKS

```
```
