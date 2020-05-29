# Ajustement des politiques de pare-feu

## Sur R1 :
- Permettre à R1 de pouvoir réaliser ses tests de connectivité et de résolution de nom
```
! ajout d'une nouvelle zone-pair de la self-zone vers l'internet
! réutilisation de la service-policy déjà utilisée pour la zone-pair de l'internet vers la self-zone
configure terminal
 zone-pair security self-internet source self destination internet
   service-policy type inspect to-self-policy
   end
wr
```
- Correction des logs altérants la console de R1 (DHCP)
```
*May 28 19:46:10.318: %FW-6-DROP_PKT: Dropping udp session 0.0.0.0:68 255.255.255.255:67 
on zone-pair internet-self class class-default due to  DROP action found in policy-map with ip ident 38949
```
```
! modification de l'access-list de l'access-group DHCP
configure terminal
 ip access-list extended DHCP
! déjà fait  no permit udp any any eq 68
! déjà fait  no deny udp any any
  permit udp any eq 67 any eq 68
  permit udp any eq 68 any eq 67
  end
wr
```

## Sur R4
- Permettre à R4 de pouvoir réaliser ses tests de connectivité et de résolution de nom
```
! ajout d'une nouvelle zone-pair de la self-zone vers l'internet
! réutilisation de la service-policy déjà utilisée pour la zone-pair de l'internet vers la self-zone
configure terminal
 zone-pair security self-internet source self destination internet
   service-policy type inspect to-self-policy
   end
wr
```
- Correction des logs altérants la console de R1 (DNS et DHCP)
```
*May 28 19:46:10.318: %FW-6-DROP_PKT: Dropping udp session 0.0.0.0:68 255.255.255.255:67 
on zone-pair internet-self class class-default due to  DROP action found in policy-map with ip ident 38949
```
```
*May 28 19:48:12.605: %FW-6-DROP_PKT: Dropping udp session 1.1.1.1:53 192.168.122.162:51761 
on zone-pair internet-self class class-default due to  DROP action found in policy-map with ip ident 18527
```
```
! modification de l'access-list de l'access-group DHCP
configure terminal
 ip access-list extended DHCP
! déjà fait  no permit udp any any eq 68
! déjà fait  no deny udp any any
  permit udp any eq 67 any eq 68
  permit udp any eq 68 any eq 67
  end
wr
```
```
! modification de l'access-list de l'access-group DNS
configure terminal
 ip access-list extended DNS
  permit udp any any eq 53
  permit udp any eq 53 any
  deny udp any any
  end
wr
```
# Modification de l'adressage IPv6, Topologie Principale
- Passerelles virtuelles IPv6 VLANs, passerelle doit être identique pour chaque VLAN et différente des link local de DS1 et DS2 (voir tableur pour le choix retenu)
- Ajout des IPv6 publiques dans la topologie principale (couche Core et couche distribution => R1, R2, R3, DS1 et DS2 
- Adaptation hsrpv6 (standby, preempt... pour chaque vlan et pour chaque DS, soit 8 blocs à modifier)

```
! Configuration supplémentaire HSRP DS1 IPv6
interface vlan 10
 standby 16 priority 150
 standby 16 preempt
 standby version 2
 standby 16 ipv6 fe80::d3:1
!
interface vlan 20
 standby version 2
 standby 26 ipv6 fe80::d3:1
!
interface vlan 30
 standby 36 priority 150
 standby 36 preempt
 standby version 2
 standby 36 ipv6 fe80::d3:1
!
interface vlan 40
 standby version 2
 standby 46 ipv6 fe80::d3:1
end
wr
```
```
! Configuration supplémentaire HSRP DS2 IPv6
interface vlan 10
 standby version 2
 standby 16 ipv6 fe80::d3:1
!
interface vlan 20
 standby 26 priority 150
 standby 26 preempt
 standby version 2
 standby 26 ipv6 fe80::d3:1
!
interface vlan 30
 standby version 2
 standby 36 ipv6 fe80::d3:1
!
interface vlan 40
 standby 46 priority 150
 standby 46 preempt
 standby version 2
 standby 46 ipv6 fe80::d3:1
end
wr
```
- Modification Configuration des Machines Virtuelles Ubuntu
```
systemctl disable systemd-resolved
systemctl stop systemd-resolved
rm -f /etc/resolv.conf
echo "nameserver 1.1.1.1" >> /etc/resolv.conf
chattr +i /etc/resolv.conf
```
