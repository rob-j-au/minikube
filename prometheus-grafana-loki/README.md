### Install Prometheus/Grafana/Loki


```
helm install prometheus prometheus-community/prometheus \
  --namespace monitoring --create-namespace
```

```
kubectl get pods -n monitoring
```

```
helm install grafana grafana/grafana \
--namespace monitoring
```

```
kubectl get secret --namespace monitoring grafana \
  -o jsonpath="{.data.admin-password}" | base64 --decode
```

```
helm install loki grafana/loki-stack \
  --namespace monitoring \
  --set promtail.enabled=true
```


Loki as a Grafana data source requires > 2.9.3

```
helm upgrade loki grafana/loki-stack --namespace monitoring --set promtail.enabled=true --set loki.image.tag=2.9.3
```

Open Grafana
```
minikube service grafana -n monitoring
```


🎯 Next Steps

  • Add Prometheus as a data source in Grafana (Configuration → Data Sources → Add → Prometheus)

  • Add Loki as a data source (Add → Loki)

  • Import dashboards for system metrics/logs

