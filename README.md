
# MongoDB + Mongo Express on Kubernetes

This project demonstrates deploying a basic MongoDB instance with Mongo Express, a web-based MongoDB admin interface, using Kubernetes.

It covers the following Kubernetes concepts:

- **Deployments** for MongoDB and Mongo Express
- **Services**: ClusterIP (for internal DB access) and NodePort (for external UI access)
- **Secrets** to store credentials
- **ConfigMaps** for environment configuration

---

## 🧱 Architecture

```

\[ MongoDB Pod ] <-- ClusterIP --> \[ Mongo Express Pod ] <-- NodePort --> \[ Browser ]

````

- `mongodb`: Exposed internally via a ClusterIP service
- `mongo-express`: Connects to MongoDB using environment variables and exposes a UI on port `30081`

---

## 📁 Project Files

| File                        | Purpose                                    |
|----------------------------|--------------------------------------------|
| `mongodb-secret.yaml`      | Base64-encoded root username & password    |
| `mongodb-configmap.yaml`   | MongoDB service name reference             |
| `mongodb-deployment.yaml`  | MongoDB Deployment + ClusterIP Service     |
| `mongo-express-deployment.yaml` | Mongo Express Deployment + NodePort Service |

---

## Deploy Instructions

1. Apply secrets and configmap:
   ```bash
   kubectl apply -f mongodb-secret.yaml
   kubectl apply -f mongodb-configmap.yaml
````

2. Deploy MongoDB:

   ```bash
   kubectl apply -f mongodb-deployment.yaml
   ```

3. Deploy Mongo Express:

   ```bash
   kubectl apply -f mongo-express-deployment.yaml
   ```

---

## Access Mongo Express

1. Get the public IP of the node Mongo Express was deployed to:

   ```bash
   kubectl get nodes -o wide
   ```

2. Visit in your browser:

   ```
   http://<node-public-ip>:30081
   ```

---

## 🧹 Clean Up

To delete all resources:

```bash
kubectl delete -f .
```

---

## 🔐 Notes

* Secrets are stored in base64 (not encrypted). Don't commit real credentials.
* This is a demo setup; not suitable for production without added security.

---

## 📌 Requirements

* Kubernetes cluster used AWS EC2 (Self managed)
* `kubectl` configured for the cluster

---

## ✅ Status

✅ Works as expected
📦 Simple, self-contained deployment
🛠️ Ideal for learning Kubernetes basics with databases

```

