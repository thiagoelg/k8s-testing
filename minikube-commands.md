Versions:
Minikube: 1.29.0
Kubernetes: 1.26.1
Docker driver

# Create the cluster
- `minikube start --extra-config "apiserver.cors-allowed-origins=["https://\*"]"  --ports 80:80,443:443,8443:8443 --listen-address 0.0.0.0`

# Create service account
- `kubectl apply -f service-account.yml`

# Install Ingress
- `minikube addonss enable ingress`
- `kubectl wait --namespace ingress-nginx --for=condition=ready pod --selector=app.kubernetes.io/component=controller --timeout=90s`

# Install API local proxy
- `kubectl apply -f kube-proxy.yml`

# Run dashboard (optional)
- `minikube dashboard`

# Get token
- `kubectl get secret default-secret -o jsonpath={.data.token} | base64 -d`