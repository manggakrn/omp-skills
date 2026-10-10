# Prosedur Staging Preview & Blue-Green Deployment

Sebagai Partner IT, untuk setiap pembaruan (*update*) UI, fitur aplikasi, atau perilisan versi baru, asisten **DILARANG** langsung menimpa aplikasi utama yang sedang berjalan di *Production*. Asisten wajib menggunakan metode **Blue-Green Deployment**.

## Alur Kerja Wajib (Mandatory Workflow)

### 1. Isolasi Lingkungan (Staging)
*   Aplikasi utama (Production/Blue) dibiarkan berjalan normal (misal di port `80` atau `443`).
*   Asisten menginstal atau melakukan *deploy* versi baru (Green) ke folder terpisah dan menyalakannya di *port* sementara (misalnya port `8080` atau `9999`).

### 2. Sesi Visual Preview (User Acceptance Test)
*   Asisten wajib memberikan URL *staging* tersebut kepada pengguna (contoh: `http://172.16.70.12:8080`).
*   Asisten **WAJIB BERHENTI** dan menunggu pengguna membuka URL tersebut di browser komputernya sendiri untuk melakukan pengujian visual (tampilan UI) dan fungsi.

### 3. The Switch (Pertukaran Arus Bebas Downtime)
*   Jika pengguna mengkonfirmasi **TIDAK SETUJU / REVISI**, asisten akan mematikan *port* sementara tersebut dan memperbaiki kode sesuai arahan. Aplikasi utama tetap aman.
*   Jika pengguna mengkonfirmasi **SETUJU / OKE**, asisten akan melakukan *Cutover*. Asisten mengonfigurasi ulang *Reverse Proxy* (seperti Nginx/Apache) untuk mengalihkan rute trafik utama ke versi baru dalam hitungan milidetik (*Zero Downtime*).

### 4. Retensi & Instant Rollback
*   Versi lama (Blue) tidak boleh langsung dihapus. Versi lama dipertahankan minimal 1x24 jam. Jika setelah rilis terjadi kendala tak terduga, asisten dapat memutar balik (*rollback*) Nginx ke versi lama dalam waktu kurang dari 2 detik.