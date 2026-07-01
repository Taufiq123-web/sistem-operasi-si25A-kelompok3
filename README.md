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
Full Name : Muhammad Taufiq
Username  : taufiq
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
* Masuk sebagai user `root`, menginstal paket `sudo`, dan menambahkan user biasa ke grup sudo.
* Menjalankan pembaruan paket sistem dengan perintah:
  ```bash
  apt update && apt upgrade -y
  apt install sudo -y
  usermod -aG sudo [nama-user-kelompok]
  reboot
  ```
* *Screenshot hasil uji coba perintah sudo oleh user biasa di bawah ini*
  ![Konfigurasi Sudo](images/07-sudo-config.png) *(Catatan: sesuaikan nama file dengan screenshot Anda)*

### 3. Instalasi Web Server Nginx & Tools Dasar
* Menginstal `net-tools`, `curl`, `git`, dan `nginx` menggunakan command line.
* Menjalankan dan mengaktifkan service Nginx agar berjalan otomatis saat booting.
  ```bash
  sudo apt install net-tools curl git nginx -y
  sudo systemctl start nginx
  sudo systemctl enable nginx
  ```
* *Screenshot status active running dari Nginx*
  ![Nginx Service Status](images/03-nginx-status.png)

### 4. Pembuatan Halaman Web Profil Kelompok
* Mengubah dokumen default Nginx pada `/var/www/html/index.html` dengan HTML profil anggota kelompok Anda.
* Melakukan restart web server untuk memuat perubahan.
  ```bash
  sudo systemctl restart nginx
  ```
* *Screenshot pengeditan index.html menggunakan nano editor*
  ![Edit index.html](images/04-edit-html.png)

### 5. Konfigurasi Port Forwarding VMware & Pengujian Host
* Melakukan pemetaan port 8080 pada Windows Host ke port 80 Debian Guest VM lewat menu Virtual Network Editor.
* Menguji akses web server Debian melalui browser di sistem operasi host.
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
