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
## Jawaban
#### 1. Pembuatan Domain http://semeruyyy.pw di Malang
#### 2. Record CNAME http://www.semeruyyy.pw di Malang
#### 3. Pembuatan Subdomain http://penanjakan.semeruyyy.pw di Malang dan mengarah ke IP Probolinggo
#### 4. Reverse DNS (Record PTR) http://semeruyyy.pw di Malang dan Mojokerto
#### 5. Membuat DNS Slave di Mojokerto
#### 6. Delegasi Subdomain http://gunung.semeruyyy.pw di Mojokerto dan mengarah ke IP Probolinggo
#### 7. Pembuatan Subdomain http://naik.gunung.semeruyyy.pw mengarah ke IP Probolinggo
#### 8. DocumentRoot http://semeruyyy.pw pada /var/www/semeruyyy.pw
#### 9. Module Rewrite http://semeruyyy.pw/index.php/home menjadi http://semeruyyy.pw/home
#### 10. DocumentRoot http://penanjakan.semeruyyy.pw pada /var/www/penanjakan.semeruyyy.pw
#### 11. Directory Listing Khusus /public pada http://penanjakan.semeruyyy.pw
#### 12. File Error
#### 13. Directory Alias http://penanjakan.semeruyyy.pw/public/javascripts menjadi http://penanjakan.semeruyyy.pw/js
#### 14.a. Port 8888 untuk http://naik.gunung.semeruyyy.pw 
#### 14.b. DocumentRoot pada /var/www/naik.gunung.semeruyyy.pw
#### 15.a. Autentikasi pada http://naik.gunung.semeruyyy.pw
#### 16. IP PROBOLINGGO Redirect http://semeruyyy.pw
#### 17. RegEx






##### 1. *Webserver: nginx/1.14.0 (Ubuntu)*
```sh
Display Filter: http.host == “testing.mekanis.me”
```
![Gambar 1.1](img/11.jpg)
```sh
Follow TCP Stream
```
![Gambar 1.2](img/12.jpg)
##### 2. *Hasil berupa gambar Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436.jpg*
```sh
File -> Export Objects -> HTTP
```
![Gambar 2.1](img/21.jpg)
```sh
Text Filter: Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436.jpg
```
![Gambar 2.2](img/22.jpg)
```sh
Save dengan format JPG
```
![Gambar 2.3](img/23.jpg)
```sh
Buka Gambar
```
![Gambar 2.4](img/24.jpg)
##### 3. *Username: 10pemuda , Password: guncangdunia*
```sh
Display Filter: http.host == "ppid.dpr.go.id"
```
![Gambar 3.1](img/31fixed.jpg)
```sh
Lihat HTML Form URL Encoded pada Paket yang memiliki Method POST
```
![Gambar 3.2](img/32.jpg)
##### 4. *Tedapat 5 Paket yang menggunakan basic authentication method*
```sh
Display Filter: http.authbasic
```
![Gambar 4.1](img/41.jpg)
##### 5. *Penyelesaian Soal dapat dilihat pada gambar*
```sh
Display Filter: http.host == “aku.pengen.pw”
```
```sh
Lihat Bagian Authorization -> Credentials di salah satu paket
```
![Gambar 5.1](img/51.png)
```sh
Selesaikan Soalnya
```
![Gambar 5.2](img/52.png)
##### 6. *Hasil berupa file PDF yang dapat terbuka*
```sh
Display Filter: ftp-data.command == "STOR zipkey.txt"
```
![Gambar 6.1](img/61.jpg)
```sh
Follow TCP Stream (Ditemukan Passwordnya)
```
![Gambar 6.2](img/62.jpg)
```sh
Display Filter: ftp-data.command == "STOR Answer.zip"
```
![Gambar 6.3](img/63.jpg)
```sh
Follow TCP Stream
```
![Gambar 6.4](img/64.jpg)
```sh
Simpan dalam format ZIP
```
![Gambar 6.5](img/65.jpg)
```sh
Buka File dalam zipfile menggunakan password yang telah ditemukan
```
![Gambar 6.6](img/66.jpg)
```sh
File Terbuka
```
![Gambar 6.7](img/67.jpg)
##### 7. *Hasil berupa file PDF*
```sh
Display Filter: ftp-data contains "Yes.pdf"
```
![Gambar 7.1](img/71.jpg)
```sh
Follow TCP Stream
```
![Gambar 7.2](img/72.jpg)
```sh
Simpan dengan Format ZIP
```
![Gambar 7.3](img/73.jpg)
```sh
Buka zipfile
```
![Gambar 7.4](img/74.jpg)
```sh
Buka Yes.pdf
```
![Gambar 7.5](img/75.jpg)
##### 8. *Readme*
```sh
Display Filter: ftp (Ditemukan bahwa ip Microsoft FTP Service adalah 198.246.117.106)
```
![Gambar 8.1](img/81fixed.jpg)
```sh
Display Filter: ftp.request.command == RETR (Object yang didownload adalah Readme)
```
![Gambar 8.2](img/81.jpg)
##### 9. Username: dhana , Password: dhana123
```sh
ftp.request.command =="USER" untuk melihat Username
```
![Gambar 9.1](img/no9.PNG)
```sh
ftp.request.command =="PASS" untuk melihat Password
```
![Gambar 9.2](img/no9pass.PNG)
##### 10. *Hasil berupa file PDF*
```sh
Control+F
```
![Gambar 10.1](img/no10(1).PNG)
```sh
Klik kanan kemudian follow tcp stream, lalu ubah show and save data as menjadi RAW
```
![Gambar 10.2](img/no10(2).PNG)
```sh
Klik tombol Save as dan simpan file pdf
```
![Gambar 10.3](img/no10(3).PNG)
```sh
Buka file yang telah didownload
```
![Gambar 10.4](img/no10(4).PNG)
#### B. Capture Filter
##### 11. *port 21*
```sh
Buat User dan Shared Folder pada Filezilla Server kemudian log in sebagai User melalui Filezilla Client
```
![Gambar 11.1](img/no11(1).PNG)
```sh
Masukkab "port 21" pada "Capture filter for selected interfaces" dari adapter loopback traffic capture
```
![Gambar 11.2](img/no11(2).PNG)
```sh
File yang melalui port 21 atau FTP sudah terfilter
```
![Gambar 11.3](img/no11(3).PNG)
##### 12. *src port 80*
```sh
Masukkab "src port 80" pada "Capture filter for selected interfaces" dari Wi-Fi, kemudian akses website HTTP misalnya monta.if.its.ac.id
```
![Gambar 12](img/no12.PNG)
##### 13. *dst port 443*
```sh
Masukkab "dst port 443" pada "Capture filter for selected interfaces" dari Wi-Fi, kemudian akses website HTTPS misalnya its.ac.id
```
![Gambar 13](img/no13.PNG)
##### 14. *src host 127.0.0.1*
```sh
Masukkab "src host 127.0.0.1" pada "Capture filter for selected interfaces" dari Adapter for loopback traffic capture
```
![Gambar 14](img/no14.PNG)
##### 15. *src host monta.if.its.ac.id*
```sh
Masukkab "src host monta.if.its.ac.id" pada "Capture filter for selected interfaces" dari Wi-Fi, kemudian akses website monta.if.its.ac.id
```
![Gambar 15](img/no15.PNG)
## Kendala
- Praktikum nya malem jadi saya agak mengantuk (Izul)
- Kelupaan menuliskan jawaban sampai 15 menit sebelum praktikum berakhir (Izul)
