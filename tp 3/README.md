# I. ARP
##1. Echange ARP
🌞Générer des requêtes ARP

effectuer un ping d'une machine à l'autre
```
[lukas@localhost ~]$ ping 10.3.1.12
PING 10.3.1.12 (10.3.1.12) 56(84) bytes of data.
64 bytes from 10.3.1.12: icmp_seq=1 ttl=64 time=2.46 ms
64 bytes from 10.3.1.12: icmp_seq=2 ttl=64 time=0.918 ms
64 bytes from 10.3.1.12: icmp_seq=3 ttl=64 time=0.943 ms
64 bytes from 10.3.1.12: icmp_seq=4 ttl=64 time=1.03 ms
64 bytes from 10.3.1.12: icmp_seq=5 ttl=64 time=1.58 ms
64 bytes from 10.3.1.12: icmp_seq=6 ttl=64 time=0.473 ms
64 bytes from 10.3.1.12: icmp_seq=7 ttl=64 time=0.745 ms
64 bytes from 10.3.1.12: icmp_seq=8 ttl=64 time=1.29 ms
64 bytes from 10.3.1.12: icmp_seq=9 ttl=64 time=0.440 ms
^C
--- 10.3.1.12 ping statistics ---
9 packets transmitted, 9 received, 0% packet loss, time 8082ms
rtt min/avg/max/mdev = 0.440/1.097/2.458/0.589 ms
```
observer les tables ARP des deux machines
repérer l'adresse MAC de john dans la table ARP de marcel et vice-versa

- adresse MAC marcel : 08:00:27:f0:b7:7a 
-  adresse MAC john : 08:00:27:5c:50:c3

prouvez que l'info est correcte (que l'adresse MAC que vous voyez dans la table est bien celle de la machine correspondante)

une commande pour voir la MAC de marcel dans la table ARP de john
```
ip neigh show
```

et une commande pour afficher la MAC de marcel, depuis marcel 
```
ip a 
```
# 2. Analyse de trames
🌞Analyse de trames

utilisez la commande tcpdump pour réaliser une capture de trame
videz vos tables ARP, sur les deux machines, puis effectuez un ping


🦈 Capture réseau tp3_arp.pcapng qui contient un ARP request et un ARP reply

Si vous ne savez pas comment récupérer votre fichier .pcapng sur votre hôte afin de l'ouvrir dans Wireshark, et me le livrer en rendu, demandez-moi.