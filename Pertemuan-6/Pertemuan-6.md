# Pertemuan-6

## Praktikum 6.1 — Melihat Proses dan Thread

### 1. Tampilkan semua proses yang berjalan:
### 2. Tampilkan proses beserta thread-nya, dapat dilihat pada kolom LWP (LightWeight Process ID):
### 3. Lihat PID shell aktif dan detail prosesnya:
### 4. Lihat hierarki proses secara visual:

<img width="1129" height="461" alt="image" src="https://github.com/user-attachments/assets/1a9f3e30-61c7-423f-9e85-a3f16ea18490" />


### Latihan 6.1
### Jalankan ps aux dan amati outputnya:<img width="957" height="114" alt="image" src="https://github.com/user-attachments/assets/d246dbf6-5bc9-46bf-91eb-ab50b63da66f" />

### 1. Berapa total proses yang berjalan? Proses apa yang memiliki PID terkecil?
  2 proses yang berjalan, proses yang memiliki PID terkecil adalah -bash
### 2. Jalankan pstree -p dan temukan proses bash Anda. Proses apa yang menjadi induk (PPID) dari bash tersebut?
### 3. Bandingkan output ps aux dan ps aux -L. Apa perbedaan yang Anda lihat?
  Perbedaan utama antara ps aux dan ps aux -L terletak pada tingkat detail unit yang ditampilkan: apakah itu proses secara keseluruhan atau thread (utas) individu di dalam proses tersebut.
