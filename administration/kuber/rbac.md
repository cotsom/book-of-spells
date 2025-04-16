# RBAC

Допустим, у вас есть namespace `dev`. Чтобы дать разработчику Alice права деплоить приложения туда, создаём:

```yaml
# 1. Роль dev-deployer в namespace dev
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: dev
  name: dev-deployer
rules:
- apiGroups: ["", "apps", "extensions"]
  resources: ["deployments", "pods", "services"]
  verbs: ["get", "list", "watch", "create", "update", "delete"]
```

```yaml
# 2. Привязка роли к пользователю Alice
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  namespace: dev
  name: dev-deployer-binding
subjects:
- kind: User
  name: alice
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: dev-deployer
  apiGroup: rbac.authorization.k8s.io
```

***

### Генерация и настройка kubeconfig для разработчика

После того, как роль и биндинг созданы, нужно выдать Alice kubeconfig, в котором будут её учётные данные и context, привязанный к namespace:

1.  **Добавляем пользователю креды** (например, клиентский сертификат):

    ```bash
    kubectl config set-credentials alice \
      --client-certificate=alice.crt \
      --client-key=alice.key \
      --embed-certs=true
    ```
2.  **Создаём context** с привязкой к кластеру и namespace:

    ```bash
    kubectl config set-context dev-alice \
      --cluster=my-cluster \
      --namespace=dev \
      --user=alice
    ```
3.  **Активируем context**:

    ```bash
    kubectl config use-context dev-alice
    ```
