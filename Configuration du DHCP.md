<details><summary><h1>Configuration du DHCP<h1></summary>  

# :one: Installation du service DHCP  
  
🌐 **Nous allons avant toute chose configurer une adresse IP statique sur notre serveur Windows :**  

➡️ Faire un clic droit sur l'icône réseau en bas à droite de la barre des tâches puis cliquer sur `Ouvrir les paramètres réseau et Internet`  

➡️ Aller dans `Ethernet` puis cliquer sur `Modifier les options d'adaptateur`  

➡️ Faire un clic droit sur la carte réseau puis cliquer sur `Propriétés`  

➡️ Dans la liste affichée, cliquer sur `Protocole Internet version 4 (TCP/IPv4)` puis sur `Propriétés`  

➡️ Modifier les paramètres IP comme suit :  

![parametresipsrvwin](https://github.com/user-attachments/assets/9f032eee-5151-4215-ae60-1f90b7c91cc4)  
  
➡️ Ouvrir PowerShell et taper la commande `Restart-NetAdapter -Name "Ethernet"` pour redémarrer la carte réseau  

## ✅🔨 Une fois la configuration IP terminée, on passe à l'installation du DHCP 
  
Aller sur le Server Manager, cliquer sur Manage -> Add Roles and Features puis une fenêtre apparaît avec les étapes suivantes :  

➡️ **Avant de commencer** : cliquer sur `Suivant`  

➡️ **Sélectionner le type d'installation** : garder `Installation basée sur un rôle ou une fonctionnalité` coché, puis cliquer sur `Suivant`    
  
➡️ **Sélectionner le serveur de destination** : on séléctionne notre serveur qui est séléctionné par défaut puis on clique sur `Suivant`  

➡️ **Sélectionner des rôles de serveurs** : on séléctionne `Serveur DHCP`, puis on clique sur `Suivant`  

➡️ **Ajouter les fonctionnalités requises pour Serveur DHCP ?** : cliquer sur `Ajouter des fonctionnalités`  

➡️ **Sélectionner des fonctionnalités** : on laisse par défaut, puis `Suivant`  

➡️ **Serveur DHCP** : `Suivant`  

➡️ **Confirmation** : `Installer`  

### ⚠️ Éteindre le serveur et aller dans les paramètres VirtualBox, puis mettre le serveur en mode d'accès `Réseau interne` et sur la carte réseau `int_lan30`. Cela va permettre de "brancher" le serveur sur l'interface réseau du routeur interne dédiée au LAN 30.  

# :two: Création des plages d'adresses IP pour chaque LAN  

➡️ Cliquer sur `Outils` -> `DCHP`. Une fenêtre DHCP apparaît, on déroule la ligne portant le nom de notre server Windows, puis on déroule la ligne `IPv4`.  

➡️ On a 3 lignes supplémentaires qui apparaissent : `Options de serveur`, `Stratégies`, et `Filtres`  

## 🧩 LAN 10 

➡️ Faire un clique droit sur IPv4 et cliquer sur `Nouvelle étendue...`. Une fenêtre apparaît, cliquer sur `Suivant`  
   
Choisir un nom pour cette plage (LAN 10) et cliquer sur `Suivant`  

Nous allons à présent configurer l'étendue d'adresses IP pour le LAN 10. Cette opération sera répétée deux fois pour créer au total trois étendues pour nos trois LANs.  
  
Nous voilà sur la fenêtre qui va nous permettre de définir notre plage d'adresses IP.  
En face de `Adresse IP de début`, on rentre l'IP **192.168.10.1** et en face de `Adresse IP de fin`, on rentre l'IP **192.168.10.100**  
  
![plagevlan10](https://github.com/user-attachments/assets/38843f5d-8476-48ba-8aa2-9f6f9104ad34)

➡️ Cliquer sur `Suivant` jusqu'à arriver à **Routeur (passerelle par défaut)**  

➡️ Ajouter l'adresse IP de l'interface LAN 10 sur notre routeur interne : `192.168.10.254` -> `Ajouter` -> `Suivant`    
  
![dhcprouteurpasserelle](https://github.com/user-attachments/assets/326d95ee-bbbd-4a04-80f1-b85ae403309f)  

## 🧩 LAN 20  

![plagevlan20](https://github.com/user-attachments/assets/3c63f242-2d58-4511-b95a-2a9def37624d)  

![dchrouteurpasserellevlan20](https://github.com/user-attachments/assets/34dfbf79-bbe9-480b-a757-2ff1f38df4e9)  
  
## 🧩 LAN 30  
  
⚠️ **On ne crée PAS d'étendue pour le LAN 30 car tous les serveurs qui s'y trouveront auront une adresse IP fixe et non dynamique**   
  
</details>  

<details><summary><h1>Configuration d'un relais DHCP sur le routeur interne<h1></summary>    

## :warning: Avant de passer à cette étape, il faut bien avoir terminé toutes les configurations sur les deux routeurs ⚠️  
  
🧑‍🏫 **Rappel** 🧑‍🏫  

➡️ **Routeur interne** : 192.168.100.253  

➡️ **Interfaces LAN** : LAN 10 - LAN 20 - LAN 30  
  
➡️ Serveur DHCP : 192.168.30.1 (LAN 30)   

➡️ Utilisateurs : LAN 10 - LAN 20  

🎯 **Objectif** 🎯  

Les clients obtiennent une IP depuis 192.168.30.1 même s'ils sont dans un autre LAN.  

🚧 **Étapes à suivre** 🚧  

➡️ Taper la commande `ip a` pour avoir un aperçu de toutes les interfaces réseau    
  
![interfacesrouteurint](https://github.com/user-attachments/assets/f084c110-0d13-4fa6-a59b-c1e6fe44e7e0)  

➡️ **Installer le service DHCP relay** : `apt update` & `apt install isc-dhcp-relay`  

➡️ **Serveurs DHCP auxquels faire suivre les requêtes de relais DHCP** : `192.168.30.1`  

➡️ **Interface où le relais DHCP sera à l'écoute** : `enp0s8 enp0s9`  

➡️ **Options supplémentaires pour le démon de relais DHCP** : laisser vide, puis `Ok`  

➡️ **Vérifier la configuration du DHCP Relay** : taper `nano /etc/default/isc-dhcp-relay`. Nous devons avoir la configuration suivante :  

![iscdhcprelay](https://github.com/user-attachments/assets/7db33299-457e-43ac-ad26-549637970284)  

📌 *La ligne "INTERFACES" ne comporte que "enp0s8 enp0s9" car ce sont les deux LAN qui demanderont des adresses IP au serveur DHCP. Les machines du LAN 30 (serveurs) auront des IP fixes*  

➡️ **Quitter le fichier avec `Ctrl + X`  

➡️ **Redémarrer le service DHCP Relay** : `systemctl restart isc-dhcp-relay`  

➡️ **Vérifier le statut du DHCP Relay** : `systemctl status isc-dhcp-relay`. Le statut du DHCP Relay doit être en **"active (running)"**  

![iscstatus](https://github.com/user-attachments/assets/1415da06-3d23-456f-a1f6-b6b4095f2492)  

➡️ **Création de règles iptables pour autoriser le DHCP** : `iptables -A INPUT -p udp --dport 67:68 -j ACCEPT` puis `iptables -A OUTPUT -p udp --dport 67:68 -j ACCEPT`  

➡️ **Sauvegarder les règles** : télécharger le paquet `apt install iptables-persistent`  

➡️ **Faut-il enregistrer les règles IPv4 actuelles ?** : `Oui`  

➡️ **Faut-il enregistrer les règles IPv6 actuelles ?** : `Oui`    

  
  
  

  
  
</details>    
