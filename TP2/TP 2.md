# I. Quelques pings

### 🌞 Prouvez que votre configuration est effective

```
> Get-NetIPAddress -InterfaceAlias "Ethernet"


IPAddress         : fe80::74b8:8023:bacc:c993%11
InterfaceIndex    : 11
InterfaceAlias    : Ethernet
AddressFamily     : IPv6
Type              : Unicast
PrefixLength      : 64
PrefixOrigin      : WellKnown
SuffixOrigin      : Link
AddressState      : Preferred
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore

IPAddress         : 10.1.1.2
InterfaceIndex    : 11
InterfaceAlias    : Ethernet
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 16
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Preferred
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore

```
### 🌞 Tester que votre LAN + votre adressage IP est fonctionnel

```
> ping 10.1.1.1

Envoi d’une requête 'Ping'  10.1.1.1 avec 32 octets de données :
Réponse de 10.1.1.1 : octets=32 temps=3 ms TTL=128
Réponse de 10.1.1.1 : octets=32 temps=1 ms TTL=128
Réponse de 10.1.1.1 : octets=32 temps=1 ms TTL=128
Réponse de 10.1.1.1 : octets=32 temps=2 ms TTL=128

Statistiques Ping pour 10.1.1.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 1ms, Maximum = 3ms, Moyenne = 1ms
```

### 🌞 Capture de ping

> voir fichier ping.pcap

# II. Utilisation des ports

### 🌞 Sur le PC serveur

```
> nc.exe -l -p 6676
```

### 🌞 Sur le PC serveur toujours
```
> netstat -a -b -n

 TCP    0.0.0.0:6676           0.0.0.0:0              LISTENING
 [nc.exe]
 ```

### 🌞 Utilisez une commande qui permet de voir la connexion en cours

```
> netstat -a -b -n

 TCP    10.1.1.2:6676          10.1.1.1:52953         ESTABLISHED
 [nc.exe]
```

### 🌞 Faites une capture Wireshark complète d'un échange

> voir netcat1.pcap

### 🌞 Inversez les rôles

> voir netcat2.pcap

#### -> Sur PC Client

```
> nc 10.1.1.1 7767
 ```

```
> netstat -a -b -n
 TCP    10.1.1.2:57578         10.1.1.1:7767          ESTABLISHED
 [nc.exe]
 ```

# III. Analyse de vos applications usuelles

## 1. Serveur web

### 🌞 Utilisez Wireshark pour capturer du trafic HTTP

> voir http.pcap

## 2. Autres services

### 🌞 Pour les 5 applications

#### Service 1 (Brave)

> voir service1.pcap

 ```
 > netstat -a -b -n

 TCP    10.33.77.173:57808     172.64.41.3:443        ESTABLISHED
 [brave.exe]
 ```
#### Service 2 (Spotify)

> voir service2.pcap

 ```
 > netstat -a -b -n

 TCP    10.33.77.173:57945     199.232.210.250:443        ESTABLISHED
 [Spotify.exe]
 ```
#### Service 3 (Xbox PcApp)
 
 > voir service 3.pcap
 
 ```
 > netstat -a -b -n

 TCP    10.33.77.173:58115     23.33.232.7:443        ESTABLISHED
 [XboxPcApp.exe]
 ```

 #### Service 4 (RiotClient)

> voir service4.pcap

 ```
 TCP    10.33.77.173:58398     172.65.252.238:5223   ESTABLISHED
 [RiotClientServices.exe]
 ```

 #### Service 5 (Rpcs3)

> voir service5.pcap

```
> netstat -a -b -n

 TCP    10.33.77.173:4259      104.26.0.191:443       ESTABLISHED
 [rpcs3.exe]
```