# Pertemuan 4

## Percobaan 1
1. Melihat direktori HOME
$ pwd
$ echo $HOME

2. Melihat direktori aktual dan parent direktori
$ pwd
$ cd .
$ pwd
$ cd ..
$ pwd
$ cd

3. Membuat satu direktori, lebih dari satu direktori atau sub direktori
$ pwd
$ mkdir A B C A/D A/E B/F A/D/A
$ ls -l
$ ls -l A
$ ls -l A/D

4. Menghapus satu atau lebih direktori hanya dapat dilakukan pada direktori kosong dan hanya dapat dihapus oleh pemiliknya kecuali bila diberikan ijin aksesnya
$ rmdir B (Terdapat pesan error, mengapa ?) : error karena direktori B tidak kosong (masih ada sub-direktori F di dalamnya).
$ ls -l B
$ rmdir B/F B
$ ls -l B (Terdapat pesan error, mengapa ?) : yang kedua error karena direktori B sudah berhasil dihapus pada perintah sebelumnya (rmdir B/F B), sehingga sistem tidak menemukannya lagi.

5. Navigasi direktori dengan instruksi cd untuk pindah dari satu direktori ke direktori lain.
$ pwd
$ ls -l
$ cd A
$ pwd
$ cd ..
$ pwd
$ cd /home/<user>/C
$ pwd
$ cd /<user>/C (Terdapat pesan error, mengapa ?) : error karena jalur (path) tersebut dianggap sebagai jalur absolut dari root (/). Seharusnya menggunakan /home/<user>/C atau jalur relatif jika Anda berada di lokasi yang tepat.
$ pwd
