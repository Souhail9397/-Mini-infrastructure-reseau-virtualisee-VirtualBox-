<details><summary><h1>## 🧭 Création du routeur Linux<h1></summary>  

# :one: Téléchargement de l'ISO  
  
Se rendre sur le site officiel Debian https://www.debian.org/CD/netinst/ et télécharger l'image ISO version amd64  

![iso debian](https://github.com/user-attachments/assets/c31baee4-8c30-49aa-9079-7c8b6beb4d23)

Attendre que le téléchargement se termine avant de passer à la création de la VM sur VirtualBox.  

# :two: Sur VirtualBox  

## ⚙️ Création de la machine  
  
Créer une nouvelle VM avec 2Go de RAM, 10Go d'espace de stockage, passer le boot sur optique en prioritaire et insérer l'image ISO récemment téléchargée.  

![vm name](https://github.com/user-attachments/assets/a7bbe1a2-8bf5-4dca-8b65-1be1e28fab6a)  

![vm hardware](https://github.com/user-attachments/assets/51d8194f-59a2-4b18-a06f-495134c35716)  

![vm hard disk](https://github.com/user-attachments/assets/04e0df6d-dfc3-4bc6-bc1d-841c889afb0a)  

![ordre amorcage](https://github.com/user-attachments/assets/131ceb2e-d8aa-463b-87a6-4f9be4153345)  

![iso](https://github.com/user-attachments/assets/250822e4-dade-41df-a877-48186630425c)  

## 📦 Installation du serveur routeur Linux 

Lancer la VM puis suivre les étapes suivantes :  

➡️ **Debian GNU/Linux installer menu (BIOS mode)** : choisir `Install`  
  
➡️ **Select a language** : French  
  
➡️ **Choix de votre situation géographique** : France  
  
➡️ **Configurer le clavier** : Français  
  
➡️ **Nom de machine** : router  
  
➡️ **Domaine** : lan  
  
➡️ **Partitionner les disques** : `Assisté - utiliser un disque entier`  
  
➡️ **Disque à partitionner** : appuyer sur Entrée pour séléctionner le disque, un seul disque devrait être proposé  
  
➡️ **Schéma de partitionnement** :  `Tout dans une seule partition (recommandé pour les débutants)` puis `Termienr le partitionnement et appliquer les changements`  
  
➡️ **Faut-il appliquer les changements surt les disques?** : `Oui`  
  
➡️ **Faut-il analyser d'autres supports d'installation?** : `Non`  
  
➡️ **Pays du miroir de l'archive Debian** : `France` puis `deb.debian.org`  
  
➡️ **Mandataire HTTP** : laisser vide  
  
➡️ **Souhaitez-vous participer à l'étude statistique sur l'utilisation des paquets?** : `Non`  
  
➡️ **Séléction des logiciels**  
⚠️ Attention, cette étape est très importante.  
Il faut bien décocher les cases `environnement de bureau Debian` et `GNOME` car nous ne voulons pas d'interface bureau.  
Nous voulons seulement un routeur en CLI (ligne de commande).  
Donc bien décocher ces deux cases, puis `Continuer`.  
  
![env bureau gnome](https://github.com/user-attachments/assets/dfa3029e-9576-4477-b9a7-201b311c1e5e)  

➡️ **Installer le programme de démarrage GRUB sur le disque principal?** : `Oui`  
  
➡️ **Périphérique où sera installé le programme de démarrage** : `/deb/sda (ata-VBOX_HARDDISK_VBe4a7f8c9-2ac879e2)`  
  
L'installation est désormais terminée, redémarrer la machine pour pouvoir accéder au serveur.  
</details> 

  










