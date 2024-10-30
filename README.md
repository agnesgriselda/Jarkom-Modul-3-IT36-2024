
# Jarkom-Modul-3-IT36-2024

## Laporan Resmi Modul 3 : DHCP dan Reverse Proxy

### IT36

| Nama                        | NRP           |
|-----------------------------|---------------|
| Fico Simhanandi                | 5027231030   |
| Agnes Zenobia Griselda Petrina | 5027231034    |



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
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.81.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.81.3.1
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.81.4.1
	netmask 255.255.255.0
```

### Fritz (DNS Server)
```
auto eth0
iface eth0 inet static
	address 10.81.4.2
	netmask 255.255.255.0
	gateway 10.81.4.1
```

### Tybur (DHCP Server)
```
auto eth0
iface eth0 inet static
	address 10.81.4.3
	netmask 255.255.255.0
	gateway 10.81.4.1
```

### Warhammer (Database Server)
```
auto eth0
iface eth0 inet static
	address 10.81.3.4
	netmask 255.255.255.0
	gateway 10.81.3.1
```

### Beast (Load Balancer Laravel)
```
auto eth0
iface eth0 inet static
	address 10.81.3.2
	netmask 255.255.255.0
	gateway 10.81.3.1
```

### Colossal (Load Balancer PHP)
```
auto eth0
iface eth0 inet static
	address 10.81.3.3
	netmask 255.255.255.0
	gateway 10.81.3.1
```

### Annie (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.1.2
	netmask 255.255.255.0
	gateway 10.81.1.1
```

### Bertholdt (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.1.3
	netmask 255.255.255.0
	gateway 10.81.1.1
```

### Reiner (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.1.4
	netmask 255.255.255.0
	gateway 10.81.1.1
```

### Armin (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.2.2
	netmask 255.255.255.0
	gateway 10.81.2.1
```

### Eren (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.2.3
	netmask 255.255.255.0
	gateway 10.81.2.1
```

### Mikasa (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.81.2.4
	netmask 255.255.255.0
	gateway 10.81.2.1
```

### Zeke, Erwin (Client) 
```
auto eth0
iface eth0 inet dhcp
```

## Soal 0

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
@       IN      NS      eldia.it36.com.
@       IN      A       10.81.2.2     ; IP Armin' > /etc/bind/eldia/eldia.it36.com

service bind9 restart
```

## Soal 1-5

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

![Marley(2)](https://github.com/user-attachments/assets/502708e5-ac7d-41ef-b6da-cd30758edf4e)

## Testing No 3

![Eldia(3)](https://github.com/user-attachments/assets/e4419b7d-ea4f-468b-be13-e56881132ac9)

## Testing No 4

![ping_erdia(4)](https://github.com/user-attachments/assets/e7c58747-9d84-46a8-8812-d53acbd174e7)

![ping_marley(4)](https://github.com/user-attachments/assets/a8d10d7f-2ef3-40fb-96da-f4404273cf7d)

## Testing No 5

### Lease Time Erwin

![lease_erwin(5)](https://github.com/user-attachments/assets/0b830282-8ce5-43e6-a209-f7b4e1fdd318)

### Lease Time Zeke

![lease_zeke(5)](https://github.com/user-attachments/assets/8db6ebc7-5ca3-40ef-81f1-8054a8b09d8c)

## Soal 6

### Armin, Eren, Mikasa
```sh
mkdir -p /var/www/eldia.it36.com

wget --no-check-certificate 'https://drive.google.com/uc?export=download&id=1TvebIeMQjRjFURKVtA32lO9aL7U2msd6' -O /root/bangsaEldia.zip
unzip /root/bangsaEldia.zip -d /var/www/eldia.it36.com
rm -rf /root/bangsaEldia.zip

echo '
server {

        listen 80;

        root /var/www/eldia.it36.com;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
        }

location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }' > /etc/nginx/sites-available/eldia.it36.com

ln -s /etc/nginx/sites-available/eldia.it36.com /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service php7.3-fpm start
service php7.3-fpm restart
service nginx restart
nginx -t

#use lynx eldia.it36.com
```
### Testing

![lynx](https://github.com/user-attachments/assets/d1b9ea09-0913-4743-8c53-d59614485e10)

## Soal 7

### Colosal
```sh
echo '
 upstream myweb  {
        server 10.81.2.2; #IP Armin
        server 10.81.2.3; #IP Eren
        server 10.81.2.4; #IP Mikasa
 }

 server {
        listen 80;
        server_name eldia.it36.com;

        location / {
        proxy_pass http://myweb;
        }
 }' > /etc/nginx/sites-available/lb-php

ln -s /etc/nginx/sites-available/lb-php /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

### Fritz
```sh
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
@       IN      NS      eldia.it36.com.
@       IN      A       10.81.3.3     ; IP Colossal' > /etc/bind/eldia/eldia.it36.com

service bind9 restart
```


## Testing
![ROUNDROBIN](https://github.com/user-attachments/assets/9d91f7a8-90ba-4d88-82d7-3cce6bcefe7d)

## Soal 8

## Colosal
```sh
echo '
 upstream myweb  {
#    hash $request_uri consistent;
#    least_conn;
    ip_hash;
        server 10.81.2.2; #IP Armin
        server 10.81.2.3; #IP Eren
        server 10.81.2.4; #IP Mikasa
 }

 server {
        listen 80;
        server_name eldia.it36.com;

        location / {
        proxy_pass http://myweb;
        }
 }' > /etc/nginx/sites-available/lb-php

ln -s /etc/nginx/sites-available/lb-php /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t

#use ab -n 'sesuai soal' -c 'sesuai soal' http://eldia.it36.com/ to test the load balancing
```
## Testing

### HASH

![HASH](https://github.com/user-attachments/assets/6ce38859-db3e-4aa8-95ef-40e40cb614f9)

### IPHASH

![IPHASH](https://github.com/user-attachments/assets/87509a0d-6402-4144-8056-df94d7eddc7f)

### LEAST

![LEAST](https://github.com/user-attachments/assets/77b0faa0-513e-4730-93ec-1a2a5c82929a)

### ROUND ROBIN

![ROUNDROBIN](https://github.com/user-attachments/assets/f55c6036-a097-4d6f-933c-9a3190df23c3)

### Grafik

![Screenshot 2024-10-28 064808](https://github.com/user-attachments/assets/6f163c21-1866-486d-8ebb-ed20b6eaf1e5)


## Soal 9

## Testing

### 1 WORKER

![1Worker](https://github.com/user-attachments/assets/f55bb82d-2745-4655-a59c-28df14e8ac34)

### 2 WORKER

![2Worker](https://github.com/user-attachments/assets/8e1e228e-a1f0-4441-9053-150e6df16b63)

### 3 WORKER

![3Worker](https://github.com/user-attachments/assets/c3b1fcc0-af1b-4eba-89fe-95e6dfa238f4)

## Grafik

![Screenshot 2024-10-28 070216](https://github.com/user-attachments/assets/974170a8-d2dc-4372-bf88-ad22f926281a)

![Screenshot 2024-10-28 070234](https://github.com/user-attachments/assets/3eec9c31-4fe0-43ee-b855-e37b3d92003a)

![Screenshot 2024-10-28 070250](https://github.com/user-attachments/assets/261ca846-6651-43ef-b69e-c136a3920b35)


## Soal 10

### Colosal
```sh
mkdir /etc/nginx/supersecret
htpasswd -b -c /etc/nginx/supersecret/htpasswd arminannie jrkmit36

echo '
 upstream myweb  {
        least_conn;
        server 10.81.2.2; #IP Armin
        server 10.81.2.3; #IP Eren
        server 10.81.2.4; #IP Mikasa
 }

 server {
        listen 80;
        server_name eldia.it36.com;

        location / {
        auth_basic "Restricted Access";
        auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        proxy_pass http://myweb;
        }
 }' > /etc/nginx/sites-available/lb-php

ln -s /etc/nginx/sites-available/lb-php /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t

#test with lynx http://eldia.it36.com/
```

## Testing

Memasukan Username

![USERNAME](https://github.com/user-attachments/assets/a99103ba-6727-438c-9e67-281b88bce2e1)

Memasukan Password

![PASS](https://github.com/user-attachments/assets/0ec7e040-ebb6-4be1-9cb7-976dca945b37)

Saat Login Success

![CORRECT](https://github.com/user-attachments/assets/787885e5-f941-4dd0-8b69-02ad202e8d64)

Saat Login Fail

![FAIL](https://github.com/user-attachments/assets/8528ec1d-6f9c-4fe7-8be5-7db68e8825f2)

## Soal 11

### Colosal
```sh
echo '
 upstream myweb  {
        least_conn;
        server 10.81.2.2; #IP Armin
        server 10.81.2.3; #IP Eren
        server 10.81.2.4; #IP Mikasa
 }

 server {
        listen 80;
        server_name eldia.it36.com;

        location / {
        auth_basic "Restricted Access";
        auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        proxy_pass http://myweb;
        }

        location /titan/ {
        proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }

        location /extrahehe {
	 proxy_pass https://zenless-zone-zero.fandom.com/wiki/Von_Lycaon;
	}
 }' > /etc/nginx/sites-available/lb-php

ln -s /etc/nginx/sites-available/lb-php /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t

#use lynx http://eldia.it36.com/titan/ to test the reverse proxy
```

## Testing

![AOTWEB](https://github.com/user-attachments/assets/75ce2682-df47-4be6-b5d6-c2ec8349e546)

## Soal 12

### Colosal
```sh
echo '
 upstream myweb  {
        least_conn;
        server 10.81.2.2; #IP Armin
        server 10.81.2.3; #IP Eren
        server 10.81.2.4; #IP Mikasa
 }

server {
	listen 80;
	server_name eldia.it36.com;

	location / {
		allow 10.81.1.77;
		allow 10.81.1.88;
		allow 10.81.2.144;
		allow 10.81.2.156;
		deny all;

		auth_basic "Restricted Content";
		auth_basic_user_file /etc/nginx/supersecret/htpasswd;
		proxy_pass http://myweb;
	}

	location /dune {
		proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
	}

    location /extrahehe {
		proxy_pass https://zenless-zone-zero.fandom.com/wiki/Von_Lycaon;
	}
}' > /etc/nginx/sites-available/lb-php

ln -s /etc/nginx/sites-available/lb-php /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

### Tybur
```sh
echo 'host Zeke{
        hardware ethernet fa:61:fb:1a:8d:5b;
        fixed-address 10.81.1.77;
}
' >> /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

### Zeke
```sh
echo 'hwaddress ether fa:61:fb:1a:8d:5b' >> /etc/network/interfaces
```

## Testing

![ERWINFORBIDEN](https://github.com/user-attachments/assets/7b8b2618-f6c1-4e60-98c8-7d04ed702b50)

## Soal 13

```sh
mysql -u root <<EOF
CREATE USER 'kelompokit36'@'%' IDENTIFIED BY 'passwordit36';
CREATE USER 'kelompokit36'@'localhost' IDENTIFIED BY 'passwordit36';
CREATE DATABASE dbkelompokit36;
GRANT ALL PRIVILEGES ON *.* TO 'kelompokit36'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'kelompokit36'@'localhost';
FLUSH PRIVILEGES;
EOF

echo '[mysqld]
skip-networking=0
skip-bind-address' > /etc/mysql/my.cnf
```

Kita tes di salah satu worker

`mysql --host=10.81.3.4 --port=3306 --user=kelompokit36 --password`

### Hasil

![Screenshot (3849)](https://github.com/user-attachments/assets/1d9ddc11-5d6c-412f-ac72-b716b3609539)

