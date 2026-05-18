# Pertemuan 11
## Latihan Tugas

### Latihan Latihan 9.A — Audit dan Kolaborasi
#### 1. Temukan file SUID aktif dengan find / -perm -4000 -type f 2>/dev/null, lalu jelaskan tiga file yang Anda kenali beserta alasannya.
<img width="770" height="47" alt="image" src="https://github.com/user-attachments/assets/ee3e6e5b-e034-49d6-b63f-093dc1cf776c" />

/usr/bin/passwd: Digunakan user biasa untuk mengubah password mereka sendiri. File ini butuh hak SUID agar bisa menulis ke file kritis /etc/shadow.
/usr/bin/sudo: Mengizinkan user biasa menjalankan perintah dengan hak akses root (setelah divalidasi oleh aturan di /etc/sudoers).
/usr/bin/chsh: Digunakan user untuk mengubah default shell mereka (menulis perubahan ke file /etc/passwd).

#### 2. Cari direktori world-writable dan tentukan mana yang valid dan mana yang berisiko.
<img width="746" height="88" alt="image" src="https://github.com/user-attachments/assets/560754f9-8496-4860-a559-28e96df9d618" />
Direktori Valid (Aman): /tmp dan /var/tmp. Direktori ini memang sengaja dibuat agar semua aplikasi/user bisa menulis data sementara. Keamanannya dijaga oleh Sticky Bit (t), sehingga user tidak bisa menghapus file milik user lain.

Direktori Berisiko: Direktori sistem atau konfigurasi seperti /etc, /bin, /usr, atau direktori aplikasi penting yang memiliki permission world-writable. Risiko utamanya adalah Local Privilege Escalation, di mana penyerang atau user biasa bisa menyisipkan script berbahaya untuk dieksekusi oleh sistem.

#### 3. Rancang konfigurasi permission standar dan ACL untuk direktori proyek /srv/webapp/ agar group webapp-team dapat menulis, user deploy hanya membaca, dan file baru selalu mewarisi group proyek.
mkdir -p /srv/webapp
chown -R root:webapp-team /srv/webapp
chmod 2775 /srv/webapp
setfacl -d -m g:webapp-team:rwx /srv/webapp
setfacl -m u:deploy:r-x /srv/webapp
setfacl -d -m u:deploy:r-x /srv/webapp

webapp-team: Bisa menulis (rwx dari group permission & ACL default).
user deploy: Hanya membaca (r-x dikunci oleh ACL khusus user).
Pewarisan Group: Dijamin oleh SGID bit (chmod 2...).

### Latihan Latihan 9.B — Kebijakan Akun dan Quota
#### Tuliskan langkah untuk membuat user intern, menambahkannya ke group labgroup, memaksa pergantian password tiap 45 hari (warning 7 hari), memberi izin sudo hanya untuk systemctl status, dan menetapkan quota ruang serta inode sederhana pada /home/
sudo groupadd labgroup
sudo useradd -m -g labgroup -s /bin/bash intern
sudo passwd intern

sudo chage -M 45 -W 7 intern

echo "intern ALL=(ALL) NOPASSWD: /usr/bin/systemctl status" | sudo tee /etc/sudoers.d/intern-policy
sudo chmod 0440 /etc/sudoers.d/intern-policy

sudo setquota -u intern 1000000 1100000 10000 11000 /home

sudo repquota -u /home | grep intern
