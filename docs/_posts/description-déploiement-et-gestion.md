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

Nous avons retenu le protocole de routage dynamique EIGRP, pour le routage interne en IPv4 et en IPv6 de la topologie principale, ainsi que pour le routage interne en IPv4 et en IPv6 du site distant Lan R4. Nous justifions ce choix par l'utilisation d'une infrastructure homogène Cisco, EIGRP (Enhanced Interior Gateway Routing Protocol) étant un protocole propriétaire Cisco et standardisé par l'IETF (Internet Engineering Task Force), via le RFC 7868.

EIGRP (IPv4 et IPv6) aussi bien qu'OSPFv2 (IPv4) et OSPFv3 (IPv6), sont des solutions fiables pour notre infrastructure. Nous avons décidé de ne pas prendre en compte le protocole RIPv2, moins évolué, bien que ce dernier soit aussi présent dans l'inventaire Ansible de notre client.


### Pare-feu

Dans notre infrastructure homogène Cisco, nous avons donc configuré un pare-feu Cisco sur le routeur R1 (réseau principal) et sur le routeur R4 (premier site distant). Toutefois, nous avons quand même configuré un pare-feu Fortinet sur le routeur R5 (second site distant) afin d'appréhender le principe de gestion unifiée des menaces (UTM) même si nous avons déployé uniquement un pare-feu.
À compléter (Stéphane ?)

### Redondance

Redondance de lien : RSTP utilisé avec la technologie Etherchannel.
Redondance de passerelle : HSRP

### Services d'infrastructure

DHCP (Dynamic Host Configuration Protocol) :

DNS (Domain Name System) :

NTP (Network Time Protocol) :

CDP (Cisco Discovery Protocol) :

### VPN IPSEC

Un tunnel VPN IPSEC est établit entre R4 (avec pare-feu Cisco) et R1 (avec pare-feu Cisco) afin de disposer d'un canal sécurisé entre deux sites distants. Le protocole de transport ESP (Encapsulating Security Payload) est préféré au protocole AH (Authentication Header) car il supporte le routage NAT et assure le chiffrement. À des fins de sécurité adéquate sont implémentés : 
- l'algorithme de chiffrement AES 256
- la fonction de hash SHA
- l'authentification des pairs par la méthode PSK
- le groupe DH 5 (le groupe DH est apprécié en fonction du contexte)

En IPv4, le tunnel est opérationnel.
En IPv6, le code est à adapter afin de rendre le tunnel opérationnel.

Nous avons ensuite tenté d'établir un tunnel VPN IPSEC entre R5 (avec pare-feu Fortinet) et R1 (avec pare-feu Cisco). Malheureusement, le tunnel n'est pas fonctionnel. Par manque de temps, nous n'avons pu poursuivre le travail sur ce point.


## Gestion

### Automatisation : Ansible


### Surveillance / Reporting : SNMP et SYSLOG

*SNMP (Simple Network Management Protocol) :*
SNMP a été déployé afin de surveiller les périphériques réseau depuis la station de contrôle. Nous avons donc implémenté ce protocole sur la station de contrôle (Centos-1) et les périphériques réseau (R1, R2, R3, DS1, DS2, AS1 et AS2). Il s'agit de la version v3 du protocole SNMP car les versions 1 et 2 sont aujourdh'hui dépréciées dues à des lacunes de sécurité. 
Dans le cas présent, la procédure de configuration de SNMPv3 s'est passée en 4 étapes :
         - Création d'une liste d'accès afin d'autoriser la station de contrôle à interroger le serveur SNMP
         - Configuration d'une "view" SNMP_RO 
         - Configuration d'un groupe ADMIN 
         - Configuration d'un utilisateur "team1" comme membre du groupe ADMIN avec authentification SHA, mot de passe et chiffrement AES 128


*Reporting SYSLOG :*




