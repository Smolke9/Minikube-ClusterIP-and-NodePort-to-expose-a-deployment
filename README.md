
# 🚀 Expose a Deployment using ClusterIP and NodePort in Minikube

This guide walks you through creating a Kubernetes Deployment and exposing it using **ClusterIP** and **NodePort** services in a **Minikube** cluster.

---

## 🛠️ Prerequisites

- Minikube installed and started
- kubectl configured
- Docker (used by Minikube)

---

## 🔁 Step 1: Start Minikube

```bash
minikube start
```

---

## 📁 Step 2: Create a Deployment

Create a file named `nginx-deployment.yaml`.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.25.3
        ports:
        - containerPort: 80
```

Apply the Deployment:

```bash
kubectl apply -f nginx-deployment.yaml
```

---

## 🔍 Step 3: Verify Pods

```bash
kubectl get pods
```

---

## 🌐 Step 4: Expose via ClusterIP

```bash
kubectl expose deployment nginx-deployment   --type=ClusterIP   --port=80   --target-port=80   --name=nginx-clusterip
```

### ✅ Verify ClusterIP service

```bash
kubectl get svc
```

You will see a service with `TYPE = ClusterIP`.

---

## 🌐 Step 5: Expose via NodePort

```bash
kubectl expose deployment nginx-deployment   --type=NodePort   --port=80   --target-port=80   --name=nginx-nodeport
```

### ✅ Verify NodePort service

```bash
kubectl get svc
```

Find the `PORT(S)` column to note the NodePort (e.g., `30036:80/TCP`).

---

## 🌐 Step 6: Access the Application

### 🧪 Open in Browser

Use Minikube's IP:

```bash
minikube ip
```

Then open in browser:

```
http://<minikube-ip>:<nodeport>
```

Example:

```
http://192.168.49.2:30036
```

---

## 🧹 Cleanup

```bash
kubectl delete svc nginx-nodeport nginx-clusterip
kubectl delete deployment nginx-deployment
```

---

## 📸 Optional: Add Screenshot to README

```markdown
![Minikube Service Screenshot](screenshots/minikube-services.jpg)
```

---

## 📦 Files in This Repo

```
.
├── nginx-deployment.yaml
└── README.md
```

---

## 📚 Useful Commands

```bash
kubectl get all
kubectl describe svc nginx-clusterip
kubectl describe svc nginx-nodeport
minikube service nginx-nodeport --url
```

---

## 📢 Author

**Suraj Molke**  
GitHub: [your-profile-url]  
LinkedIn: [your-linkedin-url]

---
