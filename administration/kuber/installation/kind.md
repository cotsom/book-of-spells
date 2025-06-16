---
description: kubernetes in docker
---

# kind

```bash
#Install kind
go install sigs.k8s.io/kind@v0.26.0
export PATH=~/go/bin:$PATH

#create cluster
kind create cluster

#delete cluster
kind delete cluster
```

{% embed url="https://iximiuz.com/en/posts/kubernetes-kind-load-docker-image/" %}
