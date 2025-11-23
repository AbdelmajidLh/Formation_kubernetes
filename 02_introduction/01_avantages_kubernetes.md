# Avantages de Kubernetes

Kubernetes sert a exploiter un cluster comme une plateforme unique pour vos conteneurs. Il automatise les taches repetitives (deploiement, mise a jour, surveillance, redemarrage) et cache la complexite des machines sous-jacentes.

- Deploiement rapide : appliquer des manifests YAML (ou Helm charts) pour lancer ou mettre a jour des services en quelques secondes; les changements sont declaratifs et reproductibles.
- Absorber rapidement les changements : nouvelle image poussee par un developpeur -> rolling update automatise, seuils de sante verifies, retour arriere (rollback) en un clic ou une commande.
- Capacite de recuperation rapide : si un pod ou un noeud tombe, Kubernetes recree les replicas ailleurs, relance les conteneurs qui echouent et maintient le nombre voulu d'instances (self-healing).
- Masquer la complexite du cluster : abstraction reseau/stockage/compute; vous decrivez l'etat desire (nombre de replicas, ports exposes, volumes), Kubernetes se charge du placement, du routage et de la persistance.
- Scalabilite controlee : horizontal pod autoscaling possible sur CPU/RAM ou metrics custom; ajout/retrait de replicas sans interruption.
