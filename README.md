# Deploiement de l'application avec helm

1. **Installation d'ArgoCD et argocd cli:**

```bash
  kubectl apply -n <student-a> -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Installation de la CLI argocd

```bash
  brew install argocd
```
[documentation d'ArgoCD](https://argo-cd.readthedocs.io/en/stable/cli_installation/)

2. **Accès à l'interface web ArgoCD :**
- Accéder à l'interface web d'ArgoCD via le service exposé.
  
```bash
  kubectl port-forward svc/argocd-server -n argocd-<student-a> 8080:443
```
- Ouvrir un navigateur et accéder à `https://localhost:8080` (le mot de passe par défaut est `admin`).

4. **Configuration du repository Git :**
  - Créez un repository Git pour l'application.
  - Copiez le contenu de ce dossier dans le repository Git.

5. **Ajout du repository Git à ArgoCD :**
  - Ajouter le repository Git dans ArgoCD pour qu'il surveille les modifications.
  - Il y a plusieurs façons de le faire
  ```bash	
  argocd repo add <URL du repository Git> --username <username> --password <password>
  ```
  -Sinon consulter [la documentation d'ArgoCD](https://argo-cd.readthedocs.io/en/stable/user-guide/private-repositories/) pour plus d'informations.

6. **Vérification du déploiement :**
  - Vérifier l'état du déploiement dans l'interface web d'ArgoCD.
  - Utiliser `kubectl` pour vérifier que les ressources ont été déployées dans le namespace dédié.

7. **Mise à jour de l'application :**
  - Modifier le code de l'application et effectuer un commit dans le repository Git.
  - Utiliser ArgoCD pour synchroniser l'application et appliquer les changements.