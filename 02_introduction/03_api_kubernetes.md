# API Kubernetes

L'API est le centre de commande du cluster. Tout passe par l'API Server : kubectl, CI/CD, dashboards ou operateurs.

## Comment on parle a Kubernetes
- **API REST/HTTP + JSON** : chaque ressource (Pod, Service, Deployment, etc.) est un objet JSON.
- **Porte d'entree unique** : c'est le seul moyen d'interagir avec le cluster, et Kubernetes lui-meme n'agit que via cette API.
- **Serialise et persiste** : les objets sont convertis en JSON puis stockes dans etcd; l'etat survit aux redemarrages.

## Declaratif vs imperatif
- **Declaratif** : on ecrit ce qu'on veut obtenir (YAML), on l'applique (`kubectl apply`, Helm, kustomize) et Kubernetes se debrouille pour atteindre cet etat.
- **Imperatif** : on donne une commande directe (`kubectl create`, `kubectl delete`, `kubectl scale`, `kubectl set image`) pour changer l'etat tout de suite. Pratique pour tester, moins reproductible.

## Exemple simple
- Declaratif : `kubectl apply -f deployment.yaml` (decrit 3 replicas d'une image).
- Imperatif : `kubectl scale deployment myapp --replicas=3`.

## Pourquoi l'API est essentielle
- **Controleurs / boucle de reconciliation** lisent l'etat desire dans l'API et ajustent l'etat reel (creer/supprimer/mettre a jour des Pods).
- **Securite** : auth + RBAC decident qui peut lire ou modifier quels objets.
- **Automatisation** : CI/CD, GitOps, scripts, tout le monde parle le meme langage (l'API) pour piloter le cluster.
