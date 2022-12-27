# Overview

![ObservableArch](/scripts/pic/ObservableArchDesign.jpg "ObservableArch")

# Prep

* [Prep For AWS and EKS](readme-aws.md)

# Install

```
cat > values.yaml << EOF
kube2iam:
  aws:
    region: "cn-northwest-1"
  extraArgs:
    base-role-arn: "arn:aws-cn:iam::xxxxxxxxxxxx:role/" # replace with your AWS-CN CountID
    default-role: kube2iam-default
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
