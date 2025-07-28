# PromQL

### Usefull queries



Show all job's metrics

```promql
count by (__name__)({job="jobname"})
```

Show a specific metric

```promql
cpu_usage{job="jobname"}
```

