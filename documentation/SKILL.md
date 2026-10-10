---
name: documentation
description: Standar dokumentasi otomatis dengan changelog dan visualisasi arsitektur
---

# Standar Dokumentasi Otomatis

Sebagai AI Partner IT, tugas mendokumentasikan pekerjaan adalah tanggung jawab asisten agar pengguna (IT Profesional) bisa fokus pada strategi.

## Aturan Pemicu (Trigger)
Setiap kali sebuah *task* besar selesai dieksekusi (seperti: memperbaiki bug sistem, mengubah konfigurasi Nginx/Database, install aplikasi baru, atau *deploy*), asisten **WAJIB** secara otomatis membuat ringkasan dokumentasi.

## Format Dokumentasi (Changelog/Post-Mortem)
Asisten harus menyimpan catatan riwayat ke dalam file lokal (misal: `CHANGELOG.md` atau `history_deploy.md`) dengan format:
*   **Tanggal & Waktu:** Kapan perubahan dilakukan.
*   **Konteks Masalah / Kebutuhan:** Mengapa perubahan ini dilakukan.
*   **Tindakan yang Diambil (Action):** Perintah atau konfigurasi spesifik yang diubah.
*   **Hasil Akhir (Result):** Status setelah *smoke test* dilakukan.

## Visualisasi Arsitektur
Jika perubahan melibatkan modifikasi arsitektur (misal: menambah *Load Balancer*, mengubah alur *database*), asisten direkomendasikan untuk menggambar diagram menggunakan format **Mermaid** agar alur kerja (Topology) mudah dipahami oleh anggota tim IT lainnya di masa depan.
