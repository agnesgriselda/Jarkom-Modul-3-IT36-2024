# Jarkom-Modul-3-IT36-2024

## Laporan Resmi Modul 2 : DNS dan Webserver

### IT36

| Nama                        | NRP           |
|-----------------------------|---------------|
| Fico Simhanandi                | 5027231030   |
| Agnes Zenobia Griselda Petrina | 5027231034    |


## Daftar Isi

1. [Topologi](#topologi)
2. [Setup](#setup)
3. [Soal 1](#soal-1)
4. [Soal 2](#soal-2)
5. [Soal 3](#soal-3)
6. [Soal 4](#soal-4)
7. [Soal 5](#soal-5)
8. [Soal 6](#soal-6)
9. [Soal 7](#soal-7)
10. [Soal 8](#soal-8)
11. [Soal 9](#soal-9)
12. [Soal 10](#soal-10)
13. [Soal 11](#soal-11)
14. [Soal 12](#soal-12)
15. [Soal 13](#soal-13)
16. [Soal 14](#soal-14)
17. [Soal 15](#soal-15)
18. [Soal 16](#soal-16)
19. [Soal 17](#soal-17)
20. [Soal 18](#soal-18)
21. [Soal 19](#soal-19)
22. [Soal 20](#soal-20)

## Topologi
![Screenshot 2024-10-21 191835](https://github.com/user-attachments/assets/d9fa3c0b-4406-490e-93a2-b6a9ed513ba3)


## Setup

### Paradis (DHCP Relay)
```
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.81.1.0
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.81.2.0
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.81.3.0
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.81.4.0
	netmask 255.255.255.0
```

### Fritz (DNS Server)
```
auto eth0
iface eth0 inet static
	address 10.81.4.2
	netmask 255.255.255.0
	gateway 10.81.4.0
```

### Tybur (DHCP Server)
```
auto eth0
iface eth0 inet static
	address 10.81.4.3
	netmask 255.255.255.0
	gateway 10.81.4.0
```

### Warhammer (Database Server)
```
auto eth0
iface eth0 inet static
	address 10.81.3.4
	netmask 255.255.255.0
	gateway 10.81.3.0
```

### Beast (Load Balancer Laravel)
```
auto eth0
iface eth0 inet static
	address 10.81.3.2
	netmask 255.255.255.0
	gateway 10.81.3.0
```

### Colossal (Load Balancer PHP)
```
auto eth0
iface eth0 inet static
	address 10.81.3.3
	netmask 255.255.255.0
	gateway 10.81.3.0
```

### Annie (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.1.2
	netmask 255.255.255.0
	gateway 10.81.1.0
```

### Bertholdt (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.1.3
	netmask 255.255.255.0
	gateway 10.81.1.0
```

### Reiner (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.1.4
	netmask 255.255.255.0
	gateway 10.81.1.0
```

### Armin (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.2.2
	netmask 255.255.255.0
	gateway 10.81.2.0
```

### Eren (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.2.3
	netmask 255.255.255.0
	gateway 10.81.2.0
```

### Mikasa (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.2.4
	netmask 255.255.255.0
	gateway 10.81.2.0
```

### Zeke, Erwin (Client) 
```
auto eth0
iface eth0 inet dhcp
```

# Jarkom-Modul-3-IT36-2024

## Laporan Resmi Modul 2 : DNS dan Webserver

### IT36

| Nama                        | NRP           |
|-----------------------------|---------------|
| Fico Simhanandi                | 5027231030   |
| Agnes Zenobia Griselda Petrina | 5027231034    |


## Daftar Isi

1. [Topologi](#topologi)
2. [Setup](#setup)
3. [Soal 1](#soal-1)
4. [Soal 2](#soal-2)
5. [Soal 3](#soal-3)
6. [Soal 4](#soal-4)
7. [Soal 5](#soal-5)
8. [Soal 6](#soal-6)
9. [Soal 7](#soal-7)
10. [Soal 8](#soal-8)
11. [Soal 9](#soal-9)
12. [Soal 10](#soal-10)
13. [Soal 11](#soal-11)
14. [Soal 12](#soal-12)
15. [Soal 13](#soal-13)
16. [Soal 14](#soal-14)
17. [Soal 15](#soal-15)
18. [Soal 16](#soal-16)
19. [Soal 17](#soal-17)
20. [Soal 18](#soal-18)
21. [Soal 19](#soal-19)
22. [Soal 20](#soal-20)

## Topologi
![Screenshot 2024-10-21 191835](https://github.com/user-attachments/assets/d9fa3c0b-4406-490e-93a2-b6a9ed513ba3)


## Setup

### Paradis (DHCP Relay)
```
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.81.1.1
	netmask 255.255.255.1

auto eth2
iface eth2 inet static
	address 10.81.2.1
	netmask 255.255.255.1

auto eth3
iface eth3 inet static
	address 10.81.3.1
	netmask 255.255.255.1

auto eth4
iface eth4 inet static
	address 10.81.4.1
	netmask 255.255.255.1
```

### Fritz (DNS Server)
```
auto eth0
iface eth0 inet static
	address 10.81.4.2
	netmask 255.255.255.1
	gateway 10.81.4.1
```

### Tybur (DHCP Server)
```
auto eth0
iface eth0 inet static
	address 10.81.4.3
	netmask 255.255.255.1
	gateway 10.81.4.1
```

### Warhammer (Database Server)
```
auto eth0
iface eth0 inet static
	address 10.81.3.4
	netmask 255.255.255.1
	gateway 10.81.3.1
```

### Beast (Load Balancer Laravel)
```
auto eth0
iface eth0 inet static
	address 10.81.3.2
	netmask 255.255.255.1
	gateway 10.81.3.1
```

### Colossal (Load Balancer PHP)
```
auto eth0
iface eth0 inet static
	address 10.81.3.3
	netmask 255.255.255.1
	gateway 10.81.3.1
```

### Annie (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.1.2
	netmask 255.255.255.1
	gateway 10.81.1.1
```

### Bertholdt (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.1.3
	netmask 255.255.255.1
	gateway 10.81.1.1
```

### Reiner (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.1.4
	netmask 255.255.255.1
	gateway 10.81.1.1
```

### Armin (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.2.2
	netmask 255.255.255.1
	gateway 10.81.2.1
```

### Eren (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.2.3
	netmask 255.255.255.1
	gateway 10.81.2.1
```

### Mikasa (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.2.4
	netmask 255.255.255.1
	gateway 10.81.2.1
```

### Zeke, Erwin (Client) 
```
auto eth0
iface eth0 inet dhcp
```

## Soal 0

Pulau Paradis telah menjadi tempat yang damai selama 1000 tahun, namun kedamaian tersebut tidak bertahan selamanya. Perang antara kaum Marley dan Eldia telah mencapai puncak. Kaum Marley yang dipimpin oleh Zeke, me-register domain name marley.yyy.com untuk worker Laravel mengarah pada Annie. Namun ternyata tidak hanya kaum Marley saja yang berinisiasi, kaum Eldia ternyata sudah mendaftarkan domain name eldia.yyy.com untuk worker PHP (0) mengarah pada Armin.

### [Fritz]
```sh
echo 'zone "marley.it36.com" { 
        type master; 
        file "/etc/bind/marley/marley.it36.com";
};

zone "eldia.it36.com" {
        type master;
        file "/etc/bind/eldia/eldia.it36.com";
}; ' >> /etc/bind/named.conf.local

mkdir /etc/bind/marley
mkdir /etc/bind/eldia

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     marley.it36.com. root.marley.it36.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      marley.it36.com.
@       IN      A       10.81.1.2     ; IP Annie' > /etc/bind/marley/marley.it36.com

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     eldia.it36.com. root.eldia.it36.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      eldia.16.com.
@       IN      A       10.81.2.2     ; IP Armin' > /etc/bind/eldia/eldia.it36.com

service bind9 restart
```

## Soal 1

Lakukan konfigurasi sesuai dengan peta yang sudah diberikan. Semua Client harus menggunakan konfigurasi ip address dari keluarga Tybur (dhcp)

**Note:** Karena kebanyakan kode diletakan di file yang sama, maka soal digabung agar lebih efisien

### DHCP Relay [Paradis]
```sh
#Soal ke-1
echo 'SERVERS="10.81.4.3"
INTERFACES="eth1 eth2 eth3 eth4"' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' > /etc/sysctl.conf

service isc-dhcp-relay restart
```

### DHCP Server [Tybur]

```sh
#Soal ke-1
echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server
#the time is in seconds
echo 'subnet 10.81.1.0 netmask 255.255.255.0 {

        #Soal ke-2
        range 10.81.1.05 10.81.1.25;
        range 10.81.1.50 10.81.1.100;
        option routers 10.81.1.1;

        #Soal ke-4
        option broadcast-address 10.81.1.255;
        option domain-name-servers 10.81.4.2;

        #Soal ke-5
        default-lease-time 1800;
        max-lease-time 5220;
}

subnet 10.81.2.0 netmask 255.255.255.0 {

        #Soal ke-3
        range 10.81.2.09 10.81.2.27;
        range 10.81.2.81 10.81.2.243;
        option routers 10.81.2.1;

        #Soal ke-4
        option broadcast-address 10.81.2.255;
        option domain-name-servers 10.81.4.2;

        #Soal ke-5
        default-lease-time 360;
        max-lease-time 5220;
}

subnet 10.81.3.0 netmask 255.255.255.0 {
        option routers 10.81.3.1;
}

subnet 10.81.4.0 netmask 255.255.255.0 {
        option routers 10.81.4.1;
} ' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```
## Testing No 2

![alt text](Soal1-5/Foto/Marley(2).png)

## Testing No 3

![alt text](Soal1-5/Foto/Eldia(3).png)

## Testing No 4

![alt text](Soal1-5/Foto/ping_erdia(4).png)

![alt text](Soal1-5/Foto/ping_marley(4).png)

