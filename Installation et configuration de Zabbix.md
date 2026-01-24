### 🔍 **Zabbix** est un outil qui permet de surveiller en temps réel l'état et les performances d'une infrastructure. Il permet entre autres d'alerter automatiquement lorsque quelque chose sur l'infrastructure ne fonctionne pas correctement.  

# :one: Création de la VM  

➡️ Créer une nouvelle VM avec 2Go de RAM, 20Go d'espace de stockage, passer le boot sur optique en prioritaire et insérer l'image ISO Debian.  

➡️ **Carte réseau** : `Réseau interne` | `int_lan30`  

➡️ Suivre les étapes listées dans `Création des VMs.md` pour l'installation  

# :two: Configurations IP  

➡️ **Ouvrir le fichier de configuration des interfaces réseau** : `nano /etc/network/interfaces`  

➡️ **Passer l'interface enp0s3 en static au lieu de dhcp et ajouter les lignes suivantes** : `address 192.168.30.2/24` `gateway 192.168.30.254`  

![configipzabbix](https://github.com/user-attachments/assets/06fd10dc-642d-4190-82e2-0fd649b871e6)
  
➡️ **Quitter et sauvegarder** : `Alt + X` `o`  
  
➡️ **Redémarrer le service networking** : `systemctl restart networking.service`  

➡️ **Vérifier que les modifications ont bien été prises en compte** : `ip a`  
  
![ipazabbix](https://github.com/user-attachments/assets/3b5e5401-04e1-4b15-abe1-99a3e0677509)  

# :three: Attribution d'un DNS  

➡️ **Configurer un DNS dans le fichier de configuration** : `nano /etc/resolv.conf` et ajouter la ligne `nameserver 8.8.8.8`   
➡️ **Quitter et sauvegarder** : `Alt + X` `o`    

➡️ **Redémarrer le serveur** : `init 6`  
  
# 4️⃣ Installation de Zabbix  

➡️ **Télécharger le paquet Zabbix** : `wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian12_all.deb`  
  
➡️ **Installer le paquet Zabbix** : `dpkg -i zabbix-release_6.4-1+debian12_all.deb`  

➡️ **Mettre à jour la liste des paquets** : `apt update`  

➡️  **Installation de tous les modules nécessaires** :
`apt install -y zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-agent zabbix-sql-scripts mariadb-server`  
  
### 🗄️ Configuration de la base de données MySQL    
  
➡️  **Démarrer le client MySQL** : `mysql`  

➡️  **Créer la base Zabbix** : `CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;`  

➡️ **Créer un utilisateur dans MySQL** : `CREATE USER 'zabbix'@'localhost' IDENTIFIED BY 'MotDePasseSolide';`  

➡️ **Donner tous les droits à l'utilisateur Admin** : `GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';`  

➡️ **Sauvegarder les privilèges** : `FLUSH PRIVILEGES;`  

➡️ **Quitter MySQL** : `quit`    
   
➡️ **Importer le schéma initial de Zabbix** : `zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql -u zabbix -p zabbix`, un prompt apparaîtra et demandera d'entrer le mot de passe de l'utilisateur crée. Attendre environ 10 secondes.     
  
➡️ **Configurer Zabbix server** : `nano /etc/zabbix/zabbix_server.conf` :  
- Vérifier que le fichier contient bien les lignes `DBName=zabbix` et `DBUser=zabbix`  
- Sous `DBUser=zabbix`, il y a une ligne `#DBPassword` : décommenter la ligne (= supprimer le #) et ajouter le mot de passe de l'utilisateur MySQL configuré plus tôt.  
- ✅ La ligne doit être identique à `DBPassword=MotDePasseSolide`  

➡️ **Quitter et sauvegarder le fichier** : `Alt + X` puis `o`  

➡️ **Démarrer et activer les services** :  
`systemctl restart zabbix-server zabbix-agent apache2 mariadb`  
`systemctl enable zabbix-server zabbix-agent apache2 mariadb`  

  

  
  
  

  

