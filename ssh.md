Kalau Debian kamu **gagal konek SSH**, biasanya ada beberapa penyebab umum: service SSH belum aktif, firewall blok port 22, atau server pakai port lain. Berikut langkah detail untuk mengatasinya:

---

## ✅ 1. Pastikan paket OpenSSH sudah terinstal

Masuk langsung ke server (pakai monitor/console/Proxmox/VM console), lalu cek:

```bash
dpkg -l | grep openssh-server
```

Kalau kosong, berarti belum ada. Install dengan:

```bash
sudo apt update
sudo apt install openssh-server -y
```

---

## ✅ 2. Cek status service SSH

```bash
sudo systemctl status ssh
```

atau

```bash
sudo systemctl status sshd
```

* Kalau `inactive` → jalankan:

  ```bash
  sudo systemctl start ssh
  sudo systemctl enable ssh
  ```

---

## ✅ 3. Cek port SSH

Pastikan service benar-benar buka port 22:

```bash
ss -tulnp | grep ssh
```

Kalau portnya bukan 22, lihat konfigurasi:

```bash
sudo nano /etc/ssh/sshd_config
```

Cari baris:

```
Port 22
```

Kalau misalnya diubah jadi `2222`, login pakai:

```bash
ssh -p 2222 user@ip_server
```

---

## ✅ 4. Cek firewall

Kalau pakai **ufw**:

```bash
sudo ufw status
```

Tambahkan rule kalau perlu:

```bash
sudo ufw allow 22/tcp
```

Kalau pakai **firewalld**:

```bash
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --reload
```

---

## ✅ 5. Cek IP dan jaringan

Dari client (misalnya laptop/PC), pastikan IP server bisa diakses:

```bash
ping 192.168.x.x
```

Kalau gagal ping → masalahnya di jaringan, bukan SSH.

---

## ✅ 6. Restart service SSH setelah perubahan

```bash
sudo systemctl restart ssh
```

---

⚡ Ringkasan:

1. Install `openssh-server`
2. Pastikan service `ssh` aktif
3. Pastikan port 22 terbuka (atau sesuaikan dengan konfigurasi)
4. Buka firewall untuk port tersebut
5. Tes koneksi lagi dari client

---

Mau saya bikinkan **script otomatis** untuk pengecekan & perbaikan SSH di Debian (biar tinggal copy-paste satu kali jalan)?
