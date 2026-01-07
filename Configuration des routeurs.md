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
