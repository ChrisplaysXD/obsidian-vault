
# CATATAN LENGKAP — UTS SYSADMIN 2026 (LEMP STACK)
# Server: Ubuntu 26.04.1 LTS "Resolute Raccoon"
# Tanggal: 2026-10-09

================================================================================
I. FUNGSI TIAP SERVICE (untuk pertanyaan dosen)
================================================================================

--- NGNIX ---
Fungsi:
1. Menerima request HTTP dari browser (port 80/443).
2. Melayani file statis langsung (HTML, CSS, gambar).
3. Meneruskan .php ke PHP-FPM via FastCGI socket (unix:/run/php/php-fpm.sock).
4. Mengatur index file, deny .ht, dan virtual host.
Konfigurasi tugas: index.php ditambahkan; location ~ \.php$ dengan fastcgi_pass; deny all untuk /\.ht.

--- MARIADB ---
Fungsi:
1. Menyimpan, mengelola, mengambil data relasional (SQL).
2. User access control (root, aplikasi, anonymous).
3. Transaksi (InnoDB), plugin, replikasi.
Versi: 11.8.6-5ubuntu0.1.
Keamanan: mariadb-secure-installation menghapus anonymous, test DB, remote root; unix_socket untuk root.

--- PHP-FPM ---
Fungsi:
1. Memproses kode PHP (mengeksekusi interpreter).
2. Mengelola pool worker (proses siap menerima FastCGI).
3. Komunikasi dengan Nginx (yang tidak bisa proses PHP sendiri).
Versi: PHP 8.5.4 (service: php8.5-fpm.service — BUKAN php-8.5-fpm).
Socket: /run/php/php-fpm.sock (symlink ke /etc/alternatives/php-fpm.sock).

--- PHP-MYSQL ---
Fungsi: memungkinkan PHP berkomunikasi dengan MariaDB (mysqli / PDO).
Paket: php-mysql (2:8.5+99ubuntu1).

================================================================================
II. LOG PROSES TERMINAL (step-by-step)
================================================================================

1. sudo apt update
2. sudo apt install -y mariadb-server (dpkg --configure -a diperlukan karena interupsi sebelumnya)
3. mariadb-secure-installation (sudo, interaktif — unix_socket diaktifkan, anonymous/test/root remote dihapus)
4. sudo apt install -y php-fpm php-mysql
5. Update /etc/nginx/sites-available/default (tambah index.php, location \.php$, deny /\.ht)
6. sudo nginx -t → syntax ok
7. sudo systemctl reload nginx → berhasil
8. sudo bash -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
9. curl -L http://localhost/info.php → HTTP 200 (phpinfo HTML berhasil)
10. sudo rm /var/www/html/info.php (penghapusan untuk keamanan)

================================================================================
III. KEMUNGKINAN PERTANYAAN DOSEN
================================================================================

NGINX:
- Perbedaan Nginx vs Apache dalam PHP? (Nginx tidak punya mod_php; harus proxy ke PHP-FPM via FastCGI)
- Mengapa unix socket lebih cepat dari TCP? (tidak melalui jaringan TCP/IP)
- Fungsi snippets/fastcgi-php.conf? (parameter FastCGI standar untuk PHP-FPM)

MARIADB:
- Apa yang dilakukan mariadb-secure-installation? (hapus anonymous, remote root, test DB)
- Mengapa unix_socket authentication? (hanya user Linux dengan akses socket yang bisa login root)
- Perbedaan MariaDB 11.8 vs 10.6? (InnoDB lebih cepat, JSON lebih baik, planner lebih optimal)

PHP-FPM:
- Perbedaan PHP-FPM vs PHP-CLI? (FPM daemon berkelanjutan dengan pool; CLI sekali jalan)
- Apa yang terjadi jika PHP-FPM mati? (502 Bad Gateway untuk .php; file statis tetap OK)
- Mengapa perlu php-mysql? (agar PHP bisa query MariaDB)

LEMP INTEGRASI:
- Alur lengkap browser → Nginx → PHP-FPM → MariaDB → kembali? (lihat bagian I)
- Risiko jika info.php tidak dihapus? (expose versi PHP, path, konfigurasi server → serangan target)
- Fungsi deny all /\.ht? (mencegah akses .htaccess atau .htpasswd)

================================================================================
IV. PERBEDAAN PANDUAN VS REALITA
================================================================================

- Service PHP: panduan "php-8.5-fpm" → aktual "php8.5-fpm.service"
- SSL/private key: panduan menyebut tapi server hanya HTTP (port 80)
- mariadb-secure-installation: deprecated note tapi tetap berfungsi

================================================================================
V. PERINTAH VERIFIKASI UNTUK DEMO
================================================================================

systemctl status mariadb nginx php8.5-fpm --no-pager
sudo mysql -e "SELECT User, Host FROM mysql.user;"
ls -la /run/php/
cat /etc/nginx/sites-available/default
sudo nginx -t
curl -L http://localhost/info.php (sementara)

================================================================================
VI. KEAMANAN & CLEANUP
================================================================================

- mariadb-secure-installation: OK (anonymous/test/root remote dihapus)
- info.php: sudah dibuat, diuji, dan DIHAPUS
- deny /\.ht: aktif di Nginx
- SUDO_PASSWORD=Admin123 di /home/sa24k10016/.hermes/.env (digunakan untuk tugas ini; sebaiknya dihapus setelah tugas)

DIBUAT OLEH: sa24k10016 (Hermes Agent) | TUGAS: SYSADMIN2026 ASSIGNMENT IV (UTS)
