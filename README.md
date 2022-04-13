# k8s-simple-kong-ingress-tls-argocd-push-deployment

k8s-simple-kong-ingress-tls-argocd-push-deployment

# k8s-kong-ingress-secret-tls
Tutorial
- Apply ingress kong with tls
- Apply CD argoCD
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
### 4. Generate your certificate file and certificate key from your ssl provider or letsencrypt
### 5. Create secret within ssl certificate into file awn.my.id.crt and key into awn.my.id.key
   ```bash
   kubectl create secret tls awn-tls --key="awn.my.id.key" --cert="awn.my.id.crt" -n argocd
   kubectl create secret tls awn-tls --key="awn.my.id.key" --cert="awn.my.id.crt" -n staging
   ```
### 6. Output:
![alt text](https://raw.githubusercontent.com/alendwahida/k8s-kong-ingress-secret-tls/main/blob/kong-ssl-lets-encrypt.jpg)

### 7. Run your ingress and argocd yaml
   ```bash
   kubectl apply -f .
   ```
### 8. Adding command --insecure
   ```bash
   kubectl edit deploymeny/argocd-server -n argocd
   ```
   add '--insecure' bottom command container
![alt text](https://raw.githubusercontent.com/alendwahida/k8s-simple-kong-ingress-tls-argocd-push-deployment/main/blob/enable%20insecure%20argocd%20server.jpg)
### source: https://docs.konghq.com/gateway/2.8.x/install-and-run/kubernetes/
