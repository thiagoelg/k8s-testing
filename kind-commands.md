Versions
Kind: 0.17.0
Kubernetes: 1.25.3

# Create the cluster
- `kind create cluster --config kind-cluster.yml`

# Install Ingress
- `kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml`
- `kubectl wait --namespace ingress-nginx --for=condition=ready pod --selector=app.kubernetes.io/component=controller --timeout=90s`

# Install API local proxy
- `kubectl apply -f kube-proxy.yml`

# Install dashboard (optional)
- `kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml`

# Create service account
- `kubectl apply -f service-account.yml`

# Get token
- `kubectl get secret kie-sandbox-secret -o jsonpath={.data.token} | base64 -d`