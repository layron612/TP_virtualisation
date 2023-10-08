# TP2 [réalisé par mathias habrache]

## I

### 1) 

Pour mettre en place une IP dynamique sur le routeur il faut faire la commande :

```nano/etc/sysconfig/network-scripts/ifcfg-enp0s3```

Puis y Ecrire ceci :
```
NAME=enp0s3
DEVICE=enp0s3

BOOTPROTO=dhcp
ONBOOT=yes
```
Puis il faut rentrer les 2 commandes suivantes :

```sudo nmcli con reload```

```sudo nmcli con up enp0s3```



Pour ajouter une ip statique sur le port relier au switch il faut faire cette commande :

```nano/etc/sysconfig/network-scripts/ifcfg-enp0s8```

Puis il faut y écrire ou remplacer ceci :
```
NAME=enp0s8
DEVICE=enp0s8

BOOTPROTO=static
ONBOOT=yes

IPADDR=10.2.1.254
NETMASK=255.255.255.0
```
Et un fois refermé il faut lancer ces 2 commandes :

```sudo nmcli con reload```

```sudo nmcli con up enp0s8```

Puis la commande ip a révelera les informations suivantes :
```
1:  lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOW group default qlen 1000
     link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
     inet 127.0.0.1/8 scope host lo
        valid_lft forever preferred_lft forever
     inet6 ::1/128 scope host
        valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAS,UP,LOWER_CUP> mtu 1500 qdisc fq_cdel state UP group default qlen 1000
    link/ether 08:00:27:36:5d:06 brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.235/24 brd 192.168.255 scope global dynamic noperf ixroute enp0s3
        valid_lft 2363sec preferred_lft 2363sec
    inet6 fe80: :a00:27ff :fe36 :5d06/64 scope link noperf ixroute
        valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAS,UP,LOWER_CUP> mtu 1500 qdisc fq_cdel state UP group default qlen 1000
    link/ether 08:00:27:d5:95:b8 brd ff:ff:ff:ff:ff:ff
    inet  10.2.1.254/24 brd 10.2.1.255 scope global dynamic noperf ixroute enp0s3
        valid_lft 2363sec preferred_lft 2363sec
    inet6 fe80: :a00:27ff :fe36 :5d06/64 scope link noperf ixroute
        valid_lft forever preferred_lft forever
```
### 2)

```
PING 10.2.1.254 56(84) bytes of data.
64 bytes from par21s23-in-f14.1e100.net (10.2.1.254): icmp_seq=1 ttl=117 time=25.2 ms
64 bytes from par21s23-in-f14.1e100.net (10.2.1.254): icmp_seq=2 ttl=117 time=47.2 ms
64 bytes from par21s23-in-f14.1e100.net (10.2.1.254): icmp_seq=3 ttl=117 time=37.4 ms
^C
--- 10.2.1.254 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2001ms
rtt min/avg/max/mdev = 25.190/36.578/47.186/8.996 ms
```
Pour installer la route il faut modifier le fichier de conf se trouvant dans ```/etc/sysconfig/network-scripts/ifcfg-enp0s3``` en y accédant il suffit d’ajouter une ligne gateway de ce style
```GATEWAY=10.2.1.254```


Voici le ping de google.com une fois la route par défaut installée :
```
PING google.com (216.58.214.174) 56(84) bytes of data.
64 bytes from mad01s26-in-f14.1e100.net (216.58.214.174): icmp_seq=1 ttl=117 time=39.8 ms
64 bytes from mad01s26-in-f174.1e100.net (216.58.214.174): icmp_seq=2 ttl=117 time=29.7 ms
^C
--- google.com ping statistics ---
3 packets transmitted, 2 received, 33.3333% packet loss, time 2003ms
rtt min/avg/max/mdev = 29.719/34.754/39.790/5.035 ms
```





