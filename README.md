# todo-k8s-manifest

> [!WARNING]
> If you want to use this manifest as a reference, you need to modify the `spec.certificateARNs` in `IngressClassParams`, the `spec.template.spec.containers[].image` in `Deployment`, and the `spec.rules[].host` in `Ingress`.

This repository manages the Kubernetes manifests used in the EKS Cluster built with the [eks-project-example](https://github.com/gotokazuki/eks-project-example) repository.  
For more details, please refer to the [eks-project-example](https://github.com/gotokazuki/eks-project-example) repository.

Installing ArgoCD:

```shell
# create argocd namespace
kubectl apply -f manifests/argocd/init
# install ArgoCD in argocd namespace
kubectl apply -n argocd -f manifests/argocd/install
```

Registering the ApplicationSet:

```shell
kubectl apply -f manifests/argocd/application-set
```

Uninstalling ArgoCD:

```shell
kubectl delete -n argocd -f manifests/argocd/install
```

Since deleting the namespace with kubectl delete may get stuck, use the following command to delete it:

```shell
(
NAMESPACE=argocd
kubectl proxy &
kubectl get namespace $NAMESPACE -o json |jq '.spec = {"finalizers":[]}' >temp.json
curl -k -H "Content-Type: application/json" -X PUT --data-binary @temp.json 127.0.0.1:8001/api/v1/namespaces/$NAMESPACE/finalize
)
rm temp.json
```

The contents under `manifests/argocd/env/` are managed by ArgoCD.
