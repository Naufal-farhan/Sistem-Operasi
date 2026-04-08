# Praktikum 6

## Praktikum 6.1 — Mengenali Bash dan Menyiapkan Workspace

### 1. Lihat shell login dan shell aktif saat ini:
echo " Shell login : $SHELL "
echo " Shell aktif : $0"
bash --version | head -n 1
<img width="823" height="280" alt="image" src="https://github.com/user-attachments/assets/9b4d66a1-5642-46d2-a766-540896aa9775" />

### 2. Lihat proses shell yang sedang berjalan:
echo $$
ps -p $$ -o pid , ppid , args =
<img width="751" height="401" alt="image" src="https://github.com/user-attachments/assets/be4c84cd-4895-4a13-a90a-2766cea38b94" />


### 3. Buat workspace praktikum:
mkdir -p ~/ praktikum - os / week07 - bash /{ bin , backup , logs ,
sampel , ruang - nama }
cd ~/ praktikum - os / week04 - bash
pwd

### 4. Buat beberapa file contoh yang akan dipakai pada praktikum berikutnya:
touch sample - app . conf
touch logs / app -01. log logs / app -02. log logs / app -03. log
touch sampel / catatan - a . txt sampel / catatan - b . txt
touch sampel / backup -01. tar sampel / backup -02. tar
touch sampel / laporan - harian . log sampel / laporan -
mingguan . log sampel / laporan - bulanan . log
touch "ruang - nama / laporan server april .txt"
touch "ruang - nama / backup [ mingguan ] server . conf "
ls -R
<img width="1344" height="772" alt="image" src="https://github.com/user-attachments/assets/e333ac8a-4a58-457c-b8c5-27506731a7f2" />


## Praktikum 6.2 — Membuat Ringkasan Sesi Terminal

### 1. Masuk ke workspace praktikum:
cd ~/ praktikum - os / week04 - bash
<img width="499" height="44" alt="image" src="https://github.com/user-attachments/assets/b91ec102-6394-4d6f-9cf1-768be76aec6b" />

### 2. Simpan informasi sesi terminal ke file laporan:
{
echo "=== RINGKASAN SESI BASH ==="
date
echo " User : $( whoami )"
echo " Hostname : $( hostname )"
echo " Shell login : $SHELL "
echo " Shell aktif : $0"
echo "PID shell : $$"
echo " Direktori : $(pwd)"
} | tee session - info . txt
<img width="849" height="781" alt="image" src="https://github.com/user-attachments/assets/448c84d8-abc5-4c58-8e8b-86f0df327f99" />


### 3. Verifikasi isi file laporan:
cat session - info . txt
<img width="647" height="236" alt="image" src="https://github.com/user-attachments/assets/2e69c710-6692-4e37-9024-ac17dc3beb2f" />


## Praktikum 6.3 — Menambahkan Konfigurasi Aman pada .bashrc

### 1. Lihat file konfigurasi Bash pada home directory:
ls - la ~ | grep -E 'bashrc | bash_profile | profile '
<img width="978" height="95" alt="image" src="https://github.com/user-attachments/assets/ff2c8652-9334-4ded-928d-05048b102686" />


### 2. Buat backup .bashrc:
cp ~/. bashrc ~/. bashrc . bak - praktikum
<img width="825" height="29" alt="image" src="https://github.com/user-attachments/assets/80c530ba-8e9a-4cd7-a5a7-ff0d1f704bb2" />

### 3. Tambahkan blok konfigurasi praktikum:
cat <<'EOF ' >> ~/.bashrc
# --- Praktikum Bash Shell ---
export PRAKTIKUM_BASH_DIR =" $HOME / praktikum -os/week04 -
bash "
export EDITOR = nano
# --- End Praktikum Bash Shell ---
EOF
<img width="913" height="267" alt="image" src="https://github.com/user-attachments/assets/7c64bc08-d112-4191-90bc-0046196d26de" />

### 4. Terapkan konfigurasi tanpa logout:
source ~/.bashrc
echo " $PRAKTIKUM_BASH_DIR "
echo " $EDITOR "
<img width="712" height="87" alt="image" src="https://github.com/user-attachments/assets/19d8f011-749b-4b80-953e-bd280dd9c054" />

## Praktikum 6.4 — Menyiapkan .bash_profile untuk Shell Login

### 1. Backup .bash_profile jika sudah ada:
[ -f ~/. bash_profile ] && cp ~/. bash_profile ~/.
bash_profile . bak - praktikum
<img width="1314" height="47" alt="image" src="https://github.com/user-attachments/assets/d7995832-fd7b-4432-8ed2-486ae00c82de" />

### 2. Tambahkan konfigurasi login shell:
cat <<'EOF ' >> ~/. bash_profile
# --- Praktikum Bash Login Shell ---
if [ -f ~/. bashrc ]; then
. ~/. bashrc
fi
echo " Login Bash pada $( date '+%F %T ')" >> " $HOME /
praktikum -os/week07 - bash /login - audit .log"
# --- End Praktikum Bash Login Shell ---
EOF
<img width="1282" height="324" alt="image" src="https://github.com/user-attachments/assets/43e88c83-c0ba-482b-b8d3-ade745c1dba9" />

### 3. Uji dengan membuka login shell baru:
bash -l
tail -n 3 ~/ praktikum - os / week07 - bash / login - audit . log
exit
<img width="1086" height="226" alt="image" src="https://github.com/user-attachments/assets/7501d6d1-4413-4eee-a378-95d60d076a64" />

## Praktikum 6.5 — Membedakan Variabel Shell dan Environment Variable

### 1. Buat variabel lokal:
KELAS_OS =" Sistem Operasi A"
echo " $KELAS_OS "
<img width="923" height="144" alt="image" src="https://github.com/user-attachments/assets/95af12f1-8bd2-4ca1-8ab6-21210d216db6" />

### 2. Buka subshell dan cek apakah variabel masih ada:
bash
echo " $KELAS_OS "
exit
<img width="769" height="215" alt="image" src="https://github.com/user-attachments/assets/accdcfe4-48fe-4b93-88d6-088e63e187e8" />

### 3. Sekarang ubah menjadi environment variable:
export KELAS_OS =" Sistem Operasi A"
bash
echo " $KELAS_OS "
exit
<img width="817" height="252" alt="image" src="https://github.com/user-attachments/assets/c6d3786b-e675-4d17-a8df-fe7a48fe6f52" />

### 4. Lihat isi PATH dan lokasi beberapa perintah:
echo " $PATH "
which bash
type ls
<img width="1352" height="265" alt="image" src="https://github.com/user-attachments/assets/043b62e2-1752-45c7-9c5c-ed41a2aef2ed" />

## Praktikum 6.6 — Menambahkan Direktori Script Pribadi ke PATH

### 1. Pastikan direktori bin praktikum tersedia:
mkdir -p ~/ praktikum - os / week07 - bash / bin
<img width="736" height="45" alt="image" src="https://github.com/user-attachments/assets/f7bcbe87-3e7b-4b6e-97d2-e55fded7a8a7" />

### 2. Tambahkan direktori tersebut ke PATH melalui .bashrc:
cat <<'EOF ' >> ~/. bashrc
# --- Praktikum PATH ---
export PATH =" $HOME / praktikum -os/week07 - bash /bin : $PATH "
# --- End Praktikum PATH ---
EOF
source ~/. bashrc
echo " $PATH "
<img width="1348" height="636" alt="image" src="https://github.com/user-attachments/assets/699d676e-e4bf-4ecf-a9b1-a77e6d975812" />

### 3. Buat script ringkasan sistem:
cat <<'EOF ' > ~/ praktikum - os / week07 - bash / bin / ringkas -
sistem
#!/ usr/bin/env bash
echo " Hostname : $( hostname )"
echo " User : $( whoami )"
echo " Uptime : $( uptime -p)"
echo " Disk / :"
df -h /
EOF
chmod + x ~/ praktikum - os / week07 - bash / bin / ringkas - sistem
<img width="1123" height="640" alt="image" src="https://github.com/user-attachments/assets/b1860cb4-f457-4b96-8ffc-73aa9b077ad2" />

### 4. Jalankan script dari direktori yang berbeda:
cd ~
ringkas - sistem
<img width="1131" height="136" alt="image" src="https://github.com/user-attachments/assets/0d71b0d9-828a-4bef-8b64-d405528d0de2" />

## Praktikum 6.7 — Membuat Alias Produktivitas Dasar

### 1. Tambahkan alias ke .bashrc:
cat <<'EOF ' >> ~/. bashrc
# --- Praktikum Alias ---
alias ll ='ls -lah --color = auto '
alias hist10 ='history | tail -n 10 '
alias cdbashlab ='cd $HOME / praktikum -os/week04 - bash '
# --- End Praktikum Alias ---
EOF
source ~/. bashrc
<img width="997" height="691" alt="image" src="https://github.com/user-attachments/assets/83bb2a64-e685-421f-bc24-a34c27cfc618" />

### 2. Uji alias:
ll
hist10
cdbashlab
pwd
type ll
<img width="1061" height="747" alt="image" src="https://github.com/user-attachments/assets/cbf8ecf6-a13a-4fa7-969d-47c00a159672" />

 ## Praktikum 6.8 — Membuat Fungsi Backup Konfigurasi
 ### 1. Siapkan file konfigurasi contoh:
echo " PORT =8080 " > ~/ praktikum - os / week07 - bash / sample -
app . conf
cat ~/ praktikum - os / week07 - bash / sample - app . conf
<img width="1185" height="123" alt="image" src="https://github.com/user-attachments/assets/102ae786-adf5-4da2-a7a8-cca585b0612b" />

 ### 2. Tambahkan fungsi ke .bashrc:
cat <<'EOF ' >> ~/. bashrc
# --- Praktikum Fungsi Shell ---
backup_conf () {
if [ $# -ne 1 ]; then
echo " Usage : backup_conf <file >"
return 1
fi
local src ="$1"
local dst =" $HOME / praktikum -os/week07 - bash / backup "
if [ ! -f " $src " ]; then
echo " File tidak ditemukan : $src "
return 2
fi
mkdir -p " $dst "
cp -- " $src " " $dst /$( basename " $src ").$( date +%F -%H%
M%S).bak"
echo " Backup selesai di $dst "
}
# --- End Praktikum Fungsi Shell ---
EOF
source ~/. bashrc
<img width="1072" height="751" alt="image" src="https://github.com/user-attachments/assets/c88ebb91-d59c-4029-aeed-9dab92995908" />

 ### 3. Uji fungsi:
backup_conf ~/ praktikum - os / week07 - bash / sample - app . conf
ls - lah ~/ praktikum - os / week07 - bash / backup
type backup_conf
<img width="1050" height="736" alt="image" src="https://github.com/user-attachments/assets/f2d97b21-c5ba-4d09-8ff5-4f42be35b8f5" />

## Praktikum 6.9 — Menggunakan Completion Dasar dan Melihat History
### 1. Pastikan file contoh tersedia:
cd ~/ praktikum - os / week07 - bash / sampel
touch laporan - harian . log laporan - mingguan . log laporan -
bulanan . log
ls
<img width="1234" height="185" alt="image" src="https://github.com/user-attachments/assets/3bcf33cd-d3e2-402d-bc95-ae6344d6ec06" />

### 2. Uji completion file:
a) Ketik cat lap lalu tekan Tab dua kali.
b) Amati daftar file yang memiliki prefix lap.
c) Ketik lebih spesifik, misalnya cat laporan-h lalu tekan Tab.
<img width="891" height="766" alt="image" src="https://github.com/user-attachments/assets/3220d964-8911-4cf3-90e8-671560862642" />
<img width="897" height="598" alt="image" src="https://github.com/user-attachments/assets/864e4e31-956a-4bd5-9f94-76a82f8fb7b6" />

### 3. Jalankan beberapa perintah sederhana:
pwd
ls - lah
date
whoami
history | tail -n 10
<img width="963" height="684" alt="image" src="https://github.com/user-attachments/assets/2de74684-75a3-467b-8266-254312cd9680" />

## Praktikum 6.10 — Menelusuri Perintah Diagnostik dengan History
### 1. Jalankan beberapa perintah diagnostik:
df -h
free -h
uptime
ps aux | head
<img width="1075" height="584" alt="image" src="https://github.com/user-attachments/assets/1bb15b09-7d0d-49cb-a6e0-29a7e58650d5" />

### 2. Cari ulang perintah diagnostik dari history:
history | grep -E 'df -h| free -h| uptime |ps aux '
<img width="1001" height="712" alt="image" src="https://github.com/user-attachments/assets/cfc80ab2-91ff-4f06-9727-a62b327db7d3" />

### 3. Jalankan ulang salah satu perintah berdasarkan nomor history:
! < NOMOR_HISTORY_ANDA >
<img width="1072" height="156" alt="image" src="https://github.com/user-attachments/assets/c987dc82-08fb-4821-9642-4f39d07c8530" />

### 4. Simpan potongan history ke file dokumentasi:
history | tail -n 20 > ~/ praktikum - os / week07 - bash / diag
- history . txt
cat ~/ praktikum - os / week07 - bash / diag - history . txt
<img width="1249" height="706" alt="image" src="https://github.com/user-attachments/assets/6db9c40f-0545-4479-93ee-1310fe6d3a9d" />

## Praktikum 6.11 — Mencoba Wildcard Dasar
### 1. Masuk ke direktori sampel:
cd ~/ praktikum - os / week07 - bash / sampel
ls

### 2. Coba beberapa pola wildcard:
ls *. log
ls catatan -?. txt
ls backup -0[12]. tar

### 3. Coba beberapa ekspansi lain:
echo log -{ pagi , siang , malam }. txt
echo ~
echo ~/ praktikum - os / week04 - bash
<img width="1179" height="485" alt="image" src="https://github.com/user-attachments/assets/963427a3-ab87-439b-8b50-65ff54ac96b9" />
(no 1-3)

## Praktikum 6.12 — Mengarsipkan Banyak Log Sekaligus
###  1. Siapkan file log tambahan:
cd ~/ praktikum - os / week07 - bash / logs
touch access -01. log access -02. log access -03. log
ls
<img width="986" height="148" alt="image" src="https://github.com/user-attachments/assets/81d50eb8-e89e-4ab7-a69d-66bcb8a0a351" />

###  2. Preview file yang akan diproses:
echo *. log
echo access -0?. log
<img width="786" height="111" alt="image" src="https://github.com/user-attachments/assets/fd063787-ab5e-4fe4-8a33-9bb20f6aef39" />

###  3. Pindahkan semua file log ke folder arsip:
mkdir -p arsip - log
mv *. log arsip - log /
ls arsip - log
<img width="681" height="118" alt="image" src="https://github.com/user-attachments/assets/b3260ab0-7f0e-4f68-888e-fa51a452ba15" />

###  4. Kompres folder arsip:
tar - czf arsip - log - $ ( date +% F ) . tar . gz arsip - log
ls - lah
<img width="1079" height="224" alt="image" src="https://github.com/user-attachments/assets/16b8d91c-4fb7-4071-b754-7536b78659cc" />

## Praktikum 6.13 — Membedakan Single Quote, Double Quote, dan Escape
### 1. Uji single quote dan double quote:
echo '$USER bekerja di $HOME '
echo " $USER bekerja di $HOME "

### 2. Uji escape karakter spasi:
cd ~/ praktikum - os / week07 - bash / ruang - nama
ls laporan \ server \ april . txt

### 3. Uji akses file yang sama dengan double quote:
cat " laporan server april .txt"

<img width="941" height="276" alt="image" src="https://github.com/user-attachments/assets/d95bb041-2a7d-44e2-ad0d-8c423a8f9b62" />
(no 1-3)

## Praktikum 6.14 — Menangani File dengan Nama Sulit Secara Aman

### 1. Pastikan file target tersedia:
cd ~/ praktikum - os / week07 - bash / ruang - nama
ls - lah

### 2. Salin file dengan nama kompleks ke folder backup:
cp -- " backup [ mingguan ] server . conf " \
" $HOME / praktikum -os/week07 - bash / backup /backup -
mingguan - server . conf "

### 3. Gunakan variabel untuk memproses path dengan aman:
file_asli =" $HOME / praktikum -os/week07 - bash /ruang - nama /
backup [ mingguan ] server . conf "
file_salinan =" $HOME / praktikum -os/week07 - bash / backup /
backup - mingguan -server -v2. conf "
cp -- " $file_asli " " $file_salinan "
ls - lah " $HOME / praktikum -os/week07 - bash / backup "

### 4. Tampilkan daftar file hasil backup:
for file in " $HOME "/ praktikum - os / week07 - bash / backup /*;
do
printf 'Hasil backup : %s\n' " $file "
done

<img width="1185" height="836" alt="image" src="https://github.com/user-attachments/assets/df9d91f6-8830-4e15-9996-d8dca071de10" />
(no 1-4)



