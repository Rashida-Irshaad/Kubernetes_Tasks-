# Task 
# KodeKloud Task: Create an Nginx Deployment on Kubernetes

## Task Description

The Nautilus DevOps team is delving into Kubernetes for app management. One team member needs to create a deployment following these details:

Create a deployment named `nginx` to deploy the application `nginx` using the image `nginx:latest` (ensure to specify the tag).

Note: The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

---

## Solution Steps

### Step 1: Check that kubectl works

```bash
kubectl get nodes
```

You should see a list of nodes with status `Ready`.

### Step 2: Create the deployment

```bash
kubectl create deployment nginx --image=nginx:latest
```

Expected output:

```
deployment.apps/nginx created
```

### Step 3: Verify the deployment

```bash
kubectl get deployments
```

Expected output (the `READY` column may show `0/1` for a few seconds, then `1/1`):

```
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   1/1     1            1           30s
```

### Step 4: Check the pod is running

```bash
kubectl get pods
```

Expected: a pod named like `nginx-xxxxxxxxxx-xxxxx` with status `Running`.

### Step 5: Confirm the image and tag (optional)

```bash
kubectl describe deployment nginx | grep Image
```

Expected:

```
Image:        nginx:latest
```

---

## Alternative: Using a YAML file

If you prefer a file-based approach, create it with `cat` to avoid indentation problems:

```bash
cat > nginx-deployment.yaml << 'EOF'
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
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
          image: nginx:latest
EOF

kubectl apply -f nginx-deployment.yaml
```

---

## How It Works

- `kubectl create deployment nginx` creates a deployment named `nginx`.
- `--image=nginx:latest` sets the container image, with the tag `latest` specified explicitly as the task requires.
- Kubernetes automatically creates a ReplicaSet and one pod for the deployment.

## Common Problems

- **Pod stuck in `ContainerCreating` or `Pending`:** Wait 30 to 60 seconds and run `kubectl get pods` again while the image downloads.
- **`ImagePullBackOff`:** Check the image name and tag for typos with `kubectl describe pod <pod-name>`.
- **`AlreadyExists` error:** A deployment named `nginx` already exists. Delete it with `kubectl delete deployment nginx` and create it again.
