LOG PROSES TERMINAL — UTS SYSADMIN 2026
========================================
Tanggal: 2026-10-09
Server: chrsdnlrbrt (Ubuntu 26.04.1 LTS "Resolute Raccoon")
User: sa24k10016

--- KENDALA AWAL ---
- apt install mariadb-server pertama kali timeout setelah 180 detik.
- dpkg terputus (interrupted): perlu sudo dpkg --configure -a sebelum lanjut.
- sudo memerlukan autentikasi (Admin123) — disimpan sementara di .env (SUDO_PASSWORD).
- mariadb-secure-installation berjalan interaktif tapi menerima input kosong untuk root password awal.

--- PROSES EKSEKUSI ---

[1] sudo apt update
Status: OK (repositori resolute berhasil di-fetch)

[2] sudo dpkg --configure -a
Status: OK (menyelesaikan konfigurasi mariadb-server yang tertunda)

[3] sudo apt install -y mariadb-server
Status: OK (11.8.6-5ubuntu0.1 terinstall, service mariadb aktif)

[4] mariadb-secure-installation (via sudo, interaktif)
Status: OK (deprecated note muncul tapi semua langkah berhasil)
Verifikasi: mysql.user hanya berisi localhost entries; test DB tidak ada.

[5] sudo apt install -y php-fpm php-mysql
Status: OK (8.5.4-0ubuntu1.3 terinstall, php8.5-fpm.service aktif)

[6] Update /etc/nginx/sites-available/default
Status: OK (index.php, fastcgi-php.conf, deny .ht semua ditambahkan)
Catatan: panduan menyebut SSL tapi server ini hanya HTTP port 80.

[7] sudo nginx -t
Status: OK (syntax ok)

[8] sudo systemctl reload nginx
Status: OK (exit 0)

[9] Pembuatan info.php
Status: OK (file dibuat, curl mengembalikan HTTP 200 dengan output phpinfo HTML)

[10] Penghapusan info.php
Status: OK (file dihapus untuk keamanan)

--- OUTPUT KUNCI ---
- systemctl status mariadb: active (running) sejak 02:47:59
- systemctl status php8.5-fpm: active (running) sejak 02:59:18
- curl localhost/info.php: HTTP 200, output <!DOCTYPE html ... (phpinfo)
- nginx -t: syntax is ok, configuration file /etc/nginx/nginx.conf test is successful
- dpkg -l mariadb-server: 1:11.8.6-5ubuntu0.1
- dpkg -l php-fpm: 2:8.5+99ubuntu1

--- KESALAHAN / PERBEDAAN DENGAN PANDUAN ---
1. Service PHP: panduan menyebut "php-8.5-fpm", aktual: "php8.5-fpm.service"
2. SSL/private key: panduan menyebutkan tapi tidak ada di konfigurasi server (hanya HTTP)
3. mariadb-secure-installation: deprecated note muncul tapi tetap berfungsi

--- KEAMANAN ---
- info.php sudah dibuat, diuji, dan DIHAPUS.
- .ht deny sudah dikonfigurasi.
- SUDO_PASSWORD (Admin123) masih tersimpan di .env — sebaiknya dihapus setelah tugas selesai.
