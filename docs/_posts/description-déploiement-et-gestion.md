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
          
![Topologie]          


## Choix technologiques

### Routage

EIGRP 

### Pare-feu

Cisco sur le réseau principal et le site distance (R4).
Fortinet pour le deuxième site distant (R5).

### Redondance

Etherchannel
RSTP (redondance de lien) utilisé avec la technologie Etherchannel.
HSRP (redondance de passerelle)

### Services d'infrastructure

NTP, DHCP, CDP, DNS,

### VPN IPSEC

tunnel entre R4 (Cisco) et R1 (Cisco) en ipv4 seulement. Code à adapter pour le rendre opérationnel en ipv6.
tunnel entre R5 (Fortinet) et R1 (Cisco) : problèmes rencontrés, tunnel non fonctionnel (interopérabilité difficile entre Cisco et Fortinet)

## Gestion

### Automatisation : Ansible

### Surveillance : SYSLOG et SNMP

