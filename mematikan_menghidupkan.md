Untuk mematikan Linux melalui **SSH**, caranya sederhana, asal kamu punya akses **root** atau pakai `sudo`. Berikut langkah-langkahnya:

1. **Matikan sistem**

   * Jika kamu login sebagai root:

     ```bash
     shutdown -h now
     ```

     atau

     ```bash
     poweroff
     ```

3. **Opsi menjadwalkan shutdown**

   * Shutdown setelah 10 menit:

     ```bash
     sudo shutdown -h +10
     ```
   * Shutdown pada jam tertentu (misalnya 23:00):

     ```bash
     sudo shutdown -h 23:00
     ```

4. **Restart Linux** (kalau mau reboot, bukan mati total):

   ```bash
   sudo reboot
   ```

