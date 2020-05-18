# Programme du jour: 18/05/2020

* Lecture de l'énoncé du projet
* Listing détaillé et répartition des tâches
* Documentation/état de l'art
* Création du journal.md (Nom définitif à préciser)
* Choix des blocs d'adressage et du protocole de routage

## Synthèse de la journée

Il s'agit du Jour 1 de notre projet. Nous avons pris le temps de poser le sujet, d'analyser les attentes du client et d'y apporter une première réponse. La journée a été essentiellement dédiée à la mise en place du squelette de notre projet, de cerner ses grandes étapes et d'établir une première planification provisoire. Une attention particulière a été portée sur la description des tâches et sous-tâches.

Le choix prochain du plan d'adressage IPv4 découlera directement de cette mise en place, le plan d'adressage IPv6 est quant-à-lui cadré par notre client.

Les prochaines journées seront dédiées à la configuration des topologies de type Tripod et Switchblock, et leurs protocoles associés. Nous inclurons progressivement une gestion centralisée Ansible, avec pour objectif majeur de la rendre parfaitement opérationnelle dans notre champ d'intervention.

## Liste des tâches

### 1- Etat de l'Art, Analyse des besoins du client, Analyse du Cahier des Charges
* Listing des tâches
* Plannification
* Détermination des tâches critiques et du chemin critique
* Affectation des rôles

### 2- Adressage IPv4 et IPv6 spécifique (blocs d'adresses indédits) & Protocole de Routage 
* Choix des topologies et Diagrammes associés
* Choix des blocs d'adressage IPv4 (1 Bloc IPv6 HE Global Unicast fourni par le formateur) pour notre topologie	finale	
* Choix du protocole de routage (EIGRP ou OSPF)	
											
### 3- Topologie Switchblock (4 vlans utiles) dans les couches Access et Distribution (assuré par RSTP, Etherchannel et HSRP)	

#### 3.1- Switch Access
* Création des VLANs				
* Configuration des ports Access et Trunk				
* Etherchannel (ports, PAgP/LACP)				
* Rapid Spanning-Tree (RSTP)				
													
#### 3.2- Switch Distribution
* Création des VLANs				
* Configuration des ports Access et Trunk				
* Etherchannel (ports, PAgP/LACP)				
* Rapid Spanning-Tree (RSTP)				
* Redondance de passerelle (HSRP)				
* Configuration des passerelles (IPv4 et IPv6)				
* Configuration du service DHCP

#### 3.3- Tests fiabilité, Diagnostics
* Connectivité
* Adressage
* à développer ...
								
### 4- Topologie Tripod (Couche Core maillée de trois routeurs)

#### 4.1- Configuration du routeur R1
* Adressage IPv4 et IPv6 + service DHCP				
* Activer routage OSPF				
* Activer l'accès internet (listes d'accès, NAT)

#### 4.2- Configuration du routeur R2
* Adressage IPv4 et IPv6 + service DHCP				
* Activer routage OSPF

#### 4.3- Configuration du routeur R3
* Adressage IPv4 et IPv6 + service DHCP				
* Activer routage OSPF

#### 4.4- Tests fiabilité, Diagnostics
* Connectivité
* Adressage
* à développer ...	

### 5- Topologie Complète : liaison Tripod - Switchblock(s)

#### 5.1- Redondance entre DS1/DS2 (Switchblock) et R2/R3 (Tripod, couche Core)					
* Etherchannel (PAgP ou LACP)				
* Rapid Spanning-Tree (RSTP)				
* Redondance de passerelle (HSRP) 	

#### 5.2- Accès Internet via un routeur NAT & Pare-feu Cisco ou Fortinet
* Configuration des pare-feux (Fortinet ou Cisco), nombre à définir
* Pare-feu sur le routeur NAT R1 interconnectant le réseau du lab au réseau internet

#### 5.3- Tests fiabilité, Diagnostics
* Connectivité
* Adressage
* à développer ...	

### 6- Fonctions complémentaires

#### 6.1- DMZ (Serveurs applicatifs, ...)
* Encore à préciser

#### 6.2- Connexion à un site distant en VPN IPSEC
* LAN et/ou VLAN à préciser
* Diagnostics fiabilité

#### 6.3- Services d'infrastuctures (NTP,DNS,DHCP,NTP/DHCPv6/DHCP Relay,RA, ...)							
* CDP ou LLDP (Voisinage immédiat)					
* Synchronisation temporelle NTP
* Diagnostics fiabilité

#### 6.4- Services de surveillance (SYSLOG, SNMP)
* SYSLOG : Gestion des logs
* Supervision SNMP
* Diagnostics fiabilité

#### 6.5- Focus sécuritaire sur toutes les solutions déployées
* Filtrage Couches 2, 3 et 7 sur routeurs, commutateurs (Switch) et autres périphériques
* Renforcer la sécurité des périphériques du réseau
* Pare-feu additionnels et contrôle des flux via listes d'accès?
* Tests sécurité, diagnostics

### 7- Extension à plusieurs Switchblocks
* Tests sécurité et fiabilité, diagnostics

### 8- Ansible, Gestion centralisée des configurations, IaC

#### 8.1- Prise en Main d'Ansible, documentation client

#### 8.2- Switchblock(s) (Couches Access et Distribution)

#### 8.3- Tripod (Couche Core)

#### 8.4- Topologie Finale (Core + Access + Distribution)

#### 8.5- Configuration des compléments

#### 8.6- Tests & Diagnostics
							
### 9- Documentation

#### 9.1- Tenue du journal de bord

#### 9.2- État de l'art

#### 9.3- Support de présentation

#### 9.4- Bibliographie

#### 9.5- Documentation technique, Rapport & Annexes


