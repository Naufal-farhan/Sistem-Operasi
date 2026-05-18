# Pertemuan 10

## Latihan Praktikum

### Tugas 10.1 Audit Penggunaan Memori Sistem
<img width="1517" height="829" alt="image" src="https://github.com/user-attachments/assets/78afbaec-1f50-47be-8308-fcfa9cc3faaf" />
<img width="902" height="732" alt="image" src="https://github.com/user-attachments/assets/e462436c-83f6-4b76-817e-2bc6d17deccf" />

#### 1. Hitung persentase memori tersedia (available / total × 100%). Apakah sistem dalam kondisi normal?
Available (Tersedia): 1.2G
Total: 3.8G
Kesimpulan: > Ya, sistem masih dalam kondisi normal. Meskipun memori yang benar-benar kosong (free) hanya 1.1G, kapasitas siap pakai (available) bagi aplikasi baru masih berada di angka 31.58%.

#### 2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut pandang ketersediaan untuk aplikasi?
Dari sudut pandang ketersediaan aplikasi, buff/cache tidak dianggap sebagai memori yang hilang atau terpakai habis.

Alasannya: Buff/cache adalah memori RAM yang digunakan oleh kernel Linux secara sementara untuk menyimpan data buatan (buffer) atau salinan file dari harddisk (cache) agar akses sistem lebih cepat.

#### 3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai SwapFree? 
SwapTotal: 0 kB
SwapFree: 0 kB

Jawaban:
Apakah SwapTotal lebih besar dari 0? Tidak, nilainya adalah 0 kB.
Berapa nilai SwapFree? Nilainya adalah 0 kB.

### Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi
<img width="982" height="192" alt="image" src="https://github.com/user-attachments/assets/1bccb4bf-0f13-434d-b35b-075dd9b2a1e8" />

#### Analisis
#### 1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
Nama Proses (COMMAND): ps aux --sort=-%mem
Nilai %MEM: 0.0%
Nilai RSS (Resident Set Size): 3892KB

#### 2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
Nilai RSS yang tertera adalah 3892 KB. kita konversikan ke MB dengan membaginya dengan 1024 = 3.80MB
Apakah wajar?
Sangat wajar. Angka 3.8 MB itu sangat kecil untuk ukuran sebuah program. Hal ini karena proses ps aux hanyalah sebuah utilitas terminal berbasis teks (CLI utility) yang bertugas mengambil cuplikan info proses lalu langsung selesai bekerja, sehingga tidak membutuhkan alokasi memori RAM yang besar.

#### 3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka gunakan bersama?
Data dari kolom %MEM:
Proses 1 (ps aux): 0.0%
Proses 2 (-bash): 0.0%
Proses 3 (head -n 11): 0.0%

Jumlah total = 0.0%

Jawaban:
Total RAM yang mereka gunakan bersama adalah 0.0% (atau mendekati 0%). Di web terminal, lingkungan sistemnya dibuat sangat minimalis. Karena semua proses tersebut menggunakan memori yang sangat sedikit di bawah tingkat presisi 1 desimal, pembulatannya terbaca sebagai 0.0% pada kolom %MEM.

### Tugas 10.3 Membuat dan Memverifikasi Swap File
<img width="987" height="187" alt="image" src="https://github.com/user-attachments/assets/6d8455ca-d89c-4511-b647-c85451b6123e" />

### Tugas 10.5 Studi Kasus Diagnosa Server Lambat
<img width="967" height="593" alt="image" src="https://github.com/user-attachments/assets/105c40a0-ad29-4bc1-bc11-9ab2850c144a" />

#### Analisis
#### 1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses, cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi terpisah?
cek_memori: Memantau kapasitas RAM dan memberi peringatan jika sisa memori < 20%.
cek_swap: Memeriksa ketersediaan dan penggunaan memori cadangan (Swap).
cek_proses: Mengidentifikasi 10 proses yang paling banyak mengonsumsi RAM.
cek_paging: Memantau aktivitas transfer data (paging) antara RAM dan disk.
ringkasan: Menyimpulkan status akhir sistem (normal/kritis) secara cepat.
Alasan dipecah: Agar kode lebih terstruktur, mudah dirawat (maintain), dan fungsi-fungsinya bisa digunakan kembali (reusable) tanpa menulis ulang.

#### 2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis? Jelaskan berdasarkan nilai threshold yang digunakan script.
Kondisi sistem adalah Normal. Script menggunakan threshold batas aman memori tersedia sebesar 20%. Berdasarkan data terminal, sisa memori RAM kamu masih berada di angka 31% (1.19 GB dari total 3.8 GB), sehingga belum menyentuh batas kritis.

#### 3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa > "$LAPORAN"? Apa keuntungannya?
Redirection (>): Hanya menyimpan output ke file teks, layar terminal akan kosong saat script berjalan.

tee: Membagi aliran output sehingga muncul di layar terminal secara real-time sekaligus tersimpan ke dalam file dalam satu waktu. Keuntungannya, kamu bisa langsung melihat hasil diagnosa tanpa perlu mengetik perintah cat.

#### 4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa implikasinya terhadap performa server?
Hasil: Nilai si (swap-in) dan so (swap-out) pada output adalah 0.

Implikasi: Performa server sangat baik dan responsif. Angka 0 menandakan RAM fisik masih longgar, sehingga sistem tidak perlu melakukan paging (tukar data) ke disk yang berpotensi membuat server lambat (thrashing).
