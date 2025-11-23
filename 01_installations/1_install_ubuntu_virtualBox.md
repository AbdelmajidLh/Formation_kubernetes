# Installation Ubuntu Desktop (ISO offline) dans VirtualBox

## 1. Telecharger l'ISO offline
- Aller sur https://ubuntu.com/download/desktop
- Choisir **Ubuntu 22.04.4 LTS** (64-bit) puis cliquer sur **Download** (ISO ~4.5 Go).
- Enregistrer l'ISO sur le disque local ou une cle USB.

## 2. Creer et parametrer la VM VirtualBox
1) Nouvelle VM :
- Nom : Ubuntu-Desktop
- Type : Linux, Version : Ubuntu (64-bit)
- Memoire : 4 Go min (8 Go recommande)
- Processeurs : 2 vCPU min (activer PAE/NX)
- Disque : VDI dynamique, 40-60 Go

2) Reglages :
- Systeme : activer EFI si vous souhaitez GPT/UEFI.
- Affichage : 128 Mo video, activer l'acceleration 3D si supportee.
- Stockage :
  - Controleur IDE/SATA : attacher **l'ISO Ubuntu** comme disque optique.
  - Disque virtuel cree precedemment comme disque principal.
- Reseau : NAT par defaut (Pont possible pour acces LAN direct).

## 3. Installer Ubuntu
1) Demarrer la VM, booter sur l'ISO, choisir **Try or Install Ubuntu** puis **Install Ubuntu**.
2) Langue/Clavier : choisir Francais si souhaite.
3) Connexion : la configuration offline suffit pour installer depuis l'ISO.
4) Type d'installation : **Installation normale** (recommande) ou minimale selon besoin.
5) Partitionnement : laisser le partitionnement automatique (ext4 + swap) sauf besoin specifique.
6) Utilisateur : definir nom d'utilisateur et mot de passe.
7) Lancer l'installation puis redemarrer; retirer l'ISO du lecteur virtuel avant le reboot.

## 4. Post-installation rapide
- Mettre a jour :
```bash
sudo apt update
sudo apt upgrade -y
```
- Installer les Additions invite VirtualBox : dans VirtualBox, **Peripheriques > Inserer l'image CD des Additions Invite** puis dans la VM :
```bash
sudo apt install -y build-essential dkms linux-headers-$(uname -r)
sudo /media/$USER/VBox_GAs*/VBoxLinuxAdditions.run
```
- Redemarrer la VM pour activer l'integration (resolution dynamique, presse-papiers partage).

## 5. Conseils
- Garder l'ISO pour reinstallation sans Internet.
- Prendre un snapshot apres mise a jour initiale.
- Pour de meilleures performances reseau, passer le mode reseau en Pont si besoin.
