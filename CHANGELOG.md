# CHANGELOG & Audit Trail

## [2026-10-10] Visual Upgrade Laporan Excel Bulanan
**Konteks Masalah / Kebutuhan:**
Tampilan laporan Excel bulanan bawaan `pandas` masih terlihat kaku, lebar kolom tidak menyesuaikan teks, tidak ada garis pembatas (border), dan *sheet summary* terlihat polos.

**Tindakan yang Diambil (Action):**
1. Membuat backup: `cp /home/monitoring/script/daily_report.sh /home/monitoring/script/daily_report.sh.bak3`
2. Menambahkan *styling logic* menggunakan library `openpyxl` di dalam Python:
   *   **Big Title:** Menambahkan judul besar di baris 1-2.
   *   **Auto-Width:** Membuat *looping* untuk mengkalkulasi panjang karakter terpanjang di setiap kolom, lalu menyesuaikan *width* kolom tersebut otomatis (min: 12, max: 50).
   *   **Borders:** Menambahkan `thin_border` di sekeliling tabel data dan baris total.
   *   **Summary Dashboard:** Mengganti nama sheet menjadi "Dashboard Summary", menyesuaikan lebar, dan memberikan warna (Hijau = Pemasukan, Merah = Pengeluaran, Biru = Saldo).
3. Melakukan eksekusi *Smoke Test* ulang untuk men-generate laporan bulan September 2026.

**Hasil Akhir (Result):**
*   **SUKSES**. File Excel dengan format visual Premium berhasil dibuat dan langsung terkirim ke Telegram. Laporan kini sangat rapi dan siap dipresentasikan di level perusahaan.


## [2026-10-10] Perombakan Skrip Laporan Bulanan (Excel)
**Konteks Masalah / Kebutuhan:**
Skrip laporan bulanan memiliki masalah: menarik semua data tanpa filter bulan, mencampur data semua user, *Storage leak*, dan tanpa validasi pengiriman.

**Tindakan yang Diambil (Action):**
1. Backup file.
2. Filter tanggal (bulan lalu) via SQL.
3. Looping untuk membuat file Excel terpisah per *active user*.
4. Auto-cleanup script (hapus `.xlsx` > 90 hari).
5. Migrasi pengiriman Telegram ke `requests` Python.

**Hasil Akhir (Result):**
*   **SUKSES**. File Excel terpisah (Angga & Casmay) berhasil dikirim via Telegram dengan rekap data bulan September 2026.


## [2026-10-10] Pemisahan Alert Laporan Keuangan Harian Telegram
**Konteks Masalah / Kebutuhan:**
Laporan keuangan 23:00 mencampur data 2 user.

**Tindakan yang Diambil (Action):**
1. Menganalisis skema tabel.
2. Melakukan *backup* file.
3. Modifikasi Python untuk iterasi per user, menghasilkan *Smart Report* (Panjang jika ada transaksi, Pendek jika tidak ada).
4. Smoke test manipulasi tanggal.

**Hasil Akhir (Result):**
*   **SUKSES**. Notifikasi berhasil dikirim terpisah. Logika cronjob kembali normal.