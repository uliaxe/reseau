# TP1 - Premier pas réseau

# I. Exploration locale en solo
## 1. Affichage d'informations sur la pile TCP/IP locale
interface wifi :
commande ipconfig /all 
```Description . . . . . . . . . . . : MediaTek Wi-Fi 6 MT7921 Wireless LAN Card
 Physical Address. . . . . . . . . : 14-13-33-F9-BB-EB
 IPv4 Address. . . . . . . . . . . : 10.33.16.146(Preferred)
 ```
 
 interface ethernet :
commande : ipconfig /all
```Description . . . . . . . . . . . : Realtek PCIe GbE Family Controller
 Physical Address. . . . . . . . . : 50-EB-F6-E4-41-70
 ip existe pas == non connecté
 ```
 
 gateway : ipconfig 
 ```
   Default Gateway . . . . . . . . . : 10.33.19.254
   ```
 
 MAC gateway :

```C:\Users\lukas>arp -a

Interface: 192.168.32.1 --- 0xa
  Internet Address      Physical Address      Type
  192.168.32.254        00-50-56-ec-34-93     dynamic
  192.168.32.255        ff-ff-ff-ff-ff-ff     static
  224.0.0.2             01-00-5e-00-00-02     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  224.77.77.77          01-00-5e-4d-4d-4d     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static

Interface: 10.33.16.146 --- 0xb
  Internet Address      Physical Address      Type
  10.33.19.254          00-c0-e7-e0-04-4e     dynamic
  10.33.19.255          ff-ff-ff-ff-ff-ff     static
  224.0.0.2             01-00-5e-00-00-02     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  224.77.77.77          01-00-5e-4d-4d-4d     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static

Interface: 192.168.136.1 --- 0x12
  Internet Address      Physical Address      Type
  192.168.136.254       00-50-56-e5-8e-b5     dynamic
  192.168.136.255       ff-ff-ff-ff-ff-ff     static
  224.0.0.2             01-00-5e-00-00-02     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  224.77.77.77          01-00-5e-4d-4d-4d     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static
  ```
  MAC : 10.33.19.254          00-c0-e7-e0-04-4e
  ### 2. Modifications des informations
  GUI :
IP : 10.33.16.146
MAC : 14-13-33-F9-BB-EB
gateway : Connection-specific DNS Suffix: 
IPv4 Default Gateway: 10.33.19.254 (control panel)

si IP changé l'adresse n'est pas reconnu par le server ainsi que par le DHCP

# II. Exploration locale en duo
## 3. Modification d'adresse IP
10.10.10.15


C:\Users\lukas>ping 10.10.10.16

Pinging 10.10.10.16 with 32 bytes of data:
Reply from 10.10.10.16: bytes=32 time=3ms TTL=128
Reply from 10.10.10.16: bytes=32 time=2ms TTL=128
Reply from 10.10.10.16: bytes=32 time=2ms TTL=128
Reply from 10.10.10.16: bytes=32 time=2ms TTL=128

Ping statistics for 10.10.10.16:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 2ms, Maximum = 3ms, Average = 2ms
    
   ``` C:\Users\lukas>arp -a

Interface: 10.10.10.15 --- 0x4
  Internet Address      Physical Address      Type
  10.10.10.16           50-81-40-84-ab-fc     dynamic
  10.10.10.255          ff-ff-ff-ff-ff-ff     static
  224.0.0.2             01-00-5e-00-00-02     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static
  ```
  
  adresse MAC : dynamic
  
  ## 4. Utilisation d'un des deux comme gateway
  C:\Users\lukas>tracert 192.168.137.1

Tracing route to LAPTOP-DS0S1GKI [192.168.137.1]
over a maximum of 30 hops:

  1     1 ms     1 ms     1 ms  LAPTOP-DS0S1GKI [192.168.137.1]

Trace complete.

C:\Users\lukas>
## 5. Petit chat privé

pc server 

netcat-1.11>nc.exe -l -p 8888
```
cccccccccccccc
cccc
helooo
```
pc client 
C:\Users\Joel\netcat-1.11>nc.exe -l -p 8888
```
hu
ho
```

Pour aller un peu plus loin
```
Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    10.33.16.169:7680      10.33.19.112:62998     TIME_WAIT
  TCP    10.33.16.169:7680      10.33.19.112:63001     TIME_WAIT
  TCP    10.33.16.169:7680      10.33.19.112:63004     TIME_WAIT
  TCP    10.33.16.169:49590     25:https               CLOSE_WAIT
  TCP    10.33.16.169:49797     20.54.232.160:https    ESTABLISHED
  TCP    10.33.16.169:49802     ec2-3-218-125-188:https  ESTABLISHED
  TCP    10.33.16.169:49803     ec2-3-218-125-188:https  ESTABLISHED
  TCP    10.33.16.169:49861     52.155.161.106:https   ESTABLISHED
  TCP    10.33.16.169:49872     172.64.108.2:https     CLOSE_WAIT
  TCP    10.33.16.169:49882     a865a9e11bc2c0d65:https  ESTABLISHED
  TCP    10.33.16.169:54338     ws-in-f188:5228        ESTABLISHED
  TCP    10.33.16.169:54344     20.90.152.133:https    ESTABLISHED
  TCP    10.33.16.169:57704     a865a9e11bc2c0d65:https  ESTABLISHED
  TCP    10.33.16.169:61377     37.244.54.10:1119      ESTABLISHED
  TCP    10.33.16.169:61380     124:4070               ESTABLISHED
  TCP    10.33.16.169:61383     47:https               ESTABLISHED
  TCP    10.33.16.169:61432     20.199.120.151:https   ESTABLISHED
  TCP    10.33.16.169:61462     40:https               ESTABLISHED
  TCP    10.33.16.169:65166     162.159.134.234:https  ESTABLISHED
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49835  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49836  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49837  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49838  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49839  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49840  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49841  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49842  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49843  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49845  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49846  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49847  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49848  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49849  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49851  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49852  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49853  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49854  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49855  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49856  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49857  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49858  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49859  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49863  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49864  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49865  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49866  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49867  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49868  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49869  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49870  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49871  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49873  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49874  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49875  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49876  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49877  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49878  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49879  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49880  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49881  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49883  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49886  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49887  TIME_WAIT
  TCP    127.0.0.1:1120         LAPTOP-DS0S1GKI:49888  TIME_WAIT
  TCP    127.0.0.1:6463         LAPTOP-DS0S1GKI:57179  ESTABLISHED
  TCP    127.0.0.1:9010         LAPTOP-DS0S1GKI:61208  ESTABLISHED
  TCP    127.0.0.1:9010         LAPTOP-DS0S1GKI:61211  ESTABLISHED
  TCP    127.0.0.1:9100         LAPTOP-DS0S1GKI:61210  ESTABLISHED
  TCP    127.0.0.1:49836        LAPTOP-DS0S1GKI:1120   TIME_WAIT
  TCP    127.0.0.1:49847        LAPTOP-DS0S1GKI:1120   TIME_WAIT
  TCP    127.0.0.1:49854        LAPTOP-DS0S1GKI:1120   TIME_WAIT
  TCP    127.0.0.1:57179        LAPTOP-DS0S1GKI:6463   ESTABLISHED
  TCP    127.0.0.1:61208        LAPTOP-DS0S1GKI:9010   ESTABLISHED
  TCP    127.0.0.1:61210        LAPTOP-DS0S1GKI:9100   ESTABLISHED
  TCP    127.0.0.1:61211        LAPTOP-DS0S1GKI:9010   ESTABLISHED
  TCP    127.0.0.1:61399        LAPTOP-DS0S1GKI:61400  ESTABLISHED
  TCP    127.0.0.1:61400        LAPTOP-DS0S1GKI:61399  ESTABLISHED
  ```
  # III. Manipulations d'autres outils/protocoles côté client
  ## 1. DHCP
  DHCP 
   DHCP Server . . . . . . . . . . . : 10.33.19.254
   
 Lease Obtained. . . . . . . . . . : Tuesday, October 4, 2022 1:37:31 PM
   Lease Expires . . . . . . . . . . : Wednesday, October 5, 2022 1:37:31 PM
   ## 2. DNS

DNS    
 DNS Servers . . . . . . . . . . . : 8.8.8.8
                                       8.8.4.4
                                       1.1.1.1
                                       



C:\Users\lukas>nslookup google.com
Server:  dns.google
Address:  8.8.8.8

Non-authoritative answer:
Name:    google.com
Addresses:  2a00:1450:4007:813::200e
          142.250.179.78


C:\Users\lukas>nslookup ynov.com
Server:  dns.google
Address:  8.8.8.8

Non-authoritative answer:
Name:    ynov.com
Addresses:  2606:4700:20::681a:ae9
          2606:4700:20::ac43:4ae2
          2606:4700:20::681a:be9
          104.26.11.233
          104.26.10.233
          172.67.74.226
          
Ynov a plusieurs serveurs web d'ou plusieurs adresses 

C:\Users\lukas>nslookup 231.34.113.12
Server:  dns.google
Address:  8.8.8.8

*** dns.google can't find 231.34.113.12: Non-existent domain

C:\Users\lukas>nslookup 78.34.2.17
Server:  dns.google
Address:  8.8.8.8

Name:    cable-78-34-2-17.nc.de
Address:  78.34.2.17

# IV. Wireshark
## 1. Intro Wireshark
 ping 
![](https://i.imgur.com/8IzbThU.png)

netcat 
![](https://i.imgur.com/BjHoq0K.png)

DNS 
![](https://i.imgur.com/zLfMYHJ.png)

## 2. Bonus : avant-goût TCP et UDP

wireshark it : youtube 
![](https://i.imgur.com/wIvGk3r.png)

