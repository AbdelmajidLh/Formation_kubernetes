# Kubernetes en bref

- **Kubernetes** est un **orchestrateur** de conteneurs : il planifie, lance, surveille et redemarre les conteneurs.
- C'est le **concurrent de Docker Swarm** : meme objectif (orchestrer des conteneurs), mais plus complet, plus utilise et plus extensible.
- Il apporte une **abstraction de l'infrastructure** : vous declarez l'etat souhaite (combien d'instances, quelles ressources, quel reseau) et Kubernetes se charge de le realiser sur vos machines.
- **Portabilite** : les memes manifestes fonctionnent en local, sur serveur physique, VM ou cloud (public/prive).
- **Resilience** : il remplace automatiquement les conteneurs en panne et repartit la charge.
- **Scalabilite** : il ajoute ou retire des replicas selon la demande.

## Vocabulaire de base
- **Cluster** : ensemble de machines (noeuds) controlees par Kubernetes.
- **Noeud (Node)** : une machine du cluster (physique ou VM) qui execute les conteneurs.
- **Pod** : plus petite unite deployable, contient un ou plusieurs conteneurs qui partagent reseau et stockage.
- **Service** : point d'acces stable pour atteindre des Pods, meme si les Pods changent.
- **Namespace** : cloison logique pour separer des applications ou des equipes.
- **Manifestes YAML** : fichiers declaratifs qui decrivent l'etat desire (deploiement, service, volumes, etc.).

## Ce que Kubernetes n'est pas
- Ce n'est pas un outil de build d'image (on utilise toujours Docker/Buildah/Podman pour construire l'image).
- Ce n'est pas un PaaS cle en main : il fournit les briques, a vous (ou votre plateforme) de les combiner.
