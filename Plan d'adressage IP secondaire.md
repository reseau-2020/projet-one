#Plan d'adressage secondaire / prévisionnel

# Plan d'adressage
L'adressage IPv4 est en /24.
L'adressage IPv6 est en /52.

## Tripod 
|Module|Interface|Description<br>Connexion|Adressage IPv6 privé|Adressage IPv6 public|
|:-:|:-:|:-:|:-:|:-:|
|R1|G0/2|connecté à R2|
|R1|G0/3|connecté à R3|
|R2|G0/1|connecté à R1|
|R2|G0/3|connecté à R3|
|R3|G0/1|connecté à R1|
|R3|G0/2|connecté à R2|


## Liaison Tripod-Switchblocks
|Module|Interface|Description/Connexion|Adressage IPv6 privé|Adressage IPv6 public|
|:-:|:-:|:-:|:-:|:-:|
|R2|G0/2|connecté à DS1|
|R2|G0/4|connecté à DS1|
|R2|G0/5|connecté à DS2|
|R2|G0/6|connecté à DS2|
|R3|G0/3|connecté à DS2|
|R3|G0/4|connecté à DS2|
|R3|G0/5|connecté à DS1|
|R3|G0/6|connecté à DS1|
|DS1|G2/0|connecté à R2|
|DS1|G3/0|connecté à R2|
|DS1|G2/1|connecté à R3|
|DS1|G3/1|connecté à R3|
|DS2|G2/0|connecté à R3|
|DS2|G3/0|connecté à R3|
|DS2|G2/1|connecté à R2|
|DS2|G3/1|connecté à R2|


