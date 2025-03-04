# Commands cheat sheet

### Get shell on node with debug pod

```bash
kubectl debug node/<node-name> -it --image=<image name>
```

```bash
kubectl debug --image=alpine --namespace=<namespace> node/<node-name> --attach=true --stdin=true --tty -- sh
```

### Node taint NoSchedule

**Add**

```bash
kubectl taint nodes node1 key1=value1:NoSchedule
```

**Remove**

```bash
kubectl taint nodes node1 key1=value1:NoSchedule-
```

### Set editor for kubectl

```bash
export KUBE_EDITOR="nano"
```

### Example with creating admin user and getting token

Creating a admin / service account user called `k8sadmin`

```
sudo kubectl create serviceaccount k8sadmin -n kube-system
```

Give the user admin privileges

```
sudo kubectl create clusterrolebinding k8sadmin --clusterrole=cluster-admin --serviceaccount=kube-system:k8sadmin
```

Get the token

```
sudo kubectl -n kube-system describe secret $(sudo kubectl -n kube-system get secret | (grep k8sadmin || echo "$_") | awk '{print $1}') | grep token: | awk '{print $2}'
```
