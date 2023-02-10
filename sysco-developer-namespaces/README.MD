# Sysco Namespaces Repo

Developer namespaces to be provisioned to the iterate cluster

Sample Carvel resource to sync this folder to the iterate cluster. tap-install-sa must be created

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
        subPath: sysco-developer-namespaces
  template:
    - ytt: {}
  deploy:
    - kapp:
        rawOptions: ["--dangerous-allow-empty-list-of-resources=true"]
 ```

values.yaml configuration

```
namespace_provisioner:
  controller: yes
  namespace_selector:
    matchExpressions:
      - key: apps.tanzu.vmware.com/tap-developer-ns
        operator: Exists
  additional_sources:
    - git:
        url: https://github.com/cpage-pivotal/namespace-provisioner.git
        subPath: sysco-developer
        ref: origin/main
      path: _ytt_lib/sysco-developer
```