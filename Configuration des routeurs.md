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
  
![configfinalerouteurinterne](https://github.com/user-attachments/assets/100900fb-10cd-4151-8f55-0872f8e1f147)  

➡️ Appuyer sur **Ctrl + X** pour quitter, et répondre à la question **Sauver l'espace modifié ?** par `O` 
  
</details>   

<details><summary><h1>Routeur Externe<h1></summary>  

# :one: Configurations réseau sur VirtualBox  

Aller dans les paramètres réseau du routeur externe et mettre une interface réseau en `NAT` et l'autre interface réseau en `Réseau interne` sur `int_transit`.  
Nous nous retrouvons donc au total avec **deux** interfaces réseau sur ce routeur :  
  
• **Adapter 1** | `Réseau interne` | `int_transit`  

• **Adapter 2** | `NAT`  


# 2️⃣ Attribution de l'adresse IP      

➡️ Taper `nano /etc/network/interfaces` pour attribuer son adresse IP (192.168.100.254) à l'interface en **Réseau interne** du routeur  
  
➡️ L'interface en **NAT** sera elle configurée en DHCP  
  
![configreseaurtrextern](https://github.com/user-attachments/assets/173e6765-98ab-4ee8-aac8-660a83457fe9)  
  
➡️ Quitter en sauvegardant avec `Ctrl + x` et `o` pour confirmer les modifications  

➡️ Redémarrer les interfaces réseau avec la commande `systemctl restart networking`  

➡️ Vérifier que le routeur a bien pris en compte les modifications apportées avec `ip a`  

⚠️ Le message d'erreur suivant est susceptible d'apparaître après la commande **systemctl restart networking** :  
`job for networking.service failed because the control process exited with error code.  
See "systemctl status networking.service" and "journalctl -xeu networking.service" for details.`  

Dans ce cas, taper la commande `ip link set enp0s3 up` puis retaper la commande `systemctl restart networking`  

➡️ La commande `ip a` devrait alors donner ceci :  
  
![iparouteurexterne2](https://github.com/user-attachments/assets/191c6a06-8d6d-42dc-b74a-f1a35b6c48a0)  

# :three: Mise en place du NAT  

*Nous allons maintenant mettre en place le NAT sur le routeur externe afin que toutes les machines du réseau puissent avoir un accès à Internet en utilisant l'IP publique du routeur externe*   
  
  
  

  
  
</details>  
