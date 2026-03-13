# SoftwareAG Helm Charts Repository

This folder contains product-specific Helm charts for:

- Adabas
- Natural
- Adabas Manager

These are sample charts for testing purposes, intended for customer evaluations and internal validation.

The charts are designed to be installed independently while sharing one Kubernetes namespace for integrated testing.

## Support And Disclaimer

- These charts are sample artifacts provided for testing and evaluation.
- These charts are not production-hardened and should not be used as-is for production workloads.
- Validate security, sizing, backups, policies, and operational controls before any production use.
- For issues or improvement requests, open a ticket in your internal tracking system or contact your SoftwareAG support team.


## Prerequisites

Install the following tools before deploying:

1. Kubernetes cluster
2. kubectl
3. Helm 3.x
4. Git

Installation links:

- Kubernetes: https://kubernetes.io/docs/setup/
- kubectl: https://kubernetes.io/docs/tasks/tools/
- Helm: https://helm.sh/docs/intro/install/
- Git: https://git-scm.com/downloads

Optional but recommended:

1. Docker Desktop, Minikube, or Rancher Desktop for local clusters
2. yq for values automation
3. kubeconform or kubeval for manifest validation

Optional tool links:

- Docker Desktop: https://www.docker.com/products/docker-desktop/
- Minikube: https://minikube.sigs.k8s.io/docs/start/
- Rancher Desktop: https://rancherdesktop.io/
- yq: https://github.com/mikefarah/yq
- kubeconform: https://github.com/yannh/kubeconform
- kubeval: https://github.com/instrumenta/kubeval

## Verify Tooling

```bash
kubectl version --client
helm version
git --version
```

## Clone Repository

Clone the repository and navigate to the Helm charts folder:

```bash
git clone https://github.com/SoftwareAG/helm-charts.git
cd helm-charts
```



## Deploy All Charts In Single Namespace

Namespace used in this example: adanat

Install all three charts into the same namespace:

```bash
helm upgrade --install adabas ./adabas -n adanat --create-namespace
helm upgrade --install natural ./natural -n adanat
helm upgrade --install adabas-manager ./adabas-manager -n adanat
```

Default values behavior:

- `helm upgrade --install adabas ./adabas ...` uses `./adabas/values.yaml`
- `helm upgrade --install natural ./natural ...` uses `./natural/values.yaml`
- `helm upgrade --install adabas-manager ./adabas-manager ...` uses `./adabas-manager/values.yaml`

Override defaults for a specific chart using:

- `-f <custom-values.yaml>`
- `--set key=value`

Validate deployment:

```bash
kubectl get all -n adanat
kubectl get configmap -n adanat
```

## Upgrade And Rollback

Upgrade one product:

```bash
helm upgrade adabas ./adabas -n adanat
```

See history:

```bash
helm history adabas -n adanat
```

Rollback:

```bash
helm rollback adabas 1 -n adanat
```

## Uninstall

```bash
helm uninstall adabas -n adanat
helm uninstall natural -n adanat
helm uninstall adabas-manager -n adanat
```

Optional namespace cleanup:

```bash
kubectl delete namespace adanat
```
