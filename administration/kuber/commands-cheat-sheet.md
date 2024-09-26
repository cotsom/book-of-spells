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
