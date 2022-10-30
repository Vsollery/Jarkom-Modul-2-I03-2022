# Jarkom-Modul-2-I03-2022

Computational Networking Module 2 Practicum Report

* Selomita Zhafirah 5025201120
* Venia Sollery Aliyya Hasna 5025201161
* Erlangga Wahyu Utomo 5025201118

## Question 1

topology with WISE as DNS Master, Berlint as DNS Slave, Eden will as Web Server, and SSS & Garden as client

![Number1](/ss/topology.jpg)


config server 

```
Ostania
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
address 10.15.1.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 10.15.2.1
netmask 255.255.255.0

auto eth3
iface eth3 inet static
address 10.15.3.1
netmask 255.255.255.0

SSS
auto eth0
iface eth0 inet static
address 10.15.1.2
netmask 255.255.255.0
gateway 10.15.1.1

Garden
auto eth0
iface eth0 inet static
address 10.15.1.3
netmask 255.255.255.0
gateway 10.15.1.1


Berlint
auto eth0
iface eth0 inet static
address 10.15.3.2
netmask 255.255.255.0
gateway 10.15.3.1

Eden
auto eth0
iface eth0 inet static
address 10.15.3.3
netmask 255.255.255.0
gateway 10.15.3.1


Wise
auto eth0
iface eth0 inet static
address 10.15.2.2
netmask 255.255.255.0
gateway 10.15.2.1
```
![Number1](/ss/1.jpg)


## Question 2

To make it easier to get information about the mission from Handler, help Loid create the main website by accessing wise.yyy.com with alias www.wise.yyy.com on the wise folder.
```
apt-get install bind9 -y

echo'zone "wise.I03.com" {
        type master;
        file "/etc/bind/Jarkom/wise.I03.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/Jarkom

cp /etc/bind/db.local /etc/bind/Jarkom/wise.I03.com

echo';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     wise.I03.com. root.wise.I03.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      wise.I03.com.
@       IN      A       192.208.2.2
@       IN      AAAA    ::1 
www      IN      CNAME   wise.I03.com.' > /etc/bind/Jarkom/wise.I03.com

service bind9 restart
```

![Number2](/ss/3.jpg)

nano resolve.conf

![nanoResolve.conf](/ss/4.jpg)

nano named.conf.local

![nano named.conf.local](/ss/5.jpg)

make folder and copy from local to jarkom directory

![make folder](/ss/6.jpg)

nano wise.I03.com

![wise.io3.com](/ss/7.jpg)

##Question 3

 After that he also wants to create a subdomain eden.wise.yyy.com with alias www.eden.wise.yyy.com whose DNS is set on WISE and leads to Eden.
 
 ```
 echo';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     wise.I03.com. root.wise.I03.com. (
                              2         ; Serial
                        604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      wise.I03.com.
@       IN      A       192.208.2.2
@       IN      AAAA    ::1 
www      IN      CNAME   wise.I03.com.
eden     IN      A       192.208.3.3
www.eden IN      A      192.208.3.3' > /etc/bind/Jarkom/wise.I03.com

service bind9 restart
```

##Question 4

Also create a reverse domain for the main domain

```
echo'zone "2.208.192.in-addr.arpa" {
    type master;
    file "/etc/bind/Jarkom/2.208.192.in-addr.arpa";
};'> nano /etc/bind/named.conf.local
cp /etc/bind/db.local /etc/bind/Jarkom/2.208.192.in-addr.arpa

echo';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     wise.I03.com. root.wise.I03.com. (
                              2         ; Serial
                         604800         ; Refresh
				    86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
2.208.192.in-addr.arpa. IN      NS      wise.I03.com.
2       IN      PTR     wise.I03.com.'> /etc/bind/Jarkom/2.208.192.in-addr.arpa

service bind9 restart
```

##Question 5

To stay in touch if the WISE server has some problem, make Berlint also as the DNS Slave for the main domain 

```
echo'zone "wise.I03.com" {
type master;
notify yes;
also-notify { 192.208.3.2; }; 
allow-transfer { 192.208.3.2; }; 
        file "/etc/bind/Jarkom/wise.I03.com";
}; 
zone "2.208.192.in-addr.arpa" {
    type master;
	notify yes;
	also-notify { 192.208.3.2; }; 
	allow-transfer { 192.208.3.2; }; 
        file "/etc/bind/Jarkom/wise.I03.com";
}; 
zone "2.208.192.in-addr.arpa" {
    type master;
    file "/etc/bind/Jarkom/2.208.192.in-addr.arpa";
};'> nano /etc/bind/named.conf.local
```



