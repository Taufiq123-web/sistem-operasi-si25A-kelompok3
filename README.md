# sistem-operasi-si25A-kelompok3
# Tugas Instalasi Debian 13 Headless - Kelompok 3
# Laporan Tugas Kelompok: Instalasi Debian 13 Headless Web Server

**Mata Kuliah:** Sistem Operasi (SI-25)  
**Program Studi:** Sistem Informasi  
**Universitas Galuh**

## 👥 Anggota Kelompok 3 (Kelas SI-2025A)
1. Ahmad Nurrohman - 7020250017
2. Febi Muhammad Fauzi - 7020250005
3. Muhammad Taufiq - 7020250009
4. Rezanur Azizah - 7020250003
5. Alya Fauziah Haq - 7020250002

## 🎯 Spesifikasi Lingkungan Server
| Komponen | Keterangan |
|----------|------------|
| Hypervisor | VMware Workstation Pro |
| Sistem Operasi | Debian 13 Headless (CLI) |
| Hostname | server-SI2025A |
| IP Address VM | 192.168.15.132 |
| Web Server | Nginx |
| Port Forwarding | Host 8080 → Guest 80 |

IP Address diperoleh menggunakan perintah:

```
ip a
```

Kemudian melihat interface **ens33**.
## 🛠️ Langkah-Langkah & Dokumentasi Praktikum

# 1. Instalasi Debian 13 Headless
Pada tahap pertama praktikum, kami melakukan instalasi sistem operasi Debian 13 menggunakan VMware Workstation Pro sebagai virtualisasi server. Instalasi dilakukan dalam mode **Headless (CLI / Command Line Interface)**, yaitu sistem dijalankan tanpa tampilan desktop grafis sehingga lebih ringan, hemat resource, dan lebih sesuai digunakan sebagai server.

## Langkah 1.Persiapan Virtual Machine
Sebelum instalasi dilakukan, kami terlebih dahulu membuat Virtual Machine baru pada VMware Workstation Pro dengan langkah-langkah berikut:

1. Membuka aplikasi VMware Workstation Pro.
2. Memilih menu:
   ```
   Create a New Virtual Machine
   ```
3. Memilih tipe konfigurasi:
   ```
   Typical (Recommended)
   ```
   Mode ini digunakan karena lebih mudah dan otomatis mengatur sebagian konfigurasi dasar VM.

## Langkah 2.Memasukkan File ISO Debian
Selanjutnya memilih file installer Debian 13 berbentuk ISO.
Pada bagian:
```
Installer disc image file (iso)
```
kami memilih file:
```
debian-13.iso
```
ISO tersebut berfungsi sebagai media instalasi sistem operasi Debian.

## Langkah 3.Menentukan Nama dan Lokasi Virtual Machine
Kemudian menentukan:
* Nama VM
* Lokasi penyimpanan file VM
Contoh:
```
Virtual Machine Name : Debian13-Server
```
Tujuannya agar VM mudah dikenali dan file tersimpan rapi.

## Langkah 4.Konfigurasi Kapasitas Harddisk Virtual
Pada tahap ini menentukan ukuran harddisk virtual.
Contoh:
```
20 GB
```
Kemudian memilih:
```
Store virtual disk as a single file
```
Penjelasan:
* Harddisk virtual digunakan sebagai media penyimpanan Debian.
* Ukuran 20 GB sudah cukup untuk kebutuhan web server sederhana.
* Single file dipilih agar performa lebih baik.

## Langkah 5.Mengatur Hardware Virtual Machine
Sebelum VM dijalankan, dilakukan pengaturan hardware tambahan dengan memilih:
```
Customize Hardware
```
Konfigurasi yang digunakan:

| Hardware |	Konfigurasi |
|----------|------------|
| RAM	| 4 GB |
| Processor	| 6 Core |
| Network Adapter |	NAT |
| CD/DVD	Debian | 13 ISO |

Penjelasan:
1. RAM Virtual Machine ditentukan berdasarkan kapasitas RAM komputer host. Pada praktikum ini digunakan 4 GB RAM karena Debian 13 Headless tidak memerlukan tampilan grafis sehingga penggunaan memori lebih ringan.

Penggunaan RAM tidak boleh terlalu besar karena komputer host juga memerlukan memori untuk menjalankan sistem operasi utama dan VMware.

Contoh:
- Jika RAM laptop 4 GB → VM cukup 1–2 GB
- Jika RAM laptop 8 GB → VM bisa 2–4 GB
- Jika RAM laptop 16 GB → VM bisa lebih besar

2. Processor

  Jumlah processor/core virtual juga disesuaikan dengan jumlah core processor komputer host.

3. Network Adapter
Mode jaringan dipilih:
```
NAT
```
Karena:
* VM bisa terhubung internet menggunakan koneksi host,
* lebih mudah dikonfigurasi,
* cocok untuk praktikum.

## Langkah 6.Menjalankan Virtual Machine
Setelah konfigurasi selesai, VM dijalankan.
Saat pertama booting akan muncul tampilan installer Debian.
Menu yang dipilih:
```
Install
```
Bukan:
```
Graphical Install
```
Karena sistem akan dibuat dalam mode CLI/headless.

## Langkah 7.Pemilihan Bahasa Sistem
Installer Debian kemudian meminta konfigurasi bahasa.
Pengaturan yang dipilih:
| Pengaturan	| Pilihan |
|----------|------------|
| Language	| English |
| Country	| Indonesia |
| Keyboard	| American English |

Penjelasan:
Language
Menentukan bahasa sistem installer Debian.

Country
Menentukan zona wilayah, mirror repository, dan format regional.

Keyboard
Menentukan tata letak keyboard agar input terminal sesuai.

## Langkah 8.Deteksi Hardware dan Network
Installer Debian akan:
* mendeteksi hardware virtual,
* mendeteksi network adapter,
* dan mencoba mendapatkan IP otomatis dari DHCP.

Jika berhasil, maka VM akan memperoleh IP Address secara otomatis.

## Langkah 9.Konfigurasi Hostname
Pada tahap ini Debian meminta nama host server.
Hostname yang digunakan:
```
server-SI2025A
```
Fungsi hostname:
* identitas server di jaringan,
* mempermudah administrasi server,
* mempermudah identifikasi device.

Contoh tampilan:
```
Hostname: server-SI2025A
```

## Langkah 10.Konfigurasi Domain Name
Installer kemudian meminta:
```
Domain Name
```
Bagian ini dikosongkan karena server hanya digunakan untuk praktikum lokal.

Lalu memilih:
```
Continue
```

## Langkah 11.Konfigurasi Password Root
Tahap berikutnya adalah membuat password administrator.
User:
```
root
```
merupakan akun dengan hak akses tertinggi pada Linux.

Password root digunakan untuk:
* menginstal aplikasi,
* mengubah konfigurasi sistem,
* mengelola service,
* dan administrasi server.
Password dimasukkan 2 kali untuk verifikasi.

## Langkah 12.Membuat User Biasa
Selain root, Debian meminta pembuatan user biasa.
Contoh:
```
Full Name : Kelompok-3
Username  : kelompok-3
```
Kemudian membuat password user.

Fungsi user biasa:
* digunakan untuk penggunaan sehari-hari,
* lebih aman dibanding selalu menggunakan root,
* mengurangi risiko kesalahan sistem.
N.Konfigurasi Zona Waktu

## Langkah 13.Konfigurasi Partisi Harddisk
Tahap partisi merupakan proses pembagian harddisk untuk sistem Linux.
Karena praktikum menggunakan konfigurasi sederhana, dipilih:
```
Guided - Use Entire Disk
```
Kemudian memilih:
```
All files in one partition (recommended for new users)
```
Penjelasan:
Metode ini membuat:
* root (/)
* home
* swap
berada dalam satu partisi sehingga lebih mudah dikelola.
Installer kemudian menampilkan tabel partisi.
Lalu memilih:
```
Finish partitioning and write changes to disk
```
Kemudian:
```
Yes
```
agar perubahan partisi benar-benar diterapkan.

## Langkah 14.Instalasi Base System Debian
Debian kemudian mulai:
* memformat partisi,
* menyalin file sistem,
* menginstal package dasar,
* dan mengkonfigurasi sistem otomatis.

Proses ini memerlukan beberapa menit tergantung spesifikasi komputer.

## Langkah 15.Software Selection (Tahap Penting)
Tahap ini sangat penting karena menentukan paket sistem yang akan diinstal.
Karena menggunakan mode headless/server, maka hanya memilih:
```
SSH Server
Standard System Utilities
```
Dan TIDAK memilih:
* GNOME
* KDE
* XFCE
* Cinnamon
* Debian Desktop Environment

Penjelasan:

SSH Server
Digunakan agar server dapat diakses jarak jauh menggunakan SSH.

Standard System Utilities

Berisi tools dasar Linux untuk administrasi sistem.

Alasan tidak menggunakan GUI:
* lebih hemat RAM,
* booting lebih cepat,
* performa server lebih optimal,
* lebih stabil,
* dan umum digunakan pada server production.

Screenshot proses menu software selection di bawah ini
* Screenshot proses menu software selection di bawah ini
  ![Software Selection](images/01-software-selection.png)

* Screenshot tampilan login terminal Debian pertama kali di bawah ini
  ![Login Terminal](images/02-debian-login.png)

### 2. Konfigurasi User Sudo & Update Repositori
Pada tahap ini dilakukan beberapa proses penting setelah instalasi Debian selesai, yaitu:

* Login sebagai *root*
* Update sistem
* Install paket *sudo*
* Menambahkan user biasa ke grup *sudo*
* Restart sistem
* Menguji akses sudo menggunakan user biasa

## Langkah 1.Login Sebagai Root

Pada Debian headless, konfigurasi administrator biasanya dilakukan menggunakan akun *root*.

Masuk ke terminal lalu login:
```
su -
```
Kemudian masukkan password root.

Jika berhasil, tampilan terminal berubah menjadi:
```
root@debian:~#
```

**Fungsi Root**

User ```root``` adalah administrator utama Linux yang memiliki hak penuh terhadap sistem, seperti:

* menginstall aplikasi
* menghapus file sistem
* mengatur jaringan
* mengelola user
* melakukan update sistem

Karena aksesnya sangat tinggi, penggunaan root secara langsung tidak disarankan untuk aktivitas sehari-hari.

## Langkah 2. Update Paket Sistem

Perintah yang digunakan:
```
apt update && apt upgrade -y
```

Penjelasan ```apt update```

Perintah:
```
apt update
```

digunakan untuk:

* mengambil daftar paket terbaru dari repositori Debian
* memperbarui informasi package
* mengecek versi terbaru aplikasi

Contoh proses:
```
Get:1 http://deb.debian.org/debian bookworm InRelease
Get:2 http://security.debian.org/debian-security InRelease
Reading package lists... Done
```

Artinya Debian sedang mengambil data paket terbaru dari server repositori.

Penjelasan ```apt upgrade -y```

Setelah daftar paket diperbarui, dilakukan upgrade:
```
apt upgrade -y
```

Fungsi:

* menginstall update terbaru
* memperbarui keamanan sistem
* memperbarui aplikasi bawaan

Penjelasan opsi ```-y```

```-y``` 
berarti:
```
yes
```
Sistem otomatis menyetujui proses install tanpa harus mengetik ```Y``` secara manual.

Fungsi Gabungan ```&&```

Simbol:
```
&&
```
berfungsi menjalankan perintah kedua jika perintah pertama berhasil.

Jadi:
```
apt update && apt upgrade -y
```
berarti:

* update daftar paket
* jika berhasil → lanjut upgrade sistem

## Langkah 3. Install Paket sudo

Perintah:
```
apt install sudo -y
```

**Fungsi sudo**

```sudo``` adalah singkatan dari:
```
Super User Do
```
Digunakan agar user biasa dapat menjalankan perintah administrator tanpa login langsung sebagai root.

Contoh:
```
sudo apt update
```

Penjelasan Perintah
| Bagian	| Fungsi |
|----------|------------|
| apt	| package manager Debian |
| install	| menginstall paket |
| sudo	| nama paket |
|-y	| otomatis menjawab yes |

Contoh Output
```
Reading package lists... Done
Building dependency tree... Done
The following NEW packages will be installed:
sudo
```
Artinya Debian akan menginstall paket sudo.

## Langkah 4. Menambahkan User ke Grup sudo

Perintah:
```
usermod -aG sudo [nama-user-kelompok]
```
Contoh:
```
usermod -aG sudo kelompok-3
```

Penjelasan Perintah
| Bagian | Fungsi |
|----------|------------|
| usermod	| mengubah konfigurasi user |
| -a	| append / menambahkan |
| -G	| group |
| sudo | grup administrator |
| kelompok3	| nama user |

**Fungsi Grup sudo**

Di Debian, hanya user yang masuk ke grup sudo yang dapat menggunakan perintah sudo.

Tanpa masuk grup tersebut, user akan mendapat pesan:
```
user is not in the sudoers file
```

## Langkah 5. Reboot Sistem

Perintah:
```
reboot
```

**Fungsi Reboot**

Digunakan untuk:

* menerapkan perubahan grup user
* menyegarkan sistem
* memastikan konfigurasi berjalan normal

Setelah reboot selesai:

* login menggunakan user biasa
* bukan root

## Langkah 6. Uji Coba sudo oleh User Biasa

Login menggunakan user yang tadi dimasukkan ke grup sudo.

Contoh:
```
login: kelompok-3
password:
```
Lalu jalankan:
```
sudo apt update
```

**Hasil yang Diharapkan**

Sistem meminta password user:
```
[sudo] password for kelompok3:
```
Masukkan password user tersebut.

Jika berhasil akan muncul proses update seperti:
```
Hit:1 http://deb.debian.org/debian bookworm InRelease
Reading package lists... Done
```
Artinya user biasa berhasil menggunakan hak administrator melalui sudo.

## Langkah 7. Alur Konfigurasi Secara Singkat
```
Login root
↓
Update sistem
↓
Install sudo
↓
Tambahkan user ke grup sudo
↓
Reboot
↓
Login user biasa
↓
Uji sudo
```
* *Screenshot hasil uji coba perintah sudo oleh user biasa di bawah ini*
  ![Konfigurasi Sudo](images/07-sudo-config.png) *(Catatan: sesuaikan nama file dengan screenshot Anda)*

### 3. Instalasi Web Server Nginx & Tools Dasar
Pada tahap ini dilakukan instalasi beberapa tools penting dan web server Nginx menggunakan command line pada sistem Debian headless.

Tools yang diinstall:

* net-tools
* curl
* git
* nginx

Kemudian:

* menjalankan service Nginx
* mengaktifkan Nginx agar otomatis berjalan saat booting

## Langkah 1. Pengertian Tools yang Diinstall

 A. net-tools

```net-tools``` adalah paket utilitas jaringan Linux yang berisi beberapa perintah penting seperti:

| Perintah	| Fungsi |
|----------|------------|
| ifconfig	| melihat IP address |
| netstat	| melihat koneksi jaringan |
| route	| melihat routing |
| arp	| melihat ARP table |

Contoh penggunaan:
```
ifconfig
```
Untuk melihat alamat IP server.

 B. curl

```curl``` digunakan untuk:

* mengambil data dari internet
* menguji koneksi server
* mengakses API
* download file dari terminal

Contoh:
```
curl google.com
```

C. git

```git``` adalah sistem version control yang digunakan untuk:

* menyimpan versi project
* clone repository GitHub
* kolaborasi coding

Contoh:
```
git clone https://github.com/user/project.git
```

 D. nginx

Nginx adalah web server yang digunakan untuk:

* menjalankan website
* reverse proxy
* load balancing
* hosting aplikasi web

Nginx terkenal:

* ringan
* cepat
* stabil
* hemat resource

## Langkah 2. Instalasi Paket

Perintah yang digunakan:
```
sudo apt install net-tools curl git nginx -y
```

## Langkah 3. Penjelasan Perintah Instalasi

| Bagian	| Fungsi |
|----------|------------|
| sudo	| menjalankan perintah sebagai administrator |
| apt	| package manager Debian |
| install	| menginstall paket |
| net-tools curl git nginx	| nama paket yang diinstall |
| -y	| otomatis menjawab yes |

## langkah 4. Proses yang Terjadi Saat Instalasi

Ketika perintah dijalankan, Debian akan:

* membaca daftar paket
* mengecek dependency
* mendownload package
* menginstall package
* membuat konfigurasi awal

Contoh Output
```
Reading package lists... Done
Building dependency tree... Done
The following NEW packages will be installed:
curl git nginx net-tools
```
Artinya sistem akan menginstall paket tersebut.

## Langkah 5. Menjalankan Service Nginx

Perintah:
```
sudo systemctl start nginx
```

## Langkah 6. Penjelasan systemctl

```systemctl``` adalah tool untuk mengatur service pada Linux systemd.

Digunakan untuk:

* start service
* stop service
* restart service
* cek status service

## Langkah 7. Penjelasan Perintah Start

| Bagian	| Fungsi |
|----------|------------|
| sudo	| hak administrator |
| systemctl	| pengatur service |
| start	| menjalankan service |
| nginx	| nama service |

## Langkah 8. Fungsi Menjalankan Nginx

Saat service dijalankan:

* web server aktif
* port 80 dibuka
* website default Nginx bisa diakses

## Langkah 9. Mengecek Status Nginx

Gunakan:
```
sudo systemctl status nginx
```
Jika berhasil:
```
active (running)
```
Artinya Nginx sedang berjalan.

## Langkah 10. Mengaktifkan Nginx Saat Booting

Perintah:
```
sudo systemctl enable nginx
```

## Langkah 11. Fungsi Enable

```enable``` digunakan agar service:

* otomatis aktif saat komputer/server hidup
* tidak perlu dijalankan manual lagi

Penjelasan
| Bagian	| Fungsi |
|----------|------------|
| systemctl	| pengatur service |
| enable	| aktif otomatis saat boot |
| nginx	| nama service |

## Langkah 12. Contoh Output Enable
```
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service
```
Artinya service berhasil diaktifkan saat boot.

## Langkah 13. Menguji Apakah Nginx Berjalan
A. Menggunakan Browser

Buka:
```
http://IP-Server
```
Contoh:
````
http://192.168.15.132
````
Jika berhasil muncul halaman:
```
Welcome to nginx!
```
B. Menggunakan curl

Dari terminal:
```
curl localhost
```
Atau:
```
curl 127.0.0.1
```
Jika berhasil akan muncul kode HTML halaman Nginx.

## Langkah 14. Mengecek Port Nginx

Gunakan:
```
sudo netstat -tulpn
```
Atau:
```
ss -tulpn
```
Hasil:
```
tcp LISTEN 0 511 0.0.0.0:80
```
Artinya Nginx berjalan di port 80.

## Langkah 15. Lokasi File Penting Nginx
| Lokasi	| Fungsi |
|----------|------------|
| /etc/nginx/nginx.conf	| konfigurasi utama |
| /etc/nginx/sites-available	| konfigurasi website |
| /var/www/html	| folder website |
| /var/log/nginx	| log nginx |

## Langkah 16. Perintah Penting Nginx
Start
```
sudo systemctl start nginx
```
Stop
```
sudo systemctl stop nginx
```
Restart
```
sudo systemctl restart nginx
````
Reload
```
sudo systemctl reload nginx
```
Status
```
sudo systemctl status nginx
```

## Langkah 17. Alur Instalasi Nginx
```
Install package
↓
Nginx terpasang
↓
Start nginx
↓
Port 80 aktif
↓
Enable nginx
↓
Otomatis berjalan saat boot
```

## Langkah 18. Screenshot yang Biasanya Dibutuhkan
A. Install package
```
sudo apt install net-tools curl git nginx -y
```
B. Menjalankan nginx
```
sudo systemctl start nginx
```
C. Enable nginx
```
sudo systemctl enable nginx
```
D. Status nginx
```
sudo systemctl status nginx
```
* *Screenshot status active running dari Nginx*
  ![Nginx Service Status](images/03-nginx-status.png)

### 4. Pembuatan Halaman Web Profil Kelompok
Pada tahap ini dilakukan pembuatan halaman website sederhana menggunakan HTML yang berisi profil anggota kelompok. File halaman web disimpan pada direktori default Nginx yaitu:
```
/var/www/html/index.html
```
Setelah file diubah, service Nginx direstart agar perubahan dapat dimuat dan ditampilkan pada browser.

## Langkah 1. Pengertian Halaman Web Profil Kelompok

Halaman web profil kelompok adalah halaman website sederhana yang berisi informasi seperti:

* nama kelompok
* anggota kelompok
* NIM
* Motto

Website ini digunakan sebagai:

* latihan dasar web server
* pengujian Nginx
* pembelajaran HTML dasar
* bukti bahwa server berhasil menjalankan website

## Langkah 2. Struktur Dasar Web Server Nginx

Pada Debian, Nginx secara default menyimpan file website di:
```
/var/www/html
```
Folder ini disebut:

**Document Root**

Artinya:

* semua file website dibaca dari folder tersebut
* file HTML di dalam folder dapat diakses melalui browser

## Langkah 3. File Default Nginx

Saat Nginx pertama kali diinstall, terdapat file bawaan:
```
/var/www/html/index.html
```
Isi file tersebut adalah halaman default:
```
Welcome to nginx!
```
File inilah yang akan diganti dengan halaman profil kelompok.

## Langkh 4. Membuka File index.html

Gunakan text editor terminal seperti nano.

Perintah:
```
sudo nano /var/www/html/index.html
```

## Langkah 5. Penjelasan Perintah
| Bagian	| Fungsi |
|----------|------------|
| sudo	| menjalankan sebagai administrator |
| nano	| text editor terminal |
| /var/www/html/index.html	| lokasi file website |

## Langkah 6. Menghapus Isi Default

Setelah file terbuka:

* hapus seluruh isi halaman default nginx
* ganti dengan kode HTML profil kelompok

## Langkah 7. Contoh HTML Profil Kelompok

Contoh sederhana:
```
<!DOCTYPE html>
<html>
    <head><title>Profil Kelompok 3</title></head>
    <body>
        <h1>Server Debian 13 Kelompok 3</h1>
        <p>Anggota      :</p>
            <p>-Ahmad Nurrohman</p>
            <p>-Febi Muhamad Fauzi</p>
            <p>-Muhammad Taufiq</p> 
            <p>-Alya Fauziah Haq</p>
            <p>-Rezanur Azizah </p>
            <p>Motto    :"Tetap Hidup untuk Masa Depan"</p>
</body>
</html>
```

## Langkah 8. Penjelasan Struktur HTML
A. ```<!DOCTYPE html>```

Menentukan bahwa dokumen menggunakan HTML5.

B. ```<html>```

Tag utama pembungkus halaman HTML.

C. ```<head>```

Berisi informasi halaman seperti:

* title
* metadata
* CSS

D. ```<title>```

Judul tab browser.

Contoh:
```
<title>Profil Kelompok 3</title>
```

E. ```<body>```

Bagian utama isi website.

F. ```<h1>```

Heading/judul besar.

G. ```<ul>``` dan ```<li>```

Digunakan membuat daftar anggota kelompok.

H. ```<p>```

Paragraf penjelasan.

## Langkah 9. Menyimpan File pada Nano

Setelah selesai:

* tekan CTRL + O
* tekan Enter
* tekan CTRL + X

Untuk keluar dari nano.

10. Restart Service Nginx

Perintah:
```
sudo systemctl restart nginx
```

## Langkah 11. Fungsi Restart Nginx

Restart digunakan untuk:

* memuat ulang perubahan website
* membaca ulang konfigurasi
* memperbarui service web server

Tanpa restart, terkadang perubahan belum langsung terbaca.

## langkah 12. Penjelasan Perintah Restart
| Bagian	| Fungsi |
|----------|------------|
| sudo	| hak administrator |
| systemctl	| pengelola service Linux |
| restart	| memulai ulang service |
| nginx	| nama service |

## Langkah13. Menguji Website
A. Menggunakan Browser

Buka browser lalu akses:
```
http://localhost
```
Contoh:
```
http://localhost8080
```
Jika berhasil maka halaman profil kelompok akan tampil.

## Langkah 14. Mengecek IP Server

Gunakan:
```
ip a
```
Atau:
```
ifconfig
```
Cari alamat:
```
inet 192.168.x.x
```

## Langkah 15. Alur Kerja Pembuatan Website
```
Edit file index.html
↓
Simpan perubahan
↓
Restart nginx
↓
Akses IP server
↓
Halaman profil tampil
```

## Langkah 16. Struktur Direktori Website
```
/var/www/html
│
├── index.html
```

## Langkah 17. Fungsi Nginx dalam Hal Ini

Nginx bertugas:

* membaca file HTML
* mengirim halaman ke browser client
* membuka akses web melalui port 80
* *Screenshot pengeditan index.html menggunakan nano editor*
  ![Edit index.html](images/04-edit-html.png)


* *Screenshot pengaturan NAT Settings VMware*
  ![NAT Settings VMware](images/05-nat-settings.png)
  
* *Screenshot halaman profil kelompok yang berhasil diakses dari browser host di http://localhost:8080*
  ![Akses Browser Host](images/06-browser-host.png)

## 🎥 Link Video Demo
Tonton Video Demo Pengerjaan Tugas Kelompok 3 di YouTube / Google Drive
(https://youtube.com/...)  
(https://drive.google.com/drive/folders/1N328_OH-5UdNnGg3x8OQ_pglddKVPWPA)

## 📝 Kesimpulan
Melalui praktikum ini, kami memperoleh pengalaman langsung dalam membangun dan mengelola server Linux menggunakan Debian 13. Selama proses pengerjaan, kami menjadi lebih memahami tahapan pembuatan Virtual Machine, instalasi sistem operasi Debian dalam mode teks (headless), instalasi aplikasi pendukung, konfigurasi web server Nginx, hingga pengaturan port forwarding agar server dapat diakses dari komputer host. Praktikum ini juga membuat kami menyadari bahwa setiap langkah konfigurasi harus dilakukan dengan teliti karena kesalahan kecil dapat menyebabkan sistem atau layanan tidak berjalan sebagaimana mestinya. Selain menambah pemahaman mengenai administrasi server Linux, kegiatan ini melatih kemampuan kami untuk bekerja sama, berdiskusi, dan menyelesaikan permasalahan yang muncul selama praktikum. Secara keseluruhan, pengalaman yang kami peroleh memberikan pemahaman yang lebih baik mengenai penerapan server Linux serta menjadi bekal yang bermanfaat untuk pembelajaran dan pengembangan kemampuan kami di bidang teknologi informasi.
