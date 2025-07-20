

# 📦 Installation de Argo CD sur Kubernetes

Ce guide explique comment installer **Argo CD** dans un cluster Kubernetes en utilisant `kubectl`.

---

## 🚀 Commandes d'installation

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v3.0.11/manifests/install.yaml



📝 Explication rapide

    kubectl create namespace argocd
    ➜ Crée un espace isolé dans Kubernetes pour Argo CD

    kubectl apply -n argocd -f <URL>
    ➜ Télécharge et applique les fichiers de configuration (manifests) nécessaires à Argo CD


✅ Étapes suivantes

Une fois Argo CD installé :

    Redirige le port pour accéder à l'interface Web :

kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 0.0.0.0 &

Ouvre ton navigateur et accède à :
http://localhost:8080

Récupère le mot de passe initial (par défaut = nom du pod argocd-server) :
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo

🔐 Sécurité

⚠️ Attention : la commande --address 0.0.0.0 rend l’interface ArgoCD accessible depuis d’autres machines.
Pour usage local uniquement, préférez :

kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 127.0.0.1

📚 Documentation officielle

Pour plus de détails :
👉 https://argo-cd.readthedocs.io/
