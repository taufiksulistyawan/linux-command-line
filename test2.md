Nah, itu pesan dari **`nano` atau `vim`** waktu kamu buka `/etc/samba/smb.conf`.
Artinya ada **file swap/lock** yang tertinggal (`.smb.conf.swp`) → biasanya karena sebelumnya file itu sudah pernah dibuka tapi editor ditutup tidak normal (misalnya SSH mati mendadak).

Makanya muncul warning:

```
bad lock file is ignored /etc/samba/.smb.conf.swp
```

---

## 🔧 Cara mengatasinya

### 1. Cek dulu apakah ada proses editor yang masih buka file itu

```bash
ps aux | grep smb.conf
```

Kalau ada proses `nano` atau `vim`, matikan dulu:

```bash
kill -9 PID
```

*(ganti `PID` dengan angka yang muncul di kolom kedua)*

---

### 2. Hapus file swap yang tertinggal

```bash
sudo rm /etc/samba/.smb.conf.swp
```

---

### 3. Buka ulang konfigurasi

```bash
sudo nano /etc/samba/smb.conf
```

---

### 4. Setelah edit, selalu cek

```bash
testparm
```

Kalau tidak ada error → restart Samba:

```bash
sudo systemctl restart smbd nmbd
```

---

⚠️ Kalau kamu sempat edit pakai `vim`, kadang file `.swp` itu isinya backup perubahan. Kalau mau hati-hati sebelum hapus, bisa pindahkan dulu:

```bash
sudo mv /etc/samba/.smb.conf.swp /tmp/
```

---

Mau saya bikinkan **template smb.conf minimal** yang sudah bersih (tidak ada printer, hanya folder share), biar tinggal copy-paste tanpa takut ada sisa lock file?
