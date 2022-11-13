# I. First steps


## Site : Spotify qui utilise du TCP

IP : 104.199.65.124

Port source : 3311
Port destinataire : 4070



## Site : Discord qui utilise du TCP

IP : 162.159.133.234

Port source : 11930
Port destinataire : 443

## Site : Telegram qui utilise du TCP

IP : 95.100.95.167

Port source : 1110
Port destinataire : 443

## 🌞 Demandez l'avis à votre OS


Site : Spotify qui utilise du TCP


🦈 Capture Wireshark



```C:\Users\33785>netstat -an | findstr 4070
    TCP    192.168.1.20:3311      104.199.65.124:4070    ESTABLISHED
````



Site : Discord qui utilise du TCP


🦈 Capture Wireshark


```
C:\Users\33785>netstat -an | findstr 162.159
    TCP    192.168.1.20:1024      162.159.136.234:https  ESTABLISHED 
```




Site : Telegram qui utilise du TCP


🦈 Capture Wireshark

```C:\Users\33785>netstat -an | findstr 1110
    TCP    192.168.1.20:1110      95.100.95.167:443      ESTABLISHED
    ```