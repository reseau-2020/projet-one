# Programme du jour: 18/05/2020

* Lecture de l'énoncé du projet
* Listing détaillé et répartition des tâches
* Documentation/état de l'art
* Création du journal.md (Nom définitif à préciser)
* Choix des blocs d'adressage et du protocole de routage

## Synthèse de la journée

Il s'agit du Jour 1 de notre projet. Nous avons pris le temps de poser le sujet, d'analyser les attentes du client et d'y apporter une première réponse. La journée a été essentiellement dédiée à la mise en place du squelette de notre projet, de cerner ses grandes étapes et d'établir une première planification provisoire. Une attention particulière a été portée sur la description des tâches et sous-tâches.
Le choix prochain du plan d'adressage IPv4 découlera directement de cette mise en place, le plan d'adressage IPv6 est quant-à-lui cadré par notre client.
Les prochaines journées seront dédiées à la configuration des topologies de type Tripod et Switchblock, et leurs protocoles associés. Nous incluerons progressivement une gestion centralisée Ansible, avec pour objectif majeur de la rendre parfaitement opérationnelle dans notre champ d'intervention.

## 1- Liste des tâches

### 1.1- Adressage IPv4 et IPv6 spécifique (bloc d'adresse indédits) et le protocole de routage EIGRP ou OSPF

* Choix des blocs d'adressage IPv4 (1 Bloc IPv6 HE Global Unicast fourni par le formateur) pour notre topologie		
* Choisir le protocole de routage	
											
### 1.2- Topologie Switchblock (4 vlans utiles) dans les couches Access et Distribution (assuré par RSTP, Etherchannel et HSRP)	

#### 1.2.1- Switch Access

* Création des VLANs				
* Configuration des ports Access et Trunk				
* Etherchannel (ports, PAgP/LACP)				
* Rapid Spanning-Tree (RSTP)				
													
#### 1.2.2- Switch Distribution

* Création des VLANs				
* Configuration des ports Access et Trunk				
* Etherchannel (ports, PAgP/LACP)				
* Rapid Spanning-Tree (RSTP)				
* Redondance de passerelle (HSRP)				
* Configuration des passerelles (IPv4 et IPv6)				
* Configuration du service DHCP										
								
### 1.3- Topologie Tripod (Couche Core maillée de trois routeurs)

#### 1.3.1- Configuration du routeur R1

* Adressage IPv4 et IPv6 + service DHCP				
* Activer routage OSPF				
* Activer l'accès internet (listes d'accès, NAT)

#### 1.3.2- Configuration du routeur R2

* Adressage IPv4 et IPv6 + service DHCP				
* Activer routage OSPF

#### 1.3.3- Configuration du routeur R3

* Adressage IPv4 et IPv6 + service DHCP				
* Activer routage OSPF	

### 1.4- Topologie Complète : liaison Tripod - Switchblock(s)

#### 1.4.1- Redondance entre DS1/DS2 (Switchblock) et R2/R3 (Tripod, couche Core)					
* Etherchannel (PAgP ou LACP)				
* Rapid Spanning-Tree (RSTP)				
* Redondance de passerelle (HSRP) 	

#### 1.4.2- Accès Internet via un routeur NAT & Pare-feu Cisco ou Fortinet
* Configuration des pare-feux (Fortinet ou Cisco), nombre à définir
* Pare-feu sur le routeur NAT R1 interconnectant le réseau du lab au réseau internet

#### 1.4.2- DMZ (Serveurs applicatifs, ...)
* Encore à préciser

#### 1.4.3- Connexion à un site distant en VPN IPSEC
* LAN et/ou VLAN à préciser

#### 1.4.4- Des services d'infrastuctures (NTP,DNS,DHCP,NTP/DHCPv6/DHCP Relay,RA, ...)							
* CDP/LLDP (Voisinage immédiat)					
* Synchronisation temporelle NTP						

#### 1.4.5- Des services de surveillance (SYSLOG, SNMP)
* SYSLOG : Gestion des logs
* Supervision SNMP

### 1.5 Focus sécuritaire sur toutes les solutions déployées

### 1.6 Extension à plusieurs Switchblocks

### 1.7 Utilisation d'Ansible, Gestion centralisée
							
## 2- Documentation

### 2.1- Tenue du journal de bord

### 2.2- État de l'art

### 2.3- Support de présentation

### 2.4- Bibliographie					


