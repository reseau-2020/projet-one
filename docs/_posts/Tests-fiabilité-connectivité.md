# Test de fiabilité et de connectivité

## Tests de fiabilité

### IPv4 Rapid Spanning-Tree Portfast (RSTP) : redondance de liens

On lance un ping continu de PC8 (VLAN40) vers sa passerelle sur DS2 (10.2.40.253)
On coupe la liaison entre AS2 et DS2 (Po4) puis on la remonte :

        DS2#conf t
        Enter configuration commands, one per line.  End with CNTL/Z.
        DS2(config)#interface po4
        DS2(config-if)#shutdown
        
        DS2(config-if)#no shutdown
        DS2(config-if)#exit

        root@PC8:~# ping 10.2.40.253
        PING 10.2.40.253 (10.2.40.253) 56(84) bytes of data.
        64 bytes from 10.2.40.253: icmp_seq=1 ttl=255 time=3.41 ms
        64 bytes from 10.2.40.253: icmp_seq=2 ttl=255 time=3.61 ms
        64 bytes from 10.2.40.253: icmp_seq=3 ttl=255 time=5.17 ms
        64 bytes from 10.2.40.253: icmp_seq=4 ttl=255 time=3.56 ms
        64 bytes from 10.2.40.253: icmp_seq=5 ttl=255 time=3.47 ms
        64 bytes from 10.2.40.253: icmp_seq=6 ttl=255 time=3.66 ms
        64 bytes from 10.2.40.253: icmp_seq=7 ttl=255 time=3.32 ms
        64 bytes from 10.2.40.253: icmp_seq=8 ttl=255 time=3.66 ms
        64 bytes from 10.2.40.253: icmp_seq=9 ttl=255 time=3.08 ms
        64 bytes from 10.2.40.253: icmp_seq=10 ttl=255 time=4.16 ms
        64 bytes from 10.2.40.253: icmp_seq=11 ttl=255 time=3.78 ms
        64 bytes from 10.2.40.253: icmp_seq=12 ttl=255 time=3.75 ms
        64 bytes from 10.2.40.253: icmp_seq=13 ttl=255 time=3.55 ms
        64 bytes from 10.2.40.253: icmp_seq=14 ttl=255 time=3.50 ms
        64 bytes from 10.2.40.253: icmp_seq=15 ttl=255 time=3.24 ms
        64 bytes from 10.2.40.253: icmp_seq=16 ttl=255 time=3.65 ms
        64 bytes from 10.2.40.253: icmp_seq=17 ttl=255 time=4.08 ms
        64 bytes from 10.2.40.253: icmp_seq=18 ttl=255 time=3.88 ms
        64 bytes from 10.2.40.253: icmp_seq=19 ttl=255 time=3.87 ms
        64 bytes from 10.2.40.253: icmp_seq=20 ttl=255 time=3.35 ms
        64 bytes from 10.2.40.253: icmp_seq=21 ttl=255 time=3.02 ms
        64 bytes from 10.2.40.253: icmp_seq=22 ttl=255 time=3.11 ms
        ** 64 bytes from 10.2.40.253: icmp_seq=23 ttl=255 time=3.41 ms **
        ** 64 bytes from 10.2.40.253: icmp_seq=28 ttl=255 time=9.36 ms **
        64 bytes from 10.2.40.253: icmp_seq=29 ttl=255 time=6.36 ms
        64 bytes from 10.2.40.253: icmp_seq=30 ttl=255 time=5.84 ms
        64 bytes from 10.2.40.253: icmp_seq=31 ttl=255 time=7.50 ms
        64 bytes from 10.2.40.253: icmp_seq=32 ttl=255 time=5.46 ms
        ^C
        --- 10.2.40.253 ping statistics ---
        112 packets transmitted, 108 received, 3% packet loss, time 111262ms
        rtt min/avg/max/mdev = 3.027/5.151/9.414/1.323 ms


On lance un ping continu de PC8 (VLAN40) vers PC3 (VLAN30, 10.2.30.51)
On coupe la liaison entre AS2 et DS2 (Po4) puis on la remonte :

        DS2(config)#interface po4
        DS2(config-if)#shutdown
        
        DS2(config-if)#no shutdown
        DS2(config-if)#exit

        root@PC8:~# ping 10.2.30.51
        PING 10.2.30.51 (10.2.30.51) 56(84) bytes of data.
        64 bytes from 10.2.30.51: icmp_seq=1 ttl=63 time=7.60 ms
        64 bytes from 10.2.30.51: icmp_seq=2 ttl=63 time=7.17 ms
        64 bytes from 10.2.30.51: icmp_seq=3 ttl=63 time=9.80 ms
        64 bytes from 10.2.30.51: icmp_seq=4 ttl=63 time=7.15 ms
        64 bytes from 10.2.30.51: icmp_seq=5 ttl=63 time=6.90 ms
        64 bytes from 10.2.30.51: icmp_seq=6 ttl=63 time=7.58 ms
        64 bytes from 10.2.30.51: icmp_seq=7 ttl=63 time=6.77 ms
        64 bytes from 10.2.30.51: icmp_seq=8 ttl=63 time=7.00 ms
        64 bytes from 10.2.30.51: icmp_seq=9 ttl=63 time=7.87 ms
        64 bytes from 10.2.30.51: icmp_seq=10 ttl=63 time=7.86 ms
        64 bytes from 10.2.30.51: icmp_seq=11 ttl=63 time=8.41 ms
        64 bytes from 10.2.30.51: icmp_seq=12 ttl=63 time=8.46 ms
        ** 64 bytes from 10.2.30.51: icmp_seq=13 ttl=63 time=8.23 ms **
        ** 64 bytes from 10.2.30.51: icmp_seq=20 ttl=63 time=9.51 ms **
        64 bytes from 10.2.30.51: icmp_seq=21 ttl=63 time=8.47 ms
        64 bytes from 10.2.30.51: icmp_seq=22 ttl=63 time=7.23 ms
        64 bytes from 10.2.30.51: icmp_seq=23 ttl=63 time=11.5 ms
        64 bytes from 10.2.30.51: icmp_seq=24 ttl=63 time=9.41 ms
        64 bytes from 10.2.30.51: icmp_seq=25 ttl=63 time=9.30 ms
        64 bytes from 10.2.30.51: icmp_seq=26 ttl=63 time=8.62 ms
        64 bytes from 10.2.30.51: icmp_seq=27 ttl=63 time=9.91 ms
        64 bytes from 10.2.30.51: icmp_seq=28 ttl=63 time=8.56 ms
        64 bytes from 10.2.30.51: icmp_seq=29 ttl=63 time=9.20 ms
        64 bytes from 10.2.30.51: icmp_seq=19 ttl=63 time=10207 ms
        64 bytes from 10.2.30.51: icmp_seq=30 ttl=63 time=8.70 ms
        64 bytes from 10.2.30.51: icmp_seq=31 ttl=63 time=9.78 ms
        64 bytes from 10.2.30.51: icmp_seq=32 ttl=63 time=8.81 ms
        ^C

        --- 10.2.30.51 ping statistics ---
        32 packets transmitted, 27 received, 15% packet loss, time 31169ms
        rtt min/avg/max/mdev = 6.774/386.203/10207.592/1926.133 ms, pipe 11

On lance un ping de PC1 (VLAN10) vers PC7 (VLAN30, 10.2.30.1)
On coupe la liaison entre DS1 et AS1 (Po1) puis on la remonte :

        DS1(config)#interface po1
        DS1(config-if)#shutdown
        
        DS1(config-if)#no shutdown
        DS1(config-if)#exit

        root@PC1:~# ping 10.2.30.1
        PING 10.2.30.1 (10.2.30.1) 56(84) bytes of data.
        64 bytes from 10.2.30.1: icmp_seq=1 ttl=63 time=9.18 ms
        64 bytes from 10.2.30.1: icmp_seq=2 ttl=63 time=9.72 ms
        64 bytes from 10.2.30.1: icmp_seq=3 ttl=63 time=8.06 ms
        64 bytes from 10.2.30.1: icmp_seq=4 ttl=63 time=8.23 ms
        64 bytes from 10.2.30.1: icmp_seq=5 ttl=63 time=9.67 ms
        64 bytes from 10.2.30.1: icmp_seq=6 ttl=63 time=9.62 ms
        64 bytes from 10.2.30.1: icmp_seq=7 ttl=63 time=9.05 ms
        64 bytes from 10.2.30.1: icmp_seq=8 ttl=63 time=8.68 ms
        64 bytes from 10.2.30.1: icmp_seq=9 ttl=63 time=10.1 ms
        64 bytes from 10.2.30.1: icmp_seq=10 ttl=63 time=8.33 ms
        64 bytes from 10.2.30.1: icmp_seq=11 ttl=63 time=10.0 ms
        64 bytes from 10.2.30.1: icmp_seq=12 ttl=63 time=9.05 ms
        64 bytes from 10.2.30.1: icmp_seq=13 ttl=63 time=9.82 ms
        64 bytes from 10.2.30.1: icmp_seq=14 ttl=63 time=10.2 ms
        ** 64 bytes from 10.2.30.1: icmp_seq=15 ttl=63 time=9.54 ms **
        ** 64 bytes from 10.2.30.1: icmp_seq=20 ttl=63 time=7.86 ms **
        64 bytes from 10.2.30.1: icmp_seq=21 ttl=63 time=7.98 ms
        64 bytes from 10.2.30.1: icmp_seq=22 ttl=63 time=6.92 ms
        64 bytes from 10.2.30.1: icmp_seq=23 ttl=63 time=8.05 ms
        64 bytes from 10.2.30.1: icmp_seq=24 ttl=63 time=8.15 ms
        64 bytes from 10.2.30.1: icmp_seq=25 ttl=63 time=8.71 ms
        64 bytes from 10.2.30.1: icmp_seq=26 ttl=63 time=7.26 ms
        64 bytes from 10.2.30.1: icmp_seq=27 ttl=63 time=7.88 ms
        64 bytes from 10.2.30.1: icmp_seq=28 ttl=63 time=7.49 ms
        64 bytes from 10.2.30.1: icmp_seq=29 ttl=63 time=7.77 ms
        64 bytes from 10.2.30.1: icmp_seq=30 ttl=63 time=6.87 ms
        64 bytes from 10.2.30.1: icmp_seq=31 ttl=63 time=7.45 ms
        64 bytes from 10.2.30.1: icmp_seq=32 ttl=63 time=7.76 ms
        64 bytes from 10.2.30.1: icmp_seq=33 ttl=63 time=6.78 ms
        64 bytes from 10.2.30.1: icmp_seq=34 ttl=63 time=6.98 ms
        ^C
        --- 10.2.30.1 ping statistics ---
        34 packets transmitted, 30 received, 11% packet loss, time 33138ms
        rtt min/avg/max/mdev = 6.789/8.447/10.246/1.052 ms

On lance un ping de PC1 (VLAN10) vers PC7 (VLAN30, 10.2.30.1)
On coupe la liaison entre DS1 et AS2 (Po5) puis on la remonte :
        
        DS1(config)#interface po5
        DS1(config-if)#shutdown
        
        DS1(config-if)#no shutdown
        DS1(config-if)#exit

        root@PC1:~# ping 10.2.30.1
        PING 10.2.30.1 (10.2.30.1) 56(84) bytes of data.
        64 bytes from 10.2.30.1: icmp_seq=1 ttl=63 time=9.42 ms
        64 bytes from 10.2.30.1: icmp_seq=2 ttl=63 time=8.57 ms
        64 bytes from 10.2.30.1: icmp_seq=3 ttl=63 time=8.62 ms
        64 bytes from 10.2.30.1: icmp_seq=4 ttl=63 time=9.32 ms
        64 bytes from 10.2.30.1: icmp_seq=5 ttl=63 time=9.37 ms
        64 bytes from 10.2.30.1: icmp_seq=6 ttl=63 time=9.54 ms
        64 bytes from 10.2.30.1: icmp_seq=7 ttl=63 time=9.44 ms
        64 bytes from 10.2.30.1: icmp_seq=8 ttl=63 time=24.5 ms
        64 bytes from 10.2.30.1: icmp_seq=9 ttl=63 time=9.48 ms
        64 bytes from 10.2.30.1: icmp_seq=10 ttl=63 time=8.82 ms
        64 bytes from 10.2.30.1: icmp_seq=11 ttl=63 time=8.99 ms
        64 bytes from 10.2.30.1: icmp_seq=12 ttl=63 time=9.51 ms
        64 bytes from 10.2.30.1: icmp_seq=13 ttl=63 time=9.18 ms
        64 bytes from 10.2.30.1: icmp_seq=14 ttl=63 time=10.3 ms
        64 bytes from 10.2.30.1: icmp_seq=15 ttl=63 time=9.84 ms
        64 bytes from 10.2.30.1: icmp_seq=16 ttl=63 time=9.24 ms
        64 bytes from 10.2.30.1: icmp_seq=17 ttl=63 time=10.1 ms
        64 bytes from 10.2.30.1: icmp_seq=18 ttl=63 time=10.2 ms
        64 bytes from 10.2.30.1: icmp_seq=19 ttl=63 time=9.45 ms
        ** 64 bytes from 10.2.30.1: icmp_seq=20 ttl=63 time=9.95 ms **
        ** 64 bytes from 10.2.30.1: icmp_seq=26 ttl=63 time=8.20 ms **
        64 bytes from 10.2.30.1: icmp_seq=27 ttl=63 time=7.98 ms
        64 bytes from 10.2.30.1: icmp_seq=28 ttl=63 time=8.05 ms
        64 bytes from 10.2.30.1: icmp_seq=29 ttl=63 time=6.43 ms
        64 bytes from 10.2.30.1: icmp_seq=30 ttl=63 time=7.13 ms
        64 bytes from 10.2.30.1: icmp_seq=31 ttl=63 time=8.03 ms
        64 bytes from 10.2.30.1: icmp_seq=32 ttl=63 time=7.22 ms
        64 bytes from 10.2.30.1: icmp_seq=33 ttl=63 time=8.12 ms
        64 bytes from 10.2.30.1: icmp_seq=34 ttl=63 time=7.70 ms
        64 bytes from 10.2.30.1: icmp_seq=35 ttl=63 time=7.80 ms
        ^C
        --- 10.2.30.1 ping statistics ---
        35 packets transmitted, 30 received, 14% packet loss, time 34162ms
        rtt min/avg/max/mdev = 6.439/9.359/24.555/2.983 ms


On lance un ping continu de PC2 (VLAN20) vers sa passerelle sur DS2 (10.2.20.253)
On coupe la liaison entre AS1 et DS2 (Po2) puis on la remonte :

        DS2#conf t
        Enter configuration commands, one per line.  End with CNTL/Z.
        DS2(config)#interface po2
        DS2(config-if)#shutdown
        
        DS2(config-if)#no shutdown
        DS2(config-if)#exit

        root@PC2:~# ping 10.2.20.253
        PING 10.2.20.253 (10.2.20.253) 56(84) bytes of data.
        64 bytes from 10.2.20.253: icmp_seq=1 ttl=255 time=3.52 ms
        64 bytes from 10.2.20.253: icmp_seq=2 ttl=255 time=3.59 ms
        64 bytes from 10.2.20.253: icmp_seq=3 ttl=255 time=4.24 ms
        64 bytes from 10.2.20.253: icmp_seq=4 ttl=255 time=3.55 ms
        64 bytes from 10.2.20.253: icmp_seq=5 ttl=255 time=3.93 ms
        64 bytes from 10.2.20.253: icmp_seq=6 ttl=255 time=3.57 ms
        64 bytes from 10.2.20.253: icmp_seq=7 ttl=255 time=3.67 ms
        64 bytes from 10.2.20.253: icmp_seq=8 ttl=255 time=3.22 ms
        64 bytes from 10.2.20.253: icmp_seq=9 ttl=255 time=3.93 ms
        64 bytes from 10.2.20.253: icmp_seq=10 ttl=255 time=3.72 ms
        64 bytes from 10.2.20.253: icmp_seq=11 ttl=255 time=3.73 ms
        64 bytes from 10.2.20.253: icmp_seq=12 ttl=255 time=4.30 ms
        64 bytes from 10.2.20.253: icmp_seq=13 ttl=255 time=3.81 ms
        64 bytes from 10.2.20.253: icmp_seq=14 ttl=255 time=3.77 ms
        64 bytes from 10.2.20.253: icmp_seq=15 ttl=255 time=3.97 ms
        64 bytes from 10.2.20.253: icmp_seq=16 ttl=255 time=4.32 ms
        64 bytes from 10.2.20.253: icmp_seq=17 ttl=255 time=3.81 ms
        64 bytes from 10.2.20.253: icmp_seq=18 ttl=255 time=3.88 ms
        64 bytes from 10.2.20.253: icmp_seq=19 ttl=255 time=3.85 ms
        64 bytes from 10.2.20.253: icmp_seq=20 ttl=255 time=3.58 ms
        ** 64 bytes from 10.2.20.253: icmp_seq=21 ttl=255 time=3.32 ms **
        ** 64 bytes from 10.2.20.253: icmp_seq=26 ttl=255 time=5.66 ms **
        64 bytes from 10.2.20.253: icmp_seq=27 ttl=255 time=6.25 ms
        64 bytes from 10.2.20.253: icmp_seq=28 ttl=255 time=5.82 ms
        64 bytes from 10.2.20.253: icmp_seq=29 ttl=255 time=5.37 ms
        64 bytes from 10.2.20.253: icmp_seq=30 ttl=255 time=5.56 ms
        64 bytes from 10.2.20.253: icmp_seq=31 ttl=255 time=6.23 ms
        64 bytes from 10.2.20.253: icmp_seq=32 ttl=255 time=5.85 ms
        64 bytes from 10.2.20.253: icmp_seq=33 ttl=255 time=4.97 ms
        64 bytes from 10.2.20.253: icmp_seq=34 ttl=255 time=5.84 ms
        ^C

        --- 10.2.20.253 ping statistics ---
        34 packets transmitted, 30 received, 11% packet loss, time 33145ms
        rtt min/avg/max/mdev = 3.221/4.366/6.258/0.948 ms

On lance un ping continu de PC2 (VLAN20) vers PC6 (10.2.20.51)
On coupe la liaison entre AS1 et DS2 (Po2) puis on la remonte :

        DS2#conf t
        Enter configuration commands, one per line.  End with CNTL/Z.
        DS2(config)#interface po2
        DS2(config-if)#shutdown
        
        DS2(config-if)#no shutdown
        DS2(config-if)#exit

        root@PC2:~# ping 10.2.20.51
        PING 10.2.20.51 (10.2.20.51) 56(84) bytes of data.
        64 bytes from 10.2.20.51: icmp_seq=1 ttl=64 time=10.3 ms
        64 bytes from 10.2.20.51: icmp_seq=2 ttl=64 time=6.18 ms
        64 bytes from 10.2.20.51: icmp_seq=3 ttl=64 time=6.77 ms
        64 bytes from 10.2.20.51: icmp_seq=4 ttl=64 time=6.26 ms
        64 bytes from 10.2.20.51: icmp_seq=5 ttl=64 time=5.25 ms
        64 bytes from 10.2.20.51: icmp_seq=6 ttl=64 time=6.05 ms
        64 bytes from 10.2.20.51: icmp_seq=7 ttl=64 time=5.36 ms
        64 bytes from 10.2.20.51: icmp_seq=8 ttl=64 time=5.33 ms
        64 bytes from 10.2.20.51: icmp_seq=9 ttl=64 time=6.03 ms
        64 bytes from 10.2.20.51: icmp_seq=10 ttl=64 time=6.34 ms
        64 bytes from 10.2.20.51: icmp_seq=11 ttl=64 time=6.40 ms
        64 bytes from 10.2.20.51: icmp_seq=12 ttl=64 time=5.89 ms
        64 bytes from 10.2.20.51: icmp_seq=13 ttl=64 time=6.02 ms
        64 bytes from 10.2.20.51: icmp_seq=14 ttl=64 time=6.26 ms
        64 bytes from 10.2.20.51: icmp_seq=15 ttl=64 time=4.86 ms
        64 bytes from 10.2.20.51: icmp_seq=16 ttl=64 time=5.40 ms
        64 bytes from 10.2.20.51: icmp_seq=17 ttl=64 time=6.54 ms
        ** 64 bytes from 10.2.20.51: icmp_seq=18 ttl=64 time=5.52 ms **
        ** 64 bytes from 10.2.20.51: icmp_seq=23 ttl=64 time=7.25 ms **
        64 bytes from 10.2.20.51: icmp_seq=24 ttl=64 time=7.19 ms
        64 bytes from 10.2.20.51: icmp_seq=25 ttl=64 time=7.47 ms
        64 bytes from 10.2.20.51: icmp_seq=26 ttl=64 time=7.42 ms
        64 bytes from 10.2.20.51: icmp_seq=27 ttl=64 time=6.57 ms
        64 bytes from 10.2.20.51: icmp_seq=28 ttl=64 time=7.82 ms
        64 bytes from 10.2.20.51: icmp_seq=29 ttl=64 time=8.07 ms
        64 bytes from 10.2.20.51: icmp_seq=30 ttl=64 time=8.26 ms
        64 bytes from 10.2.20.51: icmp_seq=31 ttl=64 time=7.57 ms
        64 bytes from 10.2.20.51: icmp_seq=32 ttl=64 time=172 ms
        64 bytes from 10.2.20.51: icmp_seq=33 ttl=64 time=7.06 ms
        ^C
        --- 10.2.20.51 ping statistics ---
        33 packets transmitted, 29 received, 12% packet loss, time 32137ms
        rtt min/avg/max/mdev = 4.869/12.362/172.945/30.368 ms

On lance un ping continu de PC2 (VLAN20) vers PC4 (VLAN40, 10.2.40.1)
On coupe la liaison entre AS1 et DS2 (Po2) puis on la remonte :

        DS2#conf t
        Enter configuration commands, one per line.  End with CNTL/Z.
        DS2(config)#interface po2
        DS2(config-if)#shutdown
        
        DS2(config-if)#no shutdown
        DS2(config-if)#exit

        root@PC2:~# ping 10.2.40.1
        PING 10.2.40.1 (10.2.40.1) 56(84) bytes of data.
        64 bytes from 10.2.40.1: icmp_seq=1 ttl=63 time=5.87 ms
        64 bytes from 10.2.40.1: icmp_seq=2 ttl=63 time=5.05 ms
        64 bytes from 10.2.40.1: icmp_seq=3 ttl=63 time=5.54 ms
        64 bytes from 10.2.40.1: icmp_seq=4 ttl=63 time=5.24 ms
        64 bytes from 10.2.40.1: icmp_seq=5 ttl=63 time=5.89 ms
        64 bytes from 10.2.40.1: icmp_seq=6 ttl=63 time=6.05 ms
        64 bytes from 10.2.40.1: icmp_seq=7 ttl=63 time=5.34 ms
        64 bytes from 10.2.40.1: icmp_seq=8 ttl=63 time=5.60 ms
        64 bytes from 10.2.40.1: icmp_seq=9 ttl=63 time=6.10 ms
        64 bytes from 10.2.40.1: icmp_seq=10 ttl=63 time=7.26 ms
        64 bytes from 10.2.40.1: icmp_seq=11 ttl=63 time=5.55 ms
        64 bytes from 10.2.40.1: icmp_seq=12 ttl=63 time=6.08 ms
        64 bytes from 10.2.40.1: icmp_seq=13 ttl=63 time=5.32 ms
        64 bytes from 10.2.40.1: icmp_seq=14 ttl=63 time=6.07 ms
        ** 64 bytes from 10.2.40.1: icmp_seq=15 ttl=63 time=5.62 ms **
        ** 64 bytes from 10.2.40.1: icmp_seq=21 ttl=63 time=8.44 ms **
        64 bytes from 10.2.40.1: icmp_seq=22 ttl=63 time=8.21 ms
        64 bytes from 10.2.40.1: icmp_seq=23 ttl=63 time=8.63 ms
        64 bytes from 10.2.40.1: icmp_seq=24 ttl=63 time=8.97 ms
        64 bytes from 10.2.40.1: icmp_seq=25 ttl=63 time=9.87 ms
        64 bytes from 10.2.40.1: icmp_seq=26 ttl=63 time=9.16 ms
        64 bytes from 10.2.40.1: icmp_seq=27 ttl=63 time=8.69 ms
        64 bytes from 10.2.40.1: icmp_seq=28 ttl=63 time=10.8 ms
        64 bytes from 10.2.40.1: icmp_seq=29 ttl=63 time=9.61 ms
        64 bytes from 10.2.40.1: icmp_seq=30 ttl=63 time=10.0 ms
        ^C
        --- 10.2.40.1 ping statistics ---
        30 packets transmitted, 25 received, 16% packet loss, time 29153ms
        rtt min/avg/max/mdev = 5.056/7.169/10.894/1.826 ms

On lance un ping continu depuis PC5 (VLAN10) vers sa passerelle DS1.
On coupe la liaison entre AS2 et DS1 (Po5) puis on la remonte :

        root@PC5:~# ping 10.2.10.252
        PING 10.2.10.252 (10.2.10.252) 56(84) bytes of data.
        64 bytes from 10.2.10.252: icmp_seq=2 ttl=255 time=3.09 ms
        64 bytes from 10.2.10.252: icmp_seq=3 ttl=255 time=3.44 ms
        64 bytes from 10.2.10.252: icmp_seq=4 ttl=255 time=3.69 ms
        64 bytes from 10.2.10.252: icmp_seq=5 ttl=255 time=3.40 ms
        64 bytes from 10.2.10.252: icmp_seq=6 ttl=255 time=3.77 ms
        64 bytes from 10.2.10.252: icmp_seq=7 ttl=255 time=3.30 ms
        64 bytes from 10.2.10.252: icmp_seq=8 ttl=255 time=3.53 ms
        64 bytes from 10.2.10.252: icmp_seq=9 ttl=255 time=4.14 ms
        64 bytes from 10.2.10.252: icmp_seq=10 ttl=255 time=3.81 ms
        64 bytes from 10.2.10.252: icmp_seq=11 ttl=255 time=3.50 ms
        64 bytes from 10.2.10.252: icmp_seq=12 ttl=255 time=4.99 ms
        64 bytes from 10.2.10.252: icmp_seq=13 ttl=255 time=4.66 ms
        64 bytes from 10.2.10.252: icmp_seq=14 ttl=255 time=3.36 ms
        ** 64 bytes from 10.2.10.252: icmp_seq=15 ttl=255 time=3.41 ms**
        ** 64 bytes from 10.2.10.252: icmp_seq=21 ttl=255 time=4.90 ms**
        64 bytes from 10.2.10.252: icmp_seq=22 ttl=255 time=6.19 ms
        64 bytes from 10.2.10.252: icmp_seq=23 ttl=255 time=5.11 ms
        64 bytes from 10.2.10.252: icmp_seq=24 ttl=255 time=5.71 ms
        64 bytes from 10.2.10.252: icmp_seq=25 ttl=255 time=5.57 ms
        64 bytes from 10.2.10.252: icmp_seq=26 ttl=255 time=5.53 ms
        64 bytes from 10.2.10.252: icmp_seq=27 ttl=255 time=5.52 ms
        64 bytes from 10.2.10.252: icmp_seq=28 ttl=255 time=5.18 ms
        64 bytes from 10.2.10.252: icmp_seq=29 ttl=255 time=5.75 ms
        64 bytes from 10.2.10.252: icmp_seq=30 ttl=255 time=5.83 ms
        64 bytes from 10.2.10.252: icmp_seq=31 ttl=255 time=5.76 ms
        64 bytes from 10.2.10.252: icmp_seq=32 ttl=255 time=6.10 ms
        64 bytes from 10.2.10.252: icmp_seq=33 ttl=255 time=4.96 ms
        64 bytes from 10.2.10.252: icmp_seq=34 ttl=255 time=5.16 ms
        64 bytes from 10.2.10.252: icmp_seq=35 ttl=255 time=5.94 ms
        64 bytes from 10.2.10.252: icmp_seq=36 ttl=255 time=5.07 ms
        64 bytes from 10.2.10.252: icmp_seq=37 ttl=255 time=5.52 ms
        64 bytes from 10.2.10.252: icmp_seq=38 ttl=255 time=5.83 ms
        ^C
        --- 10.2.10.252 ping statistics ---
        38 packets transmitted, 32 received, 15% packet loss, time 37196ms
        rtt min/avg/max/mdev = 3.099/4.746/6.194/1.005 ms


### IPv6 Rapid Spanning-Tree Portfast (RSTP) : redondance de liens

Nous avons rencontré quelques problème lors des tests de la redondance de liens (RSTP) en IPv6. En effectuant des pings d'un PC à un autre ou d'un PC vers une passerelle, il se trouve que le relai n'est pas pris. Par manque de temps, nous n'avons pas pu résoudre le problème. 


### IPv4 Hot Standby Router Protocol (HSRP): redondance de passerelle

On lance un ping continu de PC8 (VLAN40) vers sa passerelle virtuelle sur DS2 (10.2.40.254.
On éteint DS2 puis on le rallume.

        root@PC8:~# ping 10.2.40.254
        PING 10.2.40.254 (10.2.40.254) 56(84) bytes of data.
        64 bytes from 10.2.40.254: icmp_seq=1 ttl=255 time=9.24 ms
        64 bytes from 10.2.40.254: icmp_seq=2 ttl=255 time=3.32 ms
        64 bytes from 10.2.40.254: icmp_seq=3 ttl=255 time=4.00 ms
        64 bytes from 10.2.40.254: icmp_seq=4 ttl=255 time=4.38 ms
        64 bytes from 10.2.40.254: icmp_seq=5 ttl=255 time=4.18 ms
        64 bytes from 10.2.40.254: icmp_seq=6 ttl=255 time=3.35 ms
        64 bytes from 10.2.40.254: icmp_seq=7 ttl=255 time=4.26 ms
        64 bytes from 10.2.40.254: icmp_seq=8 ttl=255 time=3.90 ms
        64 bytes from 10.2.40.254: icmp_seq=9 ttl=255 time=3.85 ms
        64 bytes from 10.2.40.254: icmp_seq=10 ttl=255 time=3.92 ms
        64 bytes from 10.2.40.254: icmp_seq=11 ttl=255 time=3.77 ms
        ** 64 bytes from 10.2.40.254: icmp_seq=12 ttl=255 time=3.99 ms **
        ** 64 bytes from 10.2.40.254: icmp_seq=24 ttl=255 time=3.50 ms **
        64 bytes from 10.2.40.254: icmp_seq=25 ttl=255 time=5.24 ms
        64 bytes from 10.2.40.254: icmp_seq=26 ttl=255 time=3.59 ms
        64 bytes from 10.2.40.254: icmp_seq=27 ttl=255 time=3.75 ms
        64 bytes from 10.2.40.254: icmp_seq=28 ttl=255 time=4.13 ms
        64 bytes from 10.2.40.254: icmp_seq=29 ttl=255 time=3.71 ms
        64 bytes from 10.2.40.254: icmp_seq=30 ttl=255 time=3.43 ms
        64 bytes from 10.2.40.254: icmp_seq=31 ttl=255 time=4.18 ms
        64 bytes from 10.2.40.254: icmp_seq=32 ttl=255 time=3.66 ms
        64 bytes from 10.2.40.254: icmp_seq=33 ttl=255 time=4.12 ms
        64 bytes from 10.2.40.254: icmp_seq=34 ttl=255 time=3.92 ms
        64 bytes from 10.2.40.254: icmp_seq=35 ttl=255 time=3.73 ms
        64 bytes from 10.2.40.254: icmp_seq=36 ttl=255 time=3.84 ms
        64 bytes from 10.2.40.254: icmp_seq=37 ttl=255 time=4.05 ms
        64 bytes from 10.2.40.254: icmp_seq=38 ttl=255 time=3.57 ms
        64 bytes from 10.2.40.254: icmp_seq=39 ttl=255 time=3.55 ms
        64 bytes from 10.2.40.254: icmp_seq=40 ttl=255 time=4.05 ms
        64 bytes from 10.2.40.254: icmp_seq=41 ttl=255 time=4.02 ms
        64 bytes from 10.2.40.254: icmp_seq=42 ttl=255 time=3.88 ms
        64 bytes from 10.2.40.254: icmp_seq=43 ttl=255 time=3.73 ms
        64 bytes from 10.2.40.254: icmp_seq=44 ttl=255 time=4.27 ms
        64 bytes from 10.2.40.254: icmp_seq=45 ttl=255 time=3.32 ms
        ^C
        --- 10.2.40.254 ping statistics ---
        45 packets transmitted, 34 received, 24% packet loss, time 44294ms
        rtt min/avg/max/mdev = 3.320/4.044/9.240/0.978 ms


On lance un ping continu de PC8 (VLAN40) vers PC2 (10.2.20.1).
On éteint DS2 puis on le rallume.

        root@PC8:~# ping 10.2.20.1
        PING 10.2.20.1 (10.2.20.1) 56(84) bytes of data.
        64 bytes from 10.2.20.1: icmp_seq=1 ttl=63 time=6.64 ms
        64 bytes from 10.2.20.1: icmp_seq=2 ttl=63 time=6.19 ms
        64 bytes from 10.2.20.1: icmp_seq=3 ttl=63 time=5.56 ms
        64 bytes from 10.2.20.1: icmp_seq=4 ttl=63 time=6.02 ms
        64 bytes from 10.2.20.1: icmp_seq=5 ttl=63 time=5.04 ms
        64 bytes from 10.2.20.1: icmp_seq=6 ttl=63 time=5.37 ms
        64 bytes from 10.2.20.1: icmp_seq=7 ttl=63 time=5.83 ms
        64 bytes from 10.2.20.1: icmp_seq=8 ttl=63 time=5.79 ms
        64 bytes from 10.2.20.1: icmp_seq=9 ttl=63 time=6.27 ms
        64 bytes from 10.2.20.1: icmp_seq=10 ttl=63 time=6.61 ms
        ** 64 bytes from 10.2.20.1: icmp_seq=11 ttl=63 time=6.53 ms **
        ** 64 bytes from 10.2.20.1: icmp_seq=22 ttl=63 time=8.83 ms **
        64 bytes from 10.2.20.1: icmp_seq=23 ttl=63 time=5.71 ms
        64 bytes from 10.2.20.1: icmp_seq=24 ttl=63 time=5.90 ms
        64 bytes from 10.2.20.1: icmp_seq=25 ttl=63 time=5.17 ms
        64 bytes from 10.2.20.1: icmp_seq=26 ttl=63 time=5.73 ms
        ^C
        --- 10.2.20.1 ping statistics ---
        26 packets transmitted, 16 received, 38% packet loss, time 25269ms
        rtt min/avg/max/mdev = 5.047/6.079/8.838/0.849 ms


On lance un ping continu de PC1 (VLAN10) vers PC7 (10.2.30.1).
On éteint DS1 puis on le rallume.

        root@PC1:~# ping 10.2.30.1
        PING 10.2.30.1 (10.2.30.1) 56(84) bytes of data.
        64 bytes from 10.2.30.1: icmp_seq=2 ttl=63 time=5.76 ms
        64 bytes from 10.2.30.1: icmp_seq=3 ttl=63 time=5.89 ms
        64 bytes from 10.2.30.1: icmp_seq=4 ttl=63 time=6.19 ms
        64 bytes from 10.2.30.1: icmp_seq=5 ttl=63 time=5.43 ms
        64 bytes from 10.2.30.1: icmp_seq=6 ttl=63 time=6.26 ms
        64 bytes from 10.2.30.1: icmp_seq=7 ttl=63 time=5.87 ms
        64 bytes from 10.2.30.1: icmp_seq=8 ttl=63 time=5.99 ms
        64 bytes from 10.2.30.1: icmp_seq=9 ttl=63 time=5.55 ms
        64 bytes from 10.2.30.1: icmp_seq=10 ttl=63 time=6.31 ms
        64 bytes from 10.2.30.1: icmp_seq=11 ttl=63 time=5.46 ms
        64 bytes from 10.2.30.1: icmp_seq=12 ttl=63 time=6.15 ms
        64 bytes from 10.2.30.1: icmp_seq=13 ttl=63 time=5.59 ms
        ** 64 bytes from 10.2.30.1: icmp_seq=14 ttl=63 time=6.25 ms **
        ** 64 bytes from 10.2.30.1: icmp_seq=23 ttl=63 time=6.13 ms **
        64 bytes from 10.2.30.1: icmp_seq=24 ttl=63 time=6.01 ms
        64 bytes from 10.2.30.1: icmp_seq=25 ttl=63 time=5.85 ms
        64 bytes from 10.2.30.1: icmp_seq=26 ttl=63 time=5.51 ms
        64 bytes from 10.2.30.1: icmp_seq=27 ttl=63 time=6.61 ms
        ^C
        --- 10.2.30.1 ping statistics ---
        27 packets transmitted, 18 received, 33% packet loss, time 26227ms
        rtt min/avg/max/mdev = 5.434/5.937/6.618/0.341 ms


 On lance un ping continu de PC1 (VLAN10) vers PC3 (10.2.30.51).
 On éteint DS1 puis on le rallume.

        root@PC1:~# ping 10.2.30.51
        PING 10.2.30.51 (10.2.30.51) 56(84) bytes of data.
        64 bytes from 10.2.30.51: icmp_seq=2 ttl=63 time=8.67 ms
        64 bytes from 10.2.30.51: icmp_seq=3 ttl=63 time=8.35 ms
        64 bytes from 10.2.30.51: icmp_seq=4 ttl=63 time=9.19 ms
        64 bytes from 10.2.30.51: icmp_seq=5 ttl=63 time=8.20 ms
        64 bytes from 10.2.30.51: icmp_seq=6 ttl=63 time=8.88 ms
        64 bytes from 10.2.30.51: icmp_seq=7 ttl=63 time=9.25 ms
        64 bytes from 10.2.30.51: icmp_seq=8 ttl=63 time=9.14 ms
        64 bytes from 10.2.30.51: icmp_seq=9 ttl=63 time=9.39 ms
        64 bytes from 10.2.30.51: icmp_seq=10 ttl=63 time=10.4 ms
        64 bytes from 10.2.30.51: icmp_seq=11 ttl=63 time=10.4 ms
        64 bytes from 10.2.30.51: icmp_seq=12 ttl=63 time=10.3 ms
        64 bytes from 10.2.30.51: icmp_seq=13 ttl=63 time=10.1 ms
        ** 64 bytes from 10.2.30.51: icmp_seq=14 ttl=63 time=9.49 ms **
        ** 64 bytes from 10.2.30.51: icmp_seq=21 ttl=63 time=6.01 ms **
        64 bytes from 10.2.30.51: icmp_seq=22 ttl=63 time=6.27 ms
        64 bytes from 10.2.30.51: icmp_seq=23 ttl=63 time=5.11 ms
        64 bytes from 10.2.30.51: icmp_seq=24 ttl=63 time=6.61 ms
        64 bytes from 10.2.30.51: icmp_seq=25 ttl=63 time=5.98 ms
        64 bytes from 10.2.30.51: icmp_seq=26 ttl=63 time=5.00 ms
        64 bytes from 10.2.30.51: icmp_seq=27 ttl=63 time=5.84 ms
        ^C

        --- 10.2.30.51 ping statistics ---
        27 packets transmitted, 20 received, 25% packet loss, time 26190ms
        rtt min/avg/max/mdev = 5.003/8.142/10.498/1.822 ms

### IPv6 Hot Standby Router Protocol (HSRP): redondance de passerelle

Nous avons rencontré quelques problème lors des tests de la redondance de passerelle (HSRP) en IPv6. En effectuant des pings d'un PC à un autre, il se trouve que le relai n'est pas pris. Par manque de temps, nous n'avons pas pu résoudre le problème. 

## Test de connectivité

### IPv4

Ping de PC1 vers Internet (google par exemple) :

        root@PC1:~# ping 8.8.8.8
        PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
        64 bytes from 8.8.8.8: icmp_seq=1 ttl=53 time=9.64 ms
        64 bytes from 8.8.8.8: icmp_seq=2 ttl=53 time=8.95 ms
        64 bytes from 8.8.8.8: icmp_seq=3 ttl=53 time=8.83 ms
        64 bytes from 8.8.8.8: icmp_seq=4 ttl=53 time=8.57 ms
        64 bytes from 8.8.8.8: icmp_seq=5 ttl=53 time=8.86 ms


Ping de PC1 (VLAN10) vers PC8 (VLAN 40) :

        PING 10.2.40.51 (10.2.40.51) 56(84) bytes of data.
        64 bytes from 10.2.40.51: icmp_seq=1 ttl=63 time=8.32 ms
        64 bytes from 10.2.40.51: icmp_seq=2 ttl=63 time=8.17 ms
        64 bytes from 10.2.40.51: icmp_seq=3 ttl=63 time=7.80 ms
        64 bytes from 10.2.40.51: icmp_seq=4 ttl=63 time=8.33 ms
        64 bytes from 10.2.40.51: icmp_seq=5 ttl=63 time=7.72 ms
        64 bytes from 10.2.40.51: icmp_seq=6 ttl=63 time=8.16 ms
        64 bytes from 10.2.40.51: icmp_seq=7 ttl=63 time=8.04 ms
        ^Z

### IPv6

Ping PC1 vers internet :

        root@PC1:~# ping6 test.tf
        PING test.tf(2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a)) 56 data bytes
        64 bytes from 2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a): icmp_seq=2 ttl=49 time=14.8 ms
        64 bytes from 2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a): icmp_seq=3 ttl=49 time=15.4 ms
        64 bytes from 2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a): icmp_seq=4 ttl=49 time=17.0 ms
        64 bytes from 2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a): icmp_seq=5 ttl=49 time=16.2 ms
        64 bytes from 2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a): icmp_seq=6 ttl=49 time=16.1 ms
        64 bytes from 2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a): icmp_seq=7 ttl=49 time=16.1 ms
        64 bytes from 2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a): icmp_seq=8 ttl=49 time=19.2 ms

Ping de PC1 (VLAN10) vers PC4 (VLAN40) :

        root@PC1:~# ping fd00:470:c814:1040:e16:5ff:feba:f300
        PING fd00:470:c814:1040:e16:5ff:feba:f300(fd00:470:c814:1040:e16:5ff:feba:f300) 56 data bytes
        64 bytes from fd00:470:c814:1040:e16:5ff:feba:f300: icmp_seq=2 ttl=63 time=8.53 ms
        64 bytes from fd00:470:c814:1040:e16:5ff:feba:f300: icmp_seq=3 ttl=63 time=10.2 ms
        64 bytes from fd00:470:c814:1040:e16:5ff:feba:f300: icmp_seq=4 ttl=63 time=7.99 ms
        64 bytes from fd00:470:c814:1040:e16:5ff:feba:f300: icmp_seq=5 ttl=63 time=7.54 ms
        64 bytes from fd00:470:c814:1040:e16:5ff:feba:f300: icmp_seq=6 ttl=63 time=11.4 ms


Ping de PC1 (VLAN10) vers PC8 (VLAN40) :

        root@PC1:~# ping6 fd00:470:c814:1040:e16:5ff:fe4a:1e00
        PING fd00:470:c814:1040:e16:5ff:fe4a:1e00(fd00:470:c814:1040:e16:5ff:fe4a:1e00) 56 data bytes
        64 bytes from fd00:470:c814:1040:e16:5ff:fe4a:1e00: icmp_seq=1 ttl=63 time=8.08 ms
        64 bytes from fd00:470:c814:1040:e16:5ff:fe4a:1e00: icmp_seq=2 ttl=63 time=8.66 ms
        64 bytes from fd00:470:c814:1040:e16:5ff:fe4a:1e00: icmp_seq=3 ttl=63 time=8.97 ms
        64 bytes from fd00:470:c814:1040:e16:5ff:fe4a:1e00: icmp_seq=4 ttl=63 time=8.00 ms
        64 bytes from fd00:470:c814:1040:e16:5ff:fe4a:1e00: icmp_seq=5 ttl=63 time=9.04 ms

Ping de PC1 (VLAN10) vers PC6 (VLAN20) :

        root@PC1:~# ping6 fd00:470:c814:1020:e16:5ff:fe93:3900
        PING fd00:470:c814:1020:e16:5ff:fe93:3900(fd00:470:c814:1020:e16:5ff:fe93:3900) 56 data bytes
        64 bytes from fd00:470:c814:1020:e16:5ff:fe93:3900: icmp_seq=2 ttl=63 time=8.70 ms
        64 bytes from fd00:470:c814:1020:e16:5ff:fe93:3900: icmp_seq=3 ttl=63 time=7.78 ms
        64 bytes from fd00:470:c814:1020:e16:5ff:fe93:3900: icmp_seq=4 ttl=63 time=8.10 ms
        64 bytes from fd00:470:c814:1020:e16:5ff:fe93:3900: icmp_seq=5 ttl=63 time=7.68 ms


## Test du tunnel VPN IPSEC en IPv4

On lance un ping continu depuis PC1 (10.2.10.1) vers PC9 (10.104.1.2) ainsi que depuis PC9 vers PC1. Les deux sorties ci-dessous montrent que le tunnel se monte correctement.

        root@PC1:~# ping 10.104.1.2
        PING 10.104.1.2 (10.104.1.2) 56(84) bytes of data.
        64 bytes from 10.104.1.2: icmp_seq=5 ttl=60 time=11.4 ms
        64 bytes from 10.104.1.2: icmp_seq=6 ttl=60 time=9.48 ms
        64 bytes from 10.104.1.2: icmp_seq=7 ttl=60 time=8.69 ms
        64 bytes from 10.104.1.2: icmp_seq=8 ttl=60 time=9.57 ms
        64 bytes from 10.104.1.2: icmp_seq=9 ttl=60 time=10.1 ms
        64 bytes from 10.104.1.2: icmp_seq=10 ttl=60 time=10.0 ms
        64 bytes from 10.104.1.2: icmp_seq=11 ttl=60 time=10.2 ms
        64 bytes from 10.104.1.2: icmp_seq=12 ttl=60 time=9.44 ms
        64 bytes from 10.104.1.2: icmp_seq=13 ttl=60 time=10.3 ms
        64 bytes from 10.104.1.2: icmp_seq=14 ttl=60 time=10.6 ms
        64 bytes from 10.104.1.2: icmp_seq=15 ttl=60 time=10.7 ms
        64 bytes from 10.104.1.2: icmp_seq=16 ttl=60 time=9.14 ms
        64 bytes from 10.104.1.2: icmp_seq=17 ttl=60 time=10.6 ms
        64 bytes from 10.104.1.2: icmp_seq=18 ttl=60 time=9.61 ms
        64 bytes from 10.104.1.2: icmp_seq=19 ttl=60 time=10.5 ms
        64 bytes from 10.104.1.2: icmp_seq=20 ttl=60 time=11.3 ms
        64 bytes from 10.104.1.2: icmp_seq=21 ttl=60 time=9.33 ms
        64 bytes from 10.104.1.2: icmp_seq=22 ttl=60 time=10.0 ms
        64 bytes from 10.104.1.2: icmp_seq=23 ttl=60 time=10.5 ms

        root@PC9:~# ping 10.2.10.1
        PING 10.2.10.1 (10.2.10.1) 56(84) bytes of data.
        64 bytes from 10.2.10.1: icmp_seq=1 ttl=60 time=11.9 ms
        64 bytes from 10.2.10.1: icmp_seq=2 ttl=60 time=10.3 ms
        64 bytes from 10.2.10.1: icmp_seq=3 ttl=60 time=10.1 ms
        64 bytes from 10.2.10.1: icmp_seq=4 ttl=60 time=12.2 ms
        64 bytes from 10.2.10.1: icmp_seq=5 ttl=60 time=10.7 ms
        64 bytes from 10.2.10.1: icmp_seq=6 ttl=60 time=9.95 ms
        64 bytes from 10.2.10.1: icmp_seq=7 ttl=60 time=10.0 ms
        64 bytes from 10.2.10.1: icmp_seq=8 ttl=60 time=9.35 ms
        64 bytes from 10.2.10.1: icmp_seq=9 ttl=60 time=10.4 ms
        64 bytes from 10.2.10.1: icmp_seq=10 ttl=60 time=10.9 ms
        64 bytes from 10.2.10.1: icmp_seq=11 ttl=60 time=12.9 ms
        64 bytes from 10.2.10.1: icmp_seq=12 ttl=60 time=9.97 ms
        64 bytes from 10.2.10.1: icmp_seq=13 ttl=60 time=13.9 ms
        64 bytes from 10.2.10.1: icmp_seq=14 ttl=60 time=10.2 ms
        64 bytes from 10.2.10.1: icmp_seq=15 ttl=60 time=10.4 ms
        64 bytes from 10.2.10.1: icmp_seq=16 ttl=60 time=9.98 ms
        64 bytes from 10.2.10.1: icmp_seq=17 ttl=60 time=11.0 ms
        64 bytes from 10.2.10.1: icmp_seq=18 ttl=60 time=10.8 ms
        64 bytes from 10.2.10.1: icmp_seq=19 ttl=60 time=10.0 ms
        64 bytes from 10.2.10.1: icmp_seq=20 ttl=60 time=9.79 ms
        64 bytes from 10.2.10.1: icmp_seq=21 ttl=60 time=10.1 ms
        64 bytes from 10.2.10.1: icmp_seq=22 ttl=60 time=10.6 ms
        64 bytes from 10.2.10.1: icmp_seq=23 ttl=60 time=9.93 ms


La commande "show crypto ipsec sa" appliquée sur R1 et R4 permet d'observer, entre autres, le nombre de paquets encapsulés, chiffrés, désencapsulés, déchiffrés.

        R1#show crypto ipsec sa

        interface: GigabitEthernet0/1
            Crypto map tag: cm-to-R4, local addr 192.168.122.239

           protected vrf: (none)
           local  ident (addr/mask/prot/port): (10.0.0.0/255.0.0.0/0/0)
           remote ident (addr/mask/prot/port): (10.104.1.0/255.255.255.0/0/0)
           current_peer 192.168.122.162 port 500
             PERMIT, flags={origin_is_acl,}
            #pkts encaps: 418, #pkts encrypt: 418, #pkts digest: 418
            #pkts decaps: 414, #pkts decrypt: 414, #pkts verify: 414
            #pkts compressed: 0, #pkts decompressed: 0
            #pkts not compressed: 0, #pkts compr. failed: 0
            #pkts not decompressed: 0, #pkts decompress failed: 0
            #send errors 0, #recv errors 0

             local crypto endpt.: 192.168.122.239, remote crypto endpt.: 192.168.122.162
             plaintext mtu 1438, path mtu 1500, ip mtu 1500, ip mtu idb GigabitEthernet0/1
             current outbound spi: 0x59865DD7(1501978071)
             PFS (Y/N): N, DH group: none

             inbound esp sas:
              spi: 0x64C848EF(1690847471)
                transform: esp-256-aes esp-sha-hmac ,
                in use settings ={Tunnel, }
                conn id: 1, flow_id: SW:1, sibling_flags 80000040, crypto map: cm-to-R4
                sa timing: remaining key lifetime (k/sec): (4608000/3267)
                IV size: 16 bytes
                replay detection support: Y
                Status: ACTIVE(ACTIVE)
              spi: 0x46CC67C6(1187801030)
                transform: esp-256-aes esp-sha-hmac ,
                in use settings ={Tunnel, }
                conn id: 3, flow_id: SW:3, sibling_flags 80004040, crypto map: cm-to-R4
                sa timing: remaining key lifetime (k/sec): (4162986/3273)
                IV size: 16 bytes
                replay detection support: Y
                Status: ACTIVE(ACTIVE)

             inbound ah sas:

             inbound pcp sas:

             outbound esp sas:
              spi: 0xFFE4EC5A(4293192794)
                transform: esp-256-aes esp-sha-hmac ,
                in use settings ={Tunnel, }
                conn id: 2, flow_id: SW:2, sibling_flags 80000040, crypto map: cm-to-R4
                sa timing: remaining key lifetime (k/sec): (4608000/3267)
                IV size: 16 bytes
                replay detection support: Y
                Status: ACTIVE(ACTIVE)
              spi: 0x59865DD7(1501978071)
                transform: esp-256-aes esp-sha-hmac ,
                in use settings ={Tunnel, }
                conn id: 4, flow_id: SW:4, sibling_flags 80004040, crypto map: cm-to-R4
                sa timing: remaining key lifetime (k/sec): (4162986/3273)
                IV size: 16 bytes
                replay detection support: Y
                Status: ACTIVE(ACTIVE)

             outbound ah sas:

             outbound pcp sas:

        R4#show crypto ipsec sa

        interface: GigabitEthernet0/1
            Crypto map tag: cm-to-R1, local addr 192.168.122.162

           protected vrf: (none)
           local  ident (addr/mask/prot/port): (10.104.1.0/255.255.255.0/0/0)
           remote ident (addr/mask/prot/port): (10.0.0.0/255.0.0.0/0/0)
           current_peer 192.168.122.239 port 500
             PERMIT, flags={origin_is_acl,}
            #pkts encaps: 542, #pkts encrypt: 542, #pkts digest: 542
            #pkts decaps: 547, #pkts decrypt: 547, #pkts verify: 547
            #pkts compressed: 0, #pkts decompressed: 0
            #pkts not compressed: 0, #pkts compr. failed: 0
            #pkts not decompressed: 0, #pkts decompress failed: 0
            #send errors 0, #recv errors 0

             local crypto endpt.: 192.168.122.162, remote crypto endpt.: 192.168.122.239
             plaintext mtu 1438, path mtu 1500, ip mtu 1500, ip mtu idb GigabitEthernet0/1
             current outbound spi: 0x46CC67C6(1187801030)
             PFS (Y/N): N, DH group: none

             inbound esp sas:
              spi: 0xFFE4EC5A(4293192794)
                transform: esp-256-aes esp-sha-hmac ,
                in use settings ={Tunnel, }
                conn id: 1, flow_id: SW:1, sibling_flags 80004040, crypto map: cm-to-R1
                sa timing: remaining key lifetime (k/sec): (4608000/3202)
                IV size: 16 bytes
                replay detection support: Y
                Status: ACTIVE(ACTIVE)
              spi: 0x59865DD7(1501978071)
                transform: esp-256-aes esp-sha-hmac ,
                in use settings ={Tunnel, }
                conn id: 3, flow_id: SW:3, sibling_flags 80000040, crypto map: cm-to-R1
                sa timing: remaining key lifetime (k/sec): (4332923/3209)
                IV size: 16 bytes
                replay detection support: Y
                Status: ACTIVE(ACTIVE)

             inbound ah sas:

             inbound pcp sas:

             outbound esp sas:
              spi: 0x64C848EF(1690847471)
                transform: esp-256-aes esp-sha-hmac ,
                in use settings ={Tunnel, }
                conn id: 2, flow_id: SW:2, sibling_flags 80004040, crypto map: cm-to-R1
                sa timing: remaining key lifetime (k/sec): (4608000/3202)
                IV size: 16 bytes
                replay detection support: Y
                Status: ACTIVE(ACTIVE)
              spi: 0x46CC67C6(1187801030)
                transform: esp-256-aes esp-sha-hmac ,
                in use settings ={Tunnel, }
                conn id: 4, flow_id: SW:4, sibling_flags 80000040, crypto map: cm-to-R1
                sa timing: remaining key lifetime (k/sec): (4332923/3209)
                IV size: 16 bytes
                replay detection support: Y
                Status: ACTIVE(ACTIVE)

             outbound ah sas:

             outbound pcp sas:

        interface: GigabitEthernet0/3
            Crypto map tag: cm-to-R1, local addr 0.0.0.0

           protected vrf: (none)
           local  ident (addr/mask/prot/port): (10.104.1.0/255.255.255.0/0/0)
           remote ident (addr/mask/prot/port): (10.0.0.0/255.0.0.0/0/0)
           current_peer 192.168.122.239 port 500
             PERMIT, flags={origin_is_acl,}
            #pkts encaps: 0, #pkts encrypt: 0, #pkts digest: 0
            #pkts decaps: 0, #pkts decrypt: 0, #pkts verify: 0
            #pkts compressed: 0, #pkts decompressed: 0
            #pkts not compressed: 0, #pkts compr. failed: 0
            #pkts not decompressed: 0, #pkts decompress failed: 0
            #send errors 0, #recv errors 0

             local crypto endpt.: 0.0.0.0, remote crypto endpt.: 192.168.122.239
             plaintext mtu 1500, path mtu 1500, ip mtu 1500, ip mtu idb GigabitEthernet0/3
             current outbound spi: 0x0(0)
             PFS (Y/N): N, DH group: none

             inbound esp sas:

             inbound ah sas:

             inbound pcp sas:

             outbound esp sas:

             outbound ah sas:

             outbound pcp sas:




