---
description: Some configmap examples
---

# Config Map

### configmap.yaml

```yaml
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap-env
data:
  dbhost: postgresql
  DEBUG: "false"
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap-txt-file
data:
  database.sql: |
    some text in file;
    some text in file;
    some text in file;

```



### connect configmap into deployment

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
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
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
|-----------------------------------|
|       envFrom:                    |
|       - configMapRef:             |
|           name: my-configmap-env  |
|-----------------------------------|
        ports:
        - containerPort: 80
        resources:
          requests:
            cpu: 50m
            memory: 100Mi
          limits:
            cpu: 100m
            memory: 100Mi
|------------------------------------------------|        
|       volumeMounts:                            |
|       - name: data                             |
|         mountPath: /file.txt                   |
|------------------------------------------------|
|-----------------------------------|
|   volumes:                        |
|   - name: data                    |
|     configMap:                    |
|       name: my-configmap-txt-file |
|-----------------------------------|
```
