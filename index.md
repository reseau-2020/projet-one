# Programme du jour: 18/05/2020

  * Lecture de l'énoncé du projet
  * Listing détaillé et répartition des tâche
  * Documentation/état de l'art
  * Création du journal.md
  * Choix des blocs d'adressage et du protocole de routage

# Liste des tâches

## Adressage IPv4 et IPv6 spécifique (bloc d'adresse indédits) et le protocole de routage EIGRP ou OSPF				
* choix des blocs d'adressage IPv4 (1 Bloc IPv6 HE Global Unicast fourni par le formateur) pour notre topologie		
* choisir le protocole de routage	
											
## Switchblock (4 vlans utiles) dans les couches Access et Distribution (assuré par RSTP, Etherchannel et HSRP)	

### Switch Access					
* Création des VLANs				
* Configuration des ports Access et Trunk				
* Etherchannel (ports, PAgP/LACP)				
* Rapid Spanning-Tree				
													
### Switch Distribution					
* Création des VLANs				
* Configuration des ports Access et Trunk				
* Etherchannel (ports, PAgP/LACP)				
* Rapid Spanning-Tree				
* Redondance de passerelle (HSRP)				
* Configuration des passerelles (IPv4 et IPv6)				
* Configuration du service DHCP				
								
								
## Une couche Core maillée de trois routeurs							
### Configuration du routeur R1					
* adressage IPv4 et IPv6 + service DHCP				
* activer OSPF				
* activer l'accès internet (liste d'accès, NAT)			
### Configuration du routeur R2					
* adressage IPv4 et IPv6 + service DHCP				
* activer OSPF			
### Configuration du routeur R3			
* adressage IPv4 et IPv6 + service DHCP				
* activer OSPF	

## Un maillage entre la couche Core et les switchblock							
### Redondance entre DS1/DS2 (Switchblock) et R2/R3 (couche Core)					
* Etherchannel (PAgP ou LACP)				
* Rapid ST				
* HSRP 	

## Un accès Internet avec un pare-feu/nat et une DMZ											
## Un site distant connecté en VPN IPSEC												
## Des services d'infrastuctures (NTP,DNS,DHCP,NTP/DHCPv6/DHCP Relay,RA, ...)							
* CDP/LLDP					
* Synchronisation temporelle NTP					
* Gestion des logs SYSLOG					
 Supervision SNMP	

## Des services de surveillance (SYSLOG, SNMP)											

## Le focus sécuriataire sur toutes les solutions déployées							
## Documentation														
### Tenue du journal de bord					
### État de l'art					
### Support de présentation					
### Bibliographie					


