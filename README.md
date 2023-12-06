## Praktikum Modul 4 Jaringan Komputer

**Kelompok A16 :**

| Nama | NRP |
| ----------- | ----------- |
| Clarissa Luna Maheswari | 5025211033 |
| Heru Dwi Kurniawan | 5025211055 

### VLSM
**Tree**
![10 7 0 019](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/121850356/849f97f2-3aee-4325-a8d9-1b4329b54ebc)

Bagian atas pohon VLSM merepresentasikan ruang alamat yang tersedia untuk subnetting. 10.7.0.0/19 adalah subnet induk dari mana semua subnet lainnya berasal. Subnet induk memiliki subnet mask yang lebih besar, yang menunjukkan jumlah alamat yang lebih sedikit yang digunakan untuk tujuan jaringan, dan lebih banyak alamat yang tersedia untuk host.  /19 menunjukkan bahwa 19 bit pertama alamat IP digunakan untuk menentukan jaringan. Dengan subnet mask ini, ada total 2^(32-19) = 2^13, atau 8192 alamat IP yang tersedia.

***Contoh Perhitungan***
Jika kita memerlukan subnet untuk 500 host, subnet mask dihitung sebagai berikut:
1. Mencari pangkat dua yang dapat mengakomodasi 500 host yaitu 2^9 = 512.
2. Kurangi 9 bit yang digunakan untuk host dari total 32 bit untuk mendapatkan subnet yaitu 32-9 = 23
3. Subnet mask menjadi /23 yang menyediakan 512 alamat.

**Subneting**
Dari node induk ini, kita bisa melakukan subnetting lebih lanjut untuk memenuhi kebutuhan spesifik dari berbagai segmen jaringan. contohnya pada subnet **10.7.0.0/20**, subnet ini dibagi lebih lanjut dari 10.3.0.0/19 dan menawarkan 2^(32-20) = 2^12, atau 4096 alamat IP yang tersedia. Subnet-subnet ini kemudian dapat dialokasikan lebih lanjut untuk menciptakan sub-subnet yang lebih kecil, yang disesuaikan dengan jumlah host yang diperlukan dalam masing-masing segmen jaringan. Berikut ini adalah hasil perolehan dari subnetting:

###Tabel Alokasi Subnet

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

**Topologi dan Pembagian Subnet**
![10 7 0 019 (2)](https://github.com/herukurniawann/Jarkom-Modul-4-A16-2023/assets/121850356/995931cb-fb6e-4bad-b218-6a9ab4d52f95)


**Routing**

**Hasil**


**Kendala**








### CIDR

**Topologi**


**Tree CIDR**


**Penggabungan IP**


**Pembagian IP**

**Subneting**

**Routing**

**Hasil**


**Kendala**





