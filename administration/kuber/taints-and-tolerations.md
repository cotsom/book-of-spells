# Taints and Tolerations

### NoSchedule

```bash
#add
kubectl taint nodes node1 key1=value1:NoSchedule

#delete
kubectl taint nodes node1 key1=value1:NoSchedule-
```
