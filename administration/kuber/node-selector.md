# Node Selector

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
  namespace: web-tasks
  labels:
    app: web-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: web-app
        image: nginx
        ports:
        - containerPort: 8000
        resources:
          requests:
            cpu: 50m
            memory: 100Mi
          limits:
            cpu: 100m
            memory: 100Mi
      imagePullSecrets:
        - name: registry-secret
|------------------------------------------|
|     nodeSelector:                        |
|       kubernetes.io/arch: amd64          |
|------------------------------------------|
```
