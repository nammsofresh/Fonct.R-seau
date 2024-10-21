# I. Le setup

## 2. Marche à suivre

### ☀️ Prouvez que...

> une machine du LAN1 peut joindre internet (ping un nom de domaine)
```
[root@dhcp ~]# ping google.com

PING google.com (142.251.37.46) 56(84) bytes of data.
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=1 ttl=112 time=17.8 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=2 ttl=112 time=20.5 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=3 ttl=112 time=18.6 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=4 ttl=112 time=18.5 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 17.784/18.856/20.502/1.003 ms
```

> une machine du LAN2 peut joindre internet (ping nom de domaine)
```
[root@web ~]# ping google.com

PING google.com (142.250.200.238) 56(84) bytes of data.
64 bytes from mrs08s18-in-f14.1e100.net (142.250.200.238): icmp_seq=1 ttl=111 time=17.5 ms
64 bytes from mrs08s18-in-f14.1e100.net (142.250.200.238): icmp_seq=2 ttl=111 time=18.7 ms
64 bytes from mrs08s18-in-f14.1e100.net (142.250.200.238): icmp_seq=3 ttl=111 time=20.0 ms
64 bytes from mrs08s18-in-f14.1e100.net (142.250.200.238): icmp_seq=4 ttl=111 time=17.2 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3006ms
rtt min/avg/max/mdev = 17.169/18.342/19.987/1.104 ms
```

> une machine du LAN1 peut joindre une machine du LAN2 (ping une adresse IP)
```
[root@dhcp ~]# ping 10.6.2.11

PING 10.6.2.11 (10.6.2.11) 56(84) bytes of data.
64 bytes from 10.6.2.11: icmp_seq=1 ttl=63 time=1.54 ms
64 bytes from 10.6.2.11: icmp_seq=2 ttl=63 time=1.49 ms
64 bytes from 10.6.2.11: icmp_seq=3 ttl=63 time=1.97 ms
64 bytes from 10.6.2.11: icmp_seq=4 ttl=63 time=1.72 ms
^C
--- 10.6.2.11 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 1.491/1.680/1.967/0.186 ms
```

# II. LAN clients

## 2. Client

### ☀️ Prouvez que...

> le client a bien récupéré une adresse IP en DHCP

```
louis@client1:~$ ip a

2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:12:19:e6 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.37/24 metric 100 brd 10.6.1.255 scope global dynamic enp0s8
       valid_lft 380sec preferred_lft 380sec
    inet6 fe80::a00:27ff:fe12:19e6/64 scope link 
       valid_lft forever preferred_lft forever
```

> vous avez bien 1.1.1.1 en DNS
```
louis@client1:~$ cat /etc/resolv.conf 

nameserver 1.1.1.1
options edns0 trust-ad
search .
```

> vous avez bien la bonne passerelle indiquée
```
louis@client1:~$ ip route

default via 10.6.1.254 dev enp0s8 proto dhcp src 10.6.1.37 metric 100 
1.1.1.1 via 10.6.1.254 dev enp0s8 proto dhcp src 10.6.1.37 metric 100 
10.6.1.0/24 dev enp0s8 proto kernel scope link src 10.6.1.37 metric 100 
10.6.1.254 dev enp0s8 proto dhcp scope link src 10.6.1.37 metric 100
```

> que ça ping un nom de domaine public sans problème magueule
```
louis@client1:~$ ping google.com

PING google.com (142.251.37.46) 56(84) bytes of data.
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=1 ttl=112 time=19.5 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=2 ttl=112 time=19.0 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=3 ttl=112 time=17.9 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=4 ttl=112 time=18.4 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 17.880/18.712/19.513/0.610 ms
```

# III. LAN serveurzzzz

## 1. Serveur Web

### ☀️ Déterminer sur quel port écoute le serveur NGINX
```
[root@web ~]# ss -tuln | grep :80

tcp   LISTEN 0      511          0.0.0.0:80        0.0.0.0:*
tcp   LISTEN 0      511             [::]:80           [::]:*
```
### ☀️ Ouvrir ce port dans le firewall
```
[root@web ~]# firewall-cmd --zone=public --permanent --add-service=http

success

[root@web ~]# firewall-cmd --reload

success
```
### ☀️ Visitez le site web !
```
louis@client1:~$ curl http://10.6.2.11
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/
      
      html {
        height: 100%;
        width: 100%;
      }  
```

## 2. Serveur DNS

### ☀️ Déterminer sur quel(s) port(s) écoute le service BIND9

```
[root@dns ~]# ss -tuln | grep :53

udp   UNCONN 0      0          10.6.2.12:53        0.0.0.0:*
udp   UNCONN 0      0          127.0.0.1:53        0.0.0.0:*
udp   UNCONN 0      0              [::1]:53           [::]:*
tcp   LISTEN 0      10         10.6.2.12:53        0.0.0.0:*
tcp   LISTEN 0      10         127.0.0.1:53        0.0.0.0:*
tcp   LISTEN 0      10             [::1]:53           [::]:*
```

### ☀️ Ouvrir ce(s) port(s) dans le firewall

```
[root@dns ~]# firewall-cmd --zone=public --permanent --add-port=53/tcp

success

[root@dns ~]# firewall-cmd --zone=public --permanent --add-port=53/udp

success

[root@dns ~]# firewall-cmd --reload

success
```
### ☀️ Effectuez des requêtes DNS manuellement depuis le serveur DNS lui-même dans un premier temps
```
[root@dns ~]# dig web.tp6.b1 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> web.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 29348
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 23612a7e60b375890100000067161422baeb6ccff81d3f8e (good)
;; QUESTION SECTION:
;web.tp6.b1.                    IN      A

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 10:43:14 CEST 2024
;; MSG SIZE  rcvd: 83
```
```
[root@dns ~]# dig dns.tp6.b1 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> dns.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 60268
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 1590f5dd0b6aeefa0100000067161466c675bfe4af76976b (good)
;; QUESTION SECTION:
;dns.tp6.b1.                    IN      A

;; ANSWER SECTION:
dns.tp6.b1.             86400   IN      A       10.6.2.12

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 10:44:22 CEST 2024
;; MSG SIZE  rcvd: 83
```
```
[root@dns ~]# dig ynov.com @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> ynov.com @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 5639
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 4fb8f9cacdaec1d40100000067161484cf1a7320e0ce5086 (good)
;; QUESTION SECTION:
;ynov.com.                      IN      A

;; ANSWER SECTION:
ynov.com.               300     IN      A       104.26.11.233
ynov.com.               300     IN      A       104.26.10.233
ynov.com.               300     IN      A       172.67.74.226

;; Query time: 466 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 10:44:52 CEST 2024
;; MSG SIZE  rcvd: 113
```
```
[root@dns ~]# dig -x 10.6.2.11 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.11 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 31047
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 4b0df59752f99acd010000006716149760f5604f439fd3b8 (good)
;; QUESTION SECTION:
;11.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
11.2.6.10.in-addr.arpa. 86400   IN      PTR     web.tp6.b1.

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 10:45:11 CEST 2024
;; MSG SIZE  rcvd: 103
```
```
[root@dns ~]# dig -x 10.6.2.12 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.12 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 14207
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 1c946a05fff2830c01000000671614a902eb9f1cfbb46b1a (good)
;; QUESTION SECTION:
;12.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
12.2.6.10.in-addr.arpa. 86400   IN      PTR     dns.tp6.b1.

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 10:45:29 CEST 2024
;; MSG SIZE  rcvd: 103
```

### ☀️ Effectuez une requête DNS manuellement depuis client1.tp6.b1

```
louis@client1:~$ dig web/tp6.b1 @10.6.2.12

; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> web/tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 11393
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 23a35526d6a928680100000067161525991231ec0dc84d3c (good)
;; QUESTION SECTION:
;web/tp6.b1.			IN	A

;; AUTHORITY SECTION:
.			10800	IN	SOA	a.root-servers.net. nstld.verisign-grs.com. 2024102100 1800 900 604800 86400

;; Query time: 124 msec
;; SERVER: 10.6.2.12#53(10.6.2.12) (UDP)
;; WHEN: Mon Oct 21 10:47:33 CEST 2024
;; MSG SIZE  rcvd: 142
```

### ☀️ Capturez une requête DNS et la réponse de votre serveur

voir dns_query.pcap

## 3. Serveur DHCP

### ☀️ Créez un nouveau client client2.tp6.b1 vitefé

> récupérez une IP en DHCP sur ce nouveau client2.tp6.b1

```
louis@client1:~$ ip a

2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:2c:24:80 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.38/24 metric 100 brd 10.6.1.255 scope global dynamic enp0s8
       valid_lft 545sec preferred_lft 545sec
    inet6 fe80::a00:27ff:fe2c:2480/64 scope link 
       valid_lft forever preferred_lft forever
```

> vérifiez que vous avez bien 10.6.2.12 comme serveur DNS à contacter

```
louis@client1:~$ cat /etc/resolv.conf

nameserver 10.6.2.12
options edns0 trust-ad
search .
```

> vous devriez pouvoir visiter http://web.tp6.b1 avec le navigateur, ça devrait fonctionner sans aucune autre action.

```
louis@client1:~$ curl http://web.tp6.b1
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/
      
      html {
        height: 100%;
        width: 100%;
      }  
        body {
  background: rgb(20,72,50);
  background: -moz-linear-gradient(180deg, rgba(23,43,70,1) 30%, rgba(0,0,0,1) 90%)  ;
  ```