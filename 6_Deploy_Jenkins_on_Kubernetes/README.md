# Deploy Jenkins on Kubernetes

## Overview

The Nautilus DevOps team is planning to set up a Jenkins CI server to create/manage some deployment pipelines for some of the projects. They want to set up the Jenkins server on Kubernetes cluster. Below you can find more details about the task:


1) Create a namespace `jenkins`

2) Create a Service for jenkins deployment. Service name should be `jenkins-service` under `jenkins` namespace, type should be NodePort, nodePort should be 30008

3) Create a Jenkins Deployment under jenkins namespace, It should be name as `jenkins-deployment` , labels app should be jenkins , container name should be jenkins-container , use jenkins/jenkins image , containerPort should be 8080 and replicas count should be 1.


## Solution
1) Create a namespace jenkins

```bash
kubectl create namespace jenkins
```
2) Create service & deployment using below yaml file

```yaml
apiVersion: v1
kind: Service
metadata:
  name: jenkins-service
  namespace: jenkins
spec:
  type: NodePort
  selector:
    app: jenkins
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
      nodePort: 30008
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: jenkins-deployment
  namespace: jenkins
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins
  template:
    metadata:
      labels:
        app: jenkins
    spec:
      containers:
      - name: jenkins-container
        image: jenkins/jenkins
        ports:
        - containerPort: 8080
```

3) Apply the yaml file

```bash
kubectl apply -f jenkins.yaml
# change context to jenkins namespace
kubectl config set-context --current --namespace=jenkins
```