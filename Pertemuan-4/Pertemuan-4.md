# Pertemuan 4

## Percobaan 1
1. Melihat direktori HOME
$ pwd
$ echo $HOME
![Alt text](Picture/Percobaan1/1.png)

2. Melihat direktori aktual dan parent direktori
$ pwd
$ cd .
$ pwd
$ cd ..
$ pwd
$ cd
![Alt text](Picture/Percobaan1/2.png)

3. Membuat satu direktori, lebih dari satu direktori atau sub direktori
$ pwd
$ mkdir A B C A/D A/E B/F A/D/A
$ ls -l
$ ls -l A
$ ls -l A/D
![Alt text](Picture/Percobaan1/3.png)

4. Menghapus satu atau lebih direktori hanya dapat dilakukan pada direktori kosong dan hanya dapat dihapus oleh pemiliknya kecuali bila diberikan ijin aksesnya
$ rmdir B (Terdapat pesan error, mengapa ?) : error karena direktori B tidak kosong (masih ada sub-direktori F di dalamnya).
$ ls -l B
$ rmdir B/F B
$ ls -l B (Terdapat pesan error, mengapa ?) : yang kedua error karena direktori B sudah berhasil dihapus pada perintah sebelumnya (rmdir B/F B), sehingga sistem tidak menemukannya lagi.
![Alt text](Picture/Percobaan1/4.png)

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
![Alt text](Picture/Percobaan1/5.png)

## Percobaan 2: Manipulasi File

1. Perintah cp untuk mengkopi file atau seluruh direktori
   $ cat > contoh
   $ cp contoh contoh1
   $ ls -l
   $ cp contoh A
   $ ls -l A
   $ cp contoh contoh1 A/D
   $ ls -l A/D
![Alt text](Picture/Percobaan2/1.png)

2. Perintah mv untuk memindah file
   $ mv contoh contoh2
   $ ls -l
   $ mv contoh1 contoh2 A/D
   $ ls -l A/D
   $ mv contoh contoh1 C
![Alt text](Picture/Percobaan2/2.png)

3. Perintah rm untuk menghapus file
   $ rm contoh2
   $ ls -l
   $ rm -i contoh
   $ rm -rf A C
   $ ls -l
![Alt text](Picture/Percobaan2/3.png)

## Percobaan 3: Symbolic Link

1. Membuat shortcut (file link)
   $ echo "Hallo apa khabar" > halo.txt
   $ ls -l
   $ ln halo.txt z
   $ ls -l
   $ cat z
   $ mkdir mydir
   $ ln z mydir/halo.juga
   $ cat mydir/halo.juga
   $ ln -s z bye.txt
   $ ls -l bye.txt
   $ cat bye.txt
![Alt text](Picture/Percobaan3/1.png)

## Percobaan 4: Melihat Isi File

   $ ls -l
   $ file halo.txt
   $ file bye.txt
![Alt text](Picture/Percobaan4/1.png)

## Percobaan 5: Mencari file

1. Perintah find
   $ find /home -name "*.txt" -print > myerror.txt
   $ cat myerror.txt
   $ find . -name "*.txt" -exec wc -l '{}' ';'
![Alt text](Picture/Percobaan5/1.png)

2. Perintah which
   $ which ls
![Alt text](Picture/Percobaan5/2.png)

3. Perintah locate
   $ locate "*.txt"
![Alt text](Picture/Percobaan5/3.png)

## Percobaan 6 Mencari text pada file
   $ grep Hallo *.txt
![Alt text](Picture/Percobaan6/1.png)

   
## Latihan
LATIHAN:
1. Cobalah urutan perintah berikut :
   $ cd
   $ pwd
   $ ls -al
   $ cd .
   $ pwd
   $ cd ..
   $ pwd
   $ ls -al
   $ cd ..
   $ pwd
   $ ls -al
   $ cd /etc
   $ ls -al | more
   $ cat passwd
   $ cd -
   $ pwd
![Alt text](Picture/Latihan/1.1.png)
![Alt text](Picture/Latihan/1.2.png)
![Alt text](Picture/Latihan/1.3.png)
![Alt text](Picture/Latihan/1.4.png)

2. Lanjutkan penelusuran pohon pada sistem file menggunakan cd, ls, pwd dan cat. Telusuri direktori /bin, /usr/bin, /sbin, /tmp dan /boot.
![Alt text](Picture/Latihan/2.1.png)

3. Telusuri direktori /dev. Identifikasi perangkat yang tersedia. Identifikasi tty (terminal) Anda (ketik who am i); siapa pemilih tty Anda (gunakan ls -l).
![Alt text](Picture/Latihan/3.png)

4. Telusuri directory /proc. Tampilkan isi file interrupts, devices, cpuinfo, meminfo dan uptime menggunakan perintah cat. Dapatkah Anda melihat mengapa directory /proc disebut pseudo-filesystem yang memungkinkan akses ke struktur data kernel ?
![Alt text](Picture/Latihan/4.png)

5. Ubahlah direktori home ke user lain secara langsung menggunakan cd ~username.
![Alt text](Picture/Latihan/5.png)

6. Ubah kembali ke direktori home Anda.
![Alt text](Picture/Latihan/6.png)

7. Buat subdirektori work dan play.

8. Hapus subdirektori work.

9. Copy file /etc/passwd ke direktori home Anda.

10. Pindahkan ke subdirectory play.

11. Ubahlah ke subdirektori play dan buat symbolic link dengan nama terminal yang menunjuk ke perangkat tty. Apa yang terjadi jika melakukan hard link ke perangkat tty ?

12. Buatlah file bernama hello.txt yang berisi kata "hello word". Dapatkah Anda gunakan cp menggunakan "terminal" sebagai file asal untuk menghasilkan efek yang sama ?

13. Copy hello.txt ke terminal. Apa yang terjadi ?

14. Masih direktori home, copy keseluruhan direktori play ke direktori bernama work menggunakan symbolic link.

15. Hapus direktori work dan isinya dengan satu perintah.
![Alt text](Picture/Latihan/7.png)
(SS latihan 7-15)





