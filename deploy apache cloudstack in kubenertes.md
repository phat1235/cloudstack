# Complete Guide: Deploying Apache CloudStack on Kubernetes

## What is Apache CloudStack?

Apache CloudStack is an open-source Infrastructure-as-a-Service (IaaS) cloud computing platform that enables organizations to deploy and manage large networks of virtual machines as highly available and scalable cloud computing services. Originally developed by VMware (under the name VMOps), CloudStack was later acquired by Citrix and eventually donated to the Apache Software Foundation in 2012.

## Core Capabilities

### Infrastructure as a Service (IaaS)
CloudStack provides complete IaaS capabilities, allowing users to create, deploy, and manage virtual machines, storage volumes, and network resources through a web-based interface or comprehensive APIs. It abstracts underlying hardware resources and presents them as consumable cloud services.

### Multi-Hypervisor Support
One of CloudStack’s most powerful features is its ability to support multiple hypervisor technologies within the same cloud infrastructure:
- **KVM** (Kernel-based Virtual Machine): Open-source virtualization built into Linux
- **VMware vSphere**: Enterprise-grade virtualization platform
- **XenServer/Citrix Hypervisor**: High-performance server virtualization
- **Microsoft Hyper-V**: Windows Server virtualization role
- **Oracle VM**: Enterprise-class server virtualization platform

### Multi-Tenancy and Isolation
CloudStack provides robust multi-tenancy capabilities with complete isolation between different users, departments, or customers. It supports:
- Account-based resource isolation
- Network segregation with VLANs and security groups
- Resource quotas and billing integration
- Role-based access control (RBAC)

## Architecture Overview

### Management Server
The CloudStack Management Server is the central orchestration component that:
- Manages the cloud infrastructure and resources
- Provides REST APIs for all cloud operations
- Handles user authentication and authorization
- Coordinates with hypervisors and storage systems
- Manages virtual machine lifecycle operations

### Database Layer
CloudStack uses MySQL as its primary database to store:
- Configuration information
- Resource metadata
- User accounts and permissions
- Usage and billing data
- Virtual machine and storage information

### Hypervisor Hosts
Physical servers running hypervisor software that actually host the virtual machines. CloudStack agents installed on these hosts communicate with the Management Server to execute VM operations.

### Storage Systems
CloudStack integrates with various storage systems:
- **Primary Storage**: High-performance storage for running VMs (NFS, iSCSI, FC, local storage)
- **Secondary Storage**: Repository for VM templates, ISO images, and snapshots (typically NFS)

### Network Infrastructure
CloudStack manages complex networking, including:
- Physical network integration
- VLAN management for network isolation
- Load balancing and firewall services
- VPN connectivity
- Public IP allocation and NAT services

## Key Features and Benefits

### Self-Service Portal
CloudStack provides an intuitive web interface allowing users to:
- Deploy virtual machines from templates
- Manage storage volumes and snapshots
- Configure network settings and security groups
- Monitor resource usage and costs
- Access virtual machines through the console

### Comprehensive APIs
CloudStack offers extensive REST APIs enabling:
- Integration with existing enterprise systems
- Custom portal development
- Automation and orchestration tools integration
- Third-party tool integration

### High Availability and Disaster Recovery
Built-in features for enterprise reliability:
- Automatic VM restart on host failure
- Storage replication and snapshots
- Multi-site deployment capabilities
- Live migration of virtual machines
- Redundant management servers

### Scalability
CloudStack can scale from small deployments to massive cloud infrastructures:
- Supports thousands of physical hosts
- Manages hundreds of thousands of virtual machines
- Horizontal scaling of management components
- Geographic distribution across multiple data centers

### Cost Management
Comprehensive cost tracking and management:
- Detailed usage metering and reporting
- Integration with billing systems
- Resource quotas and limits
- Chargeback and showback capabilities

## Use Cases and Applications

### Private Cloud Deployment
Organizations use CloudStack to build private clouds that:
- Provide self-service infrastructure to internal teams
- Maintain complete control over data and security
- Integrate with existing enterprise systems
- Reduce infrastructure costs through resource pooling

### Public Cloud Services
Service providers use CloudStack to offer public cloud services:
- Multi-tenant cloud hosting
- Virtual private server (VPS) hosting
- Disaster recovery as a service
- Development and testing environments

### Hybrid Cloud Integration
CloudStack enables hybrid cloud architectures by:
- Providing consistent APIs across environments
- Supporting workload migration between clouds
- Maintaining unified management interfaces
- Enabling cloud bursting capabilities

### Educational and Research Institutions
Academic organizations benefit from CloudStack’s:
- Cost-effective virtualization platform
- Research computing resources
- Teaching laboratory environments
- Multi-departmental resource sharing

## CloudStack vs Other Cloud Platforms

### Compared to OpenStack
- **Simplicity**: CloudStack offers simpler installation and management
- **Monolithic Architecture**: Single management plane vs OpenStack’s modular approach
- **Multi-hypervisor**: Native support for multiple hypervisors in a single deployment
- **Maturity**: More mature networking and storage integration

### Compared to VMware vCloud
- **Cost**: Open-source with no licensing fees
- **Vendor Independence**: Not tied to VMware ecosystem
- **Flexibility**: Support for multiple hypervisor types
- **Community**: Large open-source community and ecosystem

### Compared to AWS/Azure
- **Control**: Complete control over infrastructure and data
- **Customization**: Highly customizable to specific requirements
- **Cost**: Lower long-term costs for large deployments
- **Compliance**: Easier compliance with data sovereignty requirements

## Technical Architecture Deep Dive

### Zone-Based Architecture
CloudStack organizes infrastructure into hierarchical zones:
- **Zone**: Typically represents a data center or availability zone
- **Pod**: A rack of hardware with Layer-2 switching
- **Cluster**: Group of identical hypervisor hosts sharing primary storage
- **Host**: Individual physical servers running hypervisor software

### Storage Architecture
CloudStack’s storage model supports:
- **Primary Storage**: Live VM storage (local, NFS, iSCSI, Fiber Channel)
- **Secondary Storage**: Templates, snapshots, ISO images (NFS, object storage)
- **Volume Management**: Create, attach, detach, and snapshot volumes
- **Storage Policies**: Quality of service and placement policies

### Network Architecture
Sophisticated networking capabilities:
- **Physical Networks**: Maps to actual network infrastructure
- **Traffic Types**: Management, public, guest, and storage traffic separation
- **Virtual Networks**: Isolated networks for different tenants
- **Advanced Networking**: Load balancing, VPN, firewall services

## Introduction to Kubernetes Deployment

Deploying Apache CloudStack on Kubernetes represents a modern approach to cloud infrastructure management, combining the power of container orchestration with cloud computing platform capabilities. This deployment model offers enhanced scalability, resilience, and operational efficiency by leveraging Kubernetes’ native features for service discovery, load balancing, auto-scaling, and self-healing.

### Why Containerize CloudStack?

#### Modern Infrastructure Patterns
Containerizing CloudStack aligns with modern infrastructure practices:
- **Immutable Infrastructure**: Containers provide consistent, reproducible deployments
- **Microservices Architecture**: CloudStack components can be independently scaled and updated
- **DevOps Integration**: Container-based deployment integrates with CI/CD pipelines
- **Cloud-Native Benefits**: Leverage cloud-native tools and practices

#### Operational Advantages
Running CloudStack on Kubernetes provides several operational benefits:
- **Simplified Deployment**: Standardized deployment procedures across environments
- **Automated Scaling**: Automatic scaling based on resource usage and demand
- **Self-Healing**: Automatic restart of failed components
- **Rolling Updates**: Zero-downtime updates and rollbacks
- **Resource Optimization**: Better resource utilization through container scheduling

#### Enterprise Integration
Kubernetes deployment enables better enterprise integration:
- **Unified Platform**: Single platform for both CloudStack and containerized applications
- **Consistent Tooling**: Use same monitoring, logging, and security tools
- **Policy Management**: Unified policy and governance frameworks
- **Cost Optimization**: Shared infrastructure reducing overall costs

In this comprehensive guide, we’ll walk through the process of containerizing CloudStack components and deploying them on Kubernetes, covering everything from cluster preparation to production-ready deployments with high availability and monitoring.

## Why Deploy CloudStack on Kubernetes?

### Benefits
- **Scalability**: Automatic scaling of CloudStack components based on demand
- **High Availability**: Built-in redundancy and failover capabilities
- **Resource Efficiency**: Better resource utilization through container scheduling
- **Operational Simplicity**: Standardized deployment, updates, and maintenance
- **Cloud Native Integration**: Native integration with cloud-native tools and practices
- **Cost Optimization**: Efficient resource allocation and usage
- **DevOps Alignment**: Container-based deployment aligns with modern DevOps practices

### Challenges and Considerations
- **Complexity**: Additional layer of abstraction and management
- **Stateful Components**: Managing stateful services like databases
- **Network Configuration**: Complex networking requirements
- **Storage**: Persistent volume management for CloudStack data
- **Security**: Container security and network policies

## Prerequisites and Requirements

### Kubernetes Cluster Requirements

#### Minimum Cluster Specifications
- **Kubernetes Version**: 1.20+ (recommended 1.24+)
- **Nodes**: Minimum 3 nodes for HA deployment
- **CPU**: 8 cores per node minimum
- **Memory**: 16GB RAM per node minimum
- **Storage**: 100GB per node, plus shared storage
- **Network**: CNI plugin installed (Calico, Flannel, or Weave)

#### Recommended Production Setup

Here’s your document reformatted in Markdown:

````markdown
# Verify Kubernetes cluster
kubectl cluster-info
kubectl get nodes

# Required components
# - CNI Plugin (network connectivity)
# - CSI Driver (storage)
# - Ingress Controller (external access)
# - Load Balancer (service exposure)
````

## Required Components

* **CNI Plugin** (network connectivity)
* **CSI Driver** (storage)
* **Ingress Controller** (external access)
* **Load Balancer** (service exposure)

# Software Prerequisites

* **Container Runtime**: Docker, containerd, or CRI-O
* **Helm**: Version 3.x for package management
* **kubectl**: Kubernetes CLI tool
* **Persistent Storage**: StorageClass configured
* **Ingress Controller**: nginx-ingress or traefik

# Containerizing CloudStack Components

## Creating CloudStack Container Images

### Management Server Dockerfile

```Dockerfile
# CloudStack Management Server Container
FROM openjdk:11-jre-slim

LABEL maintainer="cloudstack-dev@apache.org"
LABEL version="4.17"

# Install required packages
RUN apt-get update && apt-get install -y \
    wget \
    curl \
    mysql-client \
    python3 \
    python3-pip \
    supervisor \
    && rm -rf /var/lib/apt/lists/*

# Create cloudstack user
RUN useradd -m -d /var/lib/cloudstack -s /bin/bash cloudstack

# Download and install CloudStack
ENV CLOUDSTACK_VERSION=4.17.2.0
RUN wget -O /tmp/cloudstack.tar.gz \
    "https://downloads.apache.org/cloudstack/${CLOUDSTACK_VERSION}/apache-cloudstack-${CLOUDSTACK_VERSION}-bin.tar.gz" \
    && tar -xzf /tmp/cloudstack.tar.gz -C /opt \
    && mv /opt/apache-cloudstack-${CLOUDSTACK_VERSION} /opt/cloudstack \
    && rm /tmp/cloudstack.tar.gz

# Set permissions
RUN chown -R cloudstack:cloudstack /opt/cloudstack
RUN mkdir -p /var/log/cloudstack/management && \
    chown -R cloudstack:cloudstack /var/log/cloudstack

# Copy configuration files
COPY configs/management/ /opt/cloudstack/conf/
COPY scripts/start-management.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/start-management.sh

# Expose ports
EXPOSE 8080 8250 9090

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=60s --retries=3 \
    CMD curl -f http://localhost:8080/client/ || exit 1

USER cloudstack
CMD ["/usr/local/bin/start-management.sh"]
```

```Dockerfile
# CloudStack Usage Server Container
FROM openjdk:11-jre-slim

LABEL maintainer="cloudstack-dev@apache.org"
LABEL version="4.17"

# Install dependencies
RUN apt-get update && apt-get install -y \
    mysql-client \
    python3 \
    && rm -rf /var/lib/apt/lists/*

# Create cloudstack user
RUN useradd -m -d /var/lib/cloudstack -s /bin/bash cloudstack

# Install CloudStack Usage Server
ENV CLOUDSTACK_VERSION=4.17.2.0
COPY --from=cloudstack-base /opt/cloudstack /opt/cloudstack

# Copy usage server specific configs
COPY configs/usage/ /opt/cloudstack/conf/
COPY scripts/start-usage.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/start-usage.sh

USER cloudstack
CMD ["/usr/local/bin/start-usage.sh"]
```

### Build Scripts

Create a build script for all containers:

```bash
#!/bin/bash
# build-containers.sh

set -e

REGISTRY="your-registry.com/cloudstack"
VERSION="4.17.2"

echo "Building CloudStack containers..."

# Build base image
docker build -t ${REGISTRY}/cloudstack-base:${VERSION} -f Dockerfile.base .

# Build management server
docker build -t ${REGISTRY}/cloudstack-management:${VERSION} -f Dockerfile.management .

# Build usage server
docker build -t ${REGISTRY}/cloudstack-usage:${VERSION} -f Dockerfile.usage .

# Push images
docker push ${REGISTRY}/cloudstack-base:${VERSION}
docker push ${REGISTRY}/cloudstack-management:${VERSION}
docker push ${REGISTRY}/cloudstack-usage:${VERSION}

echo "Container build complete!"
```

# Kubernetes Deployment Configuration

## Namespace and RBAC

### cloudstack-namespace.yaml

```yaml
# cloudstack-namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: cloudstack
  labels:
    name: cloudstack
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: cloudstack-service-account
  namespace: cloudstack
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cloudstack-cluster-role
rules:
- apiGroups: [""]
  resources: ["pods", "services", "endpoints", "persistentvolumeclaims"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]
- apiGroups: ["apps"]
  resources: ["deployments", "statefulsets"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: cloudstack-cluster-role-binding
subjects:
- kind: ServiceAccount
  name: cloudstack-service-account
  namespace: cloudstack
roleRef:
  kind: ClusterRole
  name: cloudstack-cluster-role
  apiGroup: rbac.authorization.k8s.io
```

## ConfigMaps and Secrets

### cloudstack-config.yaml

```yaml
# cloudstack-config.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: cloudstack-config
  namespace: cloudstack
data:
  db.properties: |
    db.cloud.host=mysql-service
    db.cloud.port=3306
    db.cloud.name=cloud
    db.cloud.driver=com.mysql.cj.jdbc.Driver
    db.usage.host=mysql-service
    db.usage.port=3306
    db.usage.name=cloud_usage
    db.usage.driver=com.mysql.cj.jdbc.Driver
  
  server.properties: |
    management.server.host=0.0.0.0
    management.server.port=8080
    cluster.node.IP=${POD_IP}
    host=${POD_IP}
---
apiVersion: v1
kind: Secret
metadata:
  name: cloudstack-secrets
  namespace: cloudstack
type: Opaque
data:
  mysql-root-password: Y2xvdWRzdGFjaw==  # base64 encoded
  mysql-cloud-password: Y2xvdWRzdGFjaw==  # base64 encoded
  mysql-usage-password: Y2xvdWRzdGFjaw==  # base64 encoded
```

# MySQL Database Deployment

### mysql-deployment.yaml

```yaml
# mysql-deployment.yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql
  namespace: cloudstack
spec:
  serviceName: mysql-service
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:8.0
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: cloudstack-secrets
              key: mysql-root-password
        - name: MYSQL_DATABASE
          value: "cloud"
        - name: MYSQL_USER
          value: "cloud"
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: cloudstack-secrets
              key: mysql-cloud-password
        ports:
        - containerPort: 3306
        volumeMounts:
        - name: mysql-data
          mountPath: /var/lib/mysql
        - name: mysql-config
          mountPath: /etc/mysql/conf.d
      volumes:
      - name: mysql-config
        configMap:
          name: mysql-config
  volumeClaimTemplates:
  - metadata:
      name: mysql-data
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 100Gi
---
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
  namespace: cloudstack
spec:
  selector:
    app: mysql
  ports:
  - port: 3306
    targetPort: 3306
  clusterIP: None
```

# CloudStack Management Server Deployment

### management-server-deployment.yaml

```yaml
# management-server-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cloudstack-management
  namespace: cloudstack
spec:
  replicas: 2
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  selector:
    matchLabels:
      app: cloudstack-management
  template:
    metadata:
      labels:
        app: cloudstack-management
    spec:
      serviceAccountName: cloudstack-service-account
      containers:
      - name: cloudstack-management
        image: your-registry.com/cloudstack/cloudstack-management:4.17.2
        ports:
        - containerPort: 8080
        - containerPort: 8250
        - containerPort: 9090
        env:
        - name: POD_IP
          valueFrom:
            fieldRef:
              fieldPath: status.podIP
        - name: MYSQL_HOST
          value: "mysql-service"
        - name: MYSQL_USER
          value: "cloud"
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: cloudstack-secrets
              key: mysql-cloud-password
        volumeMounts:
        - name: cloudstack-config
          mountPath: /opt/cloudstack/conf/db.properties
          subPath: db.properties
        - name: cloudstack-config
          mountPath: /opt/cloudstack/conf/server.properties
          subPath: server.properties
        - name: cloudstack-logs
          mountPath: /var/log/cloudstack
        livenessProbe:
          httpGet:
            path: /client/
            port: 8080
          initialDelaySeconds: 120
          periodSeconds: 30
          timeoutSeconds: 10
        readinessProbe:
          httpGet:
            path: /client/
            port: 8080
          initialDelaySeconds: 60
          periodSeconds: 10
          timeoutSeconds: 5
        resources:
          requests:
            memory: "4Gi"
            cpu: "2"
          limits:
            memory: "8Gi"
            cpu: "4"
      volumes:
      - name: cloudstack-config
        configMap:
          name: cloudstack-config
      - name: cloudstack-logs
        emptyDir: {}
      initContainers:
      - name: wait-for-mysql
        image: busybox:1.35
        command:
        - sh
        - -c
        - |
          until nc -z mysql-service 3306; do
            echo "Waiting for MySQL..."
            sleep 10
          done
          echo "MySQL is ready!"
---
apiVersion: v1
kind: Service
metadata:
  name: cloudstack-management-service
  namespace: cloudstack
spec:
  selector:
    app: cloudstack-management
  ports:
  - name: http
    port: 8080
    targetPort: 8080
  - name: https
    port: 8443
    targetPort: 8080
  - name: api
    port: 8250
    targetPort: 8250
  type: ClusterIP
````

# CloudStack Usage Server Deployment

### usage-server-deployment.yaml

```yaml
# usage-server-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cloudstack-usage
  namespace: cloudstack
spec:
  replicas: 1
  selector:
    matchLabels:
      app: cloudstack-usage
  template:
    metadata:
      labels:
        app: cloudstack-usage
    spec:
      serviceAccountName: cloudstack-service-account
      containers:
      - name: cloudstack-usage
        image: your-registry.com/cloudstack/cloudstack-usage:4.17.2
        env:
        - name: MYSQL_HOST
          value: "mysql-service"
        - name: MYSQL_USER
          value: "cloud"
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: cloudstack-secrets
              key: mysql-usage-password
        volumeMounts:
        - name: cloudstack-config
          mountPath: /opt/cloudstack/conf/db.properties
          subPath: db.properties
        - name: usage-logs
          mountPath: /var/log/cloudstack
        resources:
          requests:
            memory: "2Gi"
            cpu: "1"
          limits:
            memory: "4Gi"
            cpu: "2"
      volumes:
      - name: cloudstack-config
        configMap:
          name: cloudstack-config
      - name: usage-logs
        emptyDir: {}
      initContainers:
      - name: wait-for-management
        image: busybox:1.35
        command:
        - sh
        - -c
        - |
          until nc -z cloudstack-management-service 8080; do
            echo "Waiting for Management Server..."
            sleep 30
          done
          echo "Management Server is ready!"
````

# Ingress Configuration
```
# cloudstack-ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: cloudstack-ingress
  namespace: cloudstack
  annotations:
    kubernetes.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
    nginx.ingress.kubernetes.io/proxy-body-size: "0"
    nginx.ingress.kubernetes.io/proxy-read-timeout: "600"
    nginx.ingress.kubernetes.io/proxy-send-timeout: "600"
    cert-manager.io/cluster-issuer: "letsencrypt-prod"
spec:
  tls:
  - hosts:
    - cloudstack.yourdomain.com
    secretName: cloudstack-tls
  rules:
  - host: cloudstack.yourdomain.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: cloudstack-management-service
            port:
              number: 8080
```
### Helm Chart for CloudStack Deployment
#### Chart Structure

```
cloudstack-helm/
├── Chart.yaml
├── values.yaml
├── templates/
│   ├── namespace.yaml
│   ├── configmap.yaml
│   ├── secrets.yaml
│   ├── mysql/
│   │   ├── statefulset.yaml
│   │   └── service.yaml
│   ├── management/
│   │   ├── deployment.yaml
│   │   └── service.yaml
│   ├── usage/
│   │   └── deployment.yaml
│   └── ingress.yaml
└── charts/
```

### Chart.yaml
```
apiVersion: v2
name: cloudstack
description: Apache CloudStack Helm Chart
version: 0.1.0
appVersion: 4.17.2
keywords:
  - cloudstack
  - cloud
  - virtualization
home: https://cloudstack.apache.org/
sources:
  - https://github.com/apache/cloudstack
maintainers:
  - name: CloudStack Team
    email: dev@cloudstack.apache.org
```

### values.yaml

```
# Default values for CloudStack
global:
  imageRegistry: "your-registry.com/cloudstack"
  imageTag: "4.17.2"
  imagePullPolicy: IfNotPresent
  storageClass: "fast-ssd"

namespace:
  name: cloudstack

mysql:
  enabled: true
  image:
    repository: mysql
    tag: "8.0"
  rootPassword: "changeme"
  cloudPassword: "changeme"
  usagePassword: "changeme"
  persistence:
    size: 100Gi
    storageClass: "fast-ssd"
  resources:
    requests:
      memory: 2Gi
      cpu: 1
    limits:
      memory: 4Gi
      cpu: 2

management:
  replicaCount: 2
  image:
    repository: cloudstack-management
    tag: "4.17.2"
  service:
    type: ClusterIP
    port: 8080
  resources:
    requests:
      memory: 4Gi
      cpu: 2
    limits:
      memory: 8Gi
      cpu: 4
  persistence:
    logs:
      size: 10Gi

usage:
  enabled: true
  replicaCount: 1
  image:
    repository: cloudstack-usage
    tag: "4.17.2"
  resources:
    requests:
      memory: 2Gi
      cpu: 1
    limits:
      memory: 4Gi
      cpu: 2

ingress:
  enabled: true
  className: nginx
  hostname: cloudstack.yourdomain.com
  tls:
    enabled: true
    secretName: cloudstack-tls

monitoring:
  enabled: true
  prometheus:
    enabled: true
  grafana:
    enabled: true

autoscaling:
  enabled: false
  minReplicas: 2
  maxReplicas: 5
  targetCPUUtilizationPercentage: 70
```

### Storage Configuration
### Persistent Volume Claims
```
# storage-pvc.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: cloudstack-nfs-primary
  namespace: cloudstack
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 1Ti
  storageClassName: nfs-storage
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: cloudstack-nfs-secondary
  namespace: cloudstack
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 500Gi
  storageClassName: nfs-storage
```
### NFS Storage Class
```
# nfs-storage-class.yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs-storage
provisioner: k8s-sigs.io/nfs-subdir-external-provisioner
parameters:
  server: nfs-server.yourdomain.com
  path: /cloudstack
  onDelete: retain
allowVolumeExpansion: true
reclaimPolicy: Retain
```

### Monitoring and Observability
#### Prometheus Configuration
```
# prometheus-config.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: prometheus-config
  namespace: cloudstack
data:
  prometheus.yml: |
    global:
      scrape_interval: 15s
    scrape_configs:
    - job_name: 'cloudstack-management'
      static_configs:
      - targets: ['cloudstack-management-service:8080']
      metrics_path: '/client/api'
      params:
        command: ['listCapacity']
        response: ['json']
    - job_name: 'kubernetes-pods'
      kubernetes_sd_configs:
      - role: pod
      relabel_configs:
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
        action: keep
        regex: true
```
### Grafana Dashboard

```
# grafana-dashboard-configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: cloudstack-dashboard
  namespace: cloudstack
  labels:
    grafana_dashboard: "1"
data:
  cloudstack.json: |
    {
      "dashboard": {
        "title": "CloudStack Monitoring",
        "panels": [
          {
            "title": "Management Server CPU Usage",
            "type": "graph",
            "targets": [
              {
                "expr": "rate(container_cpu_usage_seconds_total{pod=~\"cloudstack-management.*\"}[5m])",
                "legendFormat": "{{pod}}"
              }
            ]
          },
          {
            "title": "Management Server Memory Usage",
            "type": "graph", 
            "targets": [
              {
                "expr": "container_memory_usage_bytes{pod=~\"cloudstack-management.*\"}",
                "legendFormat": "{{pod}}"
              }
            ]
          }
        ]
      }
    }
```

### Logging with ELK Stack
```
# filebeat-configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: filebeat-config
  namespace: cloudstack
data:
  filebeat.yml: |
    filebeat.inputs:
    - type: container
      paths:
        - /var/log/containers/cloudstack-*.log
      processors:
      - add_kubernetes_metadata:
          host: ${NODE_NAME}
          matchers:
          - logs_path:
              logs_path: "/var/log/containers/"
    
    output.elasticsearch:
      hosts: ['elasticsearch:9200']
      index: "cloudstack-logs-%{+yyyy.MM.dd}"
    
    setup.template.name: "cloudstack-logs"
    setup.template.pattern: "cloudstack-logs-*"
```

### High Availability Configuration
### Anti-Affinity Rules

```
# ha-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cloudstack-management-ha
  namespace: cloudstack
spec:
  replicas: 3
  selector:
    matchLabels:
      app: cloudstack-management
  template:
    metadata:
      labels:
        app: cloudstack-management
    spec:
      affinity:
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - cloudstack-management
            topologyKey: kubernetes.io/hostname
        nodeAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 100
            preference:
              matchExpressions:
              - key: node-role.kubernetes.io/worker
                operator: In
                values:
                - "true"
      containers:
      - name: cloudstack-management
        image: your-registry.com/cloudstack/cloudstack-management:4.17.2
        # ... container configuration
```

### Pod Disruption Budget
```
# pod-disruption-budget.yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: cloudstack-management-pdb
  namespace: cloudstack
spec:
  minAvailable: 1
  selector:
    matchLabels:
      app: cloudstack-management
---
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: mysql-pdb
  namespace: cloudstack
spec:
  minAvailable: 1
  selector:
    matchLabels:
      app: mysql
```

### Security Configuration
### Network Policies

```
# network-policies.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: cloudstack-network-policy
  namespace: cloudstack
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          name: ingress-nginx
    - podSelector:
        matchLabels:
          app: cloudstack-management
    ports:
    - protocol: TCP
      port: 8080
  - from:
    - podSelector:
        matchLabels:
          app: cloudstack-management
    - podSelector:
        matchLabels:
          app: cloudstack-usage
    ports:
    - protocol: TCP
      port: 3306
  egress:
  - to: []
    ports:
    - protocol: TCP
      port: 53
    - protocol: UDP
      port: 53
  - to:
    - podSelector:
        matchLabels:
          app: mysql
    ports:
    - protocol: TCP
      port: 3306
```

### Pod Security Context
```
# security-context.yaml
apiVersion: v1
kind: Pod
spec:
  securityContext:
    runAsNonRoot: true
    runAsUser: 1000
    fsGroup: 1000
    seccompProfile:
      type: RuntimeDefault
  containers:
  - name: cloudstack-management
    securityContext:
      allowPrivilegeEscalation: false
      readOnlyRootFilesystem: true
      capabilities:
        drop:
        - ALL
        add:
        - NET_BIND_SERVICE
```

### Deployment Scripts and Automation
### Deployment Script
```
#!/bin/bash
# deploy-cloudstack.sh

set -e

NAMESPACE="cloudstack"
REGISTRY="your-registry.com/cloudstack"
VERSION="4.17.2"

echo "Deploying CloudStack on Kubernetes..."

# Create namespace
kubectl apply -f cloudstack-namespace.yaml

# Deploy MySQL
echo "Deploying MySQL..."
kubectl apply -f mysql-config.yaml
kubectl apply -f mysql-deployment.yaml

# Wait for MySQL to be ready
echo "Waiting for MySQL to be ready..."
kubectl wait --for=condition=ready pod -l app=mysql -n ${NAMESPACE} --timeout=300s

# Initialize CloudStack database
echo "Initializing CloudStack database..."
kubectl run cloudstack-db-init \
  --image=mysql:8.0 \
  --restart=Never \
  --namespace=${NAMESPACE} \
  --rm -it -- \
  mysql -h mysql-service -u root -p${MYSQL_ROOT_PASSWORD} -e "
    CREATE DATABASE IF NOT EXISTS cloud;
    CREATE DATABASE IF NOT EXISTS cloud_usage;
    GRANT ALL PRIVILEGES ON cloud.* TO 'cloud'@'%';
    GRANT ALL PRIVILEGES ON cloud_usage.* TO 'cloud'@'%';
    FLUSH PRIVILEGES;"

# Deploy CloudStack components
echo "Deploying CloudStack Management Server..."
kubectl apply -f cloudstack-config.yaml
kubectl apply -f management-server-deployment.yaml

# Wait for management server
echo "Waiting for Management Server to be ready..."
kubectl wait --for=condition=ready pod -l app=cloudstack-management -n ${NAMESPACE} --timeout=600s

# Deploy Usage Server
echo "Deploying Usage Server..."
kubectl apply -f usage-server-deployment.yaml

# Deploy Ingress
echo "Configuring Ingress..."
kubectl apply -f cloudstack-ingress.yaml

# Deploy monitoring
echo "Setting up monitoring..."
kubectl apply -f prometheus-config.yaml
kubectl apply -f grafana-dashboard-configmap.yaml

echo "CloudStack deployment completed!"
echo "Access CloudStack at: https://cloudstack.yourdomain.com"
```
### Helm Deployment
```
#!/bin/bash
# helm-deploy.sh

set -e

RELEASE_NAME="cloudstack"
NAMESPACE="cloudstack"
CHART_PATH="./cloudstack-helm"

echo "Deploying CloudStack using Helm..."

# Add required repositories
helm repo add stable https://charts.helm.sh/stable
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

# Install ingress controller if not exists
if ! kubectl get namespace ingress-nginx > /dev/null 2>&1; then
  helm install ingress-nginx ingress-nginx/ingress-nginx \
    --create-namespace \
    --namespace ingress-nginx \
    --set controller.service.type=LoadBalancer
fi

# Install CloudStack
helm upgrade --install ${RELEASE_NAME} ${CHART_PATH} \
  --namespace ${NAMESPACE} \
  --create-namespace \
  --values values-production.yaml \
  --wait \
  --timeout 15m

echo "CloudStack deployed successfully with Helm!"

# Get ingress IP
INGRESS_IP=$(kubectl get svc -n ingress-nginx ingress-nginx-controller -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
echo "Access CloudStack at: http://${INGRESS_IP} or https://cloudstack.yourdomain.com"
```

### Backup and Disaster Recovery
### Database Backup
```
# backup-cronjob.yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: cloudstack-db-backup
  namespace: cloudstack
spec:
  schedule: "0 2 * * *"  # Daily at 2 AM
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: mysql-backup
            image: mysql:8.0
            command:
            - /bin/bash
            - -c
            - |
              TIMESTAMP=$(date +%Y%m%d_%H%M%S)
              mysqldump -h mysql-service -u root -p${MYSQL_ROOT_PASSWORD} \
                --single-transaction --routines --triggers cloud > /backup/cloud_${TIMESTAMP}.sql
              mysqldump -h mysql-service -u root -p${MYSQL_ROOT_PASSWORD} \
                --single-transaction --routines --triggers cloud_usage > /backup/cloud_usage_${TIMESTAMP}.sql
              # Upload to S3 or other backup storage
              aws s3 cp /backup/cloud_${TIMESTAMP}.sql s3://cloudstack-backups/
              aws s3 cp /backup/cloud_usage_${TIMESTAMP}.sql s3://cloudstack-backups/
            env:
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: cloudstack-secrets
                  key: mysql-root-password
            volumeMounts:
            - name: backup-storage
              mountPath: /backup
          volumes:
          - name: backup-storage
            emptyDir: {}
          restartPolicy: OnFailure
```

### Velero Backup Configuration
```
# velero-backup.yaml
apiVersion: velero.io/v1
kind: Backup
metadata:
  name: cloudstack-backup
  namespace: velero
spec:
  includedNamespaces:
  - cloudstack
  excludedResources:
  - events
  - events.events.k8s.io
  ttl: 720h  # 30 days
  storageLocation: default
  volumeSnapshotLocations:
  - default
```

### Scaling and Performance Optimization
### Horizontal Pod Autoscaler
```
# hpa.yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: cloudstack-management-hpa
  namespace: cloudstack
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: cloudstack-management
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
  behavior:
    scaleDown:
      stabilizationWindowSeconds: 300
      policies:
      - type: Percent
        value: 10
        periodSeconds: 60
    scaleUp:
      stabilizationWindowSeconds: 60
      policies:
      - type: Percent
        value: 50
        periodSeconds: 60
```

### Vertical Pod Autoscaler
```
# vpa.yaml
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
  name: cloudstack-management-vpa
  namespace: cloudstack
spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: cloudstack-management
  updatePolicy:
    updateMode: "Auto"
  resourcePolicy:
    containerPolicies:
    - containerName: cloudstack-management
      maxAllowed:
        cpu: 8
        memory: 16Gi
      minAllowed:
        cpu: 1
        memory: 2Gi
```

### Troubleshooting Guide
### Common Issues and Solutions
### Pod Stuck in Pending State
```
# Check node resources
kubectl describe nodes

# Check PVC status
kubectl get pvc -n cloudstack

# Check events
kubectl get events -n cloudstack --sort-by='.lastTimestamp'
```

### Database Connection Issues
```
# Test database connectivity
kubectl run mysql-test --image=mysql:8.0 --restart=Never -n cloudstack --rm -it -- \
  mysql -h mysql-service -u cloud -p

# Check MySQL logs
kubectl logs -n cloudstack mysql-0

# Verify service DNS resolution
kubectl run dns-test --image=busybox --restart=Never -n cloudstack --rm -it -- \
  nslookup mysql-service

```
### Management Server Not Starting
```
# Check logs
kubectl logs -n cloudstack deployment/cloudstack-management

# Check configuration
kubectl describe configmap cloudstack-config -n cloudstack

# Check resource constraints
kubectl top pods -n cloudstack
```

### Ingress Not Working
```
# Check ingress status
kubectl get ingress -n cloudstack

# Verify ingress controller
kubectl get pods -n ingress-nginx

# Check service endpoints
kubectl get endpoints -n cloudstack
```
### Performance Tuning
#### JVM Optimization
```
# Add to management server deployment
env:
- name: JAVA_OPTS
  value: "-Xms4g -Xmx8g -XX:+UseG1GC -XX:+UseStringDeduplication -XX:MaxGCPauseMillis=200"
```
### Database Optimization
```
# MySQL configuration optimization
apiVersion: v1
kind: ConfigMap
metadata:
  name: mysql-config
  namespace: cloudstack
data:
  my.cnf: |
    [mysqld]
    innodb_buffer_pool_size = 4G
    innodb_log_file_size = 512M
    innodb_flush_log_at_trx_commit = 2
    query_cache_size = 512M
    max_connections = 1000
    thread_cache_size = 64
    table_open_cache = 4096
    tmp_table_size = 256M
    max_heap_table_size = 256M
```

### Production Considerations
### Security Best Practices
```
Network Segmentation: Use network policies to isolate CloudStack components
Secrets Management: Use external secret management systems (Vault, AWS Secrets Manager)
Image Security: Scan container images for vulnerabilities
RBAC: Implement least privilege access controls
TLS Encryption: Enable TLS for all communications
```
### Operational Best Practices
```
Monitoring: Implement comprehensive monitoring and alerting
Logging: Centralize logs with structured logging
Backup: Regular automated backups with tested restore procedures
Updates: Implement rolling updates with canary deployments
Resource Management: Set appropriate resource limits and requests
```
### Cost Optimization
```Resource Right-sizing: Use VPA to optimize resource allocation
Node Autoscaling: Implement cluster autoscaling for cost efficiency
Spot Instances: Use spot instances for non-critical workloads
Storage Optimization: Use appropriate storage classes for different workloads
```
### Conclusion
Deploying Apache CloudStack on Kubernetes represents a significant advancement in cloud infrastructure management, combining the robustness of CloudStack with the modern orchestration capabilities of Kubernetes. This deployment model offers:

### Key Benefits Achieved
Enhanced Scalability: Automatic scaling based on demand

Improved Reliability: Built-in redundancy and self-healing capabilities

Operational Efficiency: Standardized deployment and management processes

Cost Optimization: Better resource utilization and cost control

Modern Architecture: Cloud-native approach aligned with current best practices
### Success Factors
Proper Planning: Thorough architecture and capacity planning

Security First: Implement security measures from the beginning

Monitoring: Comprehensive observability and alerting


Testing: Extensive testing in non-production environments

Documentation: Maintain detailed documentation and runbooks

### Future Considerations
Service Mesh Integration: Consider implementing service mesh for advanced traffic management

Multi-Cloud Deployment: Explore deployment across multiple Kubernetes clusters

GitOps Integration: Implement GitOps workflows for automated deployments

Machine Learning: Integrate ML-based optimization and predictive scaling

This comprehensive guide provides the foundation for successfully deploying and managing 
Apache CloudStack on Kubernetes in production environments. Regular maintenance, 
monitoring, and updates are essential for maintaining a healthy and secure deployment.



QA;
```
Could you please share the following information for the management server Dockerfile and usage server docker file
COPY configs/management/ /opt/cloudstack/conf/
COPY scripts/start-management.sh /usr/local/bin/
COPY configs/usage/ /opt/cloudstack/conf/
COPY scripts/start-usage.sh /usr/local/bin/
Thanks
```
