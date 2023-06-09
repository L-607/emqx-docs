# Watsons PushGateway Deploy

PushGateWay 部署需要使用如下 K8S yaml 文件进行部署。

~~~yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    dce.daocloud.io/app: pushgateway-sdes
    dce.daocloud.io/component: pushgateway-sdes
    dce.daocloud.io/pushgateway: enable
  name: pushgateway-sdes
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      dce.daocloud.io/app: pushgateway-sdes
      dce.daocloud.io/component: pushgateway-sdes
      dce.daocloud.io/pushgateway: enable
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        dce.daocloud.io/app: pushgateway-sdes
        dce.daocloud.io/component: pushgateway-sdes
        dce.daocloud.io/pushgateway: enable
      name: pushgateway-sdes
    spec:
      containers:
      - args:
        - --web.listen-address=0.0.0.0:9091
        - --web.enable-admin-api
        image: 10.32.224.129/dx-insight/pushgateway:v1.4.2
        imagePullPolicy: IfNotPresent
        name: pushgateway-sdes
        ports:
        - containerPort: 9091
          name: http
          protocol: TCP
        resources:
          limits:
            cpu: '1'
            memory: 2Gi
          requests:
            cpu: 250m
            memory: 2Gi
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
status:
  availableReplicas: 1
  observedGeneration: 4
  readyReplicas: 1
  replicas: 1
  updatedReplicas: 1
---
apiVersion: v1
kind: Service
metadata:
  labels:
    dce.daocloud.io/app: pushgateway-sdes
    dce.daocloud.io/component: pushgateway-sdes
  name: pushgateway-sdes
spec:
  ports:
  - port: 9091
    protocol: TCP
    targetPort: 9091
  selector:
    dce.daocloud.io/component: pushgateway-sdes
  type: NodePort
status:
  loadBalancer: {}

~~~

Prometheus 配置文件中 PushGateWay 需要如下相关配置项。
~~~yaml
- job_name: pushgateway
  honor_timestamps: true
  honor_labels: true
  scrape_interval: 30s
  scrape_timeout: 30s
  metrics_path: /metrics
  scheme: http
  kubernetes_sd_configs:
  - role: pod
  relabel_configs:
  - source_labels: [__meta_kubernetes_pod_label_dce_daocloud_io_pushgateway]
    separator: ;
    regex: enable
    replacement: $1
    action: keep
  - source_labels: [__meta_kubernetes_pod_container_port_name]
    separator: ;
    regex: http
    replacement: $1
    action: keep
  - source_labels: [__meta_kubernetes_namespace]
    separator: ;
    regex: (.*)
    target_label: namespace
    replacement: $1
    action: replace
  - source_labels: [__meta_kubernetes_pod_container_name]
    separator: ;
    regex: (.*)
    target_label: container
    replacement: $1
    action: replace
  - source_labels: [__meta_kubernetes_pod_name]
    separator: ;
    regex: (.*)
    target_label: pod
    replacement: $1
    action: replace
  - separator: ;
    regex: (.*)
    target_label: endpoint
    replacement: http
    action: replace
~~~