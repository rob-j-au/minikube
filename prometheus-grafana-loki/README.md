### Install Prometheus/Grafana/Loki

Install Prometheus with persistence:
```
helm install prometheus prometheus-community/prometheus \
  --namespace monitoring --create-namespace \
  --values prometheus-values.yaml
```
Install Loki with Promtail:

(> 2.9.3 required to add Loki as a Grafana data source)

```
helm install loki grafana/loki-stack \
  --namespace monitoring \
  --set promtail.enabled=true \
  --set loki.image.tag=2.9.3
```

Install Grafana with automatic datasource provisioning:
```
helm install grafana grafana/grafana \
  --namespace monitoring \
  --values grafana-values.yaml
```

Get Grafana admin password:
```
kubectl get secret --namespace monitoring grafana \
  -o jsonpath="{.data.admin-password}" | base64 --decode
```

Access Grafana:
```
minikube service grafana -n monitoring
```

🎯 What's Automated

✅ Prometheus datasource automatically configured at `http://prometheus-server`

✅ Loki datasource automatically configured at `http://loki:3100`
