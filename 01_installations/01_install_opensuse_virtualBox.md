# Installation openSUSE Leap 16.0 (ISO offline) dans VirtualBox

## 1. Telecharger l'ISO offline
- Ouvrir : https://get.opensuse.org/leap/16.0/?type=desktop#download
- Dans la section **Offline Image**, choisir l'architecture **x86_64** puis cliquer sur **Download** (ISO ~4 Go).
- Conserver l'ISO sur un disque local ou une cle USB.

## 2. Preparer la VM VirtualBox
1) Creer une nouvelle VM :
- Nom : openSUSE-Leap-16
- Type : Linux, Version : openSUSE (64-bit)
- Memoire : 4 Go min (8 Go recommande)
- Processeurs : 2 vCPU min (activer PAE/NX)
- Disque dur : VDI dynamique, 40-60 Go

2) Parametrer la VM :
- Systeme : activer EFI si vous voulez GPT/UEFI.
- Affichage : 128 Mo de memoire video, activer l'acceleration 3D si supportee.
- Stockage :
  - Controleur IDE/SATA : ajouter **l'ISO telechargee** comme disque optique.
  - Disque virtuel cree precedemment comme disque principal.
- Reseau : NAT (par defaut) suffit pour debuter.

## 3. Installer openSUSE Leap
1) Demarrer la VM, booter sur l'ISO, choisir **Installation**.
2) Langue/Clavier : Francais si souhaite.
3) Partitionnement (recommande) : laisser l'option proposee (Btrfs + Swap). Si EFI active, une partition EFI sera creee.
4) Utilisateur : creer un utilisateur et definir un mot de passe root si necessaire.
5) Resume : verifier reseau, heure, paquetages; puis lancer l'installation.
6) Redemarrer : retirer l'ISO du lecteur virtuel (Peripheriques > Lecteurs optiques > Retirer le disque) puis redemarrer sur le disque virtuel.

## 4. Post-installation rapide
- Mettre a jour :
```bash
sudo zypper refresh
sudo zypper update
```
- Installer VirtualBox Guest Additions : dans VirtualBox, **Peripheriques > Inserer l'image CD des Additions invite** puis dans la VM :
```bash
sudo zypper install make gcc kernel-default-devel
sudo /run/media/$USER/VBox_GAs*/VBoxLinuxAdditions.run
```
- Redemarrer la VM pour activer l'integration (resolution dynamique, presse-papiers partage).

## 5. Conseils
- Conserver l'ISO offline pour reinstaller sans Internet.
- Sauvegarder un snapshot VirtualBox juste apres installation et mises a jour.
- Pour un usage serveur, preferer un controleur reseau en mode Pont pour un acces direct au LAN.
