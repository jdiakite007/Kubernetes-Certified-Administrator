


### 📦 Installation de Argo CD sur Kubernetes

Ce guide explique comment installer **Argo CD** dans un cluster Kubernetes en utilisant `kubectl`.

---

### 🚀 Commandes d'installation

## Étapes pour installer Argo CD

1. Créer le namespace dans Kubernetes pour Argo CD :

   ```bash
   kubectl create namespace argocd
   ```
2. Télécharger et appliquer les fichiers de configuration (manifests) nécessaires à Argo CD :  
```bash 
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v3.0.11/manifests/install.yaml     
```

3. Redirigerle port 443 du service argocd-server vers un port de ta machine locale afin
 que tu puisses accéder à l'interface Web depuis ton navigateur.
```bash 
kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 0.0.0.0 &
```
4. Ouvre ton navigateur et accède à :
http://localhost:8080

5. Récupère le mot de passe initial (par défaut = nom du pod argocd-server) :
```bash 
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo
```

⚠️ Attention : la commande --address 0.0.0.0 rend l’interface ArgoCD accessible depuis d’autres machines.
Pour usage local uniquement, préférez :
```bash 
kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 127.0.0.1
```
Pour plus de détails :
👉 [Voir la documentation officielle](https://argo-cd.readthedocs.io/en/stable/getting_started/)
