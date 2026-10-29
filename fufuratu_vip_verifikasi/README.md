# Fufuratu Visuals — VIP Card + Google Sheets

## 1. Buat database
1. Buat Google Spreadsheet baru.
2. Salin ID spreadsheet dari URL `https://docs.google.com/spreadsheets/d/ID_SPREADSHEET/edit` (bagian antara `/d/` dan `/edit`).
3. Pilih **Extensions → Apps Script**.
4. Salin isi file `Code.gs` dari paket ini ke editor Apps Script.
5. Ganti `GANTI_DENGAN_ID_GOOGLE_SHEETS_ANDA` dengan ID spreadsheet. Simpan. Tab `Cards` dan `Transactions` dibuat otomatis.

## 2. Deploy API
1. Apps Script: **Deploy → New deployment → Web app**.
2. **Execute as:** Me.
3. **Who has access:** Anyone.
4. Klik **Deploy**, beri izin bila diminta, lalu salin URL Web App yang berakhir `/exec`.
5. Jika mengubah kode: **Deploy → Manage deployments → Edit → New version → Deploy**.

## 3. Sambungkan website
1. Buka `app.js`.
2. Cari `const CONFIG = { API_URL: "TEMPEL_URL_WEB_APP_GOOGLE_APPS_SCRIPT_DI_SINI" };`
3. Ganti placeholder dengan URL `/exec` dari Apps Script.
4. Unggah semua isi folder ini ke repository GitHub. `Code.gs` juga harus ditempel ke Apps Script—mengunggahnya ke GitHub saja tidak menjalankannya.
5. Aktifkan **Settings → Pages → Deploy from a branch → main → /(root) → Save**.
6. Buka website Pages; status koneksi terlihat pada banner.

## Fitur
Kelola kartu, QR unik, scan QR, cetak kartu, verifikasi nama/nomor, diskon 20% sekali per kartu per tanggal, transaksi selanjutnya tagihan penuh, riwayat transaksi, pencarian, dan ekspor CSV.

## Keamanan dan batasan penting
Integrasi ini adalah versi awal untuk penggunaan ringan. Apps Script dengan akses `Anyone` membuat endpoint publik; URL dan kode browser bukan rahasia. Jangan simpan data sensitif. Sinkronisasi mengirim seluruh daftar kartu/transaksi dan bisa menimpa perubahan jika beberapa perangkat mengedit bersamaan. Belum aman untuk kasir serentak atau transaksi yang memerlukan validasi atomik. Status sinkronisasi pada browser berarti permintaan dikirim, bukan bukti mutlak bahwa server sudah menyimpan. Ekspor CSV sebagai cadangan rutin. Untuk penggunaan bisnis multi-kasir, tambahkan autentikasi dan backend yang memvalidasi diskon serta menulis transaksi secara atomik.


## Login (demo)
Username awal: `admin`
Password awal: `FufuratuVIP2026!`
Ubah `AUTH_USER` dan `AUTH_PASS` pada `app.js` bila diperlukan. PENTING: login ini hanya pengunci tampilan sisi browser; kode dan kredensial dapat dilihat pengunjung, jadi bukan keamanan sungguhan. Untuk keamanan bisnis, autentikasi harus dilakukan di backend.

Aturan diskon memeriksa transaksi yang tercatat hari itu; transaksi berikutnya pada hari yang sama tagihan penuh. Sinkronisasi awal ini belum aman terhadap dua kasir yang menyimpan transaksi bersamaan karena belum memvalidasi dan menulis transaksi secara atomik di server.
