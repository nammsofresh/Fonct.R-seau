# I. ARP basics

### ☀️ Avant de continuer...

```
> ipconfig /all

Adresse physique . . . . . . . . . . . : 10-68-38-8E-2E-EF
```

### ☀️ Affichez votre table ARP

```
> arp -a

Interface : 10.33.77.173 --- 0xc
  Adresse Internet      Adresse physique      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.77.77.77          01-00-5e-4d-4d-4d     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

### ☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école

```
> arp -a

10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
```

### ☀️ Supprimez la ligne qui concerne la passerelle

```
> PS C:\Windows\system32> arp -d  10.33.79.254
> PS C:\Windows\system32> arp -a

Interface : 10.33.77.173 --- 0xc
  Adresse Internet      Adresse physique      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.77.77.77          01-00-5e-4d-4d-4d     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

### ☀️ Wireshark

> voir fichier arp1.pcap

[arp2](arp1.pcap)

# II. ARP dans un réseau local

## 1. Basics

### ☀️ Déterminer

```
> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Adresse physique . . . . . . . . . . . : 10-68-38-8E-2E-EF
   Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.8(préféré)
   ```

### ☀️ DIY

```
> Get-NetIPAddress -InterfaceAlias "Wi-Fi"

IPAddress         : 2a01:cb01:3077:2c01:40c:5e11:2ecf:77a6
InterfaceIndex    : 12
InterfaceAlias    : Wi-Fi
AddressFamily     : IPv6
Type              : Unicast
PrefixLength      : 128
PrefixOrigin      : RouterAdvertisement
SuffixOrigin      : Random
AddressState      : Preferred
ValidLifetime     : 6.23:53:50
PreferredLifetime : 6.23:51:04
SkipAsSource      : False
PolicyStore       : ActiveStore

IPAddress         : 172.20.10.4
InterfaceIndex    : 12
InterfaceAlias    : Wi-Fi
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 28
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Preferred
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore
```

### ☀️ Pingz !

```
> PS C:\Windows\system32> ping 172.20.10.2

Envoi d’une requête 'Ping'  172.20.10.2 avec 32 octets de données :
Réponse de 172.20.10.2 : octets=32 temps=21 ms TTL=128
Réponse de 172.20.10.2 : octets=32 temps=14 ms TTL=128
Réponse de 172.20.10.2 : octets=32 temps=5 ms TTL=128
Réponse de 172.20.10.2 : octets=32 temps=7 ms TTL=128

Statistiques Ping pour 172.20.10.2:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 5ms, Maximum = 21ms, Moyenne = 11ms
```

```
> PS C:\Windows\system32> ping 172.20.10.9

Envoi d’une requête 'Ping'  172.20.10.9 avec 32 octets de données :
Réponse de 172.20.10.9 : octets=32 temps=26 ms TTL=128
Réponse de 172.20.10.9 : octets=32 temps=28 ms TTL=128
Réponse de 172.20.10.9 : octets=32 temps=578 ms TTL=128
Réponse de 172.20.10.9 : octets=32 temps=890 ms TTL=128

Statistiques Ping pour 172.20.10.9:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 26ms, Maximum = 890ms, Moyenne = 380ms
```

```
> PS C:\Windows\system32> ping google.com

Envoi d’une requête 'ping' sur google.com [2a00:1450:4007:80c::200e] avec 32 octets de données :
Réponse de 2a00:1450:4007:80c::200e : temps=47 ms
Réponse de 2a00:1450:4007:80c::200e : temps=91 ms
Réponse de 2a00:1450:4007:80c::200e : temps=56 ms
Réponse de 2a00:1450:4007:80c::200e : temps=43 ms

Statistiques Ping pour 2a00:1450:4007:80c::200e:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 43ms, Maximum = 91ms, Moyenne = 59ms
```

## 2. ARP

### ☀️ Affichez votre table ARP !

```
> PS C:\Windows\system32> arp -a

Interface : 172.20.10.4 --- 0xc
  Adresse Internet      Adresse physique      Type
  172.20.10.1           e6-b2-fb-e8-21-64     dynamique
  172.20.10.2           28-c5-d2-03-3c-2f     dynamique
  172.20.10.9           2c-98-11-56-bf-f1     dynamique
  172.20.10.15          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.77.77.77          01-00-5e-4d-4d-4d     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  ```

### ☀️ Capture arp2.pcap

> voir fichier arp2.pcap

[arp2](arp2.pcap)

## 3. Bonus : ARP poisoning

### ⭐ Empoisonner la table ARP de l'un des membres de votre réseau

### ⭐ Mettre en place un MITM







