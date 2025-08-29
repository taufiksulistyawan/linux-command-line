# linux-command-line

Untuk melihat disk space di Linux, ada beberapa perintah yang biasa digunakan:

1. **Menampilkan ringkasan penggunaan disk (dengan ukuran human readable):**

```bash
df -h
```

👉 Menampilkan total, terpakai, dan sisa ruang disk per filesystem.

2. **Menampilkan total penggunaan direktori tertentu:**

```bash
du -sh /path/ke/direktori
```

3. **Membersihkan APT cache (Debian/Ubuntu & turunannya)**

```bash
sudo apt-get clean
sudo apt-get autoclean
```

* `clean` → hapus semua file .deb di cache
* `autoclean` → hapus hanya paket usang

---

4. **Membersihkan Thumbnail Cache (desktop Linux seperti Ubuntu, Mint, dll)**

```bash
rm -rf ~/.cache/thumbnails/*
```
