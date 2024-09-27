# I. Récolte d'informations

### 🌞

> ipconfig
```
Carte Ethernet Ethernet 3 :

Adresse physique . . . . . . . . . . . : 0A-00-27-00-00-10
DHCP activé. . . . . . . . . . . . . . : Non
Configuration automatique activée. . . : Oui
Adresse IPv6 de liaison locale. . . . .: fe80::40c6:9c01:d294:42c1%16(préféré)
Adresse IPv4. . . . . . . . . . . . . .: 192.168.56.1(préféré)
Masque de sous-réseau. . . . . . . . . : 255.255.255.0
Passerelle par défaut. . . . . . . . . :
IAID DHCPv6 . . . . . . . . . . . : 705298471

Carte réseau sans fil Wi-Fi :

Adresse physique . . . . . . . . . . . : 10-68-38-8E-2E-EF
DHCP activé. . . . . . . . . . . . . . : Oui
Configuration automatique activée. . . : Oui
Adresse IPv6 de liaison locale. . . . .: fe80::c983:3505:f92:ec40%12(préféré)
Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.173(préféré)
Masque de sous-réseau. . . . . . . . . : 255.255.240.0
Bail obtenu. . . . . . . . . . . . . . : vendredi 27 septembre 2024 08:58:03
Bail expirant. . . . . . . . . . . . . : samedi 28 septembre 2024 08:58:05
Passerelle par défaut. . . . . . . . . : 10.33.79.254
Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
IAID DHCPv6 . . . . . . . . . . . : 135292984
```
### 🌟

> (Get-Service -Name "MpsSvc").Status
```
Running
```
>Get-NetFirewallRule
```
Profile                       : Domain, Private
Platform                      : {}
Direction                     : Inbound
Action                        : Allow
EdgeTraversalPolicy           : Block
LooseSourceMapping            : False
LocalOnlyMapping              : False
Owner                         :
PrimaryStatus                 : OK
Status                        : La règle a été analysée à partir de la banque. (65536)
EnforcementStatus             : NotApplicable
PolicyStoreSource             : PersistentStore
PolicyStoreSourceType         : Local
RemoteDynamicKeywordAddresses : {}
PolicyAppId                   :
...
```
# II. Utiliser le réseau

### 🌞

> ping 10.33.77.173
```
Envoi d’une requête 'Ping'  10.33.77.173 avec 32 octets de données :
Réponse de 10.33.77.173 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.173 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.173 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.173 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 10.33.77.173:
Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```
> ping 127.0.0.1
```
Envoi d’une requête 'Ping'  127.0.0.1 avec 32 octets de données :
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 127.0.0.1:
Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```
> ping 10.33.79.254
```
Envoi d’une requête 'Ping'  10.33.79.254 avec 32 octets de données :
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.

Statistiques Ping pour 10.33.79.254:
Paquets : envoyés = 4, reçus = 0, perdus = 4 (perte 100%),
```
> ping 10.33.66.78
```
Envoi d’une requête 'Ping'  10.33.66.78 avec 32 octets de données :
Réponse de 10.33.66.78 : octets=32 temps=86 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=26 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=96 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=120 ms TTL=64

Statistiques Ping pour 10.33.66.78:
Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
Minimum = 26ms, Maximum = 120ms, Moyenne = 82ms
```
> ping www.thinkerview.com
```
Envoi d’une requête 'ping' sur www.thinkerview.com [188.114.96.6] avec 32 octets de données :
Réponse de 188.114.96.6 : octets=32 temps=17 ms TTL=55
Réponse de 188.114.96.6 : octets=32 temps=18 ms TTL=55
Réponse de 188.114.96.6 : octets=32 temps=24 ms TTL=55
Réponse de 188.114.96.6 : octets=32 temps=23 ms TTL=55

Statistiques Ping pour 188.114.96.6:
Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
Minimum = 17ms, Maximum = 24ms, Moyenne = 20ms
```
### 🌞

> Resolve-DnsName www.thinkerview.com
```
Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
www.thinkerview.com                            AAAA   300   Answer     2a06:98c1:3120::7
www.thinkerview.com                            AAAA   300   Answer     2a06:98c1:3121::7
www.thinkerview.com                            A      300   Answer     188.114.97.7
www.thinkerview.com                            A      300   Answer     188.114.96.7
```
> Resolve-DnsName www.wikileaks.org

```
Name                           Type   TTL   Section    NameHost
----                           ----   ---   -------    --------
www.wikileaks.org              CNAME  1800  Answer     wikileaks.org

Name       : wikileaks.org
QueryType  : A
TTL        : 1800
Section    : Answer
IP4Address : 51.159.197.136


Name       : wikileaks.org
QueryType  : A
TTL        : 1800
Section    : Answer
IP4Address : 80.81.248.21


Name                   : wikileaks.org
QueryType              : SOA
TTL                    : 1800
Section                : Authority
NameAdministrator      : root.wlinfra.org
SerialNumber           : 2022082502
TimeToZoneRefresh      : 21600
TimeToZoneFailureRetry : 3600
TimeToExpiration       : 604800
DefaultTTL             : 1800
```

> Resolve-DnsName www.torproject.org

```
Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
www.torproject.org                             AAAA   150   Answer     2a01:4f8:fff0:4f:266:37ff:feae:3bbc
www.torproject.org                             AAAA   150   Answer     2a01:4f8:fff0:4f:266:37ff:fe2c:5d19
www.torproject.org                             AAAA   150   Answer     2620:7:6002:0:466:39ff:fe32:e3dd
www.torproject.org                             AAAA   150   Answer     2a01:4f9:c010:19eb::1
www.torproject.org                             AAAA   150   Answer     2620:7:6002:0:466:39ff:fe7f:1826
www.torproject.org                             A      107   Answer     116.202.120.165
www.torproject.org                             A      107   Answer     116.202.120.166
www.torproject.org                             A      107   Answer     204.8.99.146
www.torproject.org                             A      107   Answer     95.216.163.36
www.torproject.org                             A      107   Answer     204.8.99.144 
```

# III. Sniffer le réseau

### 🌞

> dossier disponible sur github.com

# IV. Network scanning et adresses IP

### 🌞

> nmap.exe -sn -PR 10.33.64.0/20

```
Starting Nmap 7.95 ( https://nmap.org ) at 2024-09-27 11:46 Paris, Madrid (heure dÆÚtÚ)
Nmap scan report for 10.33.66.78
Host is up (0.20s latency).
MAC Address: E4:B3:18:48:36:68 (Intel Corporate)
Nmap scan report for 10.33.67.113
Host is up (0.057s latency).
MAC Address: D2:91:DE:DF:9A:6E (Unknown)
Nmap scan report for 10.33.69.68
Host is up (0.090s latency).
MAC Address: EE:E8:D9:89:3F:F1 (Unknown)
Nmap scan report for 10.33.69.89
Host is up (0.13s latency).
MAC Address: AC:C9:06:10:14:B6 (Apple)
Nmap scan report for 10.33.69.90
Host is up (0.020s latency).
MAC Address: 60:E9:AA:DD:EE:4D (Cloud Network Technology Singapore PTE.)
Nmap scan report for 10.33.69.92
Host is up (1.3s latency).
MAC Address: D2:8A:D4:B4:A0:6E (Unknown)
Nmap scan report for 10.33.69.96
Host is up (0.093s latency).
MAC Address: 3E:59:E5:D6:30:1F (Unknown)
Nmap scan report for 10.33.69.102
Host is up (0.27s latency).
MAC Address: F6:F2:C4:53:28:F5 (Unknown)
```
### 🌞

> netsh interface ip set address name="Wi-Fi" static 10.33.76.1 255.255.240.0 10.33.79.254

> netsh interface ip set dns name="Wi-Fi" static 8.8.8.8

> ipconfig

Configuration IP de Windows

Carte réseau sans fil Wi-Fi :

Suffixe DNS propre à la connexion. . . :
Adresse IPv6 de liaison locale. . . . .: fe80::c983:3505:f92:ec40%12
Adresse IPv4. . . . . . . . . . . . . .: 10.33.76.1
Masque de sous-réseau. . . . . . . . . : 255.255.240.0
Passerelle par défaut. . . . . . . . . : 10.33.79.254
