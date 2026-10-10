---
name: scripting-audit
description: Prosedur audit script dan keamanan kode sebelum eksekusi
---

# Prosedur Audit Script & Keamanan Kode

Sebagai Asisten AI, sebelum menjalankan *script* panjang (Bash, Python, Node.js) baik yang diberikan oleh pengguna maupun yang di-*generate* sendiri, asisten **WAJIB** melakukan proses *Pre-Execution Audit*.

## Checklist Audit Wajib
Sebelum eksekusi, periksa hal-hal berikut di dalam *script*:

1. **Hardcoded Secrets:** 
   Apakah ada *password*, API Key, atau *Token* yang ditulis secara telanjang di dalam teks? (Saran: Gunakan *Environment Variables* atau bawaan `.env`).
2. **Destructive Commands:** 
   Apakah ada perintah berisiko tinggi seperti `rm -rf`, `DROP TABLE`, atau penimpaan file konfigurasi tanpa perintah *backup* (contoh: `cp config config.bak`) sebelumnya?
3. **Looping / Resource Leak:**
   Apakah script berpotensi memakan RAM terus-menerus atau menyebabkan *Infinite Loop*?
4. **Privilege Escalation:**
   Apakah script ini membutuhkan akses `root`? Jika aplikasinya tidak butuh akses root, jalankan dengan *user* biasa.

## Tindakan Pasca Audit
Jika ditemukan kerentanan atau risiko dari checklist di atas, asisten wajib **MENGHENTIKAN PROSES** dan memberikan peringatan keamanan (*Security Warning*) kepada pengguna beserta revisi kode yang lebih aman. Eksekusi baru boleh dilanjutkan jika pengguna telah menyetujui risiko tersebut.
