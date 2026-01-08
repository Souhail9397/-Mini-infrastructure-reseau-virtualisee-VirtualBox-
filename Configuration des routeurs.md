<details><summary><h1>Routeur Interne<h1></summary>  

# :one: Modifications partie réseau sur VirtualBox  

Ouvrir VirtualBox et aller dans les paramètres du routeur interne.  

Par défaut, VirtualBox n'active qu'une interface réseau, qui correspond aux onglets `Adapter 1-2-3-4`. Sur ce routeur, nous allons activer toutes les interfaces réseau :  

• `Adapter 1` | **Mode d'accès** : `Réseau interne` | **Name** : `int_transit` : cette interface sera connectée au Routeur Externe   

• `Adapter 2` | **Mode d'accès** : `Réseau interne` | **Name** : `int_vlan10` : cette interface sera connectée au VLAN 10 (Utilisateurs)    

• `Adapter 3` | **Mode d'accès** : `Réseau interne` | **Name** : `int_vlan20` : cette interface sera connectée au VLAN 20 (Utilisateurs)   

• `Adapter 4` | **Mode d'accès** : `Réseau interne` | **Name** : `int_vlan30` : cette interface sera connectée au VLAN 30 (Salle des serveurs)   

✅ Notre routeur est maintenant prêt à recevoir les modifications nécessaires pour la connection inter VLANs  

# :two: Attribution des adresses IP  

Démarrer le routeur, se connecter en root et taper la commande `ip a`. Cette commande va afficher toutes les interfaces réseau que nous avons activées sur VirtualBox :  
  
![iparouteurinterne](https://github.com/user-attachments/assets/4c4813c9-5d67-4689-a162-e93cd5076b6a)  

*On va maintenant procéder à l'attribution des adresses IP*  

➡️ Taper la commande `nano /etc/network/interfaces` : nous sommes dans le fichier de configuration des interfaces réseau  
  
![etcnetworkinterfaces](https://github.com/user-attachments/assets/3645eb76-af24-4847-81af-bff227b25e54)

➡️ Le fichier ne dispose que d'une interface réseau, intitulée "iface enp0s3". Dans la capture d'écran du `ip a`, on a 3 autres interfaces : **enp0s8**, **enp0s9** et **enp0s10**  

➡️ Notre objectif va être de répliquer la section "The primary network interface" pour les 3 interfaces que nous avons activées sur VirtualBox.  

➡️ Pour avoir une base correcte, nous allons effacer les lignes encadrées en rouge car nous n'allons pas implémenter d'IPv6 :  
  
![lignesasupprimer](https://github.com/user-attachments/assets/f287af81-1a4c-48cb-9c29-3354f4890c7c)  

➡️ Modifier le fichier pour avoir cette configuration exacte :  

![configfinalerouteurinterne](https://github.com/user-attachments/assets/ad3b5b01-0b1e-4426-b0a0-9a5cadffb1f5)  

➡️ Appuyer sur **Ctrl + X** pour quitter, et répondre à la question **Sauver l'espace modifié ?** par `O` 
  
</details>   

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

### ⚠️ Éteindre le serveur et aller dans les paramètres VirtualBox, puis mettre le serveur en mode d'accès `Réseau interne` et sur la carte réseau `int_vlan30`. Cela va permettre de "brancher" le serveur sur l'interface réseau du routeur interne dédiée au VLAN 30.  

# :two: Création des plages d'adresses IP pour chaque VLAN  

➡️ Cliquer sur `Outils` -> `DCHP`. Une fenêtre DHCP apparaît, on déroule la ligne portant le nom de notre server Windows, puis on déroule la ligne `IPv4`.  

➡️ On a 3 lignes supplémentaires qui apparaissent : `Options de serveur`, `Stratégies`, et `Filtres`  

## 🧩 VLAN 10 

➡️ Faire un clique droit sur IPv4 et cliquer sur `Nouvelle étendue...`. Une fenêtre apparaît, cliquer sur `Suivant`  
   
Choisir un nom pour cette plage (VLAN 10) et cliquer sur `Suivant`  

Nous allons à présent configurer l'étendue d'adresses IP pour le VLAN 10. Cette opération sera répétée deux fois pour créer au total trois étendues pour nos trois VLANs.  
  
Nous voilà sur la fenêtre qui va nous permettre de définir notre plage d'adresses IP.  
En face de `Adresse IP de début`, on rentre l'IP **192.168.10.1** et en face de `Adresse IP de fin`, on rentre l'IP **192.168.10.100**  
  
![plagevlan10](https://github.com/user-attachments/assets/38843f5d-8476-48ba-8aa2-9f6f9104ad34)

➡️ Cliquer sur `Suivant` jusqu'à arriver à **Routeur (passerelle par défaut)**  

➡️ Ajouter l'adresse IP de l'interface VLAN 10 sur notre routeur interne : `192.168.10.254` -> `Ajouter` -> `Suivant`    
  
![dhcprouteurpasserelle](https://github.com/user-attachments/assets/326d95ee-bbbd-4a04-80f1-b85ae403309f)  

## 🧩 VLAN 20  

![plagevlan20](https://github.com/user-attachments/assets/3c63f242-2d58-4511-b95a-2a9def37624d)  

![dchrouteurpasserellevlan20](https://github.com/user-attachments/assets/34dfbf79-bbe9-480b-a757-2ff1f38df4e9)  
  
## 🧩 VLAN 30  

![plagevlan30](https://github.com/user-attachments/assets/ec5ac325-2824-471a-99c9-2e1eb9a9463e)  

![dhcprouteurpasserellevlan30](https://github.com/user-attachments/assets/a036b463-b778-42f4-926f-e970884ab4cf)



  

</details> 
