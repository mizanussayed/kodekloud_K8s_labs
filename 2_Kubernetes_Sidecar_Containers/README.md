# Kubernetes Sidecar Containers

## Overview
- Create a pod named `webserver`.

- Create an `emptyDir` volume named `shared-logs`.

- Create two containers from nginx and ubuntu images with latest tag only and remember to mention tag i.e nginx:latest, nginx container name should be `nginx-container` and ubuntu container name should be `sidecar-container` on `webserver` pod.

- Add command on sidecar-container `"sh","-c","while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"`

- Mount the volume `shared-logs` on both containers at location `/var/log/nginx`, all containers should be up and running.

## Solution
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver
spec:
  volumes:
    - name: shared-logs
      emptyDir: {}
  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
    - name: sidecar-container
      image: ubuntu:latest
      command: ["sh", "-c", "while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"]
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
```
