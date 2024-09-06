---
description: If you want to release your application on the Internet
---

# Deployment-Service-Ingress Example

### Deployment

<pre class="language-yaml"><code class="lang-yaml">apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deployment
  labels:
    app: my-web
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-web
  template:
    metadata:
      labels:
        app: my-web
    spec:
      containers:
      - name: web
        image: <a data-footnote-ref href="#user-content-fn-1">localhost:5000/author/web-image:latest</a>
        ports:
        <a data-footnote-ref href="#user-content-fn-2">- containerPort: 5000</a>
      imagePullSecrets:
      - name: myregistrykey
</code></pre>

### Service

<pre class="language-yaml"><code class="lang-yaml">apiVersion: v1
kind: Service
metadata:
  name: my-web-service
  namespace: default
spec:
  selector:
    app: my-web
  ports:
    - protocol: TCP
      port: 80
      <a data-footnote-ref href="#user-content-fn-3">targetPort: 5000</a>
</code></pre>

### Ingress

<pre class="language-yaml"><code class="lang-yaml">apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
  namespace: default
  annotations:
    <a data-footnote-ref href="#user-content-fn-4">nginx.ingress.kubernetes.io/rewrite-target: /</a>
spec:
  rules:
  - host: domain.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-web-service
            port:
              number: 80
  - host: lol.domain.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: test-app-service
            port:
              number: 80
</code></pre>

### Nginx Ingress controller install

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```



### Ingress annotations cheat sheet

```
annotations:
    #choose your Ingress controller
    kubernetes.io/ingress.class: "nginx"
    kubernetes.io/ingress.class: "traefik"
    
    #for certs with traefik
    traefik.ingress.kubernetes.io/router.entrypoints: websecure
    traefik.ingress.kubernetes.io/router.tls.certresolver: "le"
    
    #for rewrite url by "/" through nginx controller
    nginx.ingress.kubernetes.io/rewrite-target: /
```

[^1]: example for private registry

[^2]: Internal app port

[^3]: internal app port

[^4]: for Nginx Ingress controller
