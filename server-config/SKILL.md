---
name: server-config
description: Standar konfigurasi server enterprise-grade dengan keamanan dan stabilitas
---

# Standar Konfigurasi Server OMP

Dokumen ini berisi standar konfigurasi *Enterprise-Grade* yang telah disesuaikan dengan kebutuhan dan keputusan pengguna (Accepted Risks).

## 1. Pengecualian Akses (Accepted Risk)
Berdasarkan keputusan pengguna, **Login SSH menggunakan user `root` dan Password DIPERBOLEHKAN** untuk lingkungan server ini (Internal/Lokal).
*   *Catatan Senior:* Risiko *human error* dan *lateral movement malware* lokal telah diterima pengguna demi kecepatan dan kemudahan akses operasional.

## 2. Keamanan Dasar Tambahan
Meskipun `root` diizinkan, lapis keamanan lain tetap direkomendasikan:
*   **Firewall (UFW / iptables):** Menutup semua port masuk kecuali port yang secara spesifik digunakan (seperti 22 untuk SSH, 80/443 untuk Web).
*   **Fail2Ban:** Mengaktifkan pemblokiran otomatis terhadap IP lokal/luar yang melakukan *spam* tebak password.

## 3. Stabilitas & Performa (Reliability & Tuning)
*   **Swap Memory:** Wajib dialokasikan untuk mencegah *Out-of-Memory* (OOM) *kill* secara tiba-tiba ketika RAM fisik penuh.
*   **Tuning `ulimit`:** Menaikkan batas *File Descriptor* maksimal agar server web/database bisa melayani banyak koneksi (koneksi tinggi) tanpa error.
*   **NTP (Time Sync):** Konfigurasi waktu server harus selalu akurat untuk validitas log dan transaksi data.

## 4. Perawatan & Visibilitas
*   **Logrotate:** Wajib dikonfigurasi pada semua *service* yang menghasilkan log (Docker, Nginx, Node.js) agar storage server tidak penuh mendadak.
*   **Monitoring Dasar:** Menyediakan *tool* atau cara cepat untuk memonitor beban CPU, RAM, dan I/O Disk.

## 5. Standar Layanan Aplikasi
Meskipun pengguna masuk sebagai `root`, saat melakukan proses *deploy* aplikasi (misal: PM2, Systemd Service), aplikasi tersebut disarankan untuk tetap dijalankan menggunakan *user environment* yang spesifik, bukan dijalankan sebagai *service root*, kecuali memang diwajibkan oleh aplikasinya.
