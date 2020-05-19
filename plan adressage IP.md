# Plan d'adressage

## Tripod 
|Module|Interface|Adressage IPv4 en /24|Adressage IPv6 en /64|Description/Connexion|
|:-:|:-:|:-:|:-:|:-:|
|R1|G0/2|10.1.1.1||connecté à R2|
|R1|G0/3|10.1.2.1||connecté à R3|
|R2|G0/1|10.1.1.2||connecté à R1|
|R2|G0/3|10.1.3.2||connecté à R3|
|R3|G0/1|10.1.2.2||connecté à R1|
|R3|G0/2|10.1.3.1||connecté à R2|


## Liaison Tripod-Switchblocks
|Module|Interface|Adressage IPv4 en /24|Adressage IPv6 en /64|Description/Connexion|
|:-:|:-:|:-:|:-:|:-:|
|R2|G0/2|10.3.1.1||connecté à DS1|
|R2|G0/4|10.3.11.1||connecté à DS1|
|R2|G0/5|10.3.4.1||connecté à DS2|
|R2|G0/6|10.3.44.1||connecté à DS2|
|R3|G0/3|10.3.3.1||connecté à DS2|
|R3|G0/4|10.3.33.1||connecté à DS2|
|R3|G0/5|10.3.2.1||connecté à DS1|
|R3|G0/6|10.3.22.1||connecté à DS1|
|DS1|G2/0|10.3.1.2||connecté à R2|
|DS1|G3/0|10.3.11.2||connecté à R2|
|DS1|G2/1|10.3.2.2||connecté à R3|
|DS1|G3/1|10.3.22.2||connecté à R3|
|DS2|G2/0|10.3.3.2||connecté à R3|
|DS2|G3/0|10.3.33.2||connecté à R3|
|DS2|G2/1|10.3.4.2||connecté à R2|
|DS2|G3/1|10.3.44.2||connecté à R2|

## VLANs
### Switchblocks
|Commutateur|Interface|Adresse IPV4|Adressses IPv6|
|:-:|:-:|:-:|:-:|
|DS1|VLAN10|10.2.10.252/24|fe80::d1:10 ; fd00:470:c814:1010::1 ; 2001:470:c814:1010::1|
|DS1|VLAN20|10.2.20.252/24|fe80::d1:20 ; fd00:470:c814:1020::1 ; 2001:470:c814:1020::1|
|DS1|VLAN30|10.2.30.252/24|fe80::d1:30 ; fd00:470:c814:1030::1 ; 2001:470:c814:1030::1|
|DS1|VLAN40|10.2.40.252/24|fe80::d1:40 ; fd00:470:c814:1040::1 ; 2001:470:c814:1040::1|
|DS2|VLAN10|10.2.10.253/24|fe80::d2:10 ; fd00:470:c814:1010::2 ; 2001:470:c814:1010::2|
|DS2|VLAN20|10.2.20.253/24|fe80::d2:20 ; fd00:470:c814:1020::2 ; 2001:470:c814:1020::2|
|DS2|VLAN30|10.2.30.253/24|fe80::d2:30 ; fd00:470:c814:1030::2 ; 2001:470:c814:1030::2|
|DS2|VLAN40|10.2.40.253/24|fe80::d2:40 ; fd00:470:c814:1040::2 ; 2001:470:c814:1040::2|

### HSRP
|VLAN|Port Access (AS1 et AS2)|Passerelle par défaut|IPv4|IPv6 Virtuelle|
|:-:|:-:|:-:|:-:|:-:|
|VLAN10|G2/0|10.2.10.254/24|10.2.10.0/24|fe80::d:10|
|VLAN20|G2/1|10.2.20.254/24|10.2.20.0/24|fe80::d:20|
|VLAN30|G2/2|10.2.30.254/24|10.2.30.0/24|fe80::d:30|
|VLAN40|G2/3|10.2.40.254/24|10.2.40.0/24|fe80::d:40|
|VLAN99|VLAN natif|-|-|-|

Besoin d'un Vlan100 pour un Vlan de Gestion?

### Etherchannel
|PortChannel|Ports Physiques|Commutateurs|
|:-:|:-:|:-:|
|PO1|G0/0,G1/0|AS1-DS1|
|PO2|G0/1,G1/1|AS1-DS2|
|PO3|G0/2,G1/2|DS1-DS2|
|PO4|G0/0,G1/0|AS2-DS2|
|PO5|G0/1,G1/1|AS2-DS1|

### Spanning-Tree
|VLANs|DS1|DS2|
|:-:|:-:|:-:|
|VLANs 10,30,99|Root Primary|Root Secondary|
|VLANs 20,40|Root Secondary|Root Primary|

