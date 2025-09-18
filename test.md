Mantap 👍 saya bikinkan checklist step-by-step untuk **recover Debian biar SSH + Samba langsung normal lagi**. Tinggal copy-paste di console server:

---

## 🛠️ Checklist Recovery SSH + Samba

### 1. Pastikan paket SSH & Samba sudah terinstall

```bash
sudo apt update
sudo apt install openssh-server samba -y
```

---

### 2. Hidupkan service SSH

```bash
sudo systemctl enable ssh --now
sudo systemctl status ssh
```

---

### 3. Hidupkan service Samba

```bash
sudo systemctl enable smbd nmbd --now
sudo systemctl status smbd
sudo systemctl status nmbd
```

---

### 4. Cek konfigurasi Samba

```bash
testparm
```

Kalau `[SharedFolder]` atau folder yang kamu share hilang → tambahkan ulang di bawah `/etc/samba/smb.conf`:

```ini
[SharedFolder]
   path = /srv/share
   browseable = yes
   writable = yes
   guest ok = yes
   create mask = 0777
   directory mask = 0777
```

Lalu buat folder & kasih izin:

```bash
sudo mkdir -p /srv/share
sudo chmod -R 0777 /srv/share
```

Restart Samba:

```bash
sudo systemctl restart smbd nmbd
```

---

### 5. Cek firewall (kalau aktif)

```bash
sudo ufw allow 22/tcp
sudo ufw allow samba
sudo ufw reload
```

---

### 6. Cek IP server

```bash
ip a
```

Gunakan IP itu untuk akses:

* SSH → `ssh user@IP_SERVER`
* Samba → `\\IP_SERVER\SharedFolder` (di Windows Explorer)

---

⚡ Dengan checklist ini, biasanya Debian langsung balik normal: **SSH bisa konek lagi** dan **folder sharing muncul di Windows**.

---

Mau saya bikinkan juga **script `.sh` otomatis** (tinggal sekali jalan, semua step di atas langsung dieksekusi)?
