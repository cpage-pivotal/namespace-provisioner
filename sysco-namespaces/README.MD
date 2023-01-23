# Sysco Namespaces Repo

Developer namespaces to be provisioned to the iterate cluster

Sample Carvel resource to sync this folder to the iterate cluster:
```
apiVersion: kappctrl.k14s.io/v1alpha1
kind: App
metadata:
  name: developer-namespaces
  namespace: tap-install
spec:
  serviceAccountName: tap-install-sa
  fetch:
    - git:
        url: https://github.com/cpage-pivotal/namespace-provisioner
        ref: origin/main
        subPath: sysco-namespaces
  template:
    - ytt: {}
  deploy:
    - kapp:
        rawOptions: ["--dangerous-allow-empty-list-of-resources=true"]
 ```
