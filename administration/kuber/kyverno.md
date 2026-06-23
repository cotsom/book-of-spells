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

# Install official politics IN AUDIT MODE
helm install kyverno-policies kyverno/kyverno-policies --namespace kyverno

# Set Enforce mode
helm upgrade kyverno-policies kyverno/kyverno-policies \
  --namespace kyverno \
  --set validationFailureAction=Enforce
  
# Set Failure Policy to Ignore
helm upgrade kyverno kyverno/kyverno -n kyverno \
  --reuse-values \
  --set features.forceFailurePolicyIgnore.enabled=true
```



## Tips

```bash
# Check cluster policies
kubectl get cpols

# Check Failure Policy
kubectl get validatingwebhookconfiguration kyverno-resource-validating-webhook-cfg -o jsonpath='{range .webhooks[*]}{.name}{": "}{.failurePolicy}{"\n"}{end}'
```
