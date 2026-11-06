# Task 
# KodeKloud Task: Create Pod `pod-httpd`

## Task Description

The Nautilus DevOps team is diving into Kubernetes for application management. One team member has a task to create a pod according to the details below:

1. Create a pod named `pod-httpd` using the `httpd` image with the `latest` tag. Ensure to specify the tag as `httpd:latest`.
2. Set the `app` label to `httpd_app`, and name the container as `httpd-container`.

**Note:** The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

---

## Solution Steps

### Step 1: Create the YAML file

```bash
vi pod-httpd.yaml
```

### Step 2: Add the pod definition

Press `i` to enter insert mode, then paste:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-httpd
  labels:
    app: httpd_app
spec:
  containers:
    - name: httpd-container
      image: httpd:latest
```

### Step 3: Save and exit

Press `Esc`, type `:wq`, and press `Enter`.

### Step 4: Create the pod

```bash
kubectl apply -f pod-httpd.yaml
```

Expected output:

```
pod/pod-httpd created
```

### Step 5: Check the pod status

```bash
kubectl get pods
```

Wait until the status shows `Running`.

### Step 6: Verify the details

```bash
kubectl get pod pod-httpd --show-labels
kubectl describe pod pod-httpd
```

Confirm:

| Requirement | Value to see |
|---|---|
| Pod name | `pod-httpd` |
| Image | `httpd:latest` |
| Label | `app=httpd_app` |
| Container name | `httpd-container` |

---

## How the YAML maps to the task

| Task requirement | YAML line |
|---|---|
| Pod named `pod-httpd` | `name: pod-httpd` |
| Label `app` = `httpd_app` | `labels:` then `app: httpd_app` |
| Container named `httpd-container` | `- name: httpd-container` |
| Image `httpd:latest` | `image: httpd:latest` |

Once the pod is `Running`, click **Check** in KodeKloud to complete the task.