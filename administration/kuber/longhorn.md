# longhorn

### Install

```bash
kubectl apply -f https://raw.githubusercontent.com/longhorn/longhorn/v1.8.0/deploy/longhorn.yaml
```

### Update engine image via api

```bash
curl http://10.233.0.1:9500/v1/engineimages -X POST -H "Content-Type: application/json" -d '{"image": "author/image:tag"}'
```
