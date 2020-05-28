# Configuration manuelle

Ajouter les blocs de commandes utilisés pour la configuration manuelle

## Station de contrôle (Centos-1)

Ajouter la configuration initiale de la station de contrôle (voir Guillaume)

Configuration de SNMPv3 :

            yum install net-tools.x86_64
            yum install net-snmp net-snmp-utils
            ! 
            USER=team1
            PASSWORD=testtest
            SECRET=$PASSWORD
            HOST=11.12.13.X 
            ! l'adresse HOST est l'adresse du périphérique à surveiller (adresse de l'interface liée à Switch1)
            !
            snmpwalk -v3 -l authPriv -u $USER -a SHA -A $PASSWORD -x AES -X $SECRET $HOST


## Stations de travail

**Sur PC1 à PC8** :
      
      Pour changer le nom de la machine :
          sudo echo PCx > /etc/hostname
          reboot

      Configuration du service DNS :
          echo "nameserver 1.1.1.1" >> /etc/resolv.conf

**Sur PC9** :


**Sur PC10** :


## Routeurs

**Sur R1** :

            !
            hostname R1
            !
            ip dhcp pool DMZ
             network 10.191.0.0 255.255.255.0
             default-router 10.191.0.1
             dns-server 10.191.0.1
            !
            ip domain name lan
            !
            ip domain lookup
            ip name-server 1.1.1.1
            ip dns server
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
             description Interface DMZ
             ip address 10.191.0.1 255.255.255.0
             zone-member security dmz
             no shutdown
            !
            !R1 vers R2
            !
            interface G0/2
             description Interface LAN
             ip address 10.1.1.1 255.255.255.0
             ip nat inside
             zone-member security lan
             no shutdown
            !
            !R1 vers R3
            !
            interface G0/3
             description Interface LAN
             ip address 10.1.2.1 255.255.255.0
             ip nat inside
             zone-member security lan
             no shutdown
            !
            ip access-list extended SSH
             permit tcp any any eq 22
             deny ip any any
            ip access-list extended DHCP
             permit udp any any eq 68
             deny udp any any
            ip access-list extended DNS
             permit udp any any eq 53
             deny udp any any
            !
            ! Adaptation du Pare-feu R1 pour le VPN
            !
            ip access-list extended ISAKMP_IPSEC
             permit udp any any eq isakmp
             permit ahp any any
             permit esp any any
             permit udp any any eq non500-isakmp
            class-map type inspect match-any vpn-class
             match access-group name ISAKMP_IPSEC
            policy-map type inspect to-self-policy
             class type inspect vpn-class
              inspect
              end
            !
            conf t
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
            !
            ! CONFIGURATION DU TUNNEL VPN IPSEC (entre R1 et R4)
            !
            conf t
            crypto isakmp policy 1
             encr aes 256
             authentication pre-share
             group 5
             lifetime 7200
            !
            crypto isakmp key cisco123 address 192.168.122.162
            !
            crypto ipsec transform-set to-R4-set esp-aes 256 esp-sha-hmac
            !
            crypto map cm-to-R4 1 ipsec-isakmp
             set peer 192.168.122.162
             set transform-set to-R4-set
             match address crypto-acl
            !
            interface G0/1
             crypto map cm-to-R4
            !
            ip access-list extended crypto-acl
             permit ip 10.0.0.0 0.255.255.255 10.104.1.0 0.0.0.255
            !
            ! no ip access-list standard LAN_NAT
            ip access-list extended LAN_NAT
             5 deny ip 10.0.0.0 0.255.255.255 10.104.1.0 0.0.0.255
             10 permit ip 10.0.0.0 0.255.255.255 any
            ! Pour la DMZ plus tard 20 permit ip 10.X.X.X 0.0.0.255 any ou 0.255.255.255
            end
            wr
            !
            ! CONFIGURATION DE SNMPv3
            conf t
            ip access-list extended LAN_SNMP
            permit ip 11.12.13.0 0.0.0.255 any
            exit
            snmp-server view SNMP-RO iso included
            snmp-server group ADMIN v3 priv read SNMP-RO access LAN_SNMP
            snmp-server user team1 ADMIN v3 auth sha testtest priv aes 128 testtest
            end
            wr
            !

**Sur R2** :

Ajouter la configuration initiale (voir Guillaume)

            ! CONFIGURATION DE SNMPv3
            conf t
            ip access-list extended LAN_SNMP
            permit ip 11.12.13.0 0.0.0.255 any
            exit
            snmp-server view SNMP-RO iso included
            snmp-server group ADMIN v3 priv read SNMP-RO access LAN_SNMP
            snmp-server user team1 ADMIN v3 auth sha testtest priv aes 128 testtest
            end
            wr
            !

**Sur R3** :

Ajouter la configuration initiale (voir Guillaume)

            ! CONFIGURATION DE SNMPv3
            conf t
            ip access-list extended LAN_SNMP
            permit ip 11.12.13.0 0.0.0.255 any
            exit
            snmp-server view SNMP-RO iso included
            snmp-server group ADMIN v3 priv read SNMP-RO access LAN_SNMP
            snmp-server user team1 ADMIN v3 auth sha testtest priv aes 128 testtest
            end
            wr
            !

**Sur R4** :

            conf t
            hostname R4
            enable secret testtest
            username root secret testtest
            !
            ! Configurer et sécuriser SSH
            ip domain-name lan
            crypto key generate rsa modulus 2048
            !
            ! Configurer l'adressage IPv4 et IPv6  
            interface GigabitEthernet0/1
            ip address dhcp
            ip nat outside
            ipv6 address fe80::dd:4 link-local
            ipv6 address fd00:470:c814:1004::1/64
            no shutdown
            exit
            !
            interface GigabitEthernet0/2
            ip nat inside
            ip address 10.104.1.1 255.255.255.0
            ipv6 address fe80::dd:4 link-local
            ipv6 address fd00:470:c814:1004::2/64
            no shutdown
            end
            !
            conf t
            ip domain lookup
            ip name-server 1.1.1.1
            ip dns server
            !
            ip dhcp pool LAN
            network 10.104.1.0 255.255.255.0
            default-router 10.104.1.1
            dns-server 10.104.1.1
            !
            exit
            !
            ipv6 unicast-routing
            !
            end
            wr
            !
            ! CONFIGURATION DU FIREWALL
            !
            conf t
            !
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
            policy-map type inspect lan-internet-policy
             class type inspect internet-trafic-class
              inspect
             class class-default
            !
            zone security lan4
            zone security internet
            zone-pair security lan4-internet source lan4 destination internet
             service-policy type inspect lan4-internet-policy
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
            interface G0/2
             description Interface LAN
             ip address 10.104.1.1 255.255.255.0
             zone-member security lan4
             no shutdown
            !
            ! ip access-list extended LAN_NAT (supprimer?)
            !  permit ip 10.0.0.0 0.0.0.255 any (supprimer?)
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
            ! Adaptation du Pare-feu R4 pour le VPN
            !
            ip access-list extended ISAKMP_IPSEC
             permit udp any any eq isakmp
             permit ahp any any
             permit esp any any
             permit udp any any eq non500-isakmp
            class-map type inspect match-any vpn-class
             match access-group name ISAKMP_IPSEC
            policy-map type inspect to-self-policy
             class type inspect vpn-class
              inspect
              end
            !
            conf t
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
            wr
            !
            ! CONFIGURATION DU VPN IPSEC
            ! Configuration du tunnel VPN IPSEC (entre R1 et R4)
            !
            conf t
            interface G0/2
             ip nat inside
            !
            ip route 0.0.0.0 0.0.0.0 192.168.122.1
            ! ip access-list extended LAN_NAT (supprimer?)
            !  permit ip 10.104.1.0 0.0.0.255 any (supprimer?)
            !
            ip nat inside source list LAN_NAT interface G0/1 overload
            !
            crypto isakmp policy 1
             encr aes 256
             authentication pre-share
             group 5
             lifetime 7200
            !
            crypto isakmp key cisco123 address 192.168.122.239
            !
            crypto ipsec transform-set to-R1-set esp-aes 256 esp-sha-hmac
            !
            crypto map cm-to-R1 1 ipsec-isakmp
             set peer 192.168.122.239
             set transform-set to-R1-set
             match address crypto-acl
            !
            interface G0/1
             crypto map cm-to-R1
            !
            ip access-list extended crypto-acl
             permit ip 10.104.1.0 0.0.0.255 10.0.0.0 0.255.255.255
            !
            ip access-list extended LAN_R4
             5 deny ip 10.104.1.0 0.0.0.255 10.0.0.0 0.255.255.255
             10 permit ip 10.104.1.0 0.0.0.255 any
            !
            end
            wr

## Sur les switchs Distribution (DS)

**Sur DS1** :

Ajouter la configuration initiale (voir Guillaume)


            ! CONFIGURATION DE SNMPv3
            conf t
            ip access-list extended LAN_SNMP
            permit ip 11.12.13.0 0.0.0.255 any
            exit
            snmp-server view SNMP-RO iso included
            snmp-server group ADMIN v3 priv read SNMP-RO access LAN_SNMP
            snmp-server user team1 ADMIN v3 auth sha testtest priv aes 128 testtest
            end
            wr
            !

**Sur DS2** :

Ajouter la configuration initiale (voir Guillaume)


            ! CONFIGURATION DE SNMPv3
            conf t
            ip access-list extended LAN_SNMP
            permit ip 11.12.13.0 0.0.0.255 any
            exit
            snmp-server view SNMP-RO iso included
            snmp-server group ADMIN v3 priv read SNMP-RO access LAN_SNMP
            snmp-server user team1 ADMIN v3 auth sha testtest priv aes 128 testtest
            end
            wr
            !

## Sur les switchs Access (AS)

**Sur AS1** :

Ajouter la configuration initiale (voir Guillaume)


            ! CONFIGURATION DE SNMPv3
            conf t
            ip access-list extended LAN_SNMP
            permit ip 11.12.13.0 0.0.0.255 any
            exit
            snmp-server view SNMP-RO iso included
            snmp-server group ADMIN v3 priv read SNMP-RO access LAN_SNMP
            snmp-server user team1 ADMIN v3 auth sha testtest priv aes 128 testtest
            end
            wr
            !

**Sur AS2** :

Ajouter la configuration initiale (voir Guillaume)


            ! CONFIGURATION DE SNMPv3
            conf t
            ip access-list extended LAN_SNMP
            permit ip 11.12.13.0 0.0.0.255 any
            exit
            snmp-server view SNMP-RO iso included
            snmp-server group ADMIN v3 priv read SNMP-RO access LAN_SNMP
            snmp-server user team1 ADMIN v3 auth sha testtest priv aes 128 testtest
            end
            wr
            !
