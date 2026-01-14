<details><summary><h1>🧭 Création des routeurs Linux<h1></summary>  

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

➡️ **Nous serons amenés à répéter cette création de VM Linux une deuxième fois afin d'avoir un routeur permettant le routage inter-LANs et un routeur permattant un accès à l'extérieur (Internet)**  
</details> 


<details><summary><h1>🖥️ Création des machines client Windows10<h1></summary> 

# :one: Téléchargement de l'ISO  

Se rendre sur le site officiel de Windows pour télécharger l'image ISO : https://www.microsoft.com/fr-fr/software-download/windows10   

Suivre les étapes suivantes :  
  
![isowin10](https://github.com/user-attachments/assets/2cdc9d33-5046-4af0-b05e-47a1f9472187)  
  
![mediacreationtoolwin10](https://github.com/user-attachments/assets/369d3c1e-5ac6-4fe2-a737-6c691bcc330e)  

Lancer l'outil d'installation lorsque le téléchargement est terminé.  

➡️ Accepter les conditions du contrat de licence.  

➡️ **Que voulez vous faire?** : `Crée un support d'installation (Clé USB, DVD ou fichier ISO) pour un autre PC`  

➡️ **Sélectionner la langue, l'architecture et l'édition** : laisser par défaut, puis `suivant`  

➡️ **Choisir le média à utiliser** : `Fichier ISO`  
  
Attendre que le téléchargement de l'ISO soit complété.  
  
![telechargementisowin](https://github.com/user-attachments/assets/7a395748-31bd-4ea9-9bfd-114b13caaa18)  

# :two: Sur VirtualBox  

## ⚙️ Création de la machine  

Nous allons créer une machine client légère. 

Créer une nouvelle VM, configurer 2Go de RAM et 20Go d'espace de stockage. Dans l'ordre d'amorçage, choisir **Optique** en 1ère position, suivi de **Disque dur** et décocher **Disquette**. Insérer ensuite l'image ISO dans le contrôleur SATA :  
![isowinsata](https://github.com/user-attachments/assets/52cb4886-bbf4-4d08-8842-d84f7b43d63c)  

## 📦 Installation de Windows10

➡️ **Langue à installer** : `Français`  
  
➡️ **Format horaire et monétaire** : `Français (France)`  
  
➡️ **Clavier ou méthode d'entrée** : `Français`  

➡️ Ensuite, cliquer sur `Ìnstaller maintenant`  

➡️ **Activer Windows** : Cliquer sur `Je n'ai pas de clé de produit (Product Key)`  

➡️ **Sélectionner le système d'exploitation à installer** : Choisir `Windows10 Professionnel`  

➡️ **Quel type d'installation voulez-vous effectuer?** : `Personnalisé : installer uniquement windows (avancé)`  

➡️ Choisir le disque dur sur lequel installer Windows. Un seul disque dur devrait être proposé (le disque dur de 20Go configuré lors de la création de la VM).  

Maintenant, les configurations finales vont avoir lieu.  

💡 **Conseil** : une série de propositions sera proposée par Windows. Choisir l'option `Ignorer`, `Passer` ou `Pas maintenant` au maximum afin de vite terminer la configuration de base.  
  
Après avoir terminé ces configurations, la VM sera prête à l'utilisation ✅  

</details>     

<details><summary><h1>🌐 Création du serveur Windows DHCP et DNS<h1></summary>  

 # :one: Téléchargement de l'ISO  
   
➡️ Aller sur le site officiel de Windows pour se procurer l'image ISO de Windows Server https://www.microsoft.com/fr-fr/evalcenter/evaluate-windows-server-2022  

➡️ Cliquer sur `Télécharger ce fichier ISO` et attendre que le téléchargement de l'ISO se termine.  

# :two: Sur VirtualBox  

➡️ Créer une nouvelle VM : 25Go d'espace de stockage et 2Go de RAM. Dans l'ordre d'amorçage, choisir **Optique** en 1ère position, suivi de **Disque dur** et décocher **Disquette**. Insérer ensuite l'image ISO dans le contrôleur SATA.    

**Démarrer la VM et suivre les étapes** :  

➡️ **Langue à installer** : `Français`  

➡️ **Fromat horaire et monétaire** : `Français (France)`  

➡️ **Clavier ou méthode d'entrée** : `Français`  

➡️ Cliquer sur `Installer maintenant`  

➡️ **Sélectionner le système d'exploitation à installer** : `Windows Server 2022 Standard Evaluation (expérience de bureau)`  

➡️ **Quel type d'installation voulez-vous effectuer ?** : `Personnalisé : installer uniquement le système d'exploitation Microsoft Server (avancé)`  

➡️ Attendre que l'installation se termine. Le serveur va ensuite redémarrer  

➡️ Choisir un mot de passe pour la session **Administrateur**  

## ✅ Installation complétée ✅

</details>   




  









