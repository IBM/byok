# BYOK (Bring Your Own Kubernetes)

The purpose of BYOK is enable end user can bring their own Kubernetes/OpenShift Cluster to deploy Cloud Native Applications on local/remote/single/multiple/on-prem/cloud Kubernetes/OCP Clusters via GitOps.

```console
guangyaliu@Guangyas-MBP-2 byoc % make local.up
15:08:05 [ .. ] preparing local dev workdir
No integration config repo configured, using local config
15:08:05 [ OK ] preparing local dev workdir
15:08:05 [ .. ] kind up
Creating cluster "local-dev" ...
 ✓ Ensuring node image (kindest/node:v1.21.2) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-local-dev"
You can now use your cluster with:

kubectl cluster-info --context kind-local-dev --kubeconfig /Users/guangyaliu/.kube/config

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
15:08:24 [ OK ] kind up
```

```console
guangyaliu@Guangyas-MBP-2 byoc % kubectl get nodes
NAME                      STATUS   ROLES                  AGE   VERSION
local-dev-control-plane   Ready    control-plane,master   25s   v1.21.2
```

```console
guangyaliu@Guangyas-MBP-2 byoc % make local.down
15:08:45 [ .. ] kind down
Deleting cluster "local-dev" ...
15:08:46 [ OK ] kind down
15:08:46 [ .. ] cleaning local dev workdir
15:08:46 [ OK ] cleaning local dev workdir
```

```console
guangyaliu@Guangyas-MBP-2 byoc % make local-dev
15:09:33 [ .. ] preparing local dev workdir
No integration config repo configured, using local config
15:09:33 [ OK ] preparing local dev workdir
15:09:33 [ .. ] kind up
Creating cluster "local-dev" ...
 ✓ Ensuring node image (kindest/node:v1.21.2) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-local-dev"
You can now use your cluster with:

kubectl cluster-info --context kind-local-dev --kubeconfig /Users/guangyaliu/.kube/config

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
15:09:52 [ OK ] kind up
15:09:52 [ .. ] installing kubectl v1.17.11
15:09:56 [ OK ] installing kubectl v1.17.11
15:09:56 [ .. ] installing kustomize v3.3.0
15:09:57 [ OK ] installing kustomize v3.3.0
15:09:57 [ .. ] installing gomplate darwin-amd64
15:09:59 [ OK ] installing gomplate darwin-amd64
15:09:59 [ .. ] installing istio 1.8.1
15:10:06 [ OK ] /Users/guangyaliu/go/src/github.com/IBM/byoc/.cache/tools/darwin_x86_64/istioctl-1.8.1 installing istio 1.8.1
Switched to context "kind-local-dev".
15:10:06 [ .. ] localdev deploy component: crossplane
[crossplane] Deploying artifacts in chart repo "crossplane-stable"...
"crossplane-stable" has been added to your repositories
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "crossplane-stable" chart repository
Update Complete. ⎈Happy Helming!⎈
[crossplane] Loading required images...
crossplane/crossplane:v1.3.0
Image: "crossplane/crossplane:v1.3.0" with ID "sha256:48eeff1ca1f672d6c8f01c5eecebf2f5a2aa485a19a19a68cbfc05b4f16a7bd8" not yet present on node "local-dev-control-plane", loading...
[crossplane] Loading required images...OK
namespace/crossplane-system created

[crossplane] Running helm upgrade --install with computed parameters...
+ /Users/guangyaliu/go/src/github.com/IBM/byoc/.cache/tools/darwin_x86_64/helm-v3.5.3 upgrade --install crossplane --namespace crossplane-system --kubeconfig /Users/guangyaliu/.kube/config crossplane-stable/crossplane --version 1.3.0 -f /Users/guangyaliu/go/src/github.com/IBM/byoc/.work/local/localdev/config/crossplane/value-overrides.yaml --atomic
Release "crossplane" does not exist. Installing it now.
NAME: crossplane
LAST DEPLOYED: Wed Apr 13 15:10:40 2022
NAMESPACE: crossplane-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Release: crossplane

Chart Name: crossplane
Chart Description: Crossplane is an open source Kubernetes add-on that enables platform teams to assemble infrastructure from multiple vendors, and expose higher level self-service APIs for application teams to consume.
Chart Version: 1.3.0
Chart Application Version: 1.3.0

Kube Version: v1.21.2
[crossplane] Running helm upgrade --install with computed parameters...OK
15:10:46 [ OK ] localdev deploy component: crossplane
```



