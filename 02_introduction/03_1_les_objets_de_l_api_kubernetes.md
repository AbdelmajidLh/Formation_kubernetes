# Les objets de l'API Kubernetes

## Pod
Plus petite brique d'un cluster. Un Pod est declare dans un manifest YAML puis planifie sur un noeud si les ressources sont libres. Il est ephemere: on ne le "re-deploie" pas, on le remplace. Atomicite: un Pod est la ou pas la; si l'un de ses conteneurs meurt, le Pod est considere en echec et un nouveau Pod prend le relais. Exemple data: un Pod `python:3.11` qui lit un CSV S3 et l'envoie dans PostgreSQL, avec un conteneur a cote qui expedie les logs.

## Controleurs (ils maintiennent l'etat souhaite)
Un controleur est un objet d'API qui decrit l'etat souhaite (nombre de Pods, version d'image) et surveille en continu l'etat reel. Si un Pod tombe ou qu'une mise a jour est demandee, le controleur agit pour revenir a l'etat voulu.

- **ReplicaSet** : assure qu'il y a toujours N Pods vivants. Exemple: garder 3 Pods en marche en permanence; si un Pod meurt, un autre est cree.
- **Deployment** : utilise des ReplicaSets pour gerer des apps stateless et les mises a jour. Exemple: passer de `v1` a `v2` d'une API FastAPI sans coupure via un rolling update.
- **StatefulSet** : identite stable + volumes attaches. Exemple: Kafka ou Timescale avec des noms fixes (`pod-0`, `pod-1`) et stockage persistant.
- **DaemonSet** : un Pod par noeud. Exemple: un agent Filebeat/Fluent Bit qui collecte les logs sur chaque machine.
- **Job / CronJob** : taches uniques ou planifiees. Exemple: un batch Spark qui recalcule un KPI, ou un CronJob qui importe un CSV chaque nuit.

## Services (exposition reseau)
Dans un monde de Pods ephemeres, le Service apporte de la persistance: il donne une IP et un nom DNS stables pour atteindre vos Pods, meme quand ils meurent et renaissent. C'est l'abstraction reseau pour dialoguer avec les apps (ex: un WordPress qui parle a sa base via un Service).
- **ClusterIP** : interne cluster. Exemple: exposer `spark-driver` pour les executors.
- **NodePort** : ouvre un port sur chaque noeud (tests rapides).
- **LoadBalancer** : load balancer externe pour exposer une API publique (ex: FastAPI d'analytics).

En coulisses, Kubernetes met a jour dynamiquement le routage selon le cycle de vie des Pods: l'IP du Service reste, le trafic est renvoye uniquement vers les Pods sains.

## Ingress
Regles HTTP/HTTPS (routes, hostnames) portees par un Ingress Controller (nginx, traefik). Exemple: `/metrics` vers Prometheus, `/ml` vers un service de model serving.

## ConfigMap et Secret
- **ConfigMap** : config non sensible. Exemple: nom de bucket, topic Kafka, fichier `spark-defaults.conf`.
- **Secret** : info sensible. Exemple: mot de passe PostgreSQL, token S3/MinIO, cle API de data warehouse.

## Stockage (Volumes et Claims)
- **PersistentVolume (PV)** : un disque fourni au cluster (NFS, CSI, cloud...).
- **PersistentVolumeClaim (PVC)** : une demande de disque (taille, mode). Monte dans les Pods pour conserver les donnees. Exemple: PVC pour `spark-history-server` ou pour un Postgres embarque.

## Namespace
Un dossier logique pour separer equipes/environnements. Exemple: `data-eng` pour pipelines Spark/Python, `bi` pour APIs de restitution.
