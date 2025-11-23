# Principes de fonctionnement de Kubernetes

- Etat desire / configuration declarative : vous decrivez l'etat cible (deployments, services, volumes) dans des manifestes YAML; Kubernetes s'occupe d'atteindre et de maintenir cet etat.
- API Kubernetes / API Server : toutes les actions passent par l'API Server (lecture/ecriture). kubectl, les CI/CD et les autres composants parlent a cette API pour declarer ou lire l'etat.
- Controleurs et boucle de controle : des controlleurs surveillent en continu l'etat actuel vs l'etat desire, et agissent pour combler l'ecart (creer des pods, remplacer ceux en panne, mettre a jour les replicas).
- Store et verite de reference : etcd stocke l'etat du cluster (ressources et configs). L'API Server y lit/ecrit pour servir de source de verite.
- Reconcilier, pas executer une fois : si quelqu'un supprime un pod attendu, le controleur le recree; si un noeud tombe, les pods sont redeployes ailleurs (self-healing).
