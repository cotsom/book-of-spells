# k8s

### Kubeadm

**Install with CRI**

> disabled\_plugins = \["cri"]

You have to remove this line to enable Kubernetes CRI

### Kubespray

```bash
git clone https://github.com/kubernetes-sigs/kubespray.git
cd kubespray
pip3 install -r requirements.txt
cp -rfp inventory/sample inventory/mycluster
```

Then if need another cni open `inventory/mycluster/group_vars/k8s_cluster/k8s-cluster.yml` :&#x20;

```yaml
kube_network_plugin: cilium
```

Configure `inventory/mycluster/inventory.ini`&#x20;

```ini
[kube_control_plane]
master1 ansible_host=10.20.10.177  ip=10.20.10.177 ansible_user=root

[etcd:children]
kube_control_plane

[kube_node]
worker5 ansible_host=10.20.20.21   ip=10.20.20.21 ansible_user=root
worker3 ansible_host=10.20.20.22   ip=10.20.20.22 ansible_user=root
worker4 ansible_host=10.20.20.23   ip=10.20.20.23 ansible_user=root

[all:vars]

ansible_ssh_private_key_file=~/.ssh/id_rsa
```

And run playbook

```bash
ansible-playbook -i inventory/mycluster/inventory.ini --become --become-user=root cluster.yml
```
