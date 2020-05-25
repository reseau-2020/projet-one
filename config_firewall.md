!
hostname R1
!
ip dhcp pool LAN
   network 192.168.59.0 255.255.255.0
   default-router 192.168.59.1
   dns-server 192.168.59.1
!
ip dhcp pool DMZ
   network 192.168.101.0 255.255.255.0
   default-router 192.168.101.1
   dns-server 192.168.101.1
!
ip domain name lan
!
ip domain-lookup
!
username root secret testtest
!
class-map type inspect match-any internet-dmz-class
 match protocol http
 match protocol https
class-map type inspect match-any icmp-class
 match protocol icmp
class-map type inspect match-any remote-access-class
 match access-group name SSH
class-map type inspect match-any dhcp-class
 match access-group name DHCP
class-map type inspect match-any dns-class
 match access-group name DNS
class-map type inspect match-any internet-trafic-class
 match protocol dns
 match protocol http
 match protocol https
 match protocol icmp
class-map type inspect match-any lan-dmz-class
 match protocol http
 match protocol https
 match protocol ssh
!
!
policy-map type inspect to-self-policy
 class type inspect remote-access-class
  pass
 class type inspect icmp-class
  inspect
 class type inspect dhcp-class
  pass
 class type inspect dns-class
  pass
 class class-default
  drop log
policy-map type inspect lan-dmz-policy
 class type inspect lan-dmz-class
  inspect
 class class-default
policy-map type inspect internet-dmz-policy
 class type inspect internet-dmz-class
  inspect
 class class-default
policy-map type inspect lan-internet-policy
 class type inspect internet-trafic-class
  inspect
 class class-default
!
zone security lan
zone security internet
zone security dmz
zone-pair security lan-internet source lan destination internet
 service-policy type inspect lan-internet-policy
zone-pair security lan-dmz source lan destination dmz
 service-policy type inspect lan-dmz-policy
zone-pair security internet-dmz source internet destination dmz
 service-policy type inspect internet-dmz-policy
zone-pair security internet-self source internet destination self
 service-policy type inspect to-self-policy
!
interface G0/1
 description Interface WAN
 ip address dhcp
 ip nat outside
 zone-member security internet
 no shutdown
!
interface G0/0
 description Interface LAN
 ip address 192.168.59.1 255.255.255.0
 ip nat inside
 zone-member security lan
 no shutdown
!
interface G0/2
 description Interface DMZ
 ip address 192.168.101.1 255.255.255.0
 zone-member security dmz
 no shutdown
!
ip dns server
ip nat inside source list LAN_NAT interface G0/1 overload
!
ip access-list extended LAN_NAT
 permit ip 192.168.59.0 0.0.0.255 any
 permit ip 192.168.101.0 0.0.0.255 any
ip access-list extended SSH
 permit tcp any any eq 22
 deny   ip any any
ip access-list extended DHCP
 permit udp any any eq 68
 deny udp any any
ip access-list extended DNS
 permit udp any any eq 53
 deny udp any any
!
line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line aux 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line vty 0 4
 login local
 transport input ssh
!
end