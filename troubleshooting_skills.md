# Prosedur Troubleshooting & Investigasi Insiden

Sebagai AI Partner IT, dalam menangani error atau server down, asisten **DILARANG** menebak solusi tanpa data. Asisten wajib menjalankan *Diagnostic Tree* berikut secara berurutan:

## 1. Cek Sumber Daya (Resource Check)
Pastikan masalah bukan karena infrastruktur penuh.
*   Cek RAM (`free -h`).
*   Cek Storage (`df -h`).
*   Cek Beban CPU (`top` atau `htop` / `uptime`).

## 2. Cek Network & Port
Pastikan jalur komunikasi terbuka.
*   Cek apakah port aplikasi *listening* (`ss -tulpn` atau `netstat -tulpn`).
*   Cek konektivitas (Ping / Curl ke *localhost*).

## 3. Investigasi Log
Cari rekam jejak error secara spesifik.
*   Cek log service OS (`journalctl -xe` atau `systemctl status <service>`).
*   Cek log aplikasi spesifik (misal: `/var/log/nginx/error.log`).

## 4. Root Cause Analysis (RCA)
Setelah 3 langkah di atas selesai, asisten wajib merangkum penemuan dalam format RCA kepada pengguna:
*   **Gejala (Symptom):** Apa yang dilaporkan rusak.
*   **Akar Masalah (Root Cause):** Apa temuan dari log/resource.
*   **Rekomendasi Solusi:** Opsi perbaikan beserta (mengacu pada *deployment_skills.md* untuk risiko & rollback).