---
title: K8S Cheatsheet
---

## Deployment

To list all deployments:

    kubectl get deployments --all-namespaces

To delete the deployment:

    kubectl delete -n NAMESPACE deployment DEPLOYMENT

## Master Node IP

    kubectl get nodes --selector=node-role.kubernetes.io/master -o jsonpath='{$.items[*].status.addresses[?(@.type=="InternalIP")].address}'
