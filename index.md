# Programme du jour: 18/05/2020

* Lecture de l'énoncé du projet
* Listing détaillé et répartition des tâches
* Documentation/état de l'art
* Création du journal.md
* Choix des blocs d'adressage et du protocole de routage

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
													
#### 1.2.2 Switch Distribution

* Création des VLANs				
* Configuration des ports Access et Trunk				
* Etherchannel (ports, PAgP/LACP)				
* Rapid Spanning-Tree (RSTP)				
* Redondance de passerelle (HSRP)				
* Configuration des passerelles (IPv4 et IPv6)				
* Configuration du service DHCP										
								
### 1.3- Une couche Core maillée de trois routeurs

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

## Un maillage entre la couche Core et les switchblock							
### Redondance entre DS1/DS2 (Switchblock) et R2/R3 (couche Core)					
* Etherchannel (PAgP ou LACP)				
* Rapid ST				
* HSRP 	

## Un accès Internet avec un pare-feu/nat et une DMZ											
## Un site distant connecté en VPN IPSEC												
## Des services d'infrastuctures (NTP,DNS,DHCP,NTP/DHCPv6/DHCP Relay,RA, ...)							
* CDP/LLDP (Voisinage immédiat)					
* Synchronisation temporelle NTP						

## Des services de surveillance (SYSLOG, SNMP)
* SYSLOG : Gestion des logs
* Supervision SNMP

## Le focus sécuriataire sur toutes les solutions déployées							
## Documentation														
### Tenue du journal de bord					
### État de l'art					
### Support de présentation					
### Bibliographie					


