# Tax Monitoring Dashboard

Dashboard statis (satu file `index.html`) untuk memantau faktur pajak.

- **Data PPN** diambil langsung dari sheet **AP FP Test Report** lewat workflow n8n **AP FP Dashboard API** (webhook GET publik, read-only):
  `https://n8.waruna-group.co.id/webhook/apfp-dashboard-api`
- Tab yang dibaca: WNS, WSI, TTP, MJS, GMI, AMT, ERROR_LOG, Report Pecahan (link PDF pecahan digabung lewat Nomor FP / File ID).
- Menu PPh, REPORT, dan SKTD masih **Data menyusul**.
- Tidak ada API key atau data rahasia di repo ini.
