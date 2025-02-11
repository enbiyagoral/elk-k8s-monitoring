# Elastic Stack Helm Installation

This repository contains Helm configurations for deploying the Elastic Stack (Elasticsearch, Logstash, Kibana, and Filebeat) on Kubernetes.

## Prerequisites

- Kubernetes cluster
- Helm 3.x
- kubectl

## Installation

### 1. Add Elastic Helm Repository

```bash
helm repo add elastic https://helm.elastic.co
helm repo update
```

### 2. Create Namespace

```bash
kubectl create namespace elastic-stack
```

### 3. Install Components

Install Elasticsearch:
```bash
helm install elasticsearch elastic/elasticsearch -f elasticsearch/elasticsearch-values.yaml -n elastic-stack
```

Install Filebeat:
```bash
helm install filebeat elastic/filebeat -f filebeat/filebeat-values.yaml -n elastic-stack
```

Install Logstash:
```bash
helm install logstash elastic/logstash -f logstash/logstash-values.yaml -n elastic-stack
```

Install Kibana:
```bash
helm install kibana elastic/kibana -f kibana/kibana-values.yaml -n elastic-stack
```

## Access

To access Kibana dashboard via NodePort:

```bash
kubectl get svc kibana-kibana -n elastic-stack
```

To get login credentials for Kibana:

```bash
# Get username
kubectl get secret elasticsearch-master-credentials -o jsonpath="{.data.username}" | base64 --decode

# Get password
kubectl get secret elasticsearch-master-credentials -o jsonpath="{.data.password}" | base64 --decode
```

Use these credentials to log in to the Kibana dashboard.

## Directory Structure

```
.
├── elasticsearch/
│   └── elasticsearch-values.yaml
├── filebeat/
│   └── filebeat-values.yaml
├── kibana/
│   └── kibana-values.yaml
├── logstash/
│   └── logstash-values.yaml
└── README.md
```

## Support

For more detailed information about configurations and troubleshooting, please refer to the official documentation:
- [Elasticsearch Helm Chart](https://github.com/elastic/helm-charts/tree/main/elasticsearch)
- [Filebeat Helm Chart](https://github.com/elastic/helm-charts/tree/main/filebeat)
- [Logstash Helm Chart](https://github.com/elastic/helm-charts/tree/main/logstash)
- [Kibana Helm Chart](https://github.com/elastic/helm-charts/tree/main/kibana)
