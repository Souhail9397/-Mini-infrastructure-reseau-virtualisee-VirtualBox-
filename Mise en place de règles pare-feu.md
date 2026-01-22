### La mise en place de règles pare-feu est une étape primordiale pour améliorer la sécurité de notre infrastructure. Ces règles vont nous permettre de décider quel trafic inter-LAN sera autorisé, et lequel sera bloqué. Nous limitons le trafic inter-LAN pour qu'en cas d'attaque malveillante sur notre infrastructure, l'attaquant ne puisse pas aller plus loin que le LAN sur lequel le poste compromis se trouve.  
___

# :one: Test des communications avant les règles pare-feu  
  
➡️ LAN 10 (Users) vers LAN 20 (Admin) : ✅  
  
![lan10verslan20](https://github.com/user-attachments/assets/697e3b17-91d1-4d84-b280-ec226f95814e)
  
➡️ LAN 10 (Users) vers LAN 30 (Servers) : ✅  
  
![lan1020verslan30](https://github.com/user-attachments/assets/5b3fd75c-b185-479b-a66e-378d5252f05f)
  
➡️ LAN 20 (Admin) vers LAN 10 (Users) : ✅  
  
![lan20verslan10](https://github.com/user-attachments/assets/28f82a66-eef6-4cc2-9cc2-3fab399dcb37)
  
➡️ LAN 20 (Admin) vers LAN 30 (Servers) : ✅  
  
![lan1020verslan30](https://github.com/user-attachments/assets/ac4675cb-e9c4-4c94-a32d-c74112f4bed2)
  
➡️ LAN 30 (Servers) vers LAN 10 (Users) : ✅  
  
![lan30verslan10](https://github.com/user-attachments/assets/92eac10a-043f-46ce-9f15-4227828a34fd)
  
➡️ LAN 30 (Servers) vers LAN 20 (Admin) : ✅  
  
![lan30verslan20](https://github.com/user-attachments/assets/092de83b-a2eb-47de-a3e3-71aa771c7b25)  

➡️ Avec l'état actuel de notre infra, tous les LANs peuvent communiquer entre eux. Nous allons maintenant remédier à ça.  

# :two: Création des règles pare-feu avec iptables (Routeur INTERNE)  

Voici un tableau le trafic autorisé que nous voulons avoir sur notre infrastructure :  

![Tableauregles](https://github.com/user-attachments/assets/56454b81-e145-4470-aba0-bb906c89ac0b)  

➡️ **Définir la politique par défaut en "DROP"** : `iptables -P FORWARD DROP` ➡️ Désormais, tous les flux sont automatiquement bloqués. Les règles suivantes vont permettent de bloquer explicitement certains flux et en autoriser d'autres.  

➡️ **Toujours autoriser les réponses aux connexions existantes** : `iptables -I FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT`  
  
➡️ **Bloquer explicitement LAN 10 vers LAN 20** : `iptables -A FORWARD -s 192.168.10.0/24 -d 192.168.20.0/24 -j DROP`  

➡️ **Bloquer explicitement LAN 10 vers LAN 30** : `iptables -A FORWARD -s 192.168.10.0/24 -d 192.168.30.0/24 -j DROP`  
  
➡️ **Bloquer explicitement LAN 30 vers LAN 10** : `iptables -A FORWARD -s 192.168.30.0/24 -d 192.168.10.0/24 -j DROP`  
  
➡️ **Bloquer explicitement LAN 30 vers LAN 20** : `iptables -A FORWARD -s 192.168.30.0/24 -d 192.168.20.0/24 -j DROP`  

➡️ **Autoriser LAN 20 vers LAN 10** : `iptables -A FORWARD -s 192.168.20.0/24 -d 192.168.10.0/24 -j ACCEPT`  
  
➡️ **Autoriser LAN 20 vers LAN 10** : `iptables -A FORWARD -s 192.168.20.0/24 -d 192.168.10.0/24 -j ACCEPT`   

➡️ **Autoriser accès Internet à chaque les LANs** :  
`iptables -A FORWARD -s 192.168.10.0/24 -d 0.0.0.0/0 -j ACCEPT`  
`iptables -A FORWARD -s 192.168.20.0/24 -d 0.0.0.0/0 -j ACCEPT`  
`iptables -A FORWARD -s 192.168.30.0/24 -d 0.0.0.0/0 -j ACCEPT`  

### 📊 Résultat :  
- LAN 10 vers LAN 20 : Non  
- LAN 10 vers LAN 30 : Non  
- LAN 30 vers LAN 10 : Non  
- LAN 30 vers LAN 20 : Non  
- LAN 20 vers LAN 10 : Oui  
- LAN 20 vers LAN 30 : Oui  
- LAN 10 vers Internet : Oui  
- LAN 20 vers Internet : Oui  
- LAN 30 vers Internet : Oui

### 🗂️ Vue de la liste FORWARD  

➡️ Taper la commande `iptables -L FORWARD --line-numbers -n`  

![listeforward](https://github.com/user-attachments/assets/d280402e-6850-4ae2-9f01-4599ea30ad4e)
  
  

  
