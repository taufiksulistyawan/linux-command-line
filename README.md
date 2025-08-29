# linux-command-line

Untuk melihat disk space di Linux, ada beberapa perintah yang biasa digunakan:

1. **Menampilkan ringkasan penggunaan disk (dengan ukuran human readable):**

```bash
df -h
```

👉 Menampilkan total, terpakai, dan sisa ruang disk per filesystem.

2. **Melihat ukuran folder/file dalam direktori saat ini:**

```bash
du -sh *
```

👉 Menampilkan ukuran setiap folder/file di direktori saat ini.

3. **Menampilkan total penggunaan direktori tertentu:**

```bash
du -sh /path/ke/direktori
```

4. **Menampilkan penggunaan disk dengan sort (butuh `ncdu` / `du`):**

```bash
ncdu /
```

👉 (jika `ncdu` sudah diinstall) tampilan interaktif untuk melihat apa yang paling banyak makan ruang.

---

Mau saya bikinkan daftar singkat + contoh output biar gampang dibaca?
