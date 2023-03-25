### Workshop Administrasi Jaringan
### 2 D4 IT B
### Kelompok 3

1. Imam Shofiuddin             (3121600037)
2. Adhika Putri Syafrina Bukka (3121600058)
3. Matiin Muhammad Rajab       (3121600059)

## Konfigurasi Mikrotik & Linux Server

**1. Setting IP**
<p>Untuk mengatur IP kita dapat masuk ke menu IP --> addresses dalam winbox, dan tambahkan IP dengan memasukkan ip address, network dan pilih interface-nya. Disini kami membuat ip address 192.168.3.1 dengan network 192.168.3.0 ke interface ether2 (ke lokal). dan IP di ether1 adalah yang mengarah ke jaringan publik.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/IP_add.jpg" height="250" /> <br>

**2. Setting Routes**
<p>Untuk konfigurasi routing kita bisa pergi ke menu IP --> Routes. Maka akan ditampilkan list route yang kita buat. Untuk membuat routing baru kita bisa klik tombol "+". Kemudian, agar jaringan kita mendapatkan internet, maka kita harus melakukan route ke jaringan luar yaitu sumber internet yang ada di topologi jaringan kita sekarang. Dalam kasus ini destination addressnya kita pakai 0.0.0.0/0 dan gatewaynya 10.252.108.212 pada interface ether1.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/IP_route.jpg" height="250" />

**3. Setting dhcp server via dhcp setup**
<p>Untuk konfigurasi dhcp server kita bisa pergi ke menu IP --> DHCP Server. lalu bisa langsung menggunakan menu DHCP Setup, sehingga akan melalui tahapan-tahapan seperti di bawah ini.</p><br>

<p>Pertama, kita pilih interface dimana DHCP Server ini diterapkan, dalam kasus ini yang mengarah ke lokal yaitu ether2.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/dhcp_setup.jpg" />
<p>Kemudian, kita masukkan network address dari ether2.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/dhcp_setup1.jpg" />
<p>Selanjutnya, kita masukkan IP gateway dari ether2.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/dhcp_setup2.jpg" />
<p>Selanjutnya, kita berikan range IP yang akan diberikan ke host, yaitu dari 192.168.3.100-192.168.3.254</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/dhcp_setup3.jpg" />
<p>Kemudian, isikan DNS Servernya.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/dhcp_setup5.jpg" />
<p>Lalu, kita berikan waktu lease time yang akan diberikan ke host.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/dhcp_setup6.jpg" />
<p>Jika seluruh tahapan diatas tidak ada masalah maka DHCP Server berhasil dibuat</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/dhcp_setup7.jpg" height="250" />

**4. Sambungkan PC atau laptop ke jaringan, cek IP address pastikan IP add dari PC mendapatkan IP add dari dhcp server**
<p>Sambungkan kabel LAN ke PC atau laptop yang mengarah ke interface ether2 mikrotiknya, kemudian setelah terhubung pastikan PC atau laptop menerima IP dari DHCP Server, untuk mengeceknya bisa masuk ke Control Panel, pilih menu Network and Internet, pilih Network and Sharing Center, lihat pada Detail Connection. Disini kami sudah berhasil mendapatkan IP dari DHCP Server. kita mendapatkan IP 192.168.3.252</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/net_connect_details.jpg" />

**5. nyalakan VM, pastikan konfigurasi jaringan ter-BRIDGE dan pastikan mendapatkan IP add dari dhcp server**
<p>Untuk mengonfigurasi jaringan pada VirtualBox kita dapat masuk ke menu seetings, lalu pilih Network atau Jaringan. Kemudian untuk mengubah adaptor ter-bridge kita bisa mengubahnya pada selection-box "Terpasang pada" seperti pada contoh.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/jaringan.jpg" height="300" />

<p>Jika sudah mengonfigurasi jaringan pada virtualBox, kita jalankan virtual machine-nya (disini kami menggunakan Linux Debian 9) dan ketika sudah masuk, pastikan kita mendapatkan IP dari dhcp server, untuk mengecek IP kita bisa menggunakan perintah <code>ip a</code> atau <code>ip address</code>. Disini kami sudah mendapatkan IP yaitu 192.168.3.250</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/chech_ip%20a.jpg" height="150" />

**6. Konfigurasi IP VM menjadi static dengan IP : 192.168.X.10**
<p>Untuk mengubah IP debian menjadi static kita bisa masuk ke file /etc/network/interfaces dengan menggunakan perintah <code>sudo nano /etc/network/interfaces</code>. Kemudian ubah isi menjadi seperti di bawah ini. Keterangan :</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/inet_static.jpg" height="200" />
<ul>
  <li>enp0s3 ==> nama interface (sesuaikan dengan vm masing-masing)</li>
  <li>inet static ==> membuat jaringan ip menjadi static</li>
  <li>address ==> ip yang akan diberikan untuk vm</li>
  <li>netmask ==> netmask dari address jaringan</li>
  <li>gateway ==> ip gateway yang mengarah ke router</li>
</ul>
<p>Jika sudah kita restart jaringan menggunakan perintah <code>sudo /etc/init.d/networking restart</code></p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/restart_net.jpg"/>
<p>Jika sudah berhasil cek kembali ip address vm, pastikan mendapatkan ip address sesuai yang kita isikan sebelumnya di file /etc/network/interfaces.</p>

**7. Konfigurasi NTP ke 0.id.pool.ntp.org**
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

**8. Konfigurasi sudo**
<p>Pada konfigurasi sudo ini , nantinya user akan dapat menjalankan seluruh perintah yang ada pada root menggunakan perintah <code>sudo</code></p>
<p>Pertama, kita install sudo dengan perintah <code>sudo apt install sudo</code></p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/sudo3.jpg" />
<p>Kemudian, masuk ke dalam file sudoers, dengan perintah <code>sudo nano /etc/sudoers</code></p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/sudo2.jpg" />
<p>Lalu, tambahkan sintax : <code>[nama user]: ALL=(ALL:ALL)</code> ALL pada <i>User Privilege Spesification</i></p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/sudo1.jpg" height="500" />


**9. Ganti hostname VM menjadi server10.kelompokX.takehome.com** 
<p>Untuk mengganti hostname, kita dapat menggantinya di file /etc/hostname. masuk dengan perintah <code>sudo nano /etc/hostname</code>.</p>
<img src="https://github.com/adhikasyafrina/Workshop-Administrasi-Jaringan/blob/main/Minggu%205/Images/hostname.jpg" height="500"/>  
<p>Jika sudah silahkan disimpan dan reboot VM-nya.</p>
