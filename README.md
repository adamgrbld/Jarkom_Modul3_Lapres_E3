# Jarkom_Modul3_Lapres_E3


## DHCP
**1. Membuat topologi jaringan**

- SSH
  - nano topo.sh
    
    ![1a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/1a.png)
    
 - UML
   
   Lakukan konfigurasi pada semua UML dengan ```interfaces``` sebagai berikut:
   
   ![1b](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/1b.png)
   ![1c](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/1c.png)
   ![1d](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/1d.png)
   ![1e](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/1e.png)
   ![1f](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/1f.png)
   ![1g](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/1g.png)
   ![1h](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/1h.png)
   ![1i](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/1i.png)
    
**2. Membuat SURABAYA sebagai perantara (DHCP Relay) antara DHCP Server dan client**

- TUBAN
  - apt-get install isc-dhcp-server
  - nano /etc/default/isc-dhcp-server
  
    *tambahkan ```INTERFACES="eth0"```*
    
    ![2a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/2a.png)

- SURABAYA
  - apt-get install isc-dhcp-relay
  - masukkan IP TUBAN enter
  
    *tambahkan ```eth1 eth2 eth3```*
    
    ![2b](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/2b.png)
  
- UML Client
  
  - nano /etc/network/interfaces
    
    Ubah semua konfigurasi yang awalnya static menjadi dhcp
    
    ![2c](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/2c.png)
    ![2d](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/2d.png)
    ![2e](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/2e.png)
    ![2f](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/2f.png)
  
**3. Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200**

- TUBAN
  - nano /etc/dhcp/dhcpd.conf
  
    ![3a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/3a.png)
    
  - service isc-dhcp-server restart
    
- GRESIK
  - ip a
  
    ![HasilGresik](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/HasilGresik.jpg)
- SIDOARJO
  -ip a
    ![HasilSidoarjo](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/HasilSidoarjo.jpg)
**4. Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70**

- TUBAN
  - nano /etc/dhcp/dhcpd.conf
  
    ![4a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/4a.png)
    
  - service isc-dhcp-server restart
  
- BANYUWANGI
    - ip a
    
    [HasilBanyuwangi](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/HasilBanyuwangi.jpg)
    
- MADIUN
  - ip a
    
    [HasilMadiun](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/HasilMadiun.jpg)
    
**5. Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP**
 
- UML Client
  - nano /etc/resolv.conf
    
    ![5a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/5a.png)
    ![5b](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/5b.png)
    ![5c](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/5c.png)
    ![5d](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/5d.png)
    
**6. Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan (6) client pada subnet 3 mendapatkan peminjaman IP selama 10 menit**

- SURABAYA
  - nano /etc/dhcp/dhcpd.conf
  
    *Subnet 1 menunjukkan ```lease time``` 300 yang berarti 300 detik / 5 menit*
    
    *Subnet 3 menunjukkan ```lease time``` 600 yang berarti 600 detik / 10 menit*
    
    ![6a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/6a.png)
    ![6b](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/6b.png)
    
  - service isc-dhcp-relay restart
  
## Proxy
  
**7. Menambahkan user autentikasi**

- MOJOKERTO
  - apt-get install squid
  - apt-get install apache2-utils
  
    ...
  
  - htpasswd -c /etc/squid/passwd userta_e03
  - nano /etc/squid/squid.conf
    
    ![7a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/7a.png)
  
  - service squid restart
    
- BROWSER
  - akan muncul kotak autentikasi seperti berikut
  
    ![7b](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/7b.png)
    
**8. Melakukan penjadwalan setiap hari Selasa-Rabu pukul 13.00-18.00**

- MOJOKERTO
  - nano /etc/squid/acl.conf
  
    *tambahkan baris berikut*
    ```
    acl TA time TW 13:00-18:00
    ```
    
  - nano /etc/squid/squid.conf
  
    *tambahkan baris berikut*
    ```
    http_access allow TA
    http_access deny all
    ```
    
  - service squid restart
    
**9. Melakukan penjadwalan setiap hari Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00)**

- MOJOKERTO
  - nano /etc/squid/acl.conf
  
    *tambahkan baris berikut*
    ```
    acl BIMBINGAN1 time TWH 21:00-23:59
    acl BIMBINGAN2 time WHF 00:00-09:00
    ```
    
  - nano /etc/squid/squid.conf
  
    *tambahkan baris berikut*
    ```
    http_access allow BIMBINGAN1
    http_access allow BIMBINGAN2
    ```
    
  - service squid restart
    
  - berikut file ```acl.conf``` dan ```squid.conf``` setelah dilakukan konfigurasi untuk no 8 dan 9
  
    ![9a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/9a.png)
    ![9b](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/9b.png)
    
- BROWSER
  - test dengan mengakses website
  
    *diakses pada hari Sabtu pukul 20:04*
    
    ![9c](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/9c.png)
    
**10. Membuat agar setiap dia mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id**
 
- MOJOKERTO
  - nano /etc/squid/squid.conf
  
    ![10a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/10a.png)
    
  - service squid restart
  
- BROWSER
  - masukkan google.com
  
    *ter-redirect menuju monta.if.its.ac.id*
    
    ![10b](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/10b.png)
    
**11. Mengubah error page default squid**

- MOJOKERTO
  - wget 10.151.36.202/ERR_ACCESS_DENIED
  - cp -r ERR_ACCESS_DENIED /usr/share/squid/errors/English/ERR_ACCESS_DENIED

- BROWSER
  - test dengan mengakses website diluar jam yang ditentukan
  
    *diakses pada hari Jumat pukul 11:00*
    
    ![11a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/11a.png)
    
**12. Menggunakan proxy cukup dengan mengetikkan domain janganlupa-ta.yyy.pw dan memasukkan port 8080**

- MALANG
  - apt-get install bind9 -y
  - nano /etc/bind/named.conf.local
  
    ![12a](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/12a.png)
    
  - mkdir /etc/bind/jarkom
  - cp /etc/bind/db.local /etc/bind/jarkom/janganlupa-ta.e03.pw
  - nano /etc/bind/jarkom/janganlupa-ta.e03.pw
  
    ![12b](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/12b.png)
    
  - service bind9 restart
  
- BROWSER
  - setting proxy dengan mengganti IP dengan ```janganlupa-ta.e03.pw```
  
    ![12c](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/12c.png)
    
  - jika berhasil maka pada autentikasi akan muncul ```janganlupa-ta.e03.pw:8080``` sebagai IP proxy
  
    ![12d](https://github.com/adamgrbld/Jarkom_Modul3_Lapres_E3/blob/main/image/12d.png)
