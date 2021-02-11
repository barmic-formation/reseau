# Contrôle et gestion d’erreurs de la couche réseau avec ICMP

Cette partie est à effectuer depuis votre ordinateur. Vous aurez besoin de [wireshark](https://www.wireshark.org/).

Lancez un traceroute vers l’un des serveurs HTTP de votre choix, par exemple www.ietf.org.
Sur windows l'utilitaire s'appel tracert.

> Note : Lorsque `tracert` ou `traceroute` vous affiche des `*` c'est que les routeurs en questions ne vous ont pas répondu.

- **Question 1** Quel serveur avez-vous choisi ? Quelle est son adresse IP ?
- **Question 2** Utilisez wireshark pour observer les paquets échangés lors du traceroute. Quels protocoles sont utilisés ? Comment fonctionne traceroute ? Observer notamment les champs de la couche réseau.
- **Question 3** Combien de routeurs le dernier paquet a-t-il traversé au total ? Quel est le temps d’aller/retour (RTT) entre votre machine et la machine distante ? Donnez les 3 valeurs observées. Y a-t-il eu des paquets perdus ?
- **Question 4** Tester le RTT avec la commande ping sur le même serveur. Utilisez l’option `-c 1` pour faire un unique test.

# Couche Transport

Cette partie nécessite GNS.
Pour ce premier TP vous n'aurez besoin que 2 de machines avec un seul lien entre elles.
N'oubliez pas de les démarrer et ouvrez une console sur chcune d'elle.

## Protocole UDP

- **Question 5** Quels sont les services fournis par UDP ?

Lancez socklab en mode udp sur les deux stations connectées :
```sh
socklab udp
```
Sur l’une des stations démarrez une capture wireshark. Sur chaque station créez une socket udp avec la commande socket.

- **Question 6** À quoi sert le numéro de port qui vous est renvoyé ? Comment la machine destinataire le connaı̂t-elle ?
Sur l’une des machines envoyez des données vers l’autre en précisant son adresse IP et son numéro de port
```sh
sendto <id de socket> <nom de machine> <port destinataire>
```
Sur la 2e machine demandez à lire les données :
```sh
recvfrom <id de socket> <nb octets>
```

- **Question 7** Quels paquets transitent sur le réseau lors de l’envoi d’un message par UDP ?
- **Question 8** Que se passe-t-il si l’on demande à lire moins d’octets que ceux envoyés ?
- **Question 9** Si l’on envoie plusieurs messages avant de lire de l’autre côté ?
- **Question 10** Si vous envoyez le message vers un port inexistant ?
- **Question 11** Si vous envoyez plus de données que la taille du MTU ? (pour envoyer 1000 octets tapez #1000 à la place du message à envoyer). La taille maximale d’un paquet est donnée par son MTU (`ifconfig`). Que signifie MTU ?
- **Question 12** Consultez les options par défaut de votre socket. Changez la taille du tampon (buffer) de réception. Expérimentez des envois de données supérieures.

## Protocole TCP

Lancez socklab en mode tcp sur les deux stations connectées :
```sh
socklab tcp
```
Sur l’une des stations démarrez une capture wireshark. Établissez une connexion TCP.
- **Question 13** Analysez les paquets échangés. Quel est le rôle du flag SYN ? Quelles sont les options dans l’en-tete du premier message ?
Établissez deux connexions vers un même port destinataire ?
- **Question 14** Qu’est-ce qui identifie une connexion TCP ?
Fermez la connexion avec close.
- **Question 15** Quels sont les messages échangés ? Faites un diagramme temporel indiquant les flags positionnés, les numéros de séquence et d’acquittement si besoin.
Établissez une connexion TCP puis déconnectez le câble réseau d’une des machines. Envoyez un message depuis la machine où vous avez lancé wireshark vers l’autre machine.
- **Question 16** Que se passe-t-il ? Et lorsque vous rebranchez le câble ? Que peut-on en conclure ? Quelle est la durée entre deux retransmissions ? Quelle est la durée entre la 1 re émission et la dernière retransmission ?
- **Question 17** Consultez les options par défaut de votre socket. Changez la taille du tampon de réception.
Expérimentez des envois de données supérieures.