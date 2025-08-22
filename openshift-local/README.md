
Install the GitOps Operator resources in OpenShift. 

```bash
mkdir -p ~/.local/src/computate-gitops/
git clone https://github.com/computate-org/computate-gitops.git
cd ~/.local/src/computate-gitops
oc apply -k openshift-local/gitops/base/
```

Wait for the GitOps Operator to start. 

```bash
oc -n openshift-operators wait pod -l control-plane=gitops-operator --for=condition=Ready --timeout=5m
oc -n openshift-gitops wait pod -l app.kubernetes.io/name=openshift-gitops-application-controller --for=condition=Ready --timeout=5m
```

Install the gitops app in OpenShift. 

```bash
oc apply -k openshift-local/gitops/app/
```

Wait for the GitOps app to start. 

```bash
oc -n openshift-gitops wait pod -l app.kubernetes.io/name=openshift-gitops-server --for=condition=Ready --timeout=5m
```
