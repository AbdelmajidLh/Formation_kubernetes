# Architecture Kubernetes (version debutant)

## Control Plane (control plane node)
Le control plane (node maitre) pilote le cluster: il planifie les Pods, suit leur etat, applique l'etat desire et sert de point d'acces principal pour l'administration (kubectl, API). Il coordonne toutes les operations de controle et de reconciliation.

- Serveur API : point d'entree principal pour toutes les operations du cluster et d'administration; c'est le hub de communication. Il est sans etat; l'etat des objets Kubernetes est persiste dans etcd.
- etcd : base cle/valeur qui stocke l'etat de reference du cluster (objets, configs) pour survivre aux redemarrages.
- Planificateur (scheduler) : decide sur quel noeud demarrer les Pods selon leurs besoins en ressources et les politiques admin.
- Gestionnaire de controlleurs (controller manager) : orchestre les differents controlleurs qui surveillent l'etat des objets (Pods, stockage, etc.) et appliquent le cycle de vie voulu.

## Nodes (worker nodes)
Un cluster est un ensemble de nodes (au moins un). C'est sur les nodes que les Pods applicatifs tournent vraiment. Un node peut etre une machine physique ou une VM, et apporte sa puissance de calcul au cluster.

Exemple: on deploie WordPress. Si le site recoit des millions de visites, un seul node peut saturer. On ajoute alors des Pods (scaling) et un equilibrage de charge pour repartir la charge, voire on ajoute des nodes pour augmenter la capacite globale.

## kubectl (client)
kubectl ne fait pas partie du control plane: c'est l'outil avec lequel nous parlons au serveur API pour administrer le cluster.

[Schema control plane](src/imgs/kubernetes_control_plan.png)
