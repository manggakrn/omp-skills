---
name: ssh
description: Koneksi SSH interaktif dengan password auth via PTY tanpa sshpass
---

# Kemampuan OMP: Koneksi SSH Interaktif (Password Auth)

Sebagai AI assistant di lingkungan OMP, saya dapat terhubung ke server SSH yang dilindungi password (tanpa SSH keys) dengan cara mensimulasikan sesi terminal interaktif (Pseudo-Terminal / PTY).

Berikut adalah langkah-langkah / *skills* bagaimana saya melakukannya:

1. **Membuka Sesi PTY Background:**
   Saya menggunakan tool `bash` untuk menjalankan perintah SSH (`ssh -o StrictHostKeyChecking=no user@host`). Saya mengatur parameter `pty: true` agar server SSH mengira ia sedang berinteraksi dengan terminal nyata.
   
2. **Mendeteksi Prompt Login:**
   Sesi bash tersebut dijalankan sebagai *service* dengan kondisi `ready` berupa teks `password:`. Ini membuat saya tahu persis kapan server meminta kata sandi.

3. **Mengirim Kata Sandi (Stdin Injection):**
   Setelah proses tersebut berstatus *ready* (prompt muncul), saya menggunakan tool `write` yang diarahkan ke URI proses tersebut (contoh: `proc://ssh_session`). Saya mengirimkan kata sandi diikuti dengan enter (`\n`) langsung ke *standard input* (stdin) dari proses tersebut.

4. **Interaksi Berkelanjutan:**
   Setelah berhasil login, saya dapat terus mengirimkan perintah Linux dengan melakukan `write` ke stdin proses tersebut dan melihat hasilnya dengan membaca `proc://ssh_session` menggunakan tool `read`.

Metode ini memungkinkan saya untuk masuk ke server manapun tanpa perlu instalasi `sshpass` atau intervensi manual dari pengguna.
