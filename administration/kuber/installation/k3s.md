# k3s

### **Развёртывание локального кластера**

Чтобы не тянуть тяжелый k8s возьмём k3s. Запустить его можно с помощью специальной утилиты [k3d](https://k3d.io/v5.5.1/)

**Запускаем кластер**

```
k3d cluster create
```

**Проверяем что кластер работает**

Для работы с кластером потребуется утилита [kubectl](https://kubernetes.io/ru/docs/tasks/tools/install-kubectl/). Также рекомендую установить [автодополнение](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

```
kubectl get pods -A
```

Все сервисы должны быть `Running` или `Completed`



### Setup private registry

`/etc/rancher/k3s/registries.yaml`

```yaml
mirrors:
  myprivateregistry.com:
    endpoint:
      - "https://myprivateregistry.com"
configs:
  "myprivateregistry.com":
    auth:
      username: myusername
      password: mypassword
```

Create secret

```bash
kubectl create secret docker-registry myregistrykey \
  --docker-server=https://index.docker.io/v1/ \
  --docker-username=myusername \
  --docker-password=mypassword \
  --docker-email=myemail@example.com

```

### Timeweb cloudinit

```bash
#!/bin/sh
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC8uPBswMKapwEO4LloeDj6egpQ2HXXnUsmiT+nUPlp0PAqRiMK0djZYMPsw3fbMcgJ2PYuD0Sk0N7+WSE3pA7zbvxetnAZoeJWWiRLr3NQHIk0AgQaLBvXc/bblpCjAEYoZbOuIrXogOI3k8fxah6o9Yze05dyCIUEAHM6s4NVd3vNKp9K7dyzVVZBkUx0BnAk7kb5Cq/Q1LeflvyptFUJgowcnmuGuuqtZXxkmkEA9wRZ5O4oB43jPhPOmlXyFQxJDfedHNqC3udmzYwx5n/eMjdh+PEoUztdyfnj7w35vGS9jrfH7cTJOf4couKbeMhxi6FcGUg7c9XEHgmGbXCH s4ar\s4ar@S4ar" > /root/.ssh/authorized_keys

curl https://get.docker.com | sh
curl -sfL https://get.k3s.io | sh -

echo bWlycm9yczoKICByZWdpc3RyeS0xLmRvY2tlci5pbzoKICAgIGVuZHBvaW50OgogICAgICAtICJodHRwczovL2NyLnlhbmRleC9taXJyb3IiCiAgICAgIC0gImh0dHBzOi8vbWlycm9yLmdjci5pbyI= | base64 -d > /etc/rancher/k3s/registries.yaml

curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4 | bash
wget https://github.com/derailed/k9s/releases/latest/download/k9s_linux_amd64.deb && apt install ./k9s_linux_amd64.deb && rm k9s_linux_amd64.deb
mkdir /root/.kube
cp /etc/rancher/k3s/k3s.yaml /root/.kube/config
systemctl restart k3s
```

