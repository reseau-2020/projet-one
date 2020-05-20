#Plan d'adressage secondaire / prévisionnel

# Plan d'adressage
L'adressage IPv4 est en /24.
L'adressage IPv6 est en /52.

## Tripod 
|Module|Interface|Description<br>Connexion|Adressage IPv6 public|Adressage IPv6 privé|
|:-:|:-:|:-:|:-:|:-:|
|R1|G0/2|connecté à R2|2001:470:c814:1001::1|fd00:470:c814:1001::1|
|R1|G0/3|connecté à R3|2001:470:c814:1002::1|fd00:470:c814:1002::1|
|R2|G0/1|connecté à R1|2001:470:c814:1002::2|fd00:470:c814:1002::2|
|R2|G0/3|connecté à R3|2001:470:c814:1003::2|fd00:470:c814:1003::2|
|R3|G0/1|connecté à R1|2001:470:c814:1002::2|fd00:470:c814:1002::2|
|R3|G0/2|connecté à R2|2001:470:c814:1003::1|fd00:470:c814:1003::1|


## Liaison Tripod-Switchblocks
|Module|Interface|Description/Connexion|Adressage IPv6 public|Adressage IPv6 privé|
|:-:|:-:|:-:|:-:|:-:|
|R2|G0/2|connecté à DS1|2001:470:c814:1301::1|fd00:470:c814:1301::1|
|R2|G0/4|connecté à DS1|2001:470:c814:1311::1|fd00:470:c814:1311::1|
|R2|G0/5|connecté à DS2|2001:470:c814:1304::1|fd00:470:c814:1304::1|
|R2|G0/6|connecté à DS2|2001:470:c814:1344::1|fd00:470:c814:1344::1|
|R3|G0/3|connecté à DS2|2001:470:c814:1303::1|fd00:470:c814:1303::1|
|R3|G0/4|connecté à DS2|2001:470:c814:1333::1|fd00:470:c814:1333::1|
|R3|G0/5|connecté à DS1|2001:470:c814:1302::1|fd00:470:c814:1302::1|
|R3|G0/6|connecté à DS1|2001:470:c814:1322::1|fd00:470:c814:1322::1|
|DS1|G2/0|connecté à R2|2001:470:c814:1301::2|fd00:470:c814:1301::2|
|DS1|G3/0|connecté à R2|2001:470:c814:1311::2|fd00:470:c814:1311::2|
|DS1|G2/1|connecté à R3|2001:470:c814:1302::2|fd00:470:c814:1302::2|
|DS1|G3/1|connecté à R3|2001:470:c814:1322::2|fd00:470:c814:1322::2|
|DS2|G2/0|connecté à R3|2001:470:c814:1303::2|fd00:470:c814:1303::2|
|DS2|G3/0|connecté à R3|2001:470:c814:1333::2|fd00:470:c814:1333::2|
|DS2|G2/1|connecté à R2|2001:470:c814:1304::2|fd00:470:c814:1304::2|
|DS2|G3/1|connecté à R2|2001:470:c814:1344::2|fd00:470:c814:1344::2|


