# I. Setup

### ☀️ Uniquement avec des commandes, prouvez-que :

### vous avez bien configuré les adresses IP demandées (un ip a suffit hein):
```
[louis@routeur ~]$ ip a

2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:eb:6d:dd brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 85143sec preferred_lft 85143sec
    inet6 fe80::a00:27ff:feeb:6ddd/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:c8:c1:dd brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fec8:c1dd/64 scope link
       valid_lft forever preferred_lft forever
```

```
> louis@client1:~$ ip a

2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:06:f8:72 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe06:f872/64 scope link 
       valid_lft forever preferred_lft forever
    inet6 fe80::dea8:7a5:2355:25c/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```
```
> louis@client2:~$ ip a

2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:ff:58:8b brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.12/24 brd 10.5.1.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:feff:588b/64 scope link 
       valid_lft forever preferred_lft forever
    inet6 fe80::a3f8:3bfc:c484:d041/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```


### vous avez bien configuré les hostnames demandés:

```
> [louis@routeur ~]$ hostnamectl

 Static hostname: routeur
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: ad6ac4a4e4b444488517d6148ac66d15
         Boot ID: 274d8a8d4f5944419d326aea4d4cf869
  Virtualization: oracle
Operating System: Rocky Linux 9.4 (Blue Onyx)
     CPE OS Name: cpe:/o:rocky:rocky:9::baseos
          Kernel: Linux 5.14.0-427.13.1.el9_4.x86_64
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
```
```
> louis@client1:~$ hostnamectl

 Static hostname: client1
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 593b66769f514ae9b5ef8484f513e3b4
         Boot ID: 41184ae7772144f8a23cffb25b303b32
  Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS              
          Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 1w 6d 
```
```
> louis@client2:~$ hostnamectl

 Static hostname: client2
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 593b66769f514ae9b5ef8484f513e3b4
         Boot ID: 4d58f28ea9654391a7b8f7d9cacc27cb
  Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS              
          Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 1w 6d 
```
### tout le monde peut se ping au sein du réseau 10.5.1.0/24:

```
> louis@client1:~$ ping 10.5.1.12

PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
64 bytes from 10.5.1.12: icmp_seq=1 ttl=64 time=0.668 ms
64 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=0.524 ms
64 bytes from 10.5.1.12: icmp_seq=3 ttl=64 time=0.542 ms
^C
--- 10.5.1.12 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2011ms
rtt min/avg/max/mdev = 0.524/0.578/0.668/0.064 ms
```
```
> louis@client2:~$ ping 10.5.1.11

PING 10.5.1.11 (10.5.1.11) 56(84) bytes of data.
64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=1.46 ms
64 bytes from 10.5.1.11: icmp_seq=2 ttl=64 time=0.555 ms
64 bytes from 10.5.1.11: icmp_seq=3 ttl=64 time=0.535 ms
^C
--- 10.5.1.11 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2001ms
```

# II. Accès internet pour tous

## 1. Accès internet routeur

### ☀️ Déjà, prouvez que le routeur a un accès internet

```
> [louis@routeur ~]$ ping ynow.com

PING ynow.com (209.196.146.115) 56(84) bytes of data.
64 bytes from 209.196.146.115 (209.196.146.115): icmp_seq=1 ttl=43 time=165 ms
64 bytes from 209.196.146.115 (209.196.146.115): icmp_seq=2 ttl=43 time=165 ms
64 bytes from 209.196.146.115 (209.196.146.115): icmp_seq=3 ttl=43 time=150 ms
64 bytes from 209.196.146.115 (209.196.146.115): icmp_seq=4 ttl=43 time=193 ms
64 bytes from 209.196.146.115 (209.196.146.115): icmp_seq=5 ttl=43 time=146 ms
^C
--- ynow.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4007ms
rtt min/avg/max/mdev = 145.700/163.939/193.119/16.571 ms
```

## 2. Accès internet clients

### ☀️ Prouvez que les clients ont un accès internet
```
> louis@client1:~$ ping ynov.com

PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=45 time=75.7 ms
64 bytes from 104.26.11.233: icmp_seq=2 ttl=45 time=61.3 ms
64 bytes from 104.26.11.233: icmp_seq=3 ttl=45 time=54.1 ms
^C64 bytes from 104.26.11.233: icmp_seq=4 ttl=45 time=50.9 ms

--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3001ms
rtt min/avg/max/mdev = 50.852/60.487/75.710/9.571 ms
```

```
> louis@client2:~$ ping ynov.com

PING ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233: icmp_seq=1 ttl=45 time=45.9 ms
64 bytes from 104.26.10.233: icmp_seq=2 ttl=45 time=80.0 ms
64 bytes from 104.26.10.233: icmp_seq=3 ttl=45 time=66.8 ms
64 bytes from 104.26.10.233: icmp_seq=4 ttl=45 time=104 ms
^C
--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 45.926/74.153/103.939/21.046 ms
```

### ☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau

```
> louis@client2:~$ cat /etc/netplan/01-netcfg.yaml

network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s8:
      dhcp4: no
      addresses: [10.5.1.12/24]
      gateway4: 10.5.1.254
      nameservers:
        addresses: [1.1.1.1]
```

## III. Serveur SSH

### ☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH

```
[louis@routeur ~]$ sudo ss -lnpt | grep 22

LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=689,fd=3))
LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=689,fd=4))
```

### ☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert

```
[louis@routeur ~]$ sudo firewall-cmd --list-all

public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: ssh
  ports:
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

## IV. Serveur DHCP

### 3. Rendu attendu

### A. Installation et configuration du serveur DHCP

### ☀️ Installez et configurez un serveur DHCP sur la machine routeur.tp5.b1

```
> [louis@routeur ~]$ sudo dnf install dhcp-server

> [louis@routeur ~]$ sudo nano /etc/dhcp/dhcpd.conf

> [louis@routeur ~]$ sudo systemctl start dhcpd
```

### B. Test avec un nouveau client

### ☀️ Créez une nouvelle machine client client3.tp5.b1

```
> louis@client1:~$ sudo hostnamectl set-hostname client3
```

```
> louis@client3:~$ sudo nano /etc/netplan/01-netcfg.yaml

network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s8:
      dhcp4: true

> louis@client3:~$ sudo netplan apply
```
```
> louis@client3:~$ ip a

2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:12:19:e6 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 metric 100 brd 10.5.1.255 scope global dynamic enp0s8
       valid_lft 43178sec preferred_lft 43178sec
    inet6 fe80::a00:27ff:fe12:19e6/64 scope link 
       valid_lft forever preferred_lft forever

> louis@client3:~$ ping ynov.com

PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=56 time=12.9 ms
64 bytes from 104.26.11.233: icmp_seq=2 ttl=56 time=12.5 ms
64 bytes from 104.26.11.233: icmp_seq=3 ttl=56 time=14.1 ms
64 bytes from 104.26.11.233: icmp_seq=4 ttl=56 time=12.7 ms
^C
--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 12.459/13.041/14.105/0.634 ms
```

### C. Consulter le bail DHCP

### ☀️ Consultez le bail DHCP qui a été créé pour notre client

```
> [louis@routeur ~]$ cat /var/lib/dhcpd/dhcpd.leases

# The format of this file is documented in the dhcpd.leases(5) manual page.
# This lease file was written by isc-dhcp-4.4.2b1

# authoring-byte-order entry is generated, DO NOT DELETE
authoring-byte-order little-endian;

server-duid "\000\001\000\001.\2403Q\010\000'\310\301\335";

lease 10.5.1.137 {
  starts 1 2024/10/14 20:08:29;
  ends 2 2024/10/15 08:08:29;
  cltt 1 2024/10/14 20:08:29;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:12:19:e6;
  uid "\377\257\201\217}\000\002\000\000\253\021\372\3506\227^\250KJ";
  client-hostname "client3";
}
```

### ☀️ Confirmez qu'il s'agit bien de la bonne adresse MAC

```
> louis@client3:~$ ip a

2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:12:19:e6 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 metric 100 brd 10.5.1.255 scope global dynamic enp0s8
       valid_lft 42391sec preferred_lft 42391sec
    inet6 fe80::a00:27ff:fe12:19e6/64 scope link 
       valid_lft forever preferred_lft forever
```



