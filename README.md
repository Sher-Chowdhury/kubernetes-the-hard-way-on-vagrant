# Intro

This vagrant project builds a 1-master and 1-worker node. You can run kubectl command inside either master or worker nodes. 

There is no loadbalancer in this setup. 


## Kubemaster / Controller / Control Plane

- etcd - stores data
- kube-apiserver - endpoint for recieving interaction from kubelet. should receive requests from loadbalancer
- kube-controller-manager -
- kube-scheduler - 

```bash
systemctl status etcd kube-apiserver kube-controller-manager kube-scheduler
```

## Worker node

- containerd
- kubelet
- kube-proxy

```bash
systemctl status kubelet kube-proxy containerd
```

## Sanity checks on kubemaster

Check kubectl command is configured:

```bash
$ cat /etc/profile.d/kubectl.sh
$ kubectl config get-clusters --kubeconfig=/root/kthw/kubeconfigs/admin.kubeconfig
NAME
codingbee_cluster
$ kubectl config get-contexts #--kubeconfig=/root/kthw/kubeconfigs/admin.kubeconfig
CURRENT   NAME      CLUSTER             AUTHINFO   NAMESPACE
*         default   codingbee_cluster   admin
```

Next do:

```bash
# kubectl get componentstatuses --kubeconfig /root/kthw/kubeconfigs/admin.kubeconfig
NAME                 STATUS    MESSAGE             ERROR
controller-manager   Healthy   ok
scheduler            Healthy   ok
etcd-0               Healthy   {"health":"true"}
```

The admin.kubeconfig contains the 'admin' login credentials for the kubecluster. So should only be used by Kubernetes Administrators, who can use it on their macbooks. 

Check the following deaemons are runnning:

```bash
systemctl status kube-apiserver.service kube-controller-manager.service kube-scheduler.service etcd
```


Check all the component version:

```bash
$ kube-apiserver --version
Kubernetes v1.10.2
$ kube-controller-manager --version
Kubernetes v1.10.2
$ kube-scheduler --version

$ kubectl version
Client Version: version.Info{Major:"1", Minor:"10", GitVersion:"v1.10.2", GitCommit:"81753b10df112992bf51bbc2c2f85208aad78335", GitTreeState:"clean", BuildDate:"2018-04-27T09:22:21Z", GoVersion:"go1.9.3", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"10", GitVersion:"v1.10.2", GitCommit:"81753b10df112992bf51bbc2c2f85208aad78335", GitTreeState:"clean", BuildDate:"2018-04-27T09:10:24Z", GoVersion:"go1.9.3", Compiler:"gc", Platform:"linux/amd64"}


$ etcd --version
etcd Version: 3.3.10
Git SHA: 27fc7e2
Go Version: go1.10.4
Go OS/Arch: linux/amd64
```


