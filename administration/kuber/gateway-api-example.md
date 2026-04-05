# Gateway Api example

#### Create cluster

```bash
kind create cluster
```

#### Install Gateway API CRD

```bash
kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.1.0/standard-install.yaml
```

#### Install Envoy Gateway

```bash
helm install eg oci://docker.io/envoyproxy/gateway-helm --version v1.1.0 -n envoy-gateway-system --create-namespace
```

#### Deploy

```bash
kubectl apply -f test-app.yml kubectl
apply -f deploy.yml
kubectl port-forward -n envoy-gateway-system svc/$ENVOY_SERVICE 8080:80
```

\
_test-app.yml:_

```yml
---
apiVersion: v1
kind: Namespace
metadata:
  name: lab-gateway
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-v1
  namespace: lab-gateway
spec:
  replicas: 1
  selector:
    matchLabels:
      app: backend
      version: v1
  template:
    metadata:
      labels:
        app: backend
        version: v1
    spec:
      containers:
      - name: backend
        image: hashicorp/http-echo
        args: ["-text=Welcome to V1"]
        ports:
        - containerPort: 5678
---
apiVersion: v1
kind: Service
metadata:
  name: backend-v1-svc
  namespace: lab-gateway
spec:
  ports:
  - port: 80
    targetPort: 5678
  selector:
    app: backend
    version: v1

```

_deploy.yml:_

```yml
---
# Create gateway class for Envoy Gateway
apiVersion: gateway.networking.k8s.io/v1
kind: GatewayClass
metadata:
  name: envoy-gateway-class
spec:
  controllerName: gateway.envoyproxy.io/gatewayclass-controller
---
# Create a Gateway that listens on port 80 and allows routes from the same namespace
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: my-gateway
  namespace: lab-gateway
spec:
  gatewayClassName: envoy-gateway-class
  listeners:
  - name: http
    protocol: HTTP
    port: 80
    allowedRoutes:
      namespaces:
        from: Same
---
# Create an HTTPRoute that matches requests with the path prefix /api and forwards them to the backend service
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: backend-route
  namespace: lab-gateway
spec:
  parentRefs:
  - name: my-gateway
  rules:
  - matches:
    - path:
        type: PathPrefix
        value: /api
    backendRefs:
    - name: backend-v1-svc
      port: 80

```
