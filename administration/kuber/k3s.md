# k3s

**Развёртывание локального кластера**

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