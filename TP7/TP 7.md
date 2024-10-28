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

## 2. On rajoute un S

#### A. Config

### 🌞 Lister les ports en écoute sur la machine

```
[root@web ~]# ss -lnpt | grep :443

LISTEN 0      511        10.7.1.11:443       0.0.0.0:*    users:(("nginx",pid=1326,fd=6),("nginx",pid=1325,fd=6))
```

### 🌞 Gérer le firewall

```
[root@web ~]# firewall-cmd --permanent --add-port=443/tcp

success

[root@web ~]# firewall-cmd --permanent --remove-port=80/tcp

success

[root@web ~]# firewall-cmd --reload

success
```

#### B. Test test test analyyyze

### 🌞 Capture tcp_https.pcap

voir tcp_https.pcap

# III. Serveur VPN

## 1. Install et conf Wireguard

### 🌞 Prouvez que vous avez bien une nouvelle carte réseau wg0

```
[root@vpn ~]# ip a

5: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none
    inet 10.7.200.1/24 scope global wg0
       valid_lft forever preferred_lft forever
```

### 🌞 Déterminer sur quel port écoute Wireguard

```
[root@vpn ~]# ss -lnpu | grep :51820

UNCONN 0      0            0.0.0.0:51820      0.0.0.0:*
UNCONN 0      0               [::]:51820         [::]:*
```

### 🌞 Ouvrez ce port dans le firewall

```
[root@vpn ~]# firewall-cmd --permanent --add-port=51820/udp

success
```

## 2. Ajout d'un client VPN

/

## 3. Proofs

### 🌞 Ping ping ping !

```
louis@client1:~$ ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
64 bytes from 10.7.200.1: icmp_seq=1 ttl=64 time=1.73 ms
64 bytes from 10.7.200.1: icmp_seq=2 ttl=64 time=1.07 ms
64 bytes from 10.7.200.1: icmp_seq=3 ttl=64 time=1.04 ms
64 bytes from 10.7.200.1: icmp_seq=4 ttl=64 time=1.78 ms
^C
--- 10.7.200.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 1.037/1.405/1.784/0.351 ms
```

### 🌞 Capture ping1_vpn.pcap

voir ping1_vpn.pcap

### 🌞 Capture ping2_vpn.pcap

voir ping2_vpn.pcap

### 🌞 Prouvez que vous avez toujours un accès internet

```
louis@client1:~$ traceroute 1.1.1.1

traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
 1  10.7.200.1 (10.7.200.1)  3.548 ms  2.944 ms  2.415 ms
```

## 4. Private service

### 🌞 Visitez le service Web à travers le VPN

```
[root@web ~]# curl https://sitedefou.tp7.b1 -k

meow!
```