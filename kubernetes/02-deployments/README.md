# Task 
# KodeKloud Task: Create a Namespace and Deploy a Pod in Kubernetes

## Task Description

The Nautilus DevOps team is planning to deploy some micro services on Kubernetes platform. The team has already set up a Kubernetes cluster and now they want to set up some namespaces, deployments etc. Based on the current requirements, the team has shared some details as below:

Create a namespace named `dev` and deploy a POD within it. Name the pod `dev-nginx-pod` and use the `nginx` image with the `latest` tag. Ensure to specify the tag as `nginx:latest`.

**Note:** The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

---

## Solution Steps

### Step 1: Check that kubectl works
```bash
kubectl get nodes
```
You should see the cluster nodes listed as `Ready`.

### Step 2: Create the namespace `dev`
```bash
kubectl create namespace dev
```
Expected output: `namespace/dev created`

### Step 3: Verify the namespace
```bash
kubectl get namespaces
```
You should see `dev` in the list with status `Active`.

### Step 4: Create the pod in the `dev` namespace
```bash
kubectl run dev-nginx-pod --image=nginx:latest -n dev
```
Expected output: `pod/dev-nginx-pod created`

### Step 5: Check the pod status
```bash
kubectl get pods -n dev
```
Wait until the status shows `Running`:
```
NAME            READY   STATUS    RESTARTS   AGE
dev-nginx-pod   1/1     Running   0          20s
```

### Step 6: Verify the image (optional)
```bash
kubectl describe pod dev-nginx-pod -n dev | grep Image
```
It should show `nginx:latest`.

---

## Alternative: Using YAML files

### Create the namespace file
```bash
vi namespace.yaml
```
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

### Create the pod file
```bash
vi pod.yaml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: dev-nginx-pod
  namespace: dev
spec:
  containers:
    - name: dev-nginx-container
      image: nginx:latest
```

### Apply both files
```bash
kubectl apply -f namespace.yaml
kubectl apply -f pod.yaml
```

---

## Expected Result
```
NAME            READY   STATUS    RESTARTS   AGE
dev-nginx-pod   1/1     Running   0          1m
```

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `namespaces "dev" not found` | Create the namespace first (Step 2), then create the pod |
| `already exists` | The resource is already created; check with `kubectl get pods -n dev` |
| Pod stuck in `ContainerCreating` | Wait a few seconds and run `kubectl get pods -n dev` again |
| `ImagePullBackOff` | Check the image name is exactly `nginx:latest` (use `kubectl describe pod dev-nginx-pod -n dev`) |
| Forgot `-n dev` | The pod went to the `default` namespace; delete it with `kubectl delete pod dev-nginx-pod` and recreate it with `-n dev` |

---

## Quick Copy-Paste Version
```bash
kubectl create namespace dev
kubectl run dev-nginx-pod --image=nginx:latest -n dev
kubectl get pods -n dev
```
