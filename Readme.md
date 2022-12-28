# Overview

![ObservableArch](/scripts/pic/ObservableArchDesign.jpg "ObservableArch")

# Prep

* [Prep For AWS and EKS](readme-aws.md)

# Install

## install For EKS with AWS credentials

```
cat > values.yaml << EOF
prometheus-to-cloudwatch:
  replicaCount: 1
  env:
    AWS_ACCESS_KEY_ID: xxxxxxxx
    AWS_SECRET_ACCESS_KEY: xxxxxxx
    CLOUDWATCH_NAMESPACE: "app-dev"
    CLOUDWATCH_REGION: "cn-northwest-1"
    PROMETHEUS_SCRAPE_URL: 'http://observableagent-kube-state-metrics.monitoring.svc.cluster.local:8080/metrics'
fluent-bit:
  enabled: true
  env:
    - name: AWS_ACCESS_KEY_ID
      value: "xxxxxx"
    - name: AWS_SECRET_ACCESS_KEY
      value: "xxxxxx"
  image:
    repository: artifact.onwalk.net/k8s/fluent-bit
    tag: "2.0.8"
    pullPolicy: Always
  config:
    outputs: |
      [OUTPUT]
          Name cloudwatch_logs
          region cn-northwest-1
          Match kube.*
          log_group_name app-dev
          log_stream_name log_stream_eks_app_dev
          auto_create_group true
EOF

helm repo add stable https://artifact.onwalk.net/chartrepo/k8s/
helm repo update
helm upgrade --install observableagent stable/observableagent -n monitoring --create-namespace -f values.yaml 
```

# Configure


# LiveDemo

# Reference 

- https://github.com/jtblin/kube2iam
- https://grafana.github.io/helm-charts
- https://deepflowys.github.io/deepflow
- https://prometheus-community.github.io/helm-charts
- https://github.com/fluent/fluent-bit-docs/blob/43c4fe134611da471e706b0edb2f9acd7cdfdbc3/administration/aws-credentials.md

# Todo

## Dev Reference 
- https://github.com/YunaiV/ruoyi-vue-pro
- https://github.com/todoadmin/vue-admin-chart
- https://github.com/ClaudioWaldvogel/cloudwatch-loki-shipper
- https://github.com/cpsrepositorio/cps-marketplace-layout
- https://github.com/Hayaking/clickhouse-keeper-on-k8s
