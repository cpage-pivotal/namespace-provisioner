# Ops Deliverable Repo

Deliverables approved for the run cluster

Sample Carvel resource to sync this folder to the run cluster.

```
apiVersion: kappctrl.k14s.io/v1alpha1
kind: App
metadata:
  name: ops-deliverables
  namespace: tap-install
spec:
  serviceAccountName: tap-install-sa
  fetch:
    - git:
        url: https://github.com/cpage-pivotal/namespace-provisioner
        ref: origin/main
        subPath: ops-deliverables
  template:
    - ytt: {}
  deploy:
    - kapp:
        rawOptions: ["--dangerous-allow-empty-list-of-resources=true"]
 ```