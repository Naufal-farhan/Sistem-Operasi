# Pertemuan 12
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
