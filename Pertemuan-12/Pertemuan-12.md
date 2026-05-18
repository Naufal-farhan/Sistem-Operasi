<img width="1443" height="352" alt="image" src="https://github.com/user-attachments/assets/26223c8c-1314-4348-b33a-295e42a73a16" /># Pertemuan 12
## Latihan

### Latihan 10.1 Audit Layanan dan Analisis Boot
Lakukan audit menyeluruh terhadap layanan yang berjalan di sistem.
1. Jalankan systemctl list-units –type=service –state=running dan catat semua layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengan systemctl status, dan jelaskan fungsinya.
<img width="738" height="100" alt="image" src="https://github.com/user-attachments/assets/344dcfc6-6b3c-453f-be0d-cc8d3943a9b4" />
-bash (PID: 354)
Fungsi: Aplikasi shell interpreter yang berfungsi menerima, menerjemahkan, dan mengeksekusi perintah Linux yang diketik pengguna.

ps aux (PID: 10016)
Fungsinya: Utilitas instan yang berfungsi menangkap dan menampilkan cuplikan (snapshot) seluruh proses yang sedang berjalan saat itu juga.

2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head -5.

Hasil: Tidak dapat dianalisis karena perintah systemd-analyze blame tidak didukung
Alasan: Manajemen booting dan inisialisasi resource pada sistem kontainer dikendalikan langsung secara terpusat oleh server utama (host container).

3. Jalankan systemctl –failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal, cari tahu penyebabnya dengan journalctl -u nama-layanan -n 30.

Hasil: Tidak ada layanan lokal yang gagal (failed).
Alasan: Karena tidak ada background services mandiri yang berjalan di dalam kontainer klien, seluruh kestabilan proses diisolasi dan dijamin langsung oleh host Docker.

#### Latihan 10.2 Layanan Kustom dengan Restart Otomatis
Buat layanan systemd kustom yang mendemonstrasikan fitur restart otomatis.
1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk.sh yang setiap 30 detik menuliskan penggunaan disk ke berkas log. Gunakan df -h dan date.
<img width="885" height="439" alt="image" src="https://github.com/user-attachments/assets/2e75252d-3fa1-4460-bd8a-056ad18026ac" />

2. Buat berkas unit /etc/systemd/system/monitor-disk.service untuk menjalankan skrip tersebut dengan konfigurasi: Restart=always, RestartSec=5s, dan berjalan sebagai pengguna kamu sendiri.
<img width="1360" height="491" alt="image" src="https://github.com/user-attachments/assets/1f8bc4bc-dfbd-4072-b6fc-d4901505eca5" />

3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk ke journal.
<img width="1704" height="581" alt="image" src="https://github.com/user-attachments/assets/dcc1b67a-f543-476c-9283-9a81642fd664" />

4. Simulasikan crash dengan membunuh proses secara paksa (kill -9), tunggu 10 detik, dan verifikasi bahwa layanan hidup kembali secara otomatis.
<img width="1602" height="513" alt="image" src="https://github.com/user-attachments/assets/a7f8b77c-7aa4-4ec6-b2f9-855f032b8ea7" />

5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai.
<img width="1126" height="145" alt="image" src="https://github.com/user-attachments/assets/e250bcae-3608-4d27-a01a-967b2d65e84f" />

#### Latihan 10.3 Investigasi Log dan Keamanan SSH

Analisis log sistem dan tingkatkan keamanan konfigurasi SSH.

1. Gunakan journalctl -b -p err untuk menemukan semua error sejak boot terakhir. Simpan hasilnya ke berkas dan hitung jumlah baris dengan wc -l. 
<img width="927" height="114" alt="image" src="https://github.com/user-attachments/assets/94f5ba70-5b3e-4319-8fdc-226b3c95d7bb" />

2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd -t, reload.
<img width="1443" height="352" alt="image" src="https://github.com/user-attachments/assets/68620cf6-d94a-4a4a-9729-bfb74a6d531c" />


3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config).
<img width="1621" height="536" alt="image" src="https://github.com/user-attachments/assets/199b42f3-358a-4226-8ea9-4bc769de5887" />


4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup. 
<img width="900" height="200" alt="image" src="https://github.com/user-attachments/assets/3209c89e-1867-49fd-ad68-5585fe1c95ac" />
