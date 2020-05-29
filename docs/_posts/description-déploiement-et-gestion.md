# Description du déploiement (choix technologiques) et de sa gestion (contrôle, reporting, surveillance)

## Contenu de la topologie

La topologie est constituée de :
- une station de contrôle (Centos-1) reliée à Internet et au réseau principal.
- un réseau principal constitué de :
          - une couche core maillée de 3 routeurs (R1, R2 et R3).
          - un switchblock contenant deux routeurs-switchs (DS1 et DS2), deux switchs (AS1 et AS2) et 8 stations de travail Ubuntu (PC1 à PC8).
          - un maillage entre la couche Core et le switchblock
          - un accès Internet
- un site distant constitué de :
          - un routeur R4 avec pare-feu Cisco
          - un accès Internet
          - une station de travail (PC9)
- un autre site distant constitué de :
          - un routeur R5 avec pare-feu Fortinet
          - un accès Internet
          - une station de travail (PC10)
          
![Topologie](https://github.com/reseau-2020/projet-one/blob/master/docs/_posts/topologie-projet-one.png)     


## Choix technologiques

### Routage

Comme nous disposons d'une infrastructure homogène Cisco, nous avons décidé de déployer le protocole de routage EIGRP (Enhanced Interior Gateway Routing Protocol) qui est un protocole propriétaire Cisco. De plus, la distance administrative du protocole EIGRP est plus faible que celle du protocole OSPF (Open Shortest Path First).

### Pare-feu

Dans notre infrastructure homogène Cisco, nous avons donc configuré un pare-feu Cisco sur le routeur R1 (réseau principal) et sur le routeur R4 (premier site distant). Toutefois, nous avons quand même configuré un pare-feu Fortinet sur le routeur R5 (second site distant) afin d'appréhender le principe de gestion unifiée des menaces (UTM) même si nous avons déployé uniquement un pare-feu.


### Redondance

Redondance de lien : RSTP utilisé avec la technologie Etherchannel.
Redondance de passerelle : HSRP

### Services d'infrastructure


DHCP (Dynamic Host Configuration Protocol) :

DNS (Domain Name System) :

NTP (Network Time Protocol) :

CDP (Cisco Discovery Protocol) :

### VPN IPSEC

tunnel entre R4 (Cisco) et R1 (Cisco) en ipv4 seulement. Code à adapter pour le rendre opérationnel en ipv6.
tunnel entre R5 (Fortinet) et R1 (Cisco) : problèmes rencontrés, tunnel non fonctionnel (interopérabilité difficile entre Cisco et Fortinet)

## Gestion

### Automatisation : Ansible

### Surveillance / Reporting : SNMP et SYSLOG

