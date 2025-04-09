---
description: Some secret examples
---

# Secret

### Create secret manualy

```bash
kubectl create secret generic test --from-literal=test1=asdf --from-literal=dbpassword=1q2w3e
kubectl get secret
kubectl get secret test -o yaml
```

### Create secret by manifest

```yaml
---
apiVersion: v1
kind: Secret
metadata:
  name: test
stringData:
  test: updated
```

### Deployment with secrets

```yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - image: nginx:1.20
        name: nginx
        env:
        - name: TEST
          value: foo
        - name: TEST_1
          valueFrom:
            secretKeyRef:
              name: test
              key: test1
        ports:
        - containerPort: 80
        resources:
          requests:
            cpu: 50m
            memory: 100Mi
          limits:
            cpu: 100m
            memory: 100Mi
```

### Check secret

```bash
kubectl get secret test -o yaml
```
