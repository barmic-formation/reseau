# Socklab

## Généralités

Lancer socklab via la commande :

```
socklab udp
```

ou

```
socklab tcp
```

une fois dans l'invite de commande vous pouvez utiliser la commande `?` ou `help` pour obtenir l'aide.

## UDP

Vous pouvez créer des sockets avec la commande `s`. Le programme vous affiche alors 2 informations :

- le numéro de socket : c'est ce qui permet d'utiliser la socket
- le numéro de port : c'est l'adresse exterieur de la socket.

Quand vous souhaiter utiliser une socket, vous devrez indiquer le numéro de socket local et le nom d'hôte (ou le port) + le port distant.


## TCP

Le fonctionnement de TCP est assez différent d'UDP et vous allez devoir l'expérimenter en utilisant socklab.

TCP est un protocole client/server :

- le serveur ouvre une socket passive puis attend une connexion avec la commande `accept`
- les clients peuvent se connecter à cette socket avec la commande `connect`

Du coté du client le reste du fonctionement est le même qu'en UDP.
Du coté du serveur, on n'utilise la socket passive _que_ pour accepter des connexions. Lorsque l'on accepte une connexion, une nouvelle socket est créé (socklab vous indique son numéro). C'est cette dernère que vous devez utiliser pour commeuniquer avec le client qui vient de se connecter.
