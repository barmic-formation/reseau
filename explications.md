
# Introduction

## Adresse MAC et adresse Internet

Chaque interface ethernet possède une adresse ethernet 1 (de couche 2, également appelée adresse MAC)
qui l’identifie et qui lui est affectée une fois pour toute lors de sa fabrication (deux machines ne
peuvent pas avoir la même adresse ethernet). Une telle adresse tient sur six octets. La notation
habituelle pour ces adresses ethernet consiste à écrire les six octets hexadécimal et à les séparer par
des « `:` ». Par exemple : `08:00:20:04:69:d6`.

Sachant que tout le monde n’utilise pas nécessairement les réseaux ethernet, autrement dit des mécanismes
différents d’adressage peuvent exister, et que des réseaux de types différents peuvent être interconnectés,
il est donc nécessaire d’attribuer une adresse logique à chaque machine qui permet de faire abstraction
de la nature des réseaux : dans notre cas c’est l’adressage Internet qu’on utilisera (adresse de niveau
"réseau" dans les couches OSI). Cette adresse comporte 4 octets (IPv4) que l’on note généralement séparés
par des points.

**Le protocole ARP** La correspondance entre les adresses Internet et les adresses de niveau 2 sont
assurées par le protocole ARP (Address Resolution Protocol). Chaque machine maintient une table ARP
contenant les correspondances entre les adresses IP et les adresses MAC. Cette table contient un champ
Time-to-Live (TTL) qui indique au bout de combien de temps une entrée doit être retirée de la table. Ce
temps est typiquement de 20 minutes après insertion d’une entrée dans la table. Lorsqu’une machine A
veut envoyer un datagramme à une machine B portant l’adresse IP 195.221.226.92 et qu’aucune entrée
dans la table ARP ne correspond à cette adresse, le protocole ARP définit les actions suivantes :

- A diffuse un paquet ARP request
- B reconnaı̂t son adresse IP dans le paquet ARP request et répond avec un paquet ARP reply.

Lorsque A reçoit la réponse de B, il note son adresse MAC dans sa table et peut alors encapsuler son
datagramme dans une trame de niveau 2.

## Routage IP

Physiquement, deux réseaux doivent être interconnectés par l’intermédiaire d’une machine qui possède
un point d’attache sur l’un et l’autre des deux réseaux. Une telle connexion n’est cependant pas suffisante
pour garantir la communication entre les machines situées sur ces deux réseaux. Il faut donc que la
station reliant les deux réseaux coopère avec les autres machines et soit capable de passer les messages,
si nécessaire, d’un réseau à l’autre. Cette station qui joue un rôle particulier sur les réseaux s’appelle un
**routeur** (ou passerelle ou en anglais _gateway_).

Le mécanisme permettant l’acheminement des paquets à bon port à travers un ensemble de réseau est
appelé routage. Ce routage peut être plus ou moins perfectionné, par exemple **statique** (les chemins sont
calculés une fois pour toute), ou encore **dynamique** (les chemins peuvent varier dans le temps suivant
différents critères, avec en particulier l’apparition ou la disparition de liens dans le réseau).

> Rappel 1 l’adresse internet (ou adresse IP) est partagée en deux parties :
1. l’adresse du réseau sur lequel la machine est située ;
2. l’adresse de cette machine sur ce réseau.

Le netmask ou masque de sous-réseau indique quelle partie de l’adresse IP correspond à l’adresse
réseau de la façon suivante : tous les bits de la partie réseau de l’adresse sont à 1 et tous les bits de la
partie machine sont à 0. Exemple : `192.168.1.1/24` a pour netmask `255.255.255.0` (24 bits de préfixe).
Le 24 correspond au nombre de bits à 1 en partant de la gauche.

C’est sur la première partie de l’adresse (partie réseau) 2 que se basent les routeurs pour faire parvenir
les messages au réseau destination. Une fois les messages arrivés sur le réseau (ie. sur une station direc-
tement connectée au réseau), les stations concernées s’arrangent pour les récupérer. Ainsi, les routeurs
n’ont plus qu’à mémoriser la liste des réseaux qu’ils peuvent atteindre et les chemins y accédant. Pour
cela, les routeurs gèrent une table appelée **table de routage** dans laquelle ils stockent ces informations.
Les stations _hosts_ doivent également gérer une telle table pour savoir à quel routeur il faut s’adresser sur
son réseau local pour atteindre le réseau destination.

On peut distinguer deux fonctionnalités indépendantes dans la couche réseau~:
1. la prise de décision sur la route à prendre au vu de la table de routage et de l’adresse destination
contenue dans le paquet
2. la mise à jour des tables de routage.
Dans ce TP nous configurerons manuellement les tables de routage.
