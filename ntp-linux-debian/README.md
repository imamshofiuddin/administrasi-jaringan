<h1>NTP</h1>
NTP (Network Time Protocol) adalah sebuah protokol yang digunakan untuk pengsinkronan waktu (menyamakan waktu) di dalam sebuah jaringan, baik itu LAN maupun jaringan internet. Protokol NTP ini berjalan pada port 123. Proses penyamaan waktu yang dilakukan oleh NTP sangatlah akurat. NTP ini berjalan pada dua sisi yaitu Server dan Client. Di server NTP ini berfungsi sebagai server yang menyimpan penanggalan waktu yang akurat dan nantinya akan di request oleh NTP Client.<br><br>

<h1>Set NTP ke 0.id.pool.ntp.org</h1>
<p>Pertama, kita set time ke Asia/Jakarta dengan perintah berikut.</p>   
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/set_time1.jpg" />
<p>Lalu jangan aktifkan RTC (Real Time Clock) ke UTC dengan perintah berikut.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/set_time2.jpg" />
<p>Aktifkan NTP client untuk sinkronisasi waktu dengan perintah berikut.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/set_ntp.jpg" />
<p>Edit timesyncd.conf untuk setting NTP servers yang anda gunakan dengan perintah <code>sudo nano /etc/systemd/timesyncd.conf</code>.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/set_ntp1.jpg" height="270" />
<p>Restart NTP dengan perintah <code>sudo systemctl restart systemd-timesyncd</code></p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/restart_systemd.jpg"  />
<p>lihat hasilnya dengan perintah <code>timedatectl</code></p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/time_date_ctl.jpg" /><br>

<h1>NTP Server</h1>
<h3><b>Instalasi NTP Server</b></h3>
<p>Untuk menginstall paket ini kita gunakan perintah <code>apt-get install ntp</code> maka ntp server akan terinstall
</p>

<h3><b>Konfigurasi NTP Server</b></h3>
Pertama buka file konfigurasi ntp dengan perintah <code>sudo nano /etc/ntp.conf</code>.<br>
Setelah itu beri tanda pagar (#) pada depan text pool 0 sampai server 3. Lalu tambahkan text baru dibawahnya untuk membuat NTP Server.<br>
<img src="images/1.jpg"><br>
- server 127.127.1.0 : membuat agar NTP Server mensinkronasikan ntp dengan waktu (penanggalan) yang ada di local sistem NTP Server<br>
- fudge 127.127.1.0 stratum 1 : membuat ntp server sebagai mode server yaitu pada stratum (strata) 1.<br><br>

Lalu buang tanda pagar (#) pada text restrict yang berada di bawah text # cryptographically authenticated. Lalu ubah menjadi network address dan netmask antara NTP Server dengan NTP Client dan tambahi notrap nomodify<br>
<img src="images/7.jpg"><br><br>
Lalu restart service ntp untuk memulai ulang service ntp serta mengaktifkan semua konfigurasi yang telah kita ubah dengan perintah <code>service ntp restart</code><br><br>
Cek dan pastikan bahwa NTP Server sudah aktif dengan perintah <code>systemctl status ntp</code><br>
<img src="images/3.jpg"><br><br>

<h3><b>Tes NTP Server</b></h3>
buka client windows, lalu buka change date and time settings untuk mengubah pewaktuan dari client.<br><br>
<img src="images/5.jpg" width="300"><br><br>
Lalu buka menu tab internet time lalu buka change setting kemudian ubah kolom server menjadi ip address dari NTP Server. Lalu klik pada tombol Update now untuk mengaktifkan NTP Client. Jika NTP berhasil maka akan muncul tulisan “The clock was Successfully synchronized”.<br><br>
<img src="images/6.jpg" width="300"><br><br>


