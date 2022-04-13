# k8s-simple-kong-ingress-tls-argocd-push-deployment

This project only show the example flow Continous Deployment using ArgoCD, so you need to know about GitOps Principal, do with your own risk

# k8s-kong-ingress-secret-tls
Tutorial
- Apply ingress kong with tls
- Deploy your project k8s yaml in your ops repository using argoCD
### 1. Install Kong Gateway (OSS) on Kubernetes native
   ```bash
   kubectl apply -f https://bit.ly/kong-ingress-dbless
   ```
### 2. Install ArgoCD
   ```bash
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```
### 3. Clone this project into your workspace
   ```bash
   https://github.com/alendwahida/k8s-simple-kong-ingress-tls-argocd-push-deployment.git
   ```
### 4. Generate your certificate file and certificate key from your ssl provider or letsencrypt (Example with wildcard SSL)
### 5. Create secret within ssl certificate into file awn.my.id.crt and key into awn.my.id.key
   ```bash
   kubectl create secret tls awn-tls --key="awn.my.id.key" --cert="awn.my.id.crt" -n argocd
   kubectl create secret tls awn-tls --key="awn.my.id.key" --cert="awn.my.id.crt" -n staging
   ```
### 6. Run your ingress and argocd yaml
   ```bash
   kubectl apply -f .
   ```
### 7. Adding command --insecure
   ```bash
   kubectl edit deploymeny/argocd-server -n argocd
   ```
   add '--insecure' bottom command container
### ![alt text](https://raw.githubusercontent.com/alendwahida/k8s-simple-kong-ingress-tls-argocd-push-deployment/main/blob/enable%20insecure%20argocd%20server.jpg)
### 8. Login ArgoCD Server
### Login
Username: admin
   ```bash
   kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
   ```
Decode password using base64 & login it
### ![alt text](https://raw.githubusercontent.com/alendwahida/k8s-simple-kong-ingress-tls-argocd-push-deployment/main/blob/argocd-login.jpg)
### 9. Setting webhook on your github yaml pk8s roject
### ![alt text](https://raw.githubusercontent.com/alendwahida/k8s-simple-kong-ingress-tls-argocd-push-deployment/main/blob/webhook-yaml-project.jpg)
### 10. Change your configuration github yaml k8s project & see argoCD change process
### ![alt text](https://raw.githubusercontent.com/alendwahida/k8s-simple-kong-ingress-tls-argocd-push-deployment/main/blob/Argocd%20CD.jpg)

### source: 
- https://docs.konghq.com/gateway/2.8.x/install-and-run/kubernetes/
- https://argo-cd.readthedocs.io/en/stable/
- https://www.gitops.tech/
