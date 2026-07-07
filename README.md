# Traefik Hub AI Demo

## Create cluster

```shell
sudo k3d cluster create ai-demo --port 80:80@loadbalancer --port 443:443@loadbalancer --k3s-arg "--disable=traefik@server:0"
k3d kubeconfig get ai-demo > ./.kubeconfig
chmod 600 ./.kubeconfig
```

## load variables

```shell
source ./.env
```

## Deploy tools

### Deploy Redis

```bash
helm upgrade --install redis-stack redis-stack/redis-stack-server --namespace redis-stack --values ./tools/redis/values.yaml --create-namespace
```

### Deploy Presidio

```shell
kubectl apply -f ./tools/presidio/presidio.yaml
```

### deploy observability

```shell
kubectl create ns observability
```

#### Deploy Otel collector

```shell
helm upgrade --install otel-collector open-telemetry/opentelemetry-collector -n observability --values ./tools/observability/otel-collector/values.yaml 
```

#### Deploy loki

```shell
helm upgrade --install loki grafana/loki -n observability --values ./tools/observability/loki/values.yaml
```

#### Deploy Jaeger

```shell
kubectl apply -f ./tools/observability/jaeger
```

#### Deploy Prometheus stack

```shell
helm upgrade --install promtail grafana/promtail -n observability --values ./tools/observability/promtail/values.yaml
kubectl create configmap grafana-traefik-dashboards --from-file=./tools/observability/prometheus-stack/traefik.json -o yaml --dry-run=client -n observability | kubectl apply -f - && kubectl label -n observability cm grafana-traefik-dashboards grafana_dashboard=true
kubectl create configmap grafana-ai-dashboard --from-file=./tools/observability/prometheus-stack/aidashboard.json -o yaml --dry-run=client -n observability | kubectl apply -f - && kubectl label -n observability cm grafana-ai-dashboard grafana_dashboard=true
helm upgrade -i prometheus-stack prometheus-community/kube-prometheus-stack -f ./tools/observability/prometheus-stack/values.yaml -n observability
```

## Deploy Traefik

### Create Traefik NS

```shell
kubectl create ns traefik
```

### Create secret from cert file

```shell
kubectl create secret tls wildcard-mageekbox --namespace traefik --cert=.lego/certificates/${CLUSTERNAME}.${DOMAINNAME}.crt --key=.lego/certificates/${CLUSTERNAME}.${DOMAINNAME}.key
```

### Create Hub token secret

```shell
kubectl create secret generic hub-license --from-literal=token="${HUB_TOKEN}" -n traefik
```

### Install with Helm

```shell
helm upgrade --install traefik traefik/traefik --create-namespace --namespace traefik --values ./hub/values.yaml
```

### Add Dashboard

```shell
envsubst < ./hub/dashboard.yaml | kubectl apply -f -
```

## Add Grafana ingress

```shell
envsubst < ./tools/observability/prometheus-stack/ingress.yaml | kubectl apply -f -
```

## Deploy AI stack

```shell
kubectl create ns ai
for i in $(find ./ai -type f -follow -print); do
  envsubst < $i | kubectl apply -f -
done
```

### add ai tools api key for Claude messagesAPI

```shell
kubectl create secret generic bedrockkey --from-literal=token="${AWS_BEARER_TOKEN_BEDROCK}" -n ai
kubectl create secret generic openaiauth --from-literal=token="Bearer ${OPENAI_APIKEY}" -n ai
kubectl create secret generic openaikey --from-literal=token="${OPENAI_APIKEY}" -n ai
```
