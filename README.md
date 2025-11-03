# minikube-nginx
## 🧭 TASK 5: Build a Kubernetes Cluster Locally with Minikube

### 🎯 **Objective**

Set up a local Kubernetes cluster using **Minikube** and deploy a simple **Nginx application** using **Kubernetes manifests**.

---

### 🧰 **Tools Used**

* **Minikube** – local Kubernetes cluster
* **kubectl** – Kubernetes command-line tool
* **Docker** – container runtime

---

### ⚙️ **Steps Performed**

#### **1. Start Minikube**

```bash
minikube start --driver=docker
```

Verify the cluster:

```bash
minikube status
```

---

#### **2. Create Deployment**

📄 **deployment.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp-container
        image: nginx:latest
        ports:
        - containerPort: 80
```

Apply the deployment:

```bash
kubectl apply -f deployment.yaml
```

Check pods and deployments:

```bash
kubectl get deployments
kubectl get pods
```

---

#### **3. Create Service**

📄 **service.yaml**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```

Apply the service:

```bash
kubectl apply -f service.yaml
```

Verify:

```bash
kubectl get svc
```

---

#### **4. Scale the Deployment**

Increase replicas:

```bash
kubectl scale deployment myapp-deployment --replicas=4
kubectl get pods
```

---

#### **5. Inspect Resources and Logs**

```bash
kubectl describe deployment myapp-deployment
kubectl describe svc myapp-service
kubectl logs <pod-name>
```

---


#### **7. Stop or Delete Cluster**

```bash
minikube stop
minikube delete
```

---


### 🏁 **Outcome**

* Set up and ran a Kubernetes cluster using Minikube
* Deployed an Nginx app using a Kubernetes **Deployment**
* Exposed it through a **Service (NodePort)**
* Scaled and verified your deployment
---
<img width="1066" height="740" alt="Screenshot 2025-11-03 214324" src="https://github.com/user-attachments/assets/0227584b-9a76-4987-9648-cb9c77bb3b81" />
