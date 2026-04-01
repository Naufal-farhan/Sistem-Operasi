# Pertemuan-6

## Praktikum 6.1 — Melihat Proses dan Thread

### 1. Tampilkan semua proses yang berjalan:
### 2. Tampilkan proses beserta thread-nya, dapat dilihat pada kolom LWP (LightWeight Process ID):
### 3. Lihat PID shell aktif dan detail prosesnya:
### 4. Lihat hierarki proses secara visual:

<img width="1129" height="461" alt="image" src="https://github.com/user-attachments/assets/1a9f3e30-61c7-423f-9e85-a3f16ea18490" />


## Latihan 6.1
### Jalankan ps aux dan amati outputnya:<img width="957" height="114" alt="image" src="https://github.com/user-attachments/assets/d246dbf6-5bc9-46bf-91eb-ab50b63da66f" />

### 1. Berapa total proses yang berjalan? Proses apa yang memiliki PID terkecil?
  2 proses yang berjalan, proses yang memiliki PID terkecil adalah -bash
### 2. Jalankan pstree -p dan temukan proses bash Anda. Proses apa yang menjadi induk (PPID) dari bash tersebut?
  Proses yang menjadi induk (PPID) dari bash tersebut adalah proses dengan PID 484.
### 3. Bandingkan output ps aux dan ps aux -L. Apa perbedaan yang Anda lihat?
  Perbedaan utama antara ps aux dan ps aux -L terletak pada tingkat detail unit yang ditampilkan: apakah itu proses secara keseluruhan atau thread (utas) individu di dalam proses tersebut.

## Praktikum 6.2 — Mengamati Siklus Hidup Proses
### 1. Buat proses di background dan amati kondisinya:
### 2. Amati perubahan exit code dari perintah yang berhasil dan gagal:<img width="1212" height="520" alt="image" src="https://github.com/user-attachments/assets/dcd8db5b-d771-4be9-b6ca-5b36d9be36ce" />


## Latihan 6.2
### 1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?<img width="986" height="146" alt="image" src="https://github.com/user-attachments/assets/e520472c-89e7-493f-a279-db8bdfea03b8" />
Pada kolom STAT, proses sleep 120 (PID 17635) memiliki status: S
Karakter S dalam sistem operasi Linux berarti Interruptible Sleep (Menunggu suatu kejadian selesai).

### 2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exitcode masing-masing. Pola apa yang Anda temukan?
Berdasarkan percobaan di atas, pola yang ditemukan adalah:

1. Status 0: Digunakan oleh sistem untuk melaporkan bahwa perintah dieksekusi dengan sukses tanpa galat.

2. Status Bukan 0 (1-255): Digunakan untuk melaporkan kegagalan. Angka yang berbeda menunjukkan jenis kesalahan yang berbeda (misalnya 127 untuk perintah tidak ada, 2 untuk file tidak ada).

## Praktikum 6.3 — Mengatur Prioritas Proses
### 1. Jalankan proses dengan prioritas rendah: nice -n 10 sleep 300 &
### 2. Verifikasi nilai nice pada kolom NI: ps aux | grep sleep
### 3. Ubah nilai nice proses yang sudah berjalan: renice -n 15 -p <PID >ps -p <PID > -o pid , ni , cmd
### 4. Bersihkan proses percobaan: kill %1
<img width="1264" height="635" alt="image" src="https://github.com/user-attachments/assets/02fd378b-ec16-47db-804f-8cc493a8e4ad" />

## Latihan 6.3
### 1. Jalankan nice -n 5 sleep 200 & dan verifikasi nilai NI-nya dengan ps.<img width="1204" height="221" alt="image" src="https://github.com/user-attachments/assets/8ef4c56e-e679-432d-a5bd-1434fd9d693a" />

### 2. Ubah nilai nice menjadi 10 menggunakan renice, lalu verifikasi kembali<img width="1004" height="246" alt="image" src="https://github.com/user-attachments/assets/0e7a7103-e867-4ce1-ada9-0df91f44022c" /><img width="687" height="55" alt="image" src="https://github.com/user-attachments/assets/6680a223-3a6d-4865-a39c-63b59d090747" />

### 3. Coba ubah nilai nice menjadi -5 tanpa sudo. Apa yang terjadi? MengapaLinux membatasi hal ini untuk user biasa?
Muncul pesan kesalahan seperti: renice: failed to set priority for [PID]: Permission denied.
Mengapa Linux membatasi hal ini?
Linux membatasi penurunan nilai nice (meningkatkan prioritas) bagi user biasa karena alasan Keamanan dan Keadilan Sumber Daya

## Praktikum 6.4 — Mengirim Sinyal ke Proses
### 1. Buat proses percobaan:
sleep 500 &
sleep 600 &
sleep 700 &
ps aux | grep -v grep | grep sleep

### 2. Hentikan satu proses dengan SIGTERM dan verifikasi:
kill <PID - sleep -500 >
ps aux | grep -v grep | grep sleep
<img width="1009" height="555" alt="image" src="https://github.com/user-attachments/assets/a3b40c5b-5b73-4ab2-8115-027b87a15d37" />

### 3. Jeda dan lanjutkan proses dengan SIGSTOP/SIGCONT:
kill - SIGSTOP <PID - sleep -600 >
ps aux | grep sleep # amati kolom STAT : berubah menjadi T
kill - SIGCONT <PID - sleep -600 >
ps aux | grep sleep # STAT kembali ke S<img width="1388" height="493" alt="image" src="https://github.com/user-attachments/assets/4917451a-de0c-4956-8c93-0b15ae935da4" />


### 4. Hentikan semua proses sleep sekaligus:
pkill sleep
<img width="1073" height="219" alt="image" src="https://github.com/user-attachments/assets/e2247a84-7233-41dd-8d13-18bf6b99ce76" />

## Latihan 6.4
### 1. Jalankan sleep 400 &, kirim SIGSTOP, dan amati perubahan kolom STAT. Kondisi apa yang muncul? <img width="1187" height="232" alt="image" src="https://github.com/user-attachments/assets/8b93876d-81a8-46c4-ae67-83c529d60149" />
Kondisi yang muncul pada kolom STAT adalah T.
### 2. Kirim SIGCONT dan verifikasi proses kembali berjalan.
<img width="1206" height="124" alt="image" src="https://github.com/user-attachments/assets/ea218a29-7de4-4dac-9600-0fcd642549b6" />

### 3. Hentikan proses dengan SIGTERM lalu verifikasi sudah tidak ada. Kapan Anda memilih SIGKILL daripada SIGTERM?
<img width="1200" height="154" alt="image" src="https://github.com/user-attachments/assets/e6c7e6ce-44d7-4ffb-bf97-17652acc2971" />
SIGTERM adalah cara "sopan" yang memberi kesempatan proses untuk menyimpan data dan menutup file secara aman. Jika proses tersebut macet (freeze), tidak responsif, atau terus memakan sumber daya sistem meskipun sudah diminta berhenti, barulah gunakan SIGKILL untuk memaksa Kernel menghentikan proses tersebut seketika tanpa ampun.

## Praktikum 6.5 — Manajemen Job Foreground dan Background

### 1. Jalankan tiga job di background:
sleep 200 &
sleep 300 &
sleep 400 &
jobs
<img width="688" height="404" alt="image" src="https://github.com/user-attachments/assets/b4850361-3a45-4be7-a462-87533ece5040" />

### 2. Bawa job pertama ke foreground, jeda, lalu kembalikan ke background:
fg %1
# Tekan Ctrl +Z untuk menjeda
bg %1
jobs
<img width="633" height="357" alt="image" src="https://github.com/user-attachments/assets/1835833c-b96d-4502-b14e-9547536498b5" />

### 3. Hentikan semua job:
kill %1 %2 %3
jobs
<img width="564" height="194" alt="image" src="https://github.com/user-attachments/assets/2c66442a-55dc-4b62-866f-9412bcc6466f" />

## Latihan 6.5
### 1. Jalankan top di foreground. Apa yang terjadi di terminal?
<img width="1135" height="275" alt="image" src="https://github.com/user-attachments/assets/0009c190-e0bc-4fb2-9681-9d9c3853674a" />
Terminal akan terkunci/terambil alih sepenuhnya oleh antarmuka interaktif top. Anda akan melihat daftar proses sistem yang terus diperbarui secara real-time. Selama top berjalan di foreground, Anda tidak dapat mengetikkan perintah shell lain (seperti ls atau cd) karena shell sedang menunggu proses top selesai.

### 2. Tekan Ctrl+Z dan cek statusnya dengan jobs. Kondisi apa yang ditampilkan?
Kondisi yang ditampilkan adalah Stopped (atau Terhenti).

Penjelasan: Menekan Ctrl+Z tidak mematikan program, melainkan mengirim sinyal SIGSTOP yang menangguhkan proses tersebut dan mengembalikan kontrol terminal ke shell.

### 3. Pindahkan ke background dengan bg. Apakah top dapat berjalan denganbaik di background? Mengapa?<img width="397" height="105" alt="image" src="https://github.com/user-attachments/assets/34dbcc1d-1f3e-442c-9c2e-a95d3b20b8af" />
top tidak dapat berjalan dengan baik di background. Statusnya biasanya akan langsung kembali menjadi Stopped (tty input) atau Stopped (tty output).
Karena top adalah aplikasi interaktif yang membutuhkan akses langsung ke terminal (TTY) untuk menampilkan antarmuka visual dan menerima input keyboard dari pengguna. Linux melarang proses di background untuk membaca input dari terminal atau menulis secara bebas ke layar yang sedang digunakan oleh shell aktif. Jika dipaksa ke background, sistem akan menghentikannya demi keamanan dan kerapihan tampilan.

### 4. Kembalikan ke foreground dengan fg, lalu keluar dengan q .<img width="1231" height="827" alt="image" src="https://github.com/user-attachments/assets/385abf16-30af-4a1e-a8e6-ca2091496d69" />

## Praktikum 6.6 — Pemantauan Proses

### 1. Temukan proses dengan penggunaan CPU dan memori tertinggi:
ps aux -- sort = -% cpu | head -10
ps aux -- sort = -% mem | head -10
<img width="1164" height="367" alt="image" src="https://github.com/user-attachments/assets/0d0cda50-9336-4af9-b970-33fa9cb30f15" />

### 2. Jalankan top dan eksplorasi shortcut-nya:
top
#Tekan M, P, 1 , u secara bergantian
#Tekan q untuk keluar
<img width="1382" height="349" alt="image" src="https://github.com/user-attachments/assets/14d57e88-726d-45fc-9926-42860348a417" />

### 3. Instal dan jalankan htop:
sudo apt install -y htop
htop
#Tekan F6 untuk pilih kolom pengurutan
#Tekan F10 atau q untuk keluar
<img width="1422" height="842" alt="image" src="https://github.com/user-attachments/assets/47ec4f55-5331-43a9-81fb-4208a56bd738" />

## Latihan 6.6
### 1. Gunakan ps aux –sort=%mem untuk menemukan proses yang menggunakan memori paling banyak di VM Anda. Proses apa itu?
<img width="1119" height="182" alt="image" src="https://github.com/user-attachments/assets/e9fa1c17-cfed-45c9-a43c-8f743feecfcc" />
proses top adalah yang paling banyak menggunakan banyak memori

### 2. Di dalam top, tekan 1 . Apa yang berubah pada tampilan? Mengapa informasi ini berguna?
Perubahan: Tampilan baris statistik CPU di bagian atas akan terpecah (expand). Jika sebelumnya hanya muncul satu baris p%Cpu(s), setelah menekan 1, akan muncul rincian untuk setiap core CPU secara individu (%Cpu0, %Cpu1, dst).

Mengapa berguna?
Deteksi Ketimpangan Beban: Anda bisa melihat apakah beban kerja terdistribusi merata ke semua core atau hanya menumpuk di satu core saja (single-thread bottleneck).

### 3. Di dalam htop, navigasikan ke proses sshd menggunakan tombol panah. Tekan F9 dan amati opsi sinyal yang tersedia.
<img width="1354" height="622" alt="image" src="https://github.com/user-attachments/assets/a664add5-209a-4a43-bfd9-504869fb85a7" />

## 1.8 Latihan
## Latihan 6.A Eksplorasi Proses Sistem
### 1. Jalankan ps aux –forest dan temukan proses dengan PID 1. Apa nama dan fungsi proses tersebut dalam sistem Linux modern?<img width="1168" height="160" alt="image" src="https://github.com/user-attachments/assets/01ec973c-2518-47d7-964e-7f1deec85d7c" />
Jika Anda menjalankan ps aux --forest, proses dengan PID 1 biasanya bernama systemd (pada Ubuntu dan mayoritas distro Linux modern) atau /sbin/init (pada sistem lama).

Fungsi Proses Tersebut:

Parent of All Processes: Ia adalah proses pertama yang dijalankan oleh Kernel saat booting. Semua proses lain di sistem adalah "anak" atau keturunan dari proses ini.

## 2. Hitung berapa proses yang dimiliki oleh user root dan berapa yang dimiliki oleh user Anda. Mengapa root memiliki lebih banyak proses?<img width="752" height="129" alt="image" src="https://github.com/user-attachments/assets/495aa737-bb76-4d8b-8083-4222bd67b415" />
Root memiliki lebih banyak proses karena ia bertanggung jawab atas seluruh infrastruktur sistem operasi.

## 3. Temukan semua proses yang berada dalam kondisi S. Mengapa sebagian besar proses di sistem berada dalam kondisi ini?<img width="1066" height="108" alt="image" src="https://github.com/user-attachments/assets/816b85fb-71ca-439c-8b5e-95407fbaff53" />
Mayoritas proses berada dalam kondisi S (Sleep) karena alasan efisiensi sumber daya


## Latihan 6.B Simulasi Manajemen Job
### 1. Jalankan tiga perintah sleep dengan durasi 100, 200, dan 300 detik di background. Verifikasi ketiganya dengan jobs.
<img width="731" height="410" alt="image" src="https://github.com/user-attachments/assets/1088789b-bd97-46b8-a160-6d4faba7c8ef" />

### 2. Bawa job kedua ke foreground, jeda dengan Ctrl+Z , lalu kembalikanke background dengan bg.
<img width="718" height="325" alt="image" src="https://github.com/user-attachments/assets/6e50a3d9-0e73-44b1-a640-59107b14b6fb" />

### 3. Hentikan job pertama dengan kill %1. Tampilkan kembali daftar job.Berapa job yang tersisa?
<img width="716" height="263" alt="image" src="https://github.com/user-attachments/assets/13e96e46-79a1-4386-bf7d-ccf17201408a" />


## Latihan 6.C Prioritas dan Sinyal
### 1. Jalankan dua proses sleep: satu dengan nice +5 dan satu dengan nice +15. Verifikasi nilai NI keduanya dengan ps.
<img width="979" height="317" alt="image" src="https://github.com/user-attachments/assets/3dad1981-21b7-4af3-a3d8-decacccb344f" />

### 2. Gunakan renice untuk mengubah nice proses pertama menjadi +10.Proses mana yang kini lebih diprioritaskan scheduler?
<img width="714" height="59" alt="image" src="https://github.com/user-attachments/assets/8dd1a303-73ca-41b9-92af-5a408f836460" />

### 3. Kirim SIGSTOP ke salah satu proses, verifikasi kondisi T-nya, lalu kirimSIGCONT. Akhiri semua proses percobaan dengan pkill sleep
<img width="607" height="96" alt="image" src="https://github.com/user-attachments/assets/827a00a9-e69a-4ae3-ab38-57098ddb4964" />
<img width="1227" height="108" alt="image" src="https://github.com/user-attachments/assets/e20b93df-c1f4-4f4c-9ac4-1304f4aab9af" />

