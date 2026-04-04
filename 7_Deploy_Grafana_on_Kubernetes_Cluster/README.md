# Deploy Grafana on Kubernetes Cluster

## Overview
The Nautilus DevOps teams is planning to set up a Grafana tool to collect and analyze analytics from some applications. They are planning to deploy it on Kubernetes cluster. Below you can find more details.

1.) Create a deployment named grafana-deployment-xfusion using any grafana image for Grafana app. Set other parameters as per your choice.

2.) Create NodePort type service with nodePort 32000 to expose the app.

## Steps to Deploy Grafana on Kubernetes Cluster
1. Create a deployment named `grafana-deployment-xfusion` & service using the following command:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-xfusion
spec:
    replicas: 1
    selector:
      matchLabels:
        app: grafana
    template:
        metadata:
        labels:
            app: grafana
        spec:
        containers:
        - name: grafana
            image: grafana/grafana:latest
            ports:
            - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: grafana-service-xfusion
spec:
  type: NodePort
  selector:
    app: grafana
  ports:
    - protocol: TCP
      port: 3000
      targetPort: 3000
      nodePort: 32000
```
