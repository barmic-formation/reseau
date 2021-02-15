# Sujet TP réseau n°2

## Configuration des interfaces (ifconfig)

La commande utilisée pour configurer les interfaces Ethernet s’appelle `ifconfig` (”InterFace CONFI-
Guration”). Configurer une interface consiste à l’initialiser, lui associer un certain nombre d’informations
(l’adresse IP de la machine entre autre). Les noms d’interface sont toujours de la forme : <nom><numéro>,
comme em0. On peut distinguer les 2 interfaces grâce à leurs adresses Ethernet (notées
en général sur la carte). En tapant `ifconfig` sans argument, on peut voir toutes les interfaces de la station.

**Configuration de l’interface :** L’objectif de l’interface est de relier la machine sur le réseau. Vous
devez donc lui associer un certain nombre de renseignements et en particulier l’adresse IP de la
machine sur le réseau :
```
ifconfig <nom_interface> <adresse IP> netmask <masque>
```
Le masque peut être donné sous la forme compacte (CIDR) :
```
ifconfig em0 10.2.0.1/24
```
ou bien de façon étendue :
```
ifconfig em0 10.2.0.1 netmask 255.255.255.0
```
Marquage de l’interface à l’état "marche" (UP) : Une fois que l’interface est initialisée et confi-
gurée, vous pouvez la marquer "prête à l’emploi" ! La commande à lancer est :
```
ifconfig <nom_interface> up
```
Désormais, votre machine peut dialoguer sur le câble Ethernet.

**Contrôle de l’état des interfaces :** À tout moment vous pouvez contrôler l’état de vos interfaces.
Pour connaı̂tre l’état de l’interface que vous venez de configurer, tapez la commande suivante :
```
ifconfig <nom_interface>
```

## Manipulation des tables de routage

Nous avons vu que toutes les stations, qu’elles soient hosts ou routeurs, gèrent une table de routage.
Nous avons la possibilité par l’intermédiaire de certains outils standard de manipuler cette table, comme
afficher les entrées, ajouter ou supprimer une entrée...

Pour afficher la table : `netstat -r`

Pour mettre à jour la table, nous utiliserons l’utilitaire route de la manière suivante :
```
route [add|delete] destination gateway
```
en remplaçant “destination” et “gateway” par leurs adresses IP respectives. La destination est toujours
une adresse de réseau, tandis que le routeur possède une adresse d’hôte.

**Exemple 1** route add 192.0.0.0/16 193.0.0.1 ajoute une route indiquant que pour aller au réseau
192.0.0.0/16 , il faut envoyer le paquet au routeur voisin 193.0.0.1. `route delete 192.0.0.0/16` supprime la route vers ce réseau.

Pour effectuer un nettoyage complet de la table de routage, taper :
```
route flush.
```