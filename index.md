<html lang = "fr">
<head>
  <title>Blog Projet-One</title>
  <meta charset = "UTF-8" />
</head>
<body>
  <h1>Programme du jour: 18/05/2020</h1>
  <p>* Lecture de l'énoncé du projet
  <p>* Listing détaillé et répartition des tâches
  <p>* Documentation/état de l'art
  <p>* Création du journal.md
  <p>* Choix des blocs d'adressage et du protocole de routage

    
  <h1>remplir ici les tâches<h1>
  <p>1.Adressage IPv4 et IPv6 spécifique (bloc d'adresse indédits) et le protocole de routage EIGRP ou OSPF							
	<p>*choix des blocs d'adressage IPv4 (1 Bloc IPv6 HE Global Unicast fourni par le formateur) pour notre topologie					
	<p>*choisir le protocole de routage											
								
2	Switchblock (4 vlans utiles) dans les couches Access et Distribution (assuré par RSTP, Etherchannel et HSRP)							
<p>2.1	Switch Access					
			2.1.1	Création des VLANs				
			2.1.2	Configuration des ports Access et Trunk				
			2.1.3	Etherchannel (ports, PAgP/LACP)				
			2.1.4	Rapid Spanning-Tree				
					
								
	Qui ?	2.2	Switch Distribution					
			2.2.1	Création des VLANs				
			2.2.2	Configuration des ports Access et Trunk				
			2.2.3	Etherchannel (ports, PAgP/LACP)				
			2.2.4	Rapid Spanning-Tree				
			2.2.5	Redondance de passerelle (HSRP)				
			2.2.6	Configuration des passerelles (IPv4 et IPv6)				
			2.2.7	Configuration du service DHCP				
								
								
3	Une couche Core maillée de trois routeurs							
	Qui ?	3.1	Configuration du routeur R1					
			3.1.1	adressage IPv4 et IPv6 + service DHCP				
			3.1.2	activer OSPF				
			3.1.3	activer l'accès internet (liste d'accès, NAT)				
	Qui ?	3.2	Configuration du routeur R2					
			3.2.1	adressage IPv4 et IPv6 + service DHCP				
			3.2.2	activer OSPF				
	Qui ?	3.3	Configuration du routeur R3					
			3.3.1	adressage IPv4 et IPv6 + service DHCP				
			3.3.2	activer OSPF				
								
								
<p>4	Un maillage entre la couche Core et les switchblock							
<p>4.1	Redondance entre DS1/DS2 (Switchblock) et R2/R3 (couche Core)					
			4.1.1	Etherchannel (PAgP ou LACP)				
			4.1.2	Rapid ST				
			4.1.3	HSRP 				
				
								
5	Un accès Internet avec un pare-feu/nat et une DMZ							
					
								
6	Un site distant connecté en VPN IPSEC							
					
								
7	Des services d'infrastuctures (NTP,DNS,DHCP,NTP/DHCPv6/DHCP Relay,RA, ...)							
	7.1	CDP/LLDP					
	7.2	Synchronisation temporelle NTP					
	7.3	Gestion des logs SYSLOG			on peut peut-être lier les points 7 et 8 ?		
		7.4	Supervision SNMP					
								
8	Des services de surveillance (SYSLOG, SNMP)							
					
								
9	Le focus sécuriataire sur toutes les solutions déployées						
					
								
								
<p>10	Documentation							
<p>10	Documentation														
<p>10.1	Tenue du journal de bord					
<p>10.2	État de l'art					
<p>10.3	Support de présentation					
<p>10.4	Bibliographie					
  <p>
  <h1>A faire</h1>
  <p>
    blabla 
  </p>
  <h1>Fait</h1>
  <p>
    blabla 
  </p>
  <h1>Programme du 19/05/2020</h1>

</body>
</html>
