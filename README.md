# Lapres Jarkom - Modul 2 - T12
## Oleh
- Mohammad Ifaizul Hasan – 05311840000029
- Anggada Putra Nagamas – 05311840000025
## Soal
![Gambar 1](img/rangkaian.png)
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

#### A. Display Filter
1. Sebutkan webserver yang digunakan pada "testing.mekanis.me"!
2. Simpan gambar "Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436.jpg"!
3. Cari username dan password ketika login di "ppid.dpr.go.id"!
4. Temukan paket dari web-web yang menggunakan basic authentication method!
5. Ikuti perintah di aku.pengen.pw! Username dan password bisa didapatkan dari file .pcapng!
6. Seseorang menyimpan file zip melalui FTP dengan nama "Answer.zip". Simpan dan Buka file "Open This.pdf" di Answer.zip. Untuk mendapatkan password zipnya, temukan dalam file zipkey.txt (passwordnya adalah isi dari file txt tersebut).
7. Ada 500 file zip yang disimpan ke FTP Server dengan nama 1.zip, 2.zip, ..., 500.zip. Salah satunya berisi pdf yang berisi puisi. Simpan dan Buka file pdf tersebut. Your Super Mega Ultra Rare Hint = nama pdf-nya "Yes.pdf"
8. Cari objek apa saja yang didownload (RETR) dari koneksi FTP dengan Microsoft FTP Service!
9. Cari username dan password ketika login FTP pada localhost!
10. Cari file .pdf di wireshark lalu download dan buka file tersebut! clue: "25 50 44 46"
#### B. Capture Filter
11. Filter sehingga wireshark hanya mengambil paket yang mengandung port 21!
12. Filter sehingga wireshark hanya mengambil paket yang berasal dari port 80!
13. Filter sehingga wireshark hanya menampilkan paket yang menuju port 443!
14. Filter sehingga wireshark hanya mengambil paket yang berasal dari ip kalian!
15. Filter sehingga wireshark hanya mengambil paket yang tujuannya ke monta.if.its.ac.id!
## Jawaban
#### A. Display Filter
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
