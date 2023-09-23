
 ## I)  Most simplest LAN h1

1)

  pour avoir les adresses mac des deux machines virtuel il faut utiliser la commande:```ip a```
  
     ainsi on obtient les addresses mac suivantes :
                     					       ```node1 :08:00:27:ee:ad:62```
						                         ```node2 :08:00:27:ee:68:7a```

2)

   `ip a`
   
``  sudo nano /etc/sysconfig/network-scripts/ifcfg-enp0s3``

écrire ou remplacer le texte par celui ci:

>NAME=enp0s3
>
>DEVICE=enp0s3
>
>BOOTPROTO=static
>
>ONBOOT=yes
>
>IPADDR=10.1.1.(1 ou 2)
>
>NETMASK=255.255.255.0


``sudo nmcli con reload``

``sudo nmcli con up enp0s3``

3)
  ``ping 10.1.1.1``
  
  ``ping 10.1.1.2``

4)

    voir le document « wireshark1 »
    le protocole qui permet de faire un ping est le protocole icmp

## II) Ajoutons un switch

1)

  comme pour la partie 1 on se sert de la commande ip a 
   les addresses mac de node 1 et 2 n’ont pas changé
   addresse mac de node 3 :  "08:00:27:16:e2:0f"
2)

  il suffit de faire la commande ip a
   pour pouvoir retrouver l’ip correspondante

3)

    ping vers node1 (ip: 10.1.1.1)
  
   >  [root@localhost ~]# ping 10.1.1.1
   >  PING 10.1.1.1 (10.1.1.1) 56(84) bytes of data.
   >
   >  64 bytes from 10.1.1.1: icmp_seq=1 ttl=64 times=0.478 ms
   >
   >  64 bytes from 10.1.1.1: icmp_seq=2 ttl=64 times=1.68 ms
   >
   >
   >^c
   >
   >--- 10.1.1.1 ping statics---
   >
   >2packets transmitted, 2received, 0% packet loss, time 1008ms
   >
   >rtt min/avg/max/mdev = 0.478/1.078/1.679/0.600 ms

      ping vers node2 (ip: 10.1.1.2)
  
>[root@localhost ~]# ping 10.1.1.2
 >  PING 10.1.1.2 (10.1.1.2) 56(84) bytes of data.
>
  > 64 bytes from 10.1.1.2: icmp_seq=1 ttl=64 times=3.36 ms
>
   >64 bytes from 10.1.1.2: icmp_seq=2 ttl=64 times=1.70 ms
>
>^c
>
>--- 10.1.1.2 ping statics---
>
>2packets transmitted, 2received, 0% packet loss, time 1002ms
>
>rtt min/avg/max/mdev = 1.702/2.530/3.358/0.828 ms

node 2 :

    ping vers node 3 (ip:10.1.1.3)

>[root@localhost ~]# ping 10.1.1.1
>
 >  PING 10.1.1.1 (10.1.1.1) 56(84) bytes of data.
>
  > 64 bytes from 10.1.1.1: icmp_seq=1 ttl=64 times=1.65 ms
>
   >64 bytes from 10.1.1.1: icmp_seq=2 ttl=64 times=1.73 ms
>
>^c
>
>--- 10.1.1.1 ping statics---
>
>2packets transmitted, 2received, 0% packet loss, time 1002ms
>
>rtt min/avg/max/mdev = 1.654/1.691/1.729/0.037 ms

## III) Serveur DHCP
