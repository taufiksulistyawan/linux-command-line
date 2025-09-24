Untuk mengaktifkan **SSH di Ubuntu Server**, ikuti langkah-langkah berikut:

---

### 1. **Pastikan paket SSH terinstal**

SSH server biasanya tidak aktif secara default, jadi perlu dipasang dulu:

```bash
sudo apt update
sudo apt install openssh-server -y
```

---

### 2. **Cek status SSH service**

Setelah terinstal, cek apakah layanan sudah berjalan:

```bash
systemctl status ssh
```

Jika aktif, statusnya akan **active (running)**.
Kalau belum aktif, jalankan:

```bash
sudo systemctl start ssh
```

---

### 3. **Aktifkan SSH agar otomatis jalan saat boot**

```bash
sudo systemctl enable ssh
```

---

### 4. **Cek port SSH (default 22)**

Gunakan:

```bash
ss -tnlp | grep ssh
```

atau

```bash
netstat -tulpn | grep ssh
```

---

### 5. **(Opsional) Konfigurasi firewall (UFW)**

Kalau kamu pakai UFW (Uncomplicated Firewall), izinkan port 22:

```bash
sudo ufw allow ssh
sudo ufw reload
```

---

### 6. **Tes koneksi dari komputer lain**

Dari PC/laptop lain di jaringan yang sama:

```bash
ssh username@ip-server
```

Contoh:

```bash
ssh admin@192.168.1.100
```
