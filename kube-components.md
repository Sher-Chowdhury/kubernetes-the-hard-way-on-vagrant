# kube components

## kubemaster components

Here is the list of components:

- kube-apiserver.service
- kube-controller-manager.service  
- kube-scheduler.service
- etcd.service

### kube-apiserver.service

This service is located at:

```
$ cat /etc/systemd/system/kube-apiserver.service
```

This service unit file needs relies on the following files:

- /usr/local/bin/kube-apiserver              (binary)
- /var/lib/kubernetes/ca.pem                 (diff /var/lib/kubernetes/ca.pem /vagrant/kube_cache/tls/01_ca/ca.pem)
- /var/lib/kubernetes/kubernetes.pem         (diff /var/lib/kubernetes/kubernetes.pem /vagrant/kube_cache/tls/06_api_server_certs/kubernetes.pem)
- /var/lib/kubernetes/kubernetes-key.pem     (diff /vagrant/kube_cache/tls/06_api_server_certs/kubernetes-key.pem)
- /var/lib/kubernetes/encryption-config.yaml (diff /var/lib/kubernetes/encryption-config.yaml /vagrant/kube_cache/encryption-configs/encryption-config.yaml)
- /var/lib/kubernetes/service-account.pem    (diff diff /var/lib/kubernetes/service-account.pem /vagrant/kube_cache/tls/07_service_account_key_pair/service-account.pem)



