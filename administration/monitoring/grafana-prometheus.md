---
description: deploy grafana, prometheus, node exporter
---

# Grafana-Prometheus

**docker-compose.yml**

```yaml
version: "3.9"
services:
  grafana:
    container_name: grafana
    image: grafana/grafana:latest
    user: "0"
    ports:
      - "3000:3000"
    volumes:
      - grafana-data:/var/lib/grafana

  prometheus:
    container_name: prometheus
    image: prom/prometheus:latest
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus-data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
    ports:
      - 9090:9090

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    restart: unless-stopped
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
    ports:
      - "9100:9100"


volumes:
  grafana-data:
  prometheus-data:
```



**prometheus.yml**

```yaml
global:
  scrape_interval:     15s 
  evaluation_interval: 15s 
scrape_configs:
  - job_name: 'node_exporter'
    scrape_interval: 15s
    static_configs:
      - targets: ['node-exporter:9100']
```



global - глобальные настройки: Comment

scrape\_interval - раз в какое время выполняется HTTP-запрос к цели. В ответ получаются метрики в своём формате, которые сохраняются в базу(Prometheus) evaluation\_interval - раз в какое время должны отрабатывать правила, на основании которых отправляются, например, алерты или записываются данные в базу.&#x20;

scrape\_configs - настройки поиска целей для мониторинга:

job\_name - имя нашего сервиса. В данном случае это 'node\_exporter'. Название можно поставить любое&#x20;

scrape\_interval - как часто собирать данные. Данную директиву можно опустить, так как она совпадает с тем, что прописано в global. Однако оставим тут для наглядности, что это можно настраивать отдельно для каждого сервиса.&#x20;

static\_configs - указание на то где находятся наши "цели". В нашем конфиге указано node-exporter:9100. То есть мы ссылаемся на наш "абстрактный сервер". В реальной жизни это был бы IP-адрес или хостнейм сервера
