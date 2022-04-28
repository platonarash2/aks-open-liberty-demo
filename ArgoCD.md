
# Setup instructions
https://argo-cd.readthedocs.io/en/stable/getting_started/

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

get the pwd:
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo


# Integrate with Azure Active Directory
https://argo-cd.readthedocs.io/en/stable/operator-manual/user-management/microsoft/#azure-ad-app-registration-auth-using-oidc

# RBAC config 
https://argo-cd.readthedocs.io/en/stable/operator-manual/rbac/

# Config files
https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/



