# Configuration manuelle

Ajouter les blocs de commandes utilisés pour la configuration manuelle

## PC

**Sur PC1 à PC8** :
      
      Pour changer le nom de la machine :
          sudo echo PCx > /etc/hostname
          reboot

      Configuration du service DNS :
          echo "nameserver 1.1.1.1" >> /etc/resolv.conf
