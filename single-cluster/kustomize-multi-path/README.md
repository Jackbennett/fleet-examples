# Kustomize Example Debugging

This example is to find a bug from generating yaml via customize has we folder-hop/

This example will deploy the [Kubernetes sample guestbook](https://github.com/kubernetes/examples/tree/master/guestbook/) application
using kustomize. The app will be deployed into the `fleet-kustomize-example` namespace.

These configs work as expected via `fleet-examples/single-cluster/kustomize-multi-path/deployment/context1$ kustomize build -o apply/ .`

## Issue1 - All resources

Expected GitRepo to deploy the app

Actually is seems to find all resoruces, bundles those, an then kustomizes it and includes into the bundle too.

```yaml
kind: GitRepo
apiVersion: fleet.cattle.io/v1alpha1
metadata:
  name: kustomize
  namespace: fleet-local
spec:
  repo: https://github.com/rancher/fleet-examples
  paths:
    - single-cluster/kustomize-multi-path
```

## Issue 2 - can't get to resources

Expected GitRepo to deploy the app

Actually customize doens't have access to the folders higher than the path specified.

```yaml
kind: GitRepo
apiVersion: fleet.cattle.io/v1alpha1
metadata:
  name: kustomize
  namespace: fleet-local
spec:
  repo: https://github.com/rancher/fleet-examples
  paths:
    - single-cluster/kustomize-multi-path/deployment/context1
```
