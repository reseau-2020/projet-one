#Plan d'adressage secondaire / prévisionnel

# Plan d'adressage
L'adressage IPv4 est en /24.
L'adressage IPv6 est en /52.

## Tripod 
|Module|Interface|Description<br>Connexion|Adressage IPv6 privé|Adressage IPv6 public|
|:-:|:-:|:-:|:-:|:-:|
|R1|G0/2|connecté à R2|10.1.1.1|fe80:
|R1|G0/3|connecté à R3|10.1.2.1|
|R2|G0/1|connecté à R1|10.1.1.2|
|R2|G0/3|connecté à R3|10.1.3.2|
|R3|G0/1|connecté à R1|10.1.2.2|
|R3|G0/2|connecté à R2|10.1.3.1|


## Liaison Tripod-Switchblocks
|Module|Interface|Description/Connexion|IPv4|IPv6 Link-local|
|:-:|:-:|:-:|:-:|:-:|
|R2|G0/2|connecté à DS1|10.3.1.1|
|R2|G0/4|connecté à DS1|10.3.11.1|
|R2|G0/5|connecté à DS2|10.3.4.1|
|R2|G0/6|connecté à DS2|10.3.44.1|
|R3|G0/3|connecté à DS2|10.3.3.1|
|R3|G0/4|connecté à DS2|10.3.33.1|
|R3|G0/5|connecté à DS1|10.3.2.1|
|R3|G0/6|connecté à DS1|10.3.22.1|
|DS1|G2/0|connecté à R2|10.3.1.2|
|DS1|G3/0|connecté à R2|10.3.11.2|
|DS1|G2/1|connecté à R3|10.3.2.2|
|DS1|G3/1|connecté à R3|10.3.22.2|
|DS2|G2/0|connecté à R3|10.3.3.2|
|DS2|G3/0|connecté à R3|10.3.33.2|
|DS2|G2/1|connecté à R2|10.3.4.2|
|DS2|G3/1|connecté à R2|10.3.44.2

