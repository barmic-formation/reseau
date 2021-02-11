# FAQ

## Se connecter sur les machines freebsd

Les machines virtuelles que vous utilisez sont installées en FreeBSD. Vous travaillerez sous le login root sans mot de passe.
Vous lancez ensuite xinit pour accéder à l’interface graphique.

## Ping ne s’arrête pas

Tapez ctrl-C.

## Connaitre la configuration réseau de votre machine virtuel

Utilisez la commande ifconfig dans un terminal.

Elle donne un résultat de la forme :

```
em0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:04:51:00:a0  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

Il s'aggit ici d'un extrait.
On peut y voir que l'interface `em0` a l'adresse `172.17.0.1`, le masque de sous réseau est `255.255.0.0` et l'adresse de broadcast est donc `172.17.255.255`.
L'adresse mac de l'interface ethernet est `02:42:04:51:00:a0`.

## Remettre à zéros la configuration réseau d'une machine virtuelle

Au choix:

- redémarrez la machine
- détruire et recréer la machine via GNS

## Libérer le clavier de la machine virtuelle

Quand vous utilisez une machine virtuelle, virtualbox va capturer toutes les touches du clavier pour la machine virtuelle. Pour quitter la machine le raccourci par défaut est la touche Ctrl de gauche.

## Vous avez l'erreur `Error while creating link: Attachment 'nat' is already configured on adapter 0. Please remove it or allow VirtualBox VM 'FreeBSD-1' to use any adapter.` dans GNS

Clique droit sur chacune de vos machines, faites clique droit > `Configure` > `Network` et cochez la case : `Allow GNS3 to use any configured VirtualBox adapter`.