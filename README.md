To **work on the project involving Node Scaling and Maintenance in Minikube**, follow the steps below. This guide breaks down how to **scale nodes**, **upgrade Minikube**, and effectively **simulate production-like environments** using a local Minikube setup.

---

## ✅ Prerequisites

Ensure the following are installed:

* **Minikube**
* **kubectl**
* **VirtualBox or Docker** (as VM driver)

---

## ⚙️ 1. Start Minikube

```bash
minikube start --cpus=2 --memory=500
```

This creates a single-node cluster with 2 CPUs and 500MB memory. But it gives error that 500MB is less than usuable minimum memory.
![caption](/img/6.minikube-start-cpu-ram.jpg)
```bash
minikube start --cpus=2 --memory=500

```
This creates a single-node cluster with 2 CPUs and 500MB memory
![caption](/img/7.minikube-cpu-ram.jpg)
---

## 🔁 2. Node Scaling in Minikube

Minikube is typically single-node, but you can simulate multiple nodes using profiles.

### Option A: Add more simulated nodes (not truly multi-node but for testing):

You can create multiple Minikube instances with different profiles:

```bash
minikube start -p node1
minikube start -p node2
```
![caption](/img/8.minikube-node1.jpg)

> Note: This does **not simulate a real multi-node cluster**, but it helps mimic some behavior.

### Option B: Use Kubeadm/DIND or other tools for real multi-node (optional):

For advanced setups (like multi-node), you may want to use:

* [Kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)
* [KIND (Kubernetes in Docker)](https://kind.sigs.k8s.io/)

---

## 🔄 3. Upgrade Minikube Kubernetes Version

To simulate upgrading the Kubernetes version:

```bash
minikube delete
minikube start --kubernetes-version=v1.28.0
```

Check version:

```bash
kubectl version --short
```
![caption](/img/10.kuber-version.jpg)

---

## 🔍 4. Check Nodes and Their Status

```bash
kubectl get nodes
```
![caption](/img/11.get-node.jpg)
---

## 🚀 5. Deploy a Test App

Create a simple app:

```bash
kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10
kubectl expose deployment hello-minikube --type=NodePort --port=8080
```
to see the cont
Access it:

```bash
minikube service hello-minikube
```
![caption](/img/13.minikube-service.jpg)
---

## 🔧 6. Maintenance Commands

### Stop cluster:

```bash
minikube stop
```

### Start again:

```bash
minikube start
```

### Delete cluster:

```bash
minikube delete
```

---

