# Lapres Jarkom - Modul 2 - T12
## Oleh
- Mohammad Ifaizul Hasan – 05311840000029
- Anggada Putra Nagamas – 05311840000025
## Soal
![Gambar 1](img/rangkaian.jpg)

Semeru adalah salah satu gunung yang terkenal di Jawa Timur. Bibah adalah salah satu juru kunci Semeru. Bibah ingin menyebarkan keindahan Semeru pada dunia sehingga dia membeli 3 buah server yang berada di MALANG, MOJOKERTO dan PROBOLINGGO. Server MALANG akan digunakan sebagai DNS Server Master, MOJOKERTO akan digunakan sebagai DNS Server Slave dan PROBOLINGGO akan digunakan sebagai Web Server. Selain 3 server terdapat 2 klien yang digunakan untuk testing oleh Bibah yaitu GRESIK dan SIDOARJO. Untuk menyambungkan semua jaringan tersebut Bibah memberi router di SURABAYA.

Kalian diminta untuk membuat sebuah website utama dengan (1) alamat http://semeruyyy.pw yang memiliki (2) alias http://www.semeruyyy.pw, dan (3) subdomain http://penanjakan.semeruyyy.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO serta dibuatkan (4) reverse domain untuk domain utama. Untuk mengantisipasi server dicuri/rusak, Bibah minta dibuatkan (5) DNS Server Slave pada MOJOKERTO agar Bibah tidak terganggu menikmati keindahan Semeru pada Website. Selain website utama Bibah juga meminta dibuatkan (6) subdomain dengan alamat http://gunung.semeruyyy.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP Server PROBOLINGGO. Bibah juga ingin memberi petunjuk mendaki gunung semeru kepada anggota komunitas sehingga dia meminta dibuatkan (7) subdomain dengan nama http://naik.gunung.semeruyyy.pw, domain ini diarahkan ke IP Server PROBOLINGGO.

Setelah selesai membuat keseluruhan domain, kamu diminta untuk segera mengatur web server. (8) Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw. Awalnya web dapat diakses menggunakan alamat http://semeruyyy.pw/index.php/home. Karena dirasa alamat urlnya kurang bagus, maka (9) diaktifkan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home. (10) Web http://penanjakan.semeruyyy.pw akan digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw dan memiliki struktur folder sebagai berikut: 

/var/www/penanjakan.semeruyyy.pw 
- /public/javascripts 
- /public/css 
- /public/images 
- /errors

(11) Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan. (12) Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache. (13) Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts. Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets menjadi http://penanjakan.semeruyyy.pw/js. 

Untuk web http://gunung.semeruyyy.pw belum dapat dikonfigurasi pada web server karena menunggu pengerjaan website selesai. (14) sedangkan web http://naik.gunung.semeruyyy.pw sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada /var/www/naik.gunung.semeruyyy.pw. Dikarenakan web http://naik.gunung.semeruyyy.pw bersifat private (15) Bibah meminta kamu membuat web http://naik.gunung.semeruyyy.pw agar diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya aman dan tidak sembarang orang bisa mengaksesnya. 

Saat Bibah mengunjungi IP PROBOLINGGO, yang muncul bukan web utama http://semeruyyy.pw melainkan laman default Apache yang bertuliskan “It works!”. (16) Karena dirasa kurang profesional, maka setiap Bibah mengunjungi IP PROBOLINGGO akan dialihkan secara otomatis ke http://semeruyyy.pw. (17) Karena pengunjung pada  /var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.
## Persiapan
Sebelum lanjut ke jawaban dari soal-soal tersebut, kami mempersiapkan beberapa alat yang diperlukan. Diantaranya adalah:
1. Xming
2. Putty
3. OpenVPN Connect

Setelah alat yang diperlukan telah disiapkan, maka kami mulai menjalankannya. Berikut langkah-langkahnya:
1. Buka OpenVPN Connect dan nyalakan VPN Profile yang telah ditambahkan dengan `dhcp-option DNS 10.151.77.146`
2. Buka Xming
3. Buka Putty
4. Konfigurasi Putty dengan hostname `10.151.36.203` dan centang pada X11 -> Enable X11 Forwarding
5. Klik Open pada Putty
6. Login dengan Username yaitu nama kelompok dan Password ******
7. Ketika berhasil login maka kami mulai mengonfigurasi **topologi.sh**, berikut konfigurasinya:
```
konfigurasinya masukin sini ngga, atau kasihin gambarnya ya gapapa
```
8. Jalankan `bash topologi.sh` ketika selesai mengonfigurasi
9. Pada router **SURABAYA** lakukan setting sysctl dengan mengetikkan perintah nano `/etc/sysctl.conf`
10. Hilangkan tanda pagar (#) pada bagian `net.ipv4.ip_forward=1`
11. Lalu ketikka `sysctl -p` untuk mengaktifkan perubahan yang ada
12. Setting IP pada setiap UML dengan mengetikkan `nano /etc/network/interfaces` Lalu setting IPnya sebagai berikut:

**SURABAYA**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.76.74
netmask 255.255.255.252
gateway 10.151.76.72

auto eth1
iface eth1 inet static
address 10.151.77.145
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 192.168.0.1
netmask 255.255.255.0
```
**MALANG**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.146
netmask 255.255.255.248
gateway 10.151.77.145
```
**MOJOKERTO**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.147
netmask 255.255.255.248
gateway 10.151.77.145
```
**PROBOLINGGO**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.148
netmask 255.255.255.248
gateway 10.151.77.145
```
**GRESIK**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.3
netmask 255.255.255.0
gateway 192.168.0.1
```
**SIDOARJO**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.255.0
gateway 192.168.0.1
```
13. Restart network dengan mengetikkan `service networking restart` atau `/etc/init.d/networking restart` di setiap UML
14. Ketikkan `iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16` pada router **SURABAYA**
15. Export proxy pada setiap UML dengan sintaks seperti di bawah ini:
```
export http_proxy="http://DPTSI-563672-7bf54:fc9ae@proxy.its.ac.id:8080"
export https_proxy="http://DPTSI-563672-7bf54:fc9ae@proxy.its.ac.id:8080"
export ftp_proxy="http://DPTSI-563672-7bf54:fc9ae@proxy.its.ac.id:8080"
```
16. Lakukan update pada setiap UML dengan mengetikkan `apt-get update`
17. Lakukan instalasi bind pada **MALANG** dan **MOJOKERTO** dengan cara `apt-get install bind9`
18. Lakukan instalasi php dan apache2 pada **PROBOLINGGO** dengan cara `apt-get install apache2` dan `apt-get install php7.0`
19. Lakukan instalasi dnsutils pada **GRESIK** dan **SIDOARJO**
19. Lakukan update pada setiap UML dengan mengetikkan `apt-get update`
## Jawaban
#### 1-3: Pembuatan Domain http://semeruyyy.pw di Malang, Record CNAME http://www.semeruyyy.pw di Malang, Pembuatan Subdomain http://penanjakan.semeruyyy.pw di Malang dan mengarah ke IP Probolinggo
- Lakukan perintah `nano /etc/bind/named.conf.local` pada **MALANG**
- Isikan konfigurasi domain dengan sintax berikut.
```
zone "semerut12.pw" {
	type master;
	file "/etc/bind/jarkom/semerut12.pw";
};
```
- Buat folder jarkom di dalam `/etc/bind` dengan cara `mkdir /etc/bind/jarkom`
- Copykan file `db.local` pada path `/etc/bind` ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi `semerut12.pw` dengan cara `cp /etc/bind/db.local /etc/bind/jarkom/semerut12.pw`
- Kemudian buka file `semerut12.pw` dengan cara `nano /etc/bind/jarkom/semerut12.pw` dan edit seperti pada gambar
- Restart bind9 dengan perintah `service bind9 restart`
- Pada client **GRESIK** dan **SIDOARJO** arahkan nameservernya dengan mengedit file `resolve.conf` menggunakan perintah `nano /etc/resolv.conf`
- Uji dengan `ping`

![Gambar 2](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%201%2C2%2Cdan%203.PNG)
#### 4. Reverse DNS (Record PTR) http://semeruyyy.pw
![Gambar 3](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%204.PNG)
#### 5. Membuat DNS Slave di Mojokerto
![Gambar 4](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%205.PNG)
#### 6-7. Delegasi Subdomain http://gunung.semeruyyy.pw di Mojokerto dan mengarah ke IP Probolinggo lalu Pembuatan Subdomain http://naik.gunung.semeruyyy.pw mengarah ke IP Probolinggo
![Gambar 5](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%206%2C7.PNG)
#### 8. DocumentRoot http://semeruyyy.pw pada /var/www/semeruyyy.pw
- Konfigurasi pada `semerut12.pw.conf`
![Gambar 6](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/semerut12.pw.conf.PNG)
- Hasilnya dapat dilihat pada browser
![Gambar 7](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%208.PNG)
#### 9. Module Rewrite http://semeruyyy.pw/index.php/home menjadi http://semeruyyy.pw/home
- Konfigurasi pada `htaccess`
![Gambar 8](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor9%20.htaccess.PNG)
- Hasilnya dapat dilihat pada browser
![Gambar 9](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor9.PNG)
#### 10. DocumentRoot http://penanjakan.semeruyyy.pw pada /var/www/penanjakan.semeruyyy.pw
![Gambar 10](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/penanjakan.semerut12.pw.conf.PNG)
![Gambar 11](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor10%20dir%20root.PNG)
#### 11. Directory Listing Khusus /public pada http://penanjakan.semeruyyy.pw
![Gambar 12](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%2010.PNG)
![Gambar 13](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%2011.PNG)
#### 12. File Error
![Gambar 14](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%2012.PNG)
#### 13. Directory Alias http://penanjakan.semeruyyy.pw/public/javascripts menjadi http://penanjakan.semeruyyy.pw/js
- Saat -indexes
![Gambar 15](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%2013%20saat%20-indexes.PNG)
- Setelah +indexes
![Gambar 16](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%2013%20setelah%20%2Bindexes.PNG)
#### 14. Port 8888 untuk http://naik.gunung.semeruyyy.pw dengan DocumentRoot pada /var/www/naik.gunung.semeruyyy.pw
![Gambar 17](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%2014.PNG)
#### 15. Autentikasi pada http://naik.gunung.semeruyyy.pw
-Gunakan Apache HTPASSWD untuk melakukan autentikasi pada situs `http://naik.gunung.semerut12.pw` pada port `8888`.
-Hal yang harus dilakukan terlebih dahulu adalah menginstall Apache Utilities Package dengan cara `apt-get install apache2 apache2-utils`.
-Buat file `.htpasswd` dengan perintah `nano .htpasswd`
-Kemudian buat password file dengan menggunakan command htpasswd -> `htpasswd -c /etc/apache2/.htpasswd semeru`. Lalu masukkan password pada user `semeru` yaitu `kuynaikgunung`.
![Gambar 18](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor15%20.htpasswd.PNG)
-Lalu lakukan konfigurasi pada `/etc/apache2/sites-available/naik.gunung.semerut12.pw.conf`
![Gambar 19](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/naik.gunung.semerut12.pw.conf.PNG)
-Autentikasi
![Gambar 19](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%2015.PNG)
#### 16. IP PROBOLINGGO Redirect http://semeruyyy.pw
![Gambar 20](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor%2016.PNG)
#### 17. RegEx
File `.htaccess` pada folder `/var/www/penanjakan.semerut12.pw/public/images`
![Gambar 21](https://raw.githubusercontent.com/IzuruSakamaki/Jarkom_Modul2_Lapres_T12/main/ss-modul2/nomor17.PNG)
## Kendala

