# Laporan Instalasi dan Konfigurasi SSH Server di Ubuntu

## 1. Instalasi Ubuntu Server
Langkah pertama yang dilakukan adalah menginstal **Ubuntu Server** pada VirtualBox. Pastikan kamu memiliki file ISO Ubuntu Server terbaru dan mengikuti langkah-langkah instalasi.

**Tangkapan layar:**
![Instalasi Ubuntu Server](./install-ubuntu-server.png)

## 2. Persiapan SSH di Ubuntu Server
Setelah Ubuntu Server terinstal, kita perlu melakukan beberapa persiapan agar server dapat menerima koneksi SSH. Langkah ini mencakup instalasi paket yang dibutuhkan.

1. **Update Ubuntu Server**
   Perintah pertama yang dijalankan adalah memperbarui paket-paket di sistem:

   ```bash
   sudo apt update
   sudo apt upgrade
   ```

   **Tangkapan layar:**
   ![Update Sistem Ubuntu](./install-apt-update.png)

2. **Instalasi OpenSSH Server**
   Instal **OpenSSH Server** untuk memungkinkan akses jarak jauh ke server:

   ```bash
   sudo apt install openssh-server
   ```

   **Tangkapan layar:**
   ![Instal OpenSSH](./install-open-ssh-server-ubuntu-server-real.png)

3. **Mengaktifkan dan Mengecek Status SSH Service**
   Setelah OpenSSH terinstal, aktifkan layanan SSH agar bisa berjalan otomatis:

   ```bash
   sudo systemctl enable ssh
   sudo systemctl start ssh
   ```

   **Tangkapan layar:**
   ![Mengaktifkan SSH Service](./mengaktifkan-ssh-service-server-real.png)

4. **Cek Status SSH**
   Untuk memastikan layanan SSH sudah berjalan, jalankan perintah berikut:

   ```bash
   sudo systemctl status ssh
   ```

   **Tangkapan layar:**
   ![Status SSH](./status-ssh-aktif.png)

## 3. Mengubah Port SSH menjadi 40
Untuk meningkatkan keamanan, port default (22) SSH diubah menjadi **port 40**.

1. **Mengedit Konfigurasi SSH**
   Buka file konfigurasi SSH:

   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

   Ubah baris `#Port 22` menjadi `Port 40`, lalu simpan dan keluar dari editor.

   **Tangkapan layar:**
   ![Mengubah Port](./mengganti-port-menjadi-40.png)

2. **Restart SSH untuk Menerapkan Perubahan**
   Setelah mengubah port, restart layanan SSH agar perubahan diterapkan:

   ```bash
   sudo systemctl restart ssh
   ```

   **Tangkapan layar:**
   ![Restart SSH](./restart-ssh-agar-port-40-diterapkan.png)

## 4. Mencoba Remote Sebelum dan Sesudah Mengubah Port
Sebelum mengubah port SSH, saya mencoba meremote Ubuntu Server menggunakan port default (22). Setelah mengubah port menjadi 40, saya mencoba kembali meremote server dan berhasil terhubung.

1. **Remote Sebelum Mengubah Port**
   Pada percobaan pertama, saya mencoba meremote dengan port default, namun terjadi **Connection Refused** karena belum membuka port di firewall:

   ```bash
   ssh username@server_ip
   ```

   **Tangkapan layar:**
   ![Connection Refused](./connection-refused.png)

2. **Remote Setelah Mengubah Port**
   Setelah port diubah menjadi 40, remote berhasil dengan perintah berikut:

   ```bash
   ssh username@server_ip -p 40
   ```

   **Tangkapan layar:**
   ![Remote Berhasil dengan Port 40](./terhubung-remote-dengan-server.png)

## 5. Bukti Remote Berhasil dan Pembuatan File di Server
Sebagai bukti bahwa remote berhasil, saya membuat file di server menggunakan perintah `touch`:

```bash
touch file-di-server.txt
```

   **Tangkapan layar:**
   ![Bukti Remote dan Pembuatan File](./bukti-remote-membuat-file-di-server.png)

---

Itulah langkah-langkah instalasi, konfigurasi SSH, dan pengubahan port pada Ubuntu Server. Semua langkah di atas telah dilakukan dan diuji, dengan hasil remote berhasil menggunakan port 40.
```
