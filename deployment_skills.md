# Kemampuan & Protokol OMP: Prosedur Eksekusi, Deploy & Modifikasi Aman (Enterprise Grade)

Sesuai dengan standar industri *Senior Engineer* dan instruksi pengguna, setiap permintaan eksekusi di server WAJIB mematuhi alur kerja berikut:

## 1. Pengecualian Read-Only
Jika perintah hanya bersifat membaca informasi (*read-only* seperti cek storage, melihat log, `ls`, `cat`), asisten TIDAK PERLU menyajikan analisis risiko.

## 2. Fase Analisis & Pre-Flight Check (Perubahan/Mutasi)
Untuk perintah yang mengubah sistem, asisten **DILARANG** langsung mengeksekusi, dan harus memvalidasi:
*   **Pre-Flight Check:** Memastikan syarat eksekusi terpenuhi.
*   **Level Risiko & Dampak:** (Rendah / Menengah / Tinggi) beserta efek *downtime*.
*   **Skenario Rollback:** Langkah pasti untuk *backup* dan *restore*.

## 3. Mandatory Pause (Konfirmasi Pengguna)
Asisten **WAJIB MENUNGGU PERSETUJUAN**. Eksekusi tidak akan berjalan sampai pengguna mengkonfirmasi.

## 4. Visualisasi Progres (Mandatory Todo List)
Saat eksekusi disetujui (terutama untuk *task* yang lebih dari 1 langkah), asisten **WAJIB** menginisiasi *Todo List* menggunakan sistem Task Management bawaan. Tujuannya agar pengguna dapat melihat daftar pekerjaan dan memantau status secara *real-time* (sedang dikerjakan -> selesai) di layar antarmuka pengguna.

## 5. Eksekusi & Post-Deployment Verification (Smoke Test)
Setelah pengguna setuju dan Todo List dibuat:
1. Jalankan perlindungan *rollback* (backup).
2. Lakukan eksekusi utama.
3. **Verification:** Asisten wajib memvalidasi hasil akhir (misal: jalankan `curl` untuk cek web server, cek keberadaan file).

## 6. Audit Trail (Log Pencatatan)
Setiap mutasi sistem yang selesai **WAJIB** dicatat sebagai rekam jejak.
