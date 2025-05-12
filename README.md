# Kubernetes Deployment for Support Desk Project

## Files Included

| File                    | Description                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| `backend-deployment.yaml`  | Deploys the backend service and exposes it via a ClusterIP service.        |
| `frontend-deployment.yaml` | Deploys the frontend application and exposes it via a NodePort service.    |
| `mongodb-secret.yaml`      | Defines MongoDB credentials securely using a Kubernetes Secret.            |
| `mongodb-service.yaml`     | Creates a headless service to expose MongoDB internally to the cluster.    |
| `mongodb-statefulset.yaml` | Deploys MongoDB as a StatefulSet with persistent volume support.           |

---

## Deployment Instructions

Make sure you have [Minikube](https://minikube.sigs.k8s.io/) running, then apply the files in the following order:

```bash
kubectl apply -f mongodb-secret.yaml
kubectl apply -f mongodb-statefulset.yaml
kubectl apply -f mongodb-service.yaml
kubectl apply -f backend-deployment.yaml
kubectl apply -f frontend-deployment.yaml
```

## MongoDB Access
MongoDB is deployed with credentials stored in mongodb-secret.yaml.

Username: Defined by mongo-user key in the secret

Password: Defined by mongo-password key

Connection string (inside cluster)

To access the DB via mongo shell:

```bash
kubectl run -it --rm mongo-client --image=mongo -- bash
```

then
```bash
mongo --host mongodb-0.mongodb --username <user> --password <password> --authenticationDatabase admin
```


