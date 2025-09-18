Ohh, paham 👍 Jadi di Debian kamu sudah install Samba, tapi ketika diakses dari Windows **yang muncul hanya printer share**, sementara folder share tidak terlihat. Ini biasanya masalah konfigurasi `smb.conf`.

---

## 🔎 Penyebab umum

1. **Folder belum dibuat atau belum diberi izin** → Windows hanya melihat share printer default.
2. **Konfigurasi share folder di `/etc/samba/smb.conf` belum ada / salah.**
3. **Hak akses user Samba tidak sesuai.**
4. **Samba perlu di-restart setelah edit config.**

---

## ✅ Solusi langkah demi langkah

### 1. Buat folder yang mau dishare

Misalnya folder `/srv/share`:

```bash
sudo mkdir -p /srv/share
sudo chmod -R 0777 /srv/share
```

*(biar gampang dulu, nanti bisa dipersempit permissionnya)*

---

### 2. Edit konfigurasi Samba

Buka file config:

```bash
sudo nano /etc/samba/smb.conf
```

Tambahkan di bagian bawah:

```ini
[SharedFolder]
   path = /srv/share
   browseable = yes
   writable = yes
   guest ok = yes
   create mask = 0777
   directory mask = 0777
```

> `[SharedFolder]` = nama yang akan tampil di Windows Explorer.

---

### 3. Cek konfigurasi Samba

```bash
testparm
```

Kalau ada error, perbaiki dulu.

---

### 4. Restart Samba

```bash
sudo systemctl restart smbd nmbd
```

---

### 5. Tambahkan user Samba (opsional, kalau mau pakai login)

```bash
sudo smbpasswd -a renders
```

---

### 6. Coba akses dari Windows

Di Windows Explorer:

```
\\192.168.10.250\SharedFolder
```

---

⚠️ Kalau masih **hanya printer yang muncul**, biasanya karena:

* Bagian `[printers]` dan `[print$]` di `smb.conf` aktif, tapi share folder belum terbaca.
* Firewall blokir port 445/139 (cek dengan `sudo ufw allow samba`).

---

Mau saya bikinkan **konfigurasi Samba minimal yang langsung work untuk folder share (tanpa printer sama sekali)** biar nggak bingung?
