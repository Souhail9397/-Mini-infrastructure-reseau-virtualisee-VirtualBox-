# -Mini-infrastructure-reseau-virtualisee-VirtualBox-

## :one: Objectif  

Ce premier projet a pour but de concevoir une mini infrastructure virtualisée à partir de VirtualBox dans un objectif de préparation a un futur homelab beaucoup plus avancé.  
L'infrastructure sera composée dans un premier temps de 3 LANs (2 utilisateurs et 1 serveurs) et de deux routeurs Debian : un pour le routage inter LANs et un pour un accès à Internet.  
Les étapes de la mise en place de ce mini réseau seront documentées ici.  

## :two: Techologies utilisées  

- VirtualBox pour la virtualisation  
- Debian pour les routeurs  
- Windows 10 pour les machines clients  
- iptables pour NAT et routage  

## :three: Plan d'adressage (résumé)  

| LAN | Nom     | Réseau IP |
|------|---------|-----------|
| 10   | USERS   | 192.168.10.0/24 |
| 20   | USERS   | 192.168.20.0/24 |
| 30   | SERVERS | 192.168.30.0/24 |

## :four: État d'avancement  

- [x] Création des réseaux VirtualBox
- [x] Configuration IP statique
- [x] Routage inter-LAN
- [x] Accès Internet (NAT)
- [ ] DHCP
- [ ] DNS local
- [ ] Firewall inter-LAN  

## :five: Schéma de l'infrastructure  

Voici un schéma de l'infrastructure, qui sera amené à évoluer au fur et à mesure que de nouveaux services viendront s'ajouter.  

![Schema](https://github.com/user-attachments/assets/56966d5c-073f-4dfe-8652-45eee1eaf893)  
  

## :five: English summary  

This first project is meant to build a small virtualized network infrastructure from VirtualBox, in order to prepare a future homelab very much more elaborated.  
The infrastructure will be composed in the first place with 3 VLANs and one Linux router giving an access to the Internet.  
All the steps from this project will be documented in this repo.  
