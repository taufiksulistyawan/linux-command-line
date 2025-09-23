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

Perintah Hapus Folder:

```bash
rm -rf /srv/render_backup/Aditya
```

* `-r` → recursive, hapus semua isi di dalam folder
* `-f` → force, supaya tidak tanya konfirmasi

Untuk cek ukuran folder, kamu bisa pakai perintah `du` (disk usage). Contohnya:

1. **Melihat ukuran masing-masing subfolder**

   ```bash
   du -sh /srv/render_backup/*
   ```

   * `-s` = summary (hanya total per folder)
   * `-h` = human readable (KB, MB, GB)

   Contoh output:

   ```
   1.2G   /srv/render_backup/proyek1
   5.6G   /srv/render_backup/proyek2
   800M   /srv/render_backup/proyek3
   ```

2. **Melihat total ukuran folder `/srv/render_backup`**

   ```bash
   du -sh /srv/render_backup
   ```

3. **Jika ingin urutkan dari yang paling besar**

   ```bash
   du -sh /srv/render_backup/* | sort -h
   ```
