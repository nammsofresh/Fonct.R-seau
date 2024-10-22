# TP7 : On dit chiffrer pas crypter

# I. Setup

ez

# II. Serveur Web

## 1. HTTP

### 🌞 Lister les ports en écoute sur la machine

```
[root@web ~]# ss -lnpt | grep :80

LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1319,fd=6),("nginx",pid=1318,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1319,fd=7),("nginx",pid=1318,fd=7))
```

### 🌞 Ouvrir le port dans le firewall de la machine

```
[root@web ~]# firewall-cmd --permanent --add-port=80/tcp
success
[root@web ~]# firewall-cmd --reload
success
```

### 🌞 Vérifier que ça a pris effet

```
louis@client1:~$ ping sitedefou.tp7.b1

PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=2.01 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=1.12 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=3 ttl=64 time=1.13 ms
^C
--- sitedefou.tp7.b1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2001ms
rtt min/avg/max/mdev = 1.116/1.419/2.014/0.420 ms
```
```
louis@client1:~$ curl sitedefou.tp7.b1 
meow!
```

### 🌞 Capture tcp_http.pcap

voir tcp_http.pcap

### 🌞 Voir la connexion établie

```
louis@client1:~$ sudo ss -tun
Netid             State             Recv-Q             Send-Q                          Local Address:Port                             Peer Address:Port             Process             
tcp               ESTAB             0                  0                                  10.7.1.101:40582                           34.107.243.93:443                                  
tcp               ESTAB             0                  0                                  10.7.1.101:57032                               10.7.1.11:80 
```