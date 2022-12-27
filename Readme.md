# Overview

![ObservableArch](/scripts/pic/ObservableArchDesign.jpg "ObservableArch")

# Prep

* [Prep For AWS and EKS](readme-aws.md)

# Install

```
cat > values.yaml << EOF
prometheus-to-cloudwatch:
  replicaCount: 1
  podAnnotations:
    iam.amazonaws.com/role:  kube2iam-default
  env:
    CLOUDWATCH_NAMESPACE: "app-dev"
    CLOUDWATCH_REGION: "cn-northwest-1"
kube2iam:
  aws:
    region: "cn-northwest-1"
  extraArgs:
    base-role-arn: "arn:aws-cn:iam::xxxxxxxxxxx:role/" # replace aws count id
    default-role: kube2iam-default
fluent-bit:
  enabled: true
  annotations:
    iam.amazonaws.com/role: kube2iam-default
  config:
    outputs: |
      [OUTPUT]
          Name cloudwatch_logs
          region "cn-northwest-1"
          Match kube.*
          log_group_name log_group_name    #replace your define name
          log_stream_name log_stream_name  #replace your define name
          auto_create_group true
EOF

helm repo add stable https://artifact.onwalk.net/chartrepo/k8s/
helm repo update
helm upgrade --install observableagent stable/observableagent -n monitoring --create-namespace -f values.yaml 
```

# Configure


# LiveDemo

# Reference 

- https://helm.neo4j.com/neo4j
- https://grafana.github.io/helm-charts
- https://deepflowys.github.io/deepflow
- https://prometheus-community.github.io/helm-charts

# Todo

## Dev Reference 
- https://github.com/YunaiV/ruoyi-vue-pro
- https://github.com/todoadmin/vue-admin-chart
- https://github.com/ClaudioWaldvogel/cloudwatch-loki-shipper
- https://github.com/cpsrepositorio/cps-marketplace-layout
- https://github.com/Hayaking/clickhouse-keeper-on-k8s
