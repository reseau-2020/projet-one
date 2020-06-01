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
          
![Topologie](https://github.com/reseau-2020/projet-one/blob/master/docs/_posts/topologie-projet-one..png)  


## Choix technologiques

### Routage

Nous avons retenu le protocole de routage dynamique EIGRP, pour le routage interne en IPv4 et en IPv6 de la topologie principale, ainsi que pour le routage interne en IPv4 et en IPv6 du site distant R4. Nous justifions ce choix par l'utilisation d'une infrastructure homogène Cisco, EIGRP (Enhanced Interior Gateway Routing Protocol) étant un protocole propriétaire Cisco et standardisé par l'IETF (Internet Engineering Task Force), via le RFC 7868.

EIGRP (IPv4 et IPv6) aussi bien qu'OSPFv2 (IPv4) et OSPFv3 (IPv6), sont des solutions fiables pour notre infrastructure. Nous avons décidé de ne pas prendre en compte le protocole RIPv2, moins évolué, bien que ce dernier soit aussi présent dans l'inventaire Ansible de notre client.

OSPF (Open Shortest Path First), standard IETF, pourrait aussurer le routage IPv6 via l'utilisation de sa version OSPFv3, et son temps de convergence est proche de celui d'EIGRP. EIGRP présente toutefois une meilleure fiabilité (distance administrative de 90 pour EIGRP contre 110 pour OSPF, 120 pour RIPv2). Pour rappel, EIGRP appartient à la catégorie des protocoles de routage interne à vecteur de distance, alors qu'OSPF est un protocole de routage interne à état de lien.

* Comparaison EIGRP - OSPF

|**EIGRP**|**OSPF**|
|:-:|:-:|
|Protocole de routage à vecteur de distance & Hybride|Protocole de routage à état de lien |
|Priopriétaire Cisco, Standard récent|Standard IETF|
|Distance Administrative: 90|Distance Administrative: 110|
|Route secondaire de secours|Pas de route secondaire|
|Algorithme DUAL|Algorithme Dijkstra|
|Système autonome|Division du réseau en aires|

Notre second site distant R5 utilise un routeur / pare-feu Fortigate de Fortinet, OSPFv2 et OSPFv3 seraient à privilégier dans le cadre de l'implémentation du routage interne dynamique au sein de ce réseau.

* Sources

https://cisco.goffinet.org/

https://www.cisco.com/c/en/us/support/docs/ip/enhanced-interior-gateway-routing-protocol-eigrp/16406-eigrp-toc.html

https://openclassrooms.com/fr/courses/2557196-administrez-une-architecture-reseau-avec-cisco/5135481-choisissez-entre-ospf-et-eigrp-pour-votre-topologie


### Pare-feu

Notre projet est basé sur une infrastructure homogène Cisco, nous avons donc configuré un premier pare-feu ZBF (Zone Based Firewall) Cisco sur le routeur R1 (réseau principal) et un second pare-feu ZBF Cisco sur le routeur R4 (site distant R4). Toutefois, nous avons quand même configuré un pare-feu Fortinet sur le routeur R5 (site distant R5) afin d'appréhender le principe de gestion unifiée des menaces (UTM), même si nous avons déployé uniquement un pare-feu.

Le pare-feu est un composant fondamental de la sécurité des réseaux. Chaque noeud d'interconnexion entre notre réseau interne et l'extérieur (vers l'internet ou un réseau étranger), doit inclure une fonctionnalité de pare-feu.  Par défaut, une fois les fonctionnalités du pare-feu activées, aucun trafic ne pourra entrer ni sortir de notre réseau, principe du moindre privilège. Suivant les politiques de sécurité retenues, le pare-feu va filtrer tout ou partie du trafic le traversant, en ne laissant passer que les types de paquets explicitement mentionnés dans sa configuration.

Dans notre cas, ces noeuds se situent aux emplacements de R1 (site principal), R4 (site distant) et R5 (site distant). On active les fonctionnalités de pare-feu Cisco sur les routeurs R1 et R4. R5 est un pare-feu Fortinet incluant des fonctionnalités de routage et de NAT.

Le ZBF Cisco nécessite de définir des zones de sécurité et de mettre en place des politiques de sécurité ciblées afin d'autoriser uniquement les flux de données nécessaires. Les politiques de sécurité sont à adapter suivant les topologies et les besoins (si présence d'une dmz, ...).

#### Cisco ZBF sur R1 (Choix similaire pour R4, sans dmz)

* Zones de sécurité et directions ajoutées (unidirectionnel)

| **Security zone** | **Interface** | **Zone-pair** | **Niveau de Confiance** |
| :-| :- | :- | :-: |
| internet | g0/1 | internet-dmz, internet-self | 0% |
| lan | g0/2, g0/3 | lan-internet, lan-dmz | 100% |
| dmz | g0/0 | - | à risque |
| self-zone | all | self-internet, internet-self | Firewall ZBF R1 |

* Zone-pair et policy-map

| **zone-pair** | **Source**| **Destination** | **Policy-map** |
| :- | :- | :- | :- |
| lan-internet | lan | internet | lan-internet-policy |
| lan-dmz | lan | dmz | lan-dmz-policy |
| internet-dmz | internet | dmz | internet-dmz-policy |
| internet-self | internet | self | to-self-policy |
| self-internet | self | internet | to-self-policy |

* Policy-map, class-map, protocoles et access-group (ACL ciblées)

| **Policy-map (*action*)** | **Class-map (*action*)** | **Match protocol class-map** | **Access-group** |
| :- | :- | :- | :- |
| lan-internet-policy (*inspect*) | internet-trafic-class (*inspect*) | dns, http, https, icmp | |
| | class-default | | |
| lan-dmz-policy (*inspect*) | lan-dmz-class (*inspect*) | http, https | |
| | class-default | | |
| internet-dmz-policy (*inspect*) | internet-dmz-class (*inspect*) | http, https | |
| | class-default | | |
| to-self-policy (*inspect*) | remote-access-class (*inspect*) | | SSH |
| | icmp-class (*inspect*) | icmp | |
| | dhcp-class (*pass*) | | DHCP |
| | dns-class (*pass*) | | DNS |
| | ntp-class (*pass*) | ntp | |
| | vpn-class (*inspect*) | | ISAKMP_IPSEC |
| | class-default (*drop log*) | | |

#### Pare-feu / routeur Fortios (Fortinet) - site distant de R5

Une seule politique a été configurée, pour un flux unidirectionnel du lan R5 vers l'internet, en autorisant certains protocoles dont http, https et icmp.

### Redondance
 
La redondance de liens est assurée par le protocole Rapid Spanning-Tree Portfast (RSTP) agissant au niveau de la couche L2 du modèle OSI. RSTP est utilisé de concert avec la technologie Etherchannel agissant au niveau de la couche L1. RSTP est préféré à STP car il possède un temps de convergence beaucoup plus court le rendant ainsi plus opérationnel. L'interêt d'utiliser la technologie Etherchannel est qu'elle permet de simplifier une topologie Spanning-Tree en diminuant le nombre de liens. Ainsi la vitesse et la tolérance aux pannes entre les switchs, routeurs, serveurs est augmentée. Etherchannel est configuré dynamiquement via un protocole qui négocie l'aggrégation : Link Aggregation Control Protocol (LACP), protocole standardisé par l'IETF.

La redondance de passerelle est assurée par le protocole Hot Standby Router Protocol (HSRP) agissant au niveau de la couche L3. HSRP est un protocole propriétaire Cisco. Ayant une topologie homogène Cisco, il est cohérent de déployer HSRP. Le "Hello Time" est de 3s et le "Hold Time" de 10s. Ces deux valeurs pourraient être ajustées afin de rendre le protocole HSRP encore plus efficace dans le délai de reprise.

### Services d'infrastructure

Les services d'infrastructure tels que DHCP (attribution dynamique d'adresses), DNS (service de résolution de noms), NTP (synchronisation temporelle) et CDP (découverte de voisins) ont été déployés.

* DHCP :Dynamic Host Configuration Protocol)
* DNS : (Domain Name System
* NTP : Network Time Protocol
* CDP : Cisco Discovery Protocol (On a désactivé CDP sur les interfaces g0/1 de R1 et g0/1 de R4, ainsi que sur les interfaces de gestion reliant nos périphériques à la station de contrôle Centos-1 via le réseau de gestion, CDP n'est actif qu'en interne)

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

### Déploiement automatisé : Ansible 

Une partie du déploiement de la topologie se fait de manière automatique à l'aide d'Ansible. Pour cela, un ensemble de livres de jeux et de fichiers de configuration est utilisé afin de paramétrer sur chacun des routeurs et périphériques des paramètres pré-établis et activer certains protocoles. 
Pour lancer ce déploiement automatique, il faut, depuis une machine de contrôle centos ou ubuntu disposant d'Ansible, importer l'ensemble de ce repository GitHub, puis lancer l'ensemble des livres de jeux à l'aide du fichier `ccna.yml` se trouvant dans le répertoire `projet-one/playbooks/`. On utilise pour cela la commande `ansible-playbook ccna.yml -v`
(/!\ Attention: Dans le cadre de ce projet, le client a demandé à ce qu'une pré-configuration soit réalisée sur l'ensemble des machines, cette pré-configuration est disponible dans le fichier `projet-one/docs/_posts/configuration-manuelle.md`

### Déploiement manuel : 

Une fois ce premier déploiement automatisé effectué, des ajouts manuels sont nécessaires afin d'activer les fonctionnalités et protocoles supplémentaires. L'ensemble des procédures à effectuer sur la topologie est regroupé dans les fichiers `projet-one/docs/_posts/configuration-manuelle.md` et `projet-one/docs/_posts/annexe_config_manuelle.md`.

Il est aussi envisageable, dans le cadre d'un déploiement manuel ou de problème sur l'un des périphériques de retrouver le fichier de configuration complet de chaque périphérique dans leur état au terme de ce projet. Ces fichiers se trouvent dans `projet-one/docs/_posts/fichiers_config/`. 

### Surveillance / Reporting : SNMP et SYSLOG

*SNMP (Simple Network Management Protocol) :*
SNMP a été déployé afin de surveiller les périphériques réseau depuis la station de contrôle. Nous avons donc implémenté ce protocole sur la station de contrôle (Centos-1) et les périphériques réseau (R1, R2, R3, DS1, DS2, AS1 et AS2). Il s'agit de la version v3 du protocole SNMP car les versions 1 et 2 sont aujourd'hui dépréciées dû à des lacunes de sécurité. 
Dans le cas présent, la procédure de configuration de SNMPv3 s'est passée en 4 étapes :
         - Création d'une liste d'accès afin d'autoriser la station de contrôle à interroger le serveur SNMP
         - Configuration d'une "view" SNMP_RO 
         - Configuration d'un groupe ADMIN 
         - Configuration d'un utilisateur "team1" comme membre du groupe ADMIN avec authentification SHA, mot de passe et chiffrement AES 128


*Reporting SYSLOG :*
Le protocole SYSLOG a pour but de transporter par le réseau les messages de journalisation générés par une application (qu'on appelle aussi log) vers un serveur hébergeant un serveur Syslog. Il permet ainsi d'assurer une concentration des journaux en un seul point. Ici nous avons donc implémenté ce protocole sur l'ensemble des périphériques réseau (R1, R2, R3, DS1, DS2, AS1 et AS2), afin que les logs, en plus d'être disponibles sur chacun de ces périphériques, soient également regroupés et disponibles sur la station de contrôle (Centos-1). 
Ainsi, en cas de souci sur un des périphériques, ou si la communication vers les périphériques est perdue, il reste possible d'accéder à l'ensemble des messages de journalisation générés et de les étudier pour comprendre les éventuels disfonctionnements. 
