# Faktur Pajak Monitoring

Dasbor statis (satu file `index.html`) untuk memantau faktur pajak. Tanpa build, tanpa data contoh.

**Live:** https://itgajahmada10.github.io/tax-monitoring-dashboard/

## Menu
- **Dashboard** – hanya 3 total: PPN Keluaran (menyusul), PPN Masukan (dihitung), PPh (menyusul).
- **PPN** – sub-tab *PPN Keluaran* (panel link sistem Clara, `CONFIG.CLARA_URL`) dan *PPN Masukan*.
  - Satu daftar semua faktur dari CSV publikasi *AP FP Test Report* (tab WNS/WSI/TTP/MJS/GMI/AMT + ERROR_LOG + Report Pecahan).
  - Tim tax memilih **PPN MASUKAN / PPN DITUNDA** + **masa**, per baris atau multi-select (bulk).
  - 5 sub-tab: Semua / PPN Masukan / PPN Ditunda / Waiting / Edited (+ filter edit menunggu head).
  - Peringatan duplikat (8 digit belakang serial) dengan aksi **Double** / **Pembetulan**.
  - **Print PDF / Unduh PDF** (PDF pecahan di Drive) otomatis menandai *Printed + Approved*.
  - **Approved tidak bisa dibatalkan.** Edit tetap bisa, tapi lewat `edit_request` yang harus di-*approve* head.
- **PPh** – 6 modul sesuai template (PPh 23, 21/26 Gaji, 21 Jasa, 4(2), 22, 15), data menyusul.
- **REPORT** – Neraca (Aktiva vs Pasiva) dan Laba Rugi sesuai template, data menyusul.
- **SKTD** – panel link Purchasing Team (`CONFIG.SKTD_URL`), link menyusul.

## Sumber data
- Faktur: CSV publikasi Google Sheet (bisa tertinggal ±5 menit). Muat ulang otomatis tiap 5 menit, tombol *Muat ulang*, cache localStorage + banner bila gagal.
- Status aksi: n8n webhook **AP FP Action API** (`CONFIG.ACTION_API`). GET = status per faktur (log di-fold), POST = tambah aksi (append-only ke tab `FP Action`).
  Aksi: `classify, masa, print, approve, batal, unbatal, pembetulan, dup_double, dup_pembetulan, dup_diganti, dup_reset, edit_request, edit_approve, edit_reject`. `unapprove` ditolak.
- Kunci faktur: `PT|kode(4)|serial(13)`.

## Pengguna (sementara)
Belum ada login. Nama user + peran (user/head) disimpan di localStorage dan dikirim sebagai `user`/`role`. **Tidak diverifikasi**; akses dasbor belum dibatasi. Menunggu keputusan ibu & head.

## Konfigurasi
Edit objek `CONFIG` di `index.html`: `CLARA_URL`, `SKTD_URL`, `ACTION_API`, `CSV_BASE`, `TABS`.
