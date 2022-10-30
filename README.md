# Jarkom-Modul-2-I03-2022

Computational Networking Module 2 Practicum Report

* Selomita Zhafirah 5025201120
* Venia Sollery Aliyya Hasna 5025201161
* Erlangga Wahyu Utomo 5025201118

## Question 1

topology with WISE as DNS Master, Berlint as DNS Slave, Eden will as Web Server, and SSS & Garden as client

![Number1](/ss/topology.jpg)

![Number1](/ss/1.jpg)

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
``c


