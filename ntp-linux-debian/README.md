**Set NTP ke 0.id.pool.ntp.org**
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
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/time_date_ctl.jpg" />
