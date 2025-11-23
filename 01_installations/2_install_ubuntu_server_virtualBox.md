# Installation Ubuntu Server (ISO offline) dans VirtualBox

## 1. Telecharger l'ISO offline
- Aller sur https://ubuntu.com/download/server
- Choisir **Ubuntu Server 22.04.4 LTS** (64-bit) puis cliquer sur **Download** (ISO ~1.6 Go).
- Enregistrer l'ISO sur le disque local ou une cle USB.

> Warning : noter soigneusement pendant l'installation vos identifiants (username, password) ainsi que le host name et le domain name choisis.

## 2. Creer et parametrer la VM VirtualBox
1) Nouvelle VM :
- Nom : Ubuntu-Server
- Type : Linux, Version : Ubuntu (64-bit)
- Memoire : 2 Go min (4 Go recommande)
- Processeurs : 2 vCPU min (activer PAE/NX)
- Disque : VDI dynamique, 20-40 Go

2) Reglages :
- Systeme : activer EFI si vous souhaitez GPT/UEFI.
- Affichage : Video minimale (pas d'interface graphique).
- Stockage :
  - Controleur IDE/SATA : attacher **l'ISO Ubuntu Server** comme disque optique.
  - Disque virtuel cree precedemment comme disque principal.
- Reseau : NAT par defaut (Pont possible pour acces LAN direct).

## 3. Installer Ubuntu Server
1) Demarrer la VM et choisir **Try or Install Ubuntu Server**.
2) Langue/Clavier : choisir Francais si souhaite.
3) Reseau : garder DHCP (NAT) ou configurer statique si besoin.
4) Stockage : partitionnement guide utilise tout le disque (par defaut LVM + swap). Laisser par defaut sauf besoin specifique.
5) Profil utilisateur : definir nom d'utilisateur, nom de machine et mot de passe.
6) OpenSSH : cocher l'installation du serveur SSH pour l'administration a distance.
7) Paquets supplementaires : selectionner les roles optionnels si necessaire (ex : Docker, PostgreSQL).
8) Lancer l'installation, puis redemarrer; retirer l'ISO avant le reboot.

## 4. Post-installation rapide
- Mettre a jour :
```bash
sudo apt update
sudo apt upgrade -y
```
- Si SSH active : copier votre cle publique pour l'acces sans mot de passe :
```bash
mkdir -p ~/.ssh
echo \"collez_votre_cle_publique_ici\" >> ~/.ssh/authorized_keys
chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys
```
- Installer les Additions invite VirtualBox (utile pour synchroniser l'heure et monter les dossiers partages) :
```bash
sudo apt install -y build-essential dkms linux-headers-$(uname -r)
sudo /media/$USER/VBox_GAs*/VBoxLinuxAdditions.run
```
- Redemarrer la VM.

## 5. Conseils
- Garder l'ISO pour reinstallation sans Internet.
- Prendre un snapshot apres configuration reseau/SSH et mises a jour.
- Pour des services exposes, utiliser le mode reseau Pont ou une regle NAT port-forward.
