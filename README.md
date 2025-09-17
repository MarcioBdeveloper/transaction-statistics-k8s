# transaction-statistics-k8s

# 📘 GitOps com ArgoCD + Minikube

Este repositório contém os manifests Kubernetes para a aplicação **transaction-statistics**, gerenciados via **ArgoCD** em um cluster **Minikube**.

---

## 🚀 Pré-requisitos

* [Minikube](https://minikube.sigs.k8s.io/docs/start/)
* [kubectl](https://kubernetes.io/docs/tasks/tools/)
* [ArgoCD](https://argo-cd.readthedocs.io/) instalado no cluster

---

## 📦 Estrutura do repositório

```
transaction-statistics-k8s/
├── infra/
│   ├── deployment.yaml      # Deployment da aplicação
│   └── service.yaml         # Service para expor a API
└── application.yaml  # Definição da Application do ArgoCD
```

---

## Aplicar a definição da Application (GitOps)

```bash
kubectl apply -f application.yaml -n argocd
```

O ArgoCD irá:

* Ler o repositório Git
* Criar/atualizar o Deployment e Service
* Garantir que o estado do cluster esteja **sempre em sync com o Git**

---

### 6. Acessar a aplicação no Minikube

```bash
minikube service transaction-statistics
```

Ou diretamente pelo NodePort:

```
https://localhost:8080/applications/argocd/transaction-statistics?view=tree&resource=
```

---

## 🔄 Fluxo GitOps

1. Desenvolvedor faz alterações nos manifests (`deployment.yaml`, `service.yaml`)
2. Faz commit e push no GitHub
3. O ArgoCD detecta a mudança e sincroniza automaticamente no cluster
4. O cluster sempre reflete o estado desejado no Git

---

## 🔍 Comandos úteis do ArgoCD

Listar aplicações:

```bash
kubectl get applications -n argocd
```

Forçar sync:

```bash
kubectl -n argocd argocd app sync transaction-statistics
```

Ver status:

```bash
kubectl -n argocd argocd app get transaction-statistics
```

---
