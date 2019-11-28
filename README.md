## Sentry for Vorwaerts
**Author:** Ruben Ceballos  
**Email:** rubendcm9708@gmail.com  
### Prerequisites:
1. Kubernetes 1.16.X Cluster with at least 1 worker node. Preferable 2 CPUS and 6 GB RAM.  
2. Minikube for local deployment.

### Deployment:
1. Install kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl/  

1. Install minikube: https://github.com/kubernetes/minikube  

1. Start minikube:  
`minikube start --vm-driver=none --memory=6144 --cpus=2`  

1. Enable ingress:  
`minikube addons enable ingress`  

1. Add sentry hostname to /etc/hosts:  
`echo "$(minikube ip) sentry.vorwaerts.com" | sudo tee -a /etc/hosts`  

1. Apply sentry config:  
`kubectl apply -f .`  

1. Check the pod status until it is running:  
`kubectl get pods -n sentry`  

1. Then access the shell for the container running in the *sentry-server* pod, copy the pod name and replace:  
`kubectl exec -n sentry -it <sentry-server-podname> -- /bin/bash `  

1. Update the sentry service:  
`sentry update`  

  **note**: This is done manually because the service is going to ask the user if he wants to create a user, so type yes and pass user email and password.  

1. Check for the entry point for the sentry-server and access the host in your web browser of preference. Finally, config the requested values by sentry:  
`service sentry-server -n sentry --url`

## References
1. https://hub.docker.com/_/sentry/
1. https://docs.sentry.io/server/installation/
