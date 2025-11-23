# Stockage dans Kubernetes

Au debut, on peut attacher un volume directement a chaque Pod. Mais si le Pod est remplace (normal dans Kubernetes), le volume disparait avec lui: c'est peu flexible pour garder des donnees.

Pour decoller cette dependance, Kubernetes introduit le **Persistent Volume (PV)** : un stockage defini et gere par l'administrateur au niveau du cluster, independant des Pods.

Quand une appli a besoin de stockage, elle fait une **demande de volume persistant** (**Persistent Volume Claim - PVC**) dans son manifest YAML. Exemple: "donne-moi 10 Go de ce type de stockage". Kubernetes va lier ce PVC a un PV disponible pour que le Pod puisse monter ce volume, meme s'il est recree ailleurs.
