# I. Setup IP
Le lab, il vous faut deux machines :

les deux machines doivent être connectées physiquement
vous devez choisir vous-mêmes les IPs à attribuer sur les interfaces réseau, les contraintes :

IPs privées (évidemment n_n)
dans un réseau qui peut contenir au moins 1000 adresses IP (il faut donc choisir un masque adapté)
oui c'est random, on s'exerce c'est tout, p'tit jog en se levant c:
le masque choisi doit être le plus grand possible (le plus proche de 32 possible) afin que le réseau soit le plus petit possible



🌞 Mettez en place une configuration réseau fonctionnelle entre les deux machines
 machine 1 : 
 ``` ip 10.10.10.69 
 networksetup -setmanual "USB 10/100/1000 LAN" 10.10.10.69 255.255.252.0 
 ```
 machine 2 : 
 ```
 ip 10.10.10.70
 netsh interface ip set address "Ethernet" static 10.10.10.70 255.255.252.0
 ```
 ```
adresse reseau 10.10.8.0
```
```
broadcast 10.10.11.255
```

🌞 Prouvez que la connexion est fonctionnelle entre les deux machines

```PS C:\WINDOWS\system32> ping 10.10.10.69

Envoi d’une requête 'Ping'  10.10.10.69 avec 32 octets de données :
Réponse de 10.10.10.69 : octets=32 temps=2 ms TTL=64
Réponse de 10.10.10.69 : octets=32 temps=2 ms TTL=64
Réponse de 10.10.10.69 : octets=32 temps=1 ms TTL=64
Réponse de 10.10.10.69 : octets=32 temps=1 ms TTL=64

Statistiques Ping pour 10.10.10.69:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 1ms, Maximum = 2ms, Moyenne = 1ms
```

🌞 Wireshark it


ping ça envoie des paquets de type ICMP (c'est pas de l'IP, c'est un de ses frères)

les paquets ICMP sont encapsulés dans des trames Ethernet, comme les paquets IP
il existe plusieurs types de paquets ICMP, qui servent à faire des trucs différents



déterminez, grâce à Wireshark, quel type de paquet ICMP est envoyé par ping

pour le ping que vous envoyez
et le pong que vous recevez en retour




Vous trouverez sur la page Wikipedia de ICMP un tableau qui répertorie tous les types ICMP et leur utilité

🦈 PCAP qui contient les paquets ICMP qui vous ont permis d'identifier les types ICMP

# II. ARP my bro
ARP permet, pour rappel, de résoudre la situation suivante :

pour communiquer avec quelqu'un dans un LAN, il FAUT connaître son adresse MAC
on admet un PC1 et un PC2 dans le même LAN :

PC1 veut joindre PC2
PC1 et PC2 ont une IP correctement définie
PC1 a besoin de connaître la MAC de PC2 pour lui envoyer des messages
dans cette situation, PC1 va utilise le protocole ARP pour connaître la MAC de PC2
une fois que PC1 connaît la mac de PC2, il l'enregistre dans sa table ARP




🌞 Check the ARP table

 ```
 arp -a

Interface : 10.10.10.70 --- 0x4
  Adresse Internet      Adresse physique      Type
  10.10.10.69           4c-e1-73-43-80-06     dynamique
  ```
  MAC gateway 
  ```
  Interface : 10.33.16.156 --- 0x8
  Adresse Internet      Adresse physique      Type
  10.33.16.202          74-8f-3c-be-6e-b6     dynamique
  10.33.18.221          78-4f-43-87-f5-11     dynamique
  10.33.19.254          00-c0-e7-e0-04-4e     dynamique
  ```

celle de votre réseau physique, WiFi, genre YNOV, car il n'y en a pas dans votre ptit LAN
c'est juste pour vous faire manipuler un peu encore :)




Il peut être utile de ré-effectuer des ping avant d'afficher la table ARP. En effet : les infos stockées dans la table ARP ne sont stockées que temporairement. Ce laps de temps est de l'ordre de ~60 secondes sur la plupart de nos machines.

🌞 Manipuler la table ARP

PS C:\WINDOWS\system32> netsh interface IP delete arpcache
Ok.

🌞 Wireshark it

vous savez maintenant comment forcer un échange ARP : il sufit de vider la table ARP et tenter de contacter quelqu'un, l'échange ARP se fait automatiquement
mettez en évidence les deux trames ARP échangées lorsque vous essayez de contacter quelqu'un pour la "première" fois

déterminez, pour les deux trames, les adresses source et destination
déterminez à quoi correspond chacune de ces adresses



🦈 PCAP qui contient les trames ARP

L'échange ARP est constitué de deux trames : un ARP broadcast et un ARP reply.


# II.5 Interlude hackerzz
Chose promise chose due, on va voir les bases de l'usurpation d'identité en réseau : on va parler d'ARP poisoning.

On peut aussi trouver ARP cache poisoning ou encore ARP spoofing, ça désigne la même chose.

Le principe est simple : on va "empoisonner" la table ARP de quelqu'un d'autre.
Plus concrètement, on va essayer d'introduire des fausses informations dans la table ARP de quelqu'un d'autre.
Entre introduire des fausses infos et usurper l'identité de quelqu'un il n'y a qu'un pas hihi.

➜ Le principe de l'attaque

on admet Alice, Bob et Eve, tous dans un LAN, chacun leur PC
leur configuration IP est ok, tout va bien dans le meilleur des mondes

Eve 'lé pa jonti (ou juste un agent de la CIA) : elle aimerait s'immiscer dans les conversations de Alice et Bob

pour ce faire, Eve va empoisonner la table ARP de Bob, pour se faire passer pour Alice
elle va aussi empoisonner la table ARP d'Alice, pour se faire passer pour Bob
ainsi, tous les messages que s'envoient Alice et Bob seront en réalité envoyés à Eve



➜ La place de ARP dans tout ça

ARP est un principe de question -> réponse (broadcast -> reply)
IL SE TROUVE qu'on peut envoyer des reply à quelqu'un qui n'a rien demandé :)
il faut donc simplement envoyer :

une trame ARP reply à Alice qui dit "l'IP de Bob se trouve à la MAC de Eve" (IP B -> MAC E)
une trame ARP reply à Bob qui dit "l'IP de Alice se trouve à la MAC de Eve" (IP A -> MAC E)


ha ouais, et pour être sûr que ça reste en place, il faut SPAM sa mum, genre 1 reply chacun toutes les secondes ou truc du genre

bah ui ! Sinon on risque que la table ARP d'Alice ou Bob se vide naturellement, et que l'échange ARP normal survienne
aussi, c'est un truc possible, mais pas normal dans cette utilisation là, donc des fois bon, ça chie, DONC ON SPAM

➜ J'peux vous aider à le mettre en place, mais vous le faites uniquement dans un cadre privé, chez vous, ou avec des VMs
➜ Je vous conseille 3 machines Linux, Alice Bob et Eve. La commande [arping](https://sandilands.info/sgordon/arp-spoofing-on-wired-lan) pourra vous carry : elle permet d'envoyer manuellement des trames ARP avec le contenu de votre choix.
GLHF.

# III. DHCP you too my brooo
DHCP pour Dynamic Host Configuration Protocol est notre p'tit pote qui nous file des IPs quand on arrive dans un réseau, parce que c'est chiant de le faire à la main :)
Quand on arrive dans un réseau, notre PC contacte un serveur DHCP, et récupère généralement 3 infos :


1. une IP à utiliser

2. l'adresse IP de la passerelle du réseau

3. l'adresse d'un serveur DNS joignable depuis ce réseau

L'échange DHCP  entre un client et le serveur DHCP consiste en 4 trames : DORA, que je vous laisse chercher sur le web vous-mêmes : D
🌞 Wireshark it

🦈 PCAP qui contient l'échange DORA


**echange DORA impossible sur win 11 ( j'ai vu avec toi )**