# Print Environment Variables

## Overview
This section demonstrates how to set, access, and print environment variables in Kubernetes. Learn various methods to manage configuration through environment variables.

## Topics Covered
- Defining environment variables in Pod specs
- Using ConfigMaps for environment variables
- Using Secrets for sensitive data
- Downward API for pod metadata
- Field references and resource limits

## Key Objectives
- Set static environment variables in pod definitions
- Inject variables from ConfigMaps and Secrets
- Access pod metadata through Downward API
- Verify environment variables in running containers
- Debug environment variable issues

## Methods
- Direct environment variable assignment
- ConfigMap references
- Secret references
- Downward API references
- Resource limits and requests

## Resources
- [Kubernetes Documentation - Environment Variables](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/)
- [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
- [Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)
- Example manifests and scripts
