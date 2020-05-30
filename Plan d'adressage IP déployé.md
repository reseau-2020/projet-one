# Plan d'adressage déployé
L'adressage IPv4 est en /24.
L'adressage IPv6 est en /64.

## Adressage IPv6 Global Unicast site principal (interface G0/1 de R1)
- Adresses des réseaux maîtrisés, routé jusqu'à votre routeur externe : `2001:470:c814:1000::/52`
- L'adresse IPv6 externe de votre routeur : `fe80::cafe:1`
- L'adresse IPv6 de la passerelle vers l'Internet : `fe80::e53:21ff:fe38:5800`


## Adressage IPv6 Global Unicast site distant (interface G0/1 de R4)
- Adresses des réseaux maîtrisés, routé jusqu'à votre routeur externe : `2001:470:c814:5000::/52`
- L'adresse IPv6 externe de votre routeur : `fe80::cafe:5`
- L'adresse IPv6 de la passerelle vers l'Internet : `fe80::e53:21ff:fe38:5800`

## Logique du plan d'adressage ipv4
- Choix de la classe A (RFC 1918), plage d'adresses IPv4 privées large : 10.0.0.0 /8

octet1.octet2.octet3.octet4

octet1 = 10 (Fixe)

octet2 = ensemble (1: Tripod, 2: Switchblock; 3:Liaison Tripod - Switchblock; 104: Site distant R4, 105: Site distant R5))

octet3 = valeur remarquable de nos sous-réseaux et VLANs

octet4 = ipv4 utilisables de .1 à .254 (/24) sauf exceptions mentionées dans pool dhcp locaux

## Logique du plan d'adressage ipv6
- Bloc IPv6 public pour site principal R1 : `2001:470:c814:1000::/52`
- Bloc IPv6 public pour site distant R4 : `2001:470:c814:5000::/52`
- Différenciation sur le quatrième mot (1000 ou 5000)



## Couche Core (Tripod) 
|Périphérique|Interface|Liaison<br>|Adresse IPv4 statique|Adresse<br>IPv6 Link-local|Adresse IPv6 publique|Adresse IPv6 privée|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|R1|G0/2|R1-R2|10.1.1.1|fe80::dd:1|2001:470:c814:1001::1|fd00:470:c814:1001::1|
|R1|G0/3|R1-R3|10.1.2.1|fe80::dd:1|2001:470:c814:1002::1|fd00:470:c814:1002::1|
|R2|G0/1|R2-R1|10.1.1.2|fe80::dd:2|2001:470:c814:1001::2|fd00:470:c814:1001::2|
|R2|G0/3|R2-R3|10.1.3.2|fe80::dd:2|2001:470:c814:1003::2|fd00:470:c814:1003::2|
|R3|G0/1|R3-R1|10.1.2.2|fe80::dd:3|2001:470:c814:1002::2|fd00:470:c814:1002::2|
|R3|G0/2|R3-R2|10.1.3.1|fe80::dd:3|2001:470:c814:1003::1|fd00:470:c814:1003::1|


## Liaison Core-Switchblock
|Périphérique|Interface|Liaison|Adresse IPv4 statique|Adresse Link-local|Adresse IPv6 publique|Adresse IPv6 privée|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|R2|G0/2|R2-DS1 (1)|10.3.1.1 /24|fe80::dd:2|2001:470:c814:1301::1|fd00:470:c814:1301::1|
|R2|G0/4|R2-DS1 (2)|10.3.11.1 /24|fe80::dd:2|2001:470:c814:1311::1|fd00:470:c814:1311::1|
|R2|G0/5|R2-DS2 (1)|10.3.4.1 /24|fe80::dd:2|2001:470:c814:1304::1|fd00:470:c814:1304::1|
|R2|G0/6|R2-DS2 (2)|10.3.44.1 /24|fe80::dd:2|2001:470:c814:1344::1|fd00:470:c814:1344::1|
|R3|G0/5|R3-DS1 (1)|10.3.2.1 /24|fe80::dd:3|2001:470:c814:1302::1|fd00:470:c814:1302::1|
|R3|G0/6|R3-DS1 (2)|10.3.22.1 /24|fe80::dd:3|2001:470:c814:1322::1|fd00:470:c814:1322::1|
|R3|G0/3|R3-DS2 (1)|10.3.3.1 /24|fe80::dd:3|2001:470:c814:1303::1|fd00:470:c814:1303::1|
|R3|G0/4|R3-DS2 (2)|10.3.33.1 /24|fe80::dd:3|2001:470:c814:1333::1|fd00:470:c814:1333::1|
|DS1|G2/0|DS1-R2 (1)|10.3.1.2 /24|fe80::d1:1|2001:470:c814:1301::2|fd00:470:c814:1301::2|
|DS1|G3/0|DS1-R2 (2)|10.3.11.2 /24|fe80::d1:1|2001:470:c814:1311::2|fd00:470:c814:1311::2|
|DS1|G2/1|DS1-R3 (1)|10.3.2.2 /24|fe80::d1:1|2001:470:c814:1302::2|fd00:470:c814:1302::2|
|DS1|G3/1|DS1-R3 (2)|10.3.22.2 /24|fe80::d1:1|2001:470:c814:1322::2|fd00:470:c814:1322::2|
|DS2|G2/1|DS2-R2 (1)|10.3.4.2 /24|fe80::d2:2|2001:470:c814:1304::2|fd00:470:c814:1304::2|
|DS2|G3/1|DS2-R2 (2)|10.3.44.2 /24|fe80::d2:2|2001:470:c814:1344::2|fd00:470:c814:1344::2|
|DS2|G2/0|DS2-R3 (1)|10.3.3.2 /24|fe80::d2:2|2001:470:c814:1303::2|fd00:470:c814:1303::2|
|DS2|G3/0|DS2-R3 (2)|10.3.33.2 /24|fe80::d2:2|2001:470:c814:1333::2|fd00:470:c814:1333::2|

## Switchblock
|Commutateur|Interface|Passerelle IPV4|Passerelle IPv4 virtuelle|Adresse Link-local|Adresse IPv6 publique|Adresse IPv6 privée|Passerelle IPv6 virtuelle|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|DS1|VLAN10|10.2.10.252 /24|10.2.10.254 /24|fe80::d1:1|2001:470:c814:1010::1|fd00:470:c814:1010::1|fe80::d3:1|
|DS1|VLAN20|10.2.20.252 /24|10.2.20.254 /24|fe80::d1:1|2001:470:c814:1020::1|fd00:470:c814:1020::1|fe80::d3:1|
|DS1|VLAN30|10.2.30.252 /24|10.2.30.254 /24|fe80::d1:1|2001:470:c814:1030::1|fd00:470:c814:1030::1|fe80::d3:1|
|DS1|VLAN40|10.2.40.252 /24|10.2.40.254 /24|fe80::d1:1|2001:470:c814:1040::1|fd00:470:c814:1040::1|fe80::d3:1|
|DS2|VLAN10|10.2.10.253 /24|10.2.10.254 /24|fe80::d2:2|2001:470:c814:1010::2|fd00:470:c814:1010::2|fe80::d3:1|
|DS2|VLAN20|10.2.20.253 /24|10.2.20.254 /24|fe80::d2:2|2001:470:c814:1020::2|fd00:470:c814:1020::2|fe80::d3:1|
|DS2|VLAN30|10.2.30.253 /24|10.2.30.254 /24|fe80::d2:2|2001:470:c814:1030::2|fd00:470:c814:1030::2|fe80::d3:1|
|DS2|VLAN40|10.2.40.253 /24|10.2.40.254 /24|fe80::d2:2|2001:470:c814:1040::2|fd00:470:c814:1040::2|fe80::d3:1|

## HSRP
|Commutateur|Interface|Passerelle IPv4 virtuelle|Passerelle IPv6 Virtuelle|
|:-:|:-:|:-:|:-:|
|DS1|VLAN10|10.2.10.254 /24|fe80::d3:1|
|DS1|VLAN20|10.2.20.254 /24|fe80::d3:1|
|DS1|VLAN30|10.2.30.254 /24|fe80::d3:1|
|DS1|VLAN40|10.2.40.254 /24|fe80::d3:1|
|DS2|VLAN10|10.2.10.254 /24|fe80::d3:1|
|DS2|VLAN20|10.2.20.254 /24|fe80::d3:1|
|DS2|VLAN30|10.2.30.254 /24|fe80::d3:1|
|DS2|VLAN40|10.2.40.254 /24|fe80::d3:1|

## VLAN
|VLAN|Port Access (AS1 et AS2)|Passerelle par défaut IPv4|Adresse réseau IPv4|
|:-:|:-:|:-:|:-:|
|VLAN10|G2/0|10.2.10.254 /24|10.2.10.0 /24|
|VLAN20|G2/1|10.2.20.254 /24|10.2.20.0 /24|
|VLAN30|G2/2|10.2.30.254 /24|10.2.30.0 /24|
|VLAN40|G2/3|10.2.40.254 /24|10.2.40.0 /24|
|VLAN99|VLAN natif|-|-|

Un Vlan de Gestion (Vlan 100) serait une bonne pratique afin de pouvoir joindre les commutateurs et éventuellement leur envoyer du trafic. Cependant, l'utilisation d'Ansible va combler cette fonction. Il n'est donc pas nécessaire ici de déployer un VLAN de gestion sur nos commutateurs. 

## Etherchannel
|PortChannel|Ports Physiques|Commutateurs|
|:-:|:-:|:-:|
|Po1|G0/0,G1/0|AS1-DS1|
|Po2|G0/1,G1/1|AS1-DS2|
|Po3|G0/2,G1/2|DS1-DS2|
|Po4|G0/0,G1/0|AS2-DS2|
|Po5|G0/1,G1/1|AS2-DS1|

## Spanning-Tree
|VLANs|DS1|DS2|
|:-:|:-:|:-:|
|VLANs 1,10,30,99|Root Primary|Root Secondary|
|VLANs 20,40|Root Secondary|Root Primary|

## Réseau distant (R4)

|Périphérique|Interface|Liaison|Adresse IPv4 statique|Adresse Réseau IPv4|Adresse	Link-Local|Adresse IPv6 publique|Adresse	IPv6 privée|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|				
|R4|G0/1|R4 - NAT3|DHCP|192.168.122.0 /24|fe80::dd:4|2001:470:c814:5004::1|fd00:470:c814:5004::1|
|R4|G0/2|R4 - PC9|10.104.1.1|10.104.1.0 /24|fe80::dd:4|2001:470:c814:5004::2|fd00:470:c814:5004::2|

## LANs

|LAN|Adresse réseau IPv4|Passerelle IPv4|
|:-:|:-:|:-:|
|LAN R1|10.191.0.0 /24|10.191.0.1|
|LAN R2|10.192.0.0 /24|10.192.0.1|
|LAN R3|10.193.0.0 /24|10.193.0.1|
|LAN R4|10.104.1.0 /24|10.104.1.1|

