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

After that he also wants to create a subdomain eden.wise.yyy.com with alias www.eden.wise.yyy.com whose DNS is set on WISE and leads to Eden.

![Number2](/ss/3.jpg.)

nano resolve.conf

![nanoResolve.conf](/ss/4.jpg.)

nano named.conf.local

![nano named.conf.local](/ss/5.jpg.)

make folder and copy from local to jarkom directory

![make folder](/ss/6.jpg.)

nano wise.I03.com

![wise.io3.com](/ss/7.jpg.)


