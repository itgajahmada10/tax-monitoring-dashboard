# Faktur Pajak Monitoring

Dashboard statis (`index.html`) untuk memantau faktur pajak (PPN Masukan) dari sheet **AP FP Test Report**.

Cara kerja mengikuti pola ACC Tes: halaman mengambil CSV hasil **File → Bagikan → Publikasikan ke web** langsung di peramban. Tidak ada kredensial di repo.

- CSV per tab (gid di dalam `index.html`).
- Muat ulang otomatis setiap 5 menit selama tab peramban terlihat, plus tombol **Muat ulang**.
- Jika pengambilan gagal, dasbor menampilkan data terakhir yang tersimpan di `localStorage` beserta banner cache lama.
- CSV publikasi Google bisa tertinggal hingga sekitar 5 menit setelah perubahan di sheet.
- Menu PPh, REPORT, dan SKTD masih **Data menyusul**.
- Webhook n8n AP FP Dashboard API hanya cadangan jika CSV tidak bisa diambil lintas domain.

## Cara membuka

Buka [GitHub Pages](https://itgajahmada10.github.io/tax-monitoring-dashboard/) atau jalankan server statis di folder ini:

```bash
python3 -m http.server 8080
```
