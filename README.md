## Praktikum Modul 4 Jaringan Komputer

**Kelompok A16 :**

| Nama | NRP |
| ----------- | ----------- |
| Clarissa Luna Maheswari | 5025211033 |
| Heru Dwi Kurniawan | 5025211055 

### VLSM
#### Tree
![10 7 0 019](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/121850356/849f97f2-3aee-4325-a8d9-1b4329b54ebc)

Bagian atas pohon VLSM merepresentasikan ruang alamat yang tersedia untuk subnetting. 10.7.0.0/19 adalah subnet induk dari mana semua subnet lainnya berasal. Subnet induk memiliki subnet mask yang lebih besar, yang menunjukkan jumlah alamat yang lebih sedikit yang digunakan untuk tujuan jaringan, dan lebih banyak alamat yang tersedia untuk host.  /19 menunjukkan bahwa 19 bit pertama alamat IP digunakan untuk menentukan jaringan. Dengan subnet mask ini, ada total 2^(32-19) = 2^13, atau 8192 alamat IP yang tersedia.

***Contoh Perhitungan***
Jika kita memerlukan subnet untuk 500 host, subnet mask dihitung sebagai berikut:
1. Mencari pangkat dua yang dapat mengakomodasi 500 host yaitu 2^9 = 512.
2. Kurangi 9 bit yang digunakan untuk host dari total 32 bit untuk mendapatkan subnet yaitu 32-9 = 23
3. Subnet mask menjadi /23 yang menyediakan 512 alamat.

#### Subneting

Dari node induk ini, kita bisa melakukan subnetting lebih lanjut untuk memenuhi kebutuhan spesifik dari berbagai segmen jaringan. contohnya pada subnet **10.7.0.0/20**, subnet ini dibagi lebih lanjut dari 10.3.0.0/19 dan menawarkan 2^(32-20) = 2^12, atau 4096 alamat IP yang tersedia. Subnet-subnet ini kemudian dapat dialokasikan lebih lanjut untuk menciptakan sub-subnet yang lebih kecil, yang disesuaikan dengan jumlah host yang diperlukan dalam masing-masing segmen jaringan. Berikut ini adalah hasil perolehan dari subnetting:

#### Tabel Alokasi Subnet

| Nama Subnet | ID | Alamat IP Awal | Subnet Mask | Alamat IP Akhir | Jumlah Host | CIDR |
|-------------|----|----------------|-------------|-----------------|-------------|------|
| Fern-Switch4-LaubHills-Switch4-AppetiteRegion | A1 | 10.7.0.0 | 255.255.248.0 | 10.7.7.255 | 1023 | /21 |
| Flamme-Fern | A2 | 10.7.24.112 | 255.255.255.252 | 10.7.24.115 | 2 | /30 |
| Flamme-Switch5-RohrRoad | A3 | 10.7.8.0 | 255.255.252.0 | 10.7.11.255 | 1001 | /22 |
| Himmel-Flamme | A4 | 10.7.24.116 | 255.255.255.252 | 10.7.24.119 | 2 | /30 |
| Himmel-Switch6-SchwerMountains | A5 | 10.7.24.96 | 255.255.255.248 | 10.7.24.113 | 6 | /29 |
| Freiren-Flamme | A6 | 10.7.24.120 | 255.255.255.252 | 10.7.24.123 | 2 | /30 |
| Freiren-Swicth3-LakeKoridor | A7 | 10.7.24.64 | 255.255.255.224 | 10.7.24.95 | 25 | /27 |
| Aura-Freiren | A8 | 10.7.24.124 | 255.255.255.252 | 10.7.24.127 | 2 | /30 |
| Denken-Aura | A9 | 10.7.24.128 | 255.255.255.252 | 10.7.24.131 | 2 | /30 |
| Denken-Switch2-RoyalCapital-Switch2-WilleRegion | A10 | 10.7.22.0 | 255.255.255.0 | 10.7.22.255 | 127 | /24 |
| Eisen-Aura | A11 | 10.7.24.132 | 255.255.255.252 | 10.7.24.135 | 2 | /30 |
| Eisen-Switch0-Stark | A12 | 10.7.24.136 | 255.255.255.252 | 10.7.24.139 | 2 | /30 |
| Eisen-Switch1-Ritcher-Switch1-Revolt | A13 | 10.7.24.104 | 255.255.255.248 | 10.7.24.111 | 3 | /29 |
| Linie-Eisen | A14 | 10.7.24.140 | 255.255.255.252 | 10.7.24.143 | 2 | /30 |
| Lawine-Linie | A15 | 10.7.24.144 | 255.255.255.252 | 10.7.24.147 | 2 | /30 |
| Lawine-Switch7-Bredtregion-Heiter | A16 | 10.7.24.0 | 255.255.255.192 | 10.7.24.63 | 31 | /26 |
| Heiter-Switch8-Sein-Switch8-RiegelCanyon | A17 | 10.7.12.0 | 255.255.252.0 | 10.7.15.255 | 512 | /22 |
| Linie-Switch11-GranzChannel | A18 | 10.7.20.0 | 255.255.254.0 | 10.7.21.255 | 255 | /23 |
| Lugner-Eisen | A19 | 10.7.24.148 | 255.255.255.252 | 10.7.24.151 | 2 | /30 |
| Lugner-Switch9-GrobeForest | A20 | 10.7.23.0 | 255.255.255.0 | 10.7.23.255 | 251 | /24

#### Topologi dan Pembagian Subnet
![10 7 0 019 (2)](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/121850356/995931cb-fb6e-4bad-b218-6a9ab4d52f95)
a) Konfigurasi Router
```
Router
Aura
Eth1 10.7.24.133
Eth2 10.7.24.129
Eth3 10.7.24.125

auto eth0
iface eth0 inet dhcp
up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.7.0.0/19

auto eth1
iface eth1 inet static
	address 10.7.24.133
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.7.24.129
	netmask 255.255.255.252

auto eth3
iface eth3 inet static
	address 10.7.24.125
	netmask 255.255.255.252


Eisen
Eth0 - a11 10.7.24.134 255.255.255.252
Eth1 - a13 10.7.24.105 255.255.255.248
Eth2 - a12 10.7.24.137 255.255.255.252
Eth3 - a14 10.7.24.141 255.255.255.252
Eth4 - a19 10.7.24.149 255.255.255.252

auto eth0
iface eth0 inet static
	address 10.7.24.134
	netmask 255.255.255.252
	gateway 10.7.24.133
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth1
iface eth1 inet static
	address 10.7.24.105
	netmask 255.255.255.248

auto eth2
iface eth2 inet static
	address 10.7.24.137
	netmask 255.255.255.252

auto eth3
iface eth3 inet static
	address 10.7.24.141
	netmask 255.255.255.252

auto eth4
iface eth4 inet static
	address 10.7.24.149
	netmask 255.255.255.252



Denken	
Eth0 - a9 10.7.24.130	255.255.255.252 
	Eth1 - a10 10.7.22.1	255.255.255.0

	auto eth0
iface eth0 inet static
	address 10.7.24.130
	netmask 255.255.255.252
	gateway 10.7.24.129
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth1
iface eth1 inet static
	address 10.7.22.1
	netmask 255.255.255.0



Frieren
Eth0 - a8 10.7.24.126	255.255.255.252
Eth1 - a7 10.7.24.65	255.255.255.224
Eth2 - a6 10.7.24.121	255.255.255.252

auto eth0
iface eth0 inet static
	address 10.7.24.126
	netmask 255.255.255.252
	gateway 10.7.24.125
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth1
iface eth1 inet static
	address 10.7.24.65
	netmask 255.255.255.224

auto eth2
iface eth2 inet static
	address 10.7.24.121
	netmask 255.255.255.252

Flamme
Eth0 - a6 10.7.24.122	255.255.255.252
Eth1 - a2 10.7.24.113	255.255.255.252
Eth2 - a3 10.7.8.1	255.255.252.0
Eth3 - a4 10.7.24.117	255.255.255.252

auto eth0
iface eth0 inet static
	address 10.7.24.122
	netmask 255.255.255.252
	gateway 10.7.24.121
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth1
iface eth1 inet static
	address 10.7.24.113
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.7.8.1
	netmask 255.255.252.0

auto eth3
iface eth3 inet static
	address 10.7.24.117
	netmask 255.255.255.252

Fern
Eth0 - a2 10.7.24.114	255.255.255.252
Eth1 - a1 10.7.0.1	255.255.248.0
	
auto eth0
iface eth0 inet static
	address 10.7.24.114
	netmask 255.255.255.252
	gateway 10.7.24.113
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth1
iface eth1 inet static
	address 10.7.0.1
	netmask 255.255.248.0


Heiter
Eth0 - a16 10.7.24.3	255.255.255.192
Eth1 - a17 10.7.12.1	255.255.252.0

auto eth0
iface eth0 inet static
	address 10.7.24.3
	netmask 255.255.255.192
	gateway 10.7.24.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth1
iface eth1 inet static
	address 10.7.12.1
	netmask 255.255.252.0

Himmel
Eth0 - a4 10.7.24.118	255.255.255.252
Eth1 - a5 10.7.24.97	25.255.255.248

auto eth0
iface eth0 inet static
	address 10.7.24.118
	netmask 255.255.255.252
	gateway 10.7.24.117
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth1
iface eth1 inet static
	address 10.7.24.97
	netmask 255.255.255.248

Lawine
Eth0 - a15 10.7.24.146 255.255.255.252
Eth1 - a16 10.7.24.1	255.255.255.192

auto eth0
iface eth0 inet static
	address 10.7.24.146
	netmask 255.255.255.252
	gateway 10.7.24.145
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth1
iface eth1 inet static
	address 10.7.24.1
	netmask 255.255.255.192

Linie
Eth0 - a14 10.7.24.142 255.255.255.252
Eth1 - a15 10.7.24.145 255.255.255.252
Eth2 - a18 10.7.20.0	255.255.254.0

auto eth0
iface eth0 inet static
	address 10.7.24.142
	netmask 255.255.255.252
	gateway 10.7.24.141
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth1
iface eth1 inet static
	address 10.7.24.145
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.7.20.1
	netmask 255.255.255.254.0

Lugner
Eth0 - a19 10.7.24.150 255.255.255.252
Eth1 - a20 10.7.23.1	255.255.255.0
Eth2 - a21 10.7.16.1	255.255.255.0

auto eth0
iface eth0 inet static
	address 10.7.24.150
	netmask 255.255.255.252
	gateway 10.7.24.149
	up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth1
iface eth1 inet static
	address 10.7.23.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.7.16.1
	netmask 255.255.252.0

```

#### Routing
```
aura
route add -net 10.7.24.64 netmask 255.255.255.224 gw 10.7.24.126
route add -net 10.7.24.116 netmask 255.255.255.252 gw 10.7.24.126
route add -net 10.7.24.112 netmask 255.255.255.252 gw 10.7.24.126
route add -net 10.7.24.120 netmask 255.255.255.252 gw 10.7.24.126
route add -net 10.7.0.0 netmask 255.255.248.0 gw 10.7.24.126
route add -net 10.7.8.0 netmask 255.255.252.0 gw 10.7.24.126
route add -net 10.7.24.96 netmask 255.255.255.248 gw 10.7.24.126
route add -net 10.7.22.0 netmask 255.255.255.0 gw 10.7.24.130
route add -net 10.7.24.104 netmask 255.255.255.248 gw 10.7.24.134
route add -net 10.7.24.136 netmask 255.255.255.252 gw 10.7.24.134
route add -net 10.7.24.140 netmask 255.255.255.252 gw 10.7.24.134
route add -net 10.7.24.0 netmask 255.255.255.192 gw 10.7.24.134
route add -net 10.7.12.0 netmask 255.255.252.0 gw 10.7.24.134
route add -net 10.7.20.0 netmask 255.255.254.0 gw 10.7.24.134
route add -net 10.7.24.144 netmask 255.255.255.252 gw 10.7.24.134
route add -net 10.7.23.0 netmask 255.255.255.0 gw 10.7.24.134
route add -net 10.7.16.0 netmask 255.255.252.0 gw 10.7.24.134
route add -net 10.7.24.148 netmask 255.255.255.252 gw 10.7.24.134

Eisen
route add -net 10.7.24.144 netmask 255.255.255.252 gw 10.7.24.142
route add -net 10.7.24.0 netmask 255.255.255.192 gw 10.7.24.142
route add -net 10.7.12.0 netmask 255.255.252.0 gw 10.7.24.142
route add -net 10.7.20.0 netmask 255.255.254.0 gw 10.7.24.142
route add -net 10.7.23.0 netmask 255.255.255.0 gw 10.7.24.150
route add -net 10.7.16.0 netmask 255.255.252.0 gw 10.7.24.150

Frieren
route add -net 10.7.24.120 netmask 255.255.255.252 gw 10.7.24.122
route add -net 10.7.0.0 netmask 255.255.248.0 gw 10.7.24.122
route add -net 10.7.8.0 netmask 255.255.252.0 gw 10.7.24.122
route add -net 10.7.24.116 netmask 255.255.255.252 gw 10.7.24.122
route add -net 10.7.24.96 netmask 255.255.255.248 gw 10.7.24.122

Flamme
route add -net 10.7.0.0 netmask 255.255.255.252 gw 10.7.24.114
route add -net 10.7.24.96 netmask 255.255.255.252 gw 10.7.24.118

Lawine
route add -net 10.7.12.0 netmask 255.255.252.0 gw 10.7.24.2

Linie
route add -net 10.7.24.0 netmask 255.255.255.192 gw 10.7.24.146
route add -net 10.7.12.0 netmask 255.255.252.0 gw 10.7.24.146

```

c) Konfigurasi Client
```
AppetiteRegion
auto eth0
iface eth0 inet static
address 10.7.0.3
netmask 255.255.248.0
gateway 10.7.0.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf

BredRegion
auto eth0
iface eth0 inet static
address 10.7.24.2
netmask 255.255.255.192
gateway 10.7.24.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf

GrabForest
auto eth0
iface eth0 inet static
address 10.7.23.2
netmask 255.255.255.0
gateway 10.7.23.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Granzchannel
auto eth0
iface eth0 inet static
address 10.7.20.2
netmask 255.255.254.0
gateway 10.7.20.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Lakekorridor
auto eth0
iface eth0 inet static
address 10.7.24.66
netmask 255.255.255.224
gateway 10.7.24.65
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Laubhills
auto eth0
iface eth0 inet static
address 10.7.0.2
netmask 255.255.248.0
gateway 10.7.0.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf

ReigelCanyon
auto eth0
iface eth0 inet static
address 10.7.12.3
netmask 255.255.252.0
gateway 10.7.12.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Revolte
auto eth0
iface eth0 inet static
address 10.7.24.107
netmask 255.255.255.248
gateway 10.7.24.105
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Richter
auto eth0
iface eth0 inet static
address 10.7.24.106
netmask 255.255.255.248
gateway 10.7.24.105
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Rohrroad
auto eth0
iface eth0 inet static
address 10.7.8.2
netmask 255.255.252.0
gateway 10.7.8.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Schwermountains
auto eth0
iface eth0 inet static
address 10.7.24.98
netmask 255.255.255.248
gateway 10.7.24.97
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Royalcapital
auto eth0
iface eth0 inet static
address 10.7.22.2
netmask 255.255.255.252
gateway 10.7.22.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Sein
auto eth0
iface eth0 inet static
address 10.7.12.2
netmask 255.255.252.0
gateway 10.7.12.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Stark
auto eth0
iface eth0 inet static
address 10.7.24.138
netmask 255.255.255.252
gateway 10.7.24.137
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Turkregion
auto eth0
iface eth0 inet static
address 10.7.16.2
netmask 255.255.252.0
gateway 10.7.16.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf

Wileregion
auto eth0
iface eth0 inet static
address 10.7.22.3
netmask 255.255.255.252
gateway 10.7.22.1
up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
**Hasil**
Berikut ini adalah pengujian ping dari antar node yang berjauhan:
![WhatsApp Image 2023-12-05 at 08 29 00_79f338dc](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/121850356/a674edab-4fb4-4205-983a-bc3e499a1d2c)
List IP:
1) Ping Sein dari Richter
Sein  10.7.12.2
Richter  10.7.24.106
2) Ping Granzchannel dari Turk Region
Granzchannel  10.7.20.2
Turk region 10.7.16.2
3) Ping Riegel Canyon dari Aura
Riegelcanyon  10.7.12.3
Aura
4) Ping Fern dari Linie
Fern 10.7.24.114
Linie  10.7.24.142
5) Ping Royalcapital dari Laubhills
Royalcapital  10.7.22.2
Laubhills  10.7.0.2
6) Ping Heiter dari Denken
Heiter  10.7.24.3
Denken address 10.7.24.130
7) Ping Schwermountains dari Lugner
Schwermountains 10.7.24.98
Lugner   10.7.24.150

### Kendala
Dalam praktikum jaringan komputer ini, saya menghadapi kendala yang cukup berat karena keterbatasan ruang penyimpanan dan memori pada laptop saya. Saat menjalankan GNS3, terminal berjalan sangat lambat dan sering kali saya harus melakukan restart berulang kali untuk memastikan bahwa memori cukup. Keadaan ini semakin diperparah dengan masalah pada kipas laptop, yang sampai mengalami error akibat beban kerja yang berlebihan. Situasi ini membuat proses praktikum menjadi lebih menantang dan membutuhkan waktu yang lebih lama dari yang diharapkan.

## CIDR

**Topologi**
Topologi dari kelompok kami sebagai berikut:

![Jarkom Heru - Frame 122](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/d792dd31-f06e-4924-a71e-ed37f2ad7cfa)

**Tree CIDR**
Tree CIDR yang telah kami buat sebagai berikut:
![frame tree](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/d858b58c-ba4b-4484-a133-378b2a4d4f0a)


**Penggabungan IP**


**Pembagian IP**
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/10d92a7f-d2b7-4154-8632-226e4804c6d7)
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/10382f9d-8e8b-4e93-984a-676dce2493bc)
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/31d958f5-f0cf-4fbd-a687-b11c17cadd14)

**Subneting**
1. LaubHills
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/a23b0b1c-3ae4-461a-9b15-2ee57144711c)

2. AppetionRegion
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/132e53ef-bd88-41aa-a291-1661b0ff6e72)

3. RorhRoad
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/4515ffb7-2bf9-45c0-93f2-00b4fc79d5c7)

4. Lakekoridor
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/cdb4c2c5-82f6-4320-bf32-1de9a1983bc7)

5. RoyalCapital
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/929c265a-55dd-46e2-a60f-aed2e8241a4d)

6. WilleRegion
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/35c3e2e2-300a-4797-85ed-b02cda1a7ab8)

7. Stark
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/202495af-5b22-4881-9ce9-b490a298cc81)

8. TurkRegion
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/afccf2a4-0590-4ea7-ba48-e1e4fff8d52a)

9. GrobeForest
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/e682645a-b155-40d0-9e2b-cdf086a4da50)

10. GranzChannel
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/7c538b99-b6f2-4f18-b7d9-052099548e98)

11. RiegelCanyon
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/e0ee223d-32d4-447d-ac3e-6fc710abbf3c)

12. Sein
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/a2ed062e-c16e-42ec-b881-f9f5b9e4a096)

13. BredtRegion
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/6bbc588e-4063-4361-bb9c-9e600189cc1a)

14. Revolte
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/82d0d464-843d-44b0-9ef3-e8102932fbef)

15. Ritcher
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/53fe2c58-4f29-45f7-80fb-c708f0e410b1)

16. SchewerMountains
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/84c12031-61e9-4f4b-ba1e-1220a786d3d8)


**Routing**
1. Aura


![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/84541a8f-716d-459d-aaff-2cce51a5f604)

3. Eisen


![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/806ba8ef-0cf0-4268-9bd1-56415f39990a)

4. Linie


![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/2a37b1b0-7012-469a-ba28-7618cc635cfd)

5. Danken


![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/8dc24ad4-853b-44df-bb54-0368bf9b1e2d)

6. Lugner


![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/f5e30305-69d8-481e-964c-04604857a0a1)

7. Lawine


![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/4dd22967-6844-49cd-875e-5a0c64b55e7a)

8. Heiter


![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/1c971dc5-86d4-4569-8ad9-2e75e61ceb8e)

9. Himmel


![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/f727cec8-f183-4ec9-b74f-b99e4fd7b141)

10. Flamme


![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/31f70ec4-1229-4eb9-9015-ddfc715f1a15)

11. Frieren


![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/d0daf926-c320-4ca9-8d2c-c6c0a35aee4e)

**Hasil**

![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/775ee7d2-c4eb-4a97-824e-879c4a9ca4dd)
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/3856774c-bfd0-4286-bad6-a2e509555de2)
![image](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/93961310/0d9b530a-2785-482f-b317-ad8820fdb65e)


**Kendala**
1. Ketika testing harus mencoba lagi terkadang failed









