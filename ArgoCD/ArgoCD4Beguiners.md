### 🚀 Déployer une App sur Minikube avec Argo CD et GitHub

### ✅  Démarrer Minikube
 ```bash
minikube start
 ```
### 📦 Installer Argo CD

1. Créer le namespace pour Argo CD :

   ```bash
   kubectl create namespace argocd
   ```
2.  Installer Argo CD:  
```bash 
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v3.0.11/manifests/install.yaml     
```

3. Exposer l'interface web d'Argo CD
   Rediriger le port 443 du service argocd-server vers un port de ta machine locale 
```bash 
kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 0.0.0.0 &
```
⚠️ Attention : la commande --address 0.0.0.0 rend l’interface ArgoCD accessible depuis d’autres machines.
Pour usage local uniquement, préférez :
```bash 
kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 127.0.0.1
```
4. Récupérer le mot de passe admin:
```bash 
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo
```
5. Accéder à l'interface Argo CD
   Ouvre ton navigateur et accède à :http://localhost:8080       
➡️ Identifiants :       
    Username : admin      
    Password : (celui récupéré à l'étape 4)      

6. Ajouter une App via GitHub
 
Exemple: avec une app Nginx dans un repo GitHub :      

➡️ Dans l'interface Argo CD:     
clique sur "NEW APP"       
Puis remplis :            
    Application Name: nginx-app     
    Project: default     
    Sync Policy: Manual ou Automatic     
    Repository URL: https://github.com/diakite007/Kubernetes-Certified-Administrator     
    Revision: HEAD    
    Path: ArgoCD   
    Cluster: https://kubernetes.default.svc      
    Namespace: default      
✅ Clique sur "Create", puis sur "Sync"     

✅ 7. Accéder à ton app déployée
Ton app utilise probablement un Service NodePort.    

Pour trouver son port :<img width="855" height="158" alt="image" src="https://github.com/user-attachments/assets/4a6149f0-c88c-4aaf-a33b-b665a39fd640" />

```bash
http://$(minikube ip):<NodePort>
```
```bash 
curl http://$(minikube ip):<NodePort>
```
<img width="928" height="386" alt="image" src="https://github.com/user-attachments/assets/2cc5cbc6-2d4c-4ce5-8a34-c798c2095ec6" />


Pour plus de détails :
👉 [Voir la documentation officielle](https://argo-cd.readthedocs.io/en/stable/getting_started/)
    
