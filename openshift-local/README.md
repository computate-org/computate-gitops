
Install the GitOps Operator resources in OpenShift. 

```bash
mkdir -p ~/.local/src/computate-gitops/
git clone https://github.com/computate-org/computate-gitops.git
oc apply -k ~/.local/src/computate-gitops/openshift-local/gitops/base/
```

Wait for the GitOps Operator to start. 

```bash
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

Install the Computate Applications in GitOps. 

```bash
oc apply -k openshift-local/gitops/applications/
```

Initialize the vault, you will need the OpenShift Local kubeadmin password for this. 

```bash
ansible-playbook playbooks/vault-configure.yaml -e OPENSHIFT_PASSWORD=...
```

