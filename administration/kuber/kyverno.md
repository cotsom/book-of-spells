# Kyverno

## Deploy

```bash
# Add helm repo
helm repo add kyverno https://kyverno.github.io/kyverno/
helm repo update

# Install
helm install kyverno kyverno/kyverno \
  --namespace kyverno \
  --create-namespace \
  --set admissionController.replicas=1
  
# Check
kubectl get pods -n kyverno -w

# Install official politics
helm install kyverno-policies kyverno/kyverno-policies --namespace kyverno
```

