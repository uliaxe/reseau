# serveur Vpn

## connexion ssh

pour ce connecter a la machine en ssh :

```bash
ssh-keygen -t rsa -b 4096
````

## installation du vpn

avec Wireguard

il faut tout d'abord installer Wireguard

```bash
sudo apt install wireguard
```

on vient ensuite créer une nouvelle paire de clé

```bash
wg genkey | sudo tee /etc/wireguard/private.key
```
ensuite on va choisir une adresse ipv4 pour le serveur




