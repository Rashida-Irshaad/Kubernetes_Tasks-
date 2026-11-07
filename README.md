# KodeKloud Kubernetes Tasks

My solutions to the KodeKloud Nautilus DevOps Kubernetes lab series.
Each task has its own folder with:

- `README.md`: task description and step-by-step solution
- YAML files used in the solution

## Tools used

- `kubectl`
- Kubernetes cluster provided by KodeKloud (via `jump-host`)

## Task Index

| # | Task | Folder | Status |
|---|------|--------|--------|
| 01 | Deploy Pods in Kubernetes Cluster | [01-deploy-pods](kubernetes/01-deploy-pods) | Done |
| 02 | Deploy Applications with Kubernetes Deployments | [02-deployments](kubernetes/02-deployments) | Done |
| 03 | Setup Kubernetes Namespaces and PODs | 03-namespaces-and-pods | Pending |
| 04 | Set Resource Limits in Kubernetes Pods | 04-resource-limits | Pending |
| 05 | Execute Rolling Updates in Kubernetes | 05-rolling-updates | Pending |
| 06 | Revert Deployment to Previous Version in Kubernetes | 06-rollback-deployment | Pending |
| 07 | Deploy ReplicaSet in Kubernetes Cluster | 07-replicaset | Pending |
| 08 | Schedule Cronjobs in Kubernetes | 08-cronjobs | Pending |
| 09 | Create Countdown Job in Kubernetes | 09-countdown-job | Pending |
| 10 | Set Up Time Check Pod in Kubernetes | 10-time-check-pod | Pending |
| 11 | Resolve Pod Deployment Issue | 11-fix-pod-deployment | Pending |
| 12 | Update Deployment and Service in Kubernetes | 12-update-deployment-service | Pending |
| 13 | Expose Application Using NodePort Service in Kubernetes | 13-nodeport-service | Pending |
| 14 | Resolve VolumeMounts Issue in Kubernetes | 14-fix-volumemounts | Pending |

## Folder structure

```
kodekloud-tasks/
├── README.md
└── kubernetes/
    ├── 01-deploy-pods/
    │   ├── README.md
    │   └── pod-httpd.yaml
    ├── 02-deployments/
    └── ...
```

## How to use

1. Open a task folder.
2. Read the task description in its `README.md`.
3. Apply the YAML:

```bash
kubectl apply -f <file>.yaml
```

## Note

These are my own learning notes. Try each task yourself first, then compare.
