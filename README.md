# Laporan Remote Linux Server dengan Linux Desktop

## Profil Mahasiswa
- **Nama**: Kevin Adiputra Mahesa
- **NIM**: 09011282328115
- **Kelas**: SK3A
- **Mata Kuliah**: Sistem Operasi dan Praktikum Sistem Operasi
- **Dosen Pengampu**: Adi Hermansyah, S.Kom., M.T.

---

## 1. Instalasi Ubuntu Server
Langkah pertama yang dilakukan adalah menginstal **Ubuntu Server** pada VirtualBox. Pastikan file ISO Ubuntu Server terbaru tersedia, dan ikuti langkah-langkah instalasi dengan benar.

![Instalasi Ubuntu Server](https://github.com/user-attachments/assets/2474a03e-6718-43c5-8e94-347527e84444)

### 1.1. Konfigurasi Ubuntu Linux Server di VirtualBox
Pada tahap ini, dilakukan konfigurasi awal di VirtualBox, seperti setting jaringan, alokasi memori, dan pengaturan disk untuk Ubuntu Server.

![Konfigurasi Ubuntu Linux Server di VirtualBox](https://github.com/user-attachments/assets/6b5c1446-15ff-434c-8a29-98027878ac53)

### 1.2. Profil Konfigurasi Server Linux
Setelah instalasi selesai, Ubuntu Server dikonfigurasi sesuai kebutuhan untuk layanan dan akses jarak jauh menggunakan SSH.

![Profil Server Linux](https://github.com/user-attachments/assets/be8de0d0-b393-48e9-b8ed-6ab01bc57bf7)

---

## 2. Persiapan SSH di Ubuntu Server
Setelah instalasi Ubuntu Server, langkah selanjutnya adalah mempersiapkan agar server bisa menerima koneksi SSH.

### 2.1. Instalasi OpenSSH Server di Linux Server
Instalasi **OpenSSH Server** dilakukan dengan menjalankan perintah berikut:

```bash
sudo apt install openssh-server
```

![Instal OpenSSH Server](https://github.com/user-attachments/assets/f0747fd9-4f70-407f-b033-18d3cdeef098)

### 2.2. Mengaktifkan dan Mengecek Status Layanan SSH
Setelah OpenSSH terinstal, layanan SSH diaktifkan agar dapat berjalan otomatis setiap kali server dinyalakan. Gunakan perintah berikut:

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

![Mengaktifkan SSH Service](https://github.com/user-attachments/assets/80a1557c-0ddd-44c9-9bbb-f82ed4940feb)

### 2.3. Cek Status Layanan SSH
Untuk memastikan layanan SSH sudah berjalan dengan baik, perintah berikut dijalankan:

```bash
sudo systemctl status ssh
```

![Cek Status SSH](https://github.com/user-attachments/assets/05ec42e4-6d41-4fee-a977-439f388bcac6)

---

## 3. Mengubah Port SSH Menjadi 40
Untuk meningkatkan keamanan, port default SSH (22) diubah menjadi **port 40**.

### 3.1. Mengedit Konfigurasi SSH
Untuk mengubah port SSH, buka file konfigurasi `sshd_config` dan ubah port menjadi 40:

```bash
sudo nano /etc/ssh/sshd_config
```

Cari baris `#Port 22`, ubah menjadi `Port 40`, lalu simpan dan keluar.

- **Linux Server:**  
  ![Mengubah Port SSH di Server](https://github.com/user-attachments/assets/a05573a4-cc53-40f0-8125-d70778a7dd58)
  
- **Linux Desktop:**  
  ![Mengganti Port di Linux Desktop](https://github.com/user-attachments/assets/2d611b5c-ecdb-4f48-aecc-4871d20cb83e)

### 3.2. Restart Layanan SSH
Setelah perubahan port, restart layanan SSH dengan perintah:

```bash
sudo systemctl restart ssh
```

- **Linux Server:**  
  ![Bukti Port 40 di Server](https://github.com/user-attachments/assets/3559fcc2-b11d-4f44-af5f-2679b529b224)
  
- **Linux Desktop:**  
  ![Port Berubah ke 40 di Desktop](https://github.com/user-attachments/assets/b4cb50e7-8c49-43b8-a2ff-c1df9d48ed68)

---

## 4. Mencoba Remote Sebelum dan Sesudah Mengubah Port

### 4.1. Remote Sebelum Mengubah Port
Sebelum mengubah port, percobaan remote dengan port default (22) dilakukan, namun koneksi ditolak karena port belum dibuka di firewall:

```bash
ssh username@server_ip
```

![Connection Refused pada Port 22](https://github.com/user-attachments/assets/9fff286b-4844-4ab4-bbd3-b0d51bacbd3f)

### 4.2. Remote Setelah Mengubah Port
Setelah port diubah menjadi 40, percobaan remote berhasil dengan perintah:

```bash
ssh username@server_ip -p 40
```

![Remote Berhasil dengan Port 40](https://github.com/user-attachments/assets/296b060d-a831-4321-b1ef-be3e639d7eaa)

---

## 5. Bukti Remote Berhasil dan Pembuatan File di Server
Setelah remote berhasil, sebuah file dibuat di server menggunakan perintah `cat`:

```bash
cat > file-di-server.txt
```

- **Linux Desktop:**  
  ![Mencoba Membuat File di Desktop](https://github.com/user-attachments/assets/081a3e8d-8d52-4d5b-9d23-39b41d682bf4)

- **Linux Server:**  
  ![Bukti Perubahan dan Remote di Ubuntu Server](https://github.com/user-attachments/assets/aa6916d8-a601-41f5-91b1-6aa95128e422)

---

## 6. Konfigurasi Linux Desktop untuk Remote
Selain mengakses server dari mesin lain, kita juga bisa melakukan remote SSH dari **Linux Desktop**. Berikut langkah instalasi SSH client di desktop.

### 6.1. Instalasi SSH Client di Linux Desktop
Jalankan perintah berikut untuk menginstal SSH client di Linux Desktop:

```bash
sudo apt install openssh-client
```

![Mengaktifkan SSH di Desktop](https://github.com/user-attachments/assets/be32ef4d-a04e-41c8-8247-f87604fc8808)

---

## Kesimpulan
Dari percobaan ini, dapat disimpulkan bahwa instalasi dan konfigurasi SSH Server di Ubuntu Server melalui VirtualBox berhasil dilakukan. Mulai dari instalasi Ubuntu Server dan OpenSSH Server hingga perubahan port SSH dari 22 ke 40 demi keamanan, seluruh proses berjalan lancar. Koneksi remote dari Linux Desktop juga berhasil setelah port baru dikonfigurasi dan perintah yang diperlukan dijalankan dengan benar. Langkah-langkah ini memberikan pemahaman yang baik terkait pengaturan SSH untuk akses jarak jauh pada server dan menunjukkan pentingnya keamanan dalam administrasi server jarak jauh.
