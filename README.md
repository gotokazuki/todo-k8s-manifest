# todo-k8s-manifest

> [!WARNING]
> If you want to use this manifest as a reference, you need to modify the `spec.certificateARNs` in `IngressClassParams`, the `spec.template.spec.containers[].image` in `Deployment`, and the `spec.rules[].host` in `Ingress`.

This repository manages the Kubernetes manifests used in the EKS Cluster built with the [eks-project-example](https://github.com/gotokazuki/eks-project-example) repository.  
For more details, please refer to the [eks-project-example](https://github.com/gotokazuki/eks-project-example) repository.

Installing ArgoCD:

```shell
kubectl apply -f manifests/argocd/install
```

Registering the ApplicationSet:

```shell
kubectl apply -f manifests/argocd/application-set
```

The contents under `manifests/argocd/env/` are managed by ArgoCD.
