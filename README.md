# -Mini-infrastructure-reseau-virtualisee-VirtualBox-

## :one: Objectif  

Ce premier projet a pour but de concevoir une mini infrastructure virtualisée à partir de VirtualBox dans un objectif de préparation a un futur homelab beaucoup plus avancé.  
L'infrastructure sera composée dans un premier temps de 3 VLANs et d'un routeur Linux permettant un accès à Internet.  
Les étapes de la mise en place de ce mini réseau seront documentées.  

## :two: Techologies utilisées  

- VirtualBox pour la virtualisation  
- Debian pour le routeur  
- Windows 10 pour les machines clients  
- iptables pour NAT et routage  

## :three: Plan d'adressage (résumé)  

| VLAN | Nom     | Réseau IP |
|------|---------|-----------|
| 10   | USERS   | 192.168.10.0/24 |
| 20   | SERVERS | 192.168.20.0/24 |
| 30   | ADMIN   | 192.168.30.0/24 |

## :four: État d'avancement  

- [ ] Création des réseaux VirtualBox
- [ ] Configuration IP statique
- [ ] Routage inter-VLAN
- [ ] Accès Internet (NAT)
- [ ] DHCP
- [ ] DNS local
- [ ] Firewall inter-VLAN  

## :five: English summary  

This first project is meant to build a small virtualized network infrastructure from VirtualBox, in order to prepare a future homelab very much more elaborated.  
The infrastructure will be composed in the first place with 3 VLANs and one Linux router giving an access to the Internet.  
All the steps from this project will be documented in this repo.  
