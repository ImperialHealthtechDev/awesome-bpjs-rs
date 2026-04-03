# Awesome BPJS untuk Rumah Sakit [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Kumpulan panduan, tools, dan referensi untuk **manajemen klaim BPJS Kesehatan di rumah sakit Indonesia** — mulai dari VClaim, INA-CBG, eClaim, hingga transisi ke INA-DRG.

Dikelola oleh tim [MedMinutes](https://medminutes.io) — pengembang software klaim dan RME untuk rumah sakit di Indonesia.

---

## Daftar Isi

- [Regulasi & Referensi Resmi](#regulasi--referensi-resmi)
- [Memahami Alur Klaim BPJS](#memahami-alur-klaim-bpjs)
- [VClaim & SEP](#vclaim--sep)
- [INA-CBG & Grouper](#ina-cbg--grouper)
- [eClaim & Proses Verifikasi](#eclaim--proses-verifikasi)
- [ICD-10 & Koding Klinis](#icd-10--koding-klinis)
- [Dokumentasi Medis & Resume](#dokumentasi-medis--resume)
- [Casemix & Tim Klaim](#casemix--tim-klaim)
- [Klaim Pending: Penyebab & Solusi](#klaim-pending-penyebab--solusi)
- [Transisi INA-CBG ke INA-DRG](#transisi-ina-cbg-ke-ina-drg)
- [SIMRS di Indonesia](#simrs-di-indonesia)
- [Tools & Software](#tools--software)
- [Integrasi SATUSEHAT](#integrasi-satusehat)
- [Kontribusi](#kontribusi)

---

## Regulasi & Referensi Resmi

| Regulasi              | Tentang                            | Link                                                                                      |
| --------------------- | ---------------------------------- | ----------------------------------------------------------------------------------------- |
| **Permenkes 76/2016** | Pedoman INA-CBG dalam JKN          | [kemkes.go.id](https://peraturan.bpk.go.id/Details/114235/permenkes-no-76-tahun-2016)     |
| **Perpres 82/2018**   | Jaminan Kesehatan                  | [peraturan.bpk.go.id](https://peraturan.bpk.go.id/Details/97312/perpres-no-82-tahun-2018) |
| **PMK 3/2023**        | Standar Tarif JKN Terbaru          | [kemkes.go.id](https://yankes.kemkes.go.id/unduhan/fileunduhan_1675827002_206129.pdf)     |
| **SE BPJS 2024**      | Ketentuan Verifikasi Klaim Digital | [bpjs-kesehatan.go.id](https://bpjs-kesehatan.go.id)                                      |
| **PMK 24/2022**       | Rekam Medis Elektronik             | [kemkes.go.id](https://peraturan.bpk.go.id/Details/229975/permenkes-no-24-tahun-2022)     |

### Portal Resmi

- [BPJS Kesehatan](https://bpjs-kesehatan.go.id) — Portal utama BPJS
- [SATUSEHAT](https://satusehat.kemkes.go.id) — Platform interoperabilitas data kesehatan nasional
- [INA-CBG Kemenkes](https://inacbg.kemkes.go.id) — Aplikasi grouper INA-CBG
- [VClaim BPJS](https://vclaim.bpjs-kesehatan.go.id) — Virtual Claim BPJS Kesehatan
- [eClaim BPJS](https://eclaim.bpjs-kesehatan.go.id) — Pengajuan klaim digital

---

## Memahami Alur Klaim BPJS

```
Pasien Datang → Registrasi & SEP (VClaim)
    → Pelayanan Klinis (DPJP)
    → Dokumentasi Medis (SOAP, Resume)
    → Koding ICD-10 & ICD-9-CM (Coder/Casemix)
    → Grouping INA-CBG (Grouper)
    → Submit eClaim
    → Verifikasi BPJS
    → Pembayaran
```

### Panduan Lengkap

- [Panduan Lengkap Klaim BPJS untuk Rumah Sakit](https://medminutes.io/blog/klaim-bpjs/) — Hub article: alur klaim dari A-Z
- [Panduan INA-CBG Grouper untuk Rumah Sakit](https://medminutes.io/blog/panduan-ina-cbg-grouper-rumah-sakit/) — Cara kerja grouper, severity level, tarif
- [Apa Itu INA-CBGs dalam Sistem BPJS](https://medminutes.io/blog/apa-itu-ina-cbgs-dalam-sistem-bpjs-kesehatan-dan-bagaimana-pengaruhnya-terhadap-klaim-rumah-sakit/) — Penjelasan komprehensif INA-CBG

---

## VClaim & SEP

VClaim (Virtual Claim) adalah sistem BPJS untuk membuat SEP (Surat Eligibilitas Peserta) secara digital. SEP menjadi entry point setiap episode klaim.

### Masalah Umum

| Error / Masalah           | Penyebab                                    | Panduan                                                                                                                                                |
| ------------------------- | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| SEP gagal dibuat          | Kepesertaan tidak aktif, data tidak sinkron | [Penarikan Data Kepesertaan via API VClaim](https://medminutes.io/blog/penarikan-data-kepesertaan-bpjs-melalui-api-vclaim/)                            |
| Error SEP Status          | Timeout, format data salah                  | [Cara Menangani Error SEP Status](https://medminutes.io/blog/cara-menangani-error-sep-status-pada-integrasi-vclaim-di-rumah-sakit/)                    |
| SEP ganda                 | Pasien terdaftar >1 SEP aktif               | [Deteksi SEP Ganda pada Rawat Inap](https://medminutes.io/blog/deteksi-sep-ganda-pada-pasien-rawat-inap-fondasi-tata-kelola-administrasi-pasien-bpjs/) |
| Double entry VClaim-SIMRS | Input duplikat antara SIMRS dan VClaim      | [Strategi Menghindari Double Entry](https://medminutes.io/blog/strategi-menghindari-double-entry-data-antara-vclaim-bpjs-dan-simrs/)                   |
| Error 28 codes            | Berbagai error VClaim                       | [Panduan VClaim Error 28](https://medminutes.io/blog/vclaim-error-28/)                                                                                 |

### Integrasi VClaim dengan SIMRS

- [VClaim sebagai Entry Point Episode Perawatan](https://medminutes.io/blog/vclaim-bpjs-sebagai-entry-point-episode-perawatan-pasien-di-rumah-sakit/)
- [Integrasi VClaim dengan Resume Medis Digital](https://medminutes.io/blog/integrasi-vclaim-bpjs-dengan-resume-medis-digital/)
- [Monitoring SEP untuk Pencegahan Pending](https://medminutes.io/blog/monitoring-sep-bpjs-untuk-pencegahan-pending-klaim-rumah-sakit/)

---

## INA-CBG & Grouper

INA-CBG (Indonesia Case Based Groups) adalah sistem pengelompokan diagnosis untuk menentukan tarif klaim. Setiap episode perawatan di-_group_ berdasarkan diagnosis utama, prosedur, dan severity level.

### Severity Level

Severity level (I-III) menentukan besaran tarif. Semakin tinggi severity, semakin besar tarif klaim.

| Level | Deskripsi               | Faktor Penentu                       |
| ----- | ----------------------- | ------------------------------------ |
| I     | Tanpa komplikasi        | Diagnosis tunggal                    |
| II    | Dengan komplikasi minor | Komorbid terdokumentasi              |
| III   | Dengan komplikasi mayor | Komplikasi berat + prosedur tambahan |

### Panduan Severity & Tarif

- [Dokumentasi Komorbid sebagai Penentu Severity](https://medminutes.io/blog/dokumentasi-komorbid-sebagai-penentu-severity-ina-cbg-dalam-klaim-bpjs-rumah-sakit/)
- [Dokumentasi Komplikasi Selama Rawat Inap](https://medminutes.io/blog/dokumentasi-komplikasi-selama-rawat-inap-fondasi-severity-level-dan-stabilitas-klaim-bpjs/)
- [Error Severity Level pada Grouper](https://medminutes.io/blog/cara-menangani-error-severity-level-pada-grouper-ina-cbg-di-rumah-sakit/)
- [Diagnosis Benar tapi Tarif Tetap Rendah](https://medminutes.io/blog/diagnosis-sudah-benar-tapi-tarif-klaim-ina-cbg-tetap-rendah/)
- [LOS 5 Hari tapi Tarif Tetap Rendah](https://medminutes.io/blog/los-5-hari-tapi-kenapa-tarif-klaim-ina-cbg-tetap-rendah/)
- [Claim Undervaluation: Penyebab Tersembunyi](https://medminutes.io/blog/claim-undervaluation-dalam-skema-ina-cbg-penyebab-tersembunyi-penurunan-pendapatan-rumah-sakit/)

---

## eClaim & Proses Verifikasi

eClaim adalah aplikasi BPJS untuk pengajuan klaim digital dari RS ke BPJS. Setelah koding selesai, data dikirim melalui eClaim untuk diverifikasi.

### Panduan

- [Panduan eClaim BPJS](https://medminutes.io/blog/eclaim-bpjs-panduan/) — Alur pengajuan, rejection codes, tips
- [Pengiriman Resume Medis ke eClaim](https://medminutes.io/blog/pengiriman-resume-medis-ke-aplikasi-e-claim-efisiensi-klaim-bpjs/)
- [Klaim Revisi Setelah Audit Internal](https://medminutes.io/blog/klaim-revisi-setelah-audit-internal-bpjs-memahami-dampaknya-terhadap-manajemen-klaim-rumah-sakit/)
- [Siap Hadapi Audit BPJS: Strategi Penguatan Internal](https://medminutes.io/blog/siap-hadapi-audit-bpjs-strategi-penguatan-proses-internal-rumah-sakit/)

---

## ICD-10 & Koding Klinis

Koding yang akurat adalah fondasi klaim yang optimal. Kesalahan koding → tarif rendah atau klaim pending.

### Kesalahan Umum Koding

| Masalah                    | Dampak                   | Panduan                                                                                                                                                                                 |
| -------------------------- | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Kode ICD-10 salah          | Tarif turun (downcoding) | [Kesalahan Kode ICD-10 Menurunkan Tarif](https://medminutes.io/blog/kesalahan-kode-icd10-menurunkan-tarif-inacbg/)                                                                      |
| Mapping diagnosis keliru   | Grouping tidak sesuai    | [Kesalahan Mapping Diagnosis ke ICD](https://medminutes.io/blog/kesalahan-mapping-diagnosis-ke-kode-icd-di-rumah-sakit/)                                                                |
| Komplikasi tidak di-coding | Severity level rendah    | [Pasien Sudah Komplikasi tapi Tidak Masuk Coding](https://medminutes.io/blog/pasien-sudah-komplikasi-tapi-tidak-masuk-coding/)                                                          |
| Coding setelah pulang      | Delay klaim              | [Coding Dilakukan Setelah Pasien Pulang](https://medminutes.io/blog/coding-dilakukan-setelah-pasien-pulang-implikasi-terhadap-kecepatan-dan-validitas-klaim-bpjs-dalam-sistem-ina-cbg/) |

### Optimasi Koding

- [Optimasi Koding ICD-10 untuk BPJS](https://medminutes.io/blog/optimasi-koding-icd10-bpjs/) — Panduan lengkap optimasi koding
- [Downcoding: Klaim Diterima tapi Nilainya Turun](https://medminutes.io/blog/klaim-tidak-ditolak-tapi-nilainya-turun-memahami-fenomena-downcoding-ina-cbg-dalam-klaim-bpjs/)
- [Tarif Klaim Berbeda untuk Pasien Sama](https://medminutes.io/blog/pasien-sama-tarif-klaim-berbeda-memahami-variasi-klaim-bpjs-dalam-sistem-ina-cbg/)

---

## Dokumentasi Medis & Resume

Dokumentasi medis yang lengkap dan akurat adalah **fondasi** klaim BPJS yang valid. Tanpa dokumentasi yang kuat, koding tidak bisa optimal.

### SOAP & Resume Medis

- [Kesalahan DPJP saat Mengisi SOAP](https://medminutes.io/blog/kesalahan-umum-dokter-saat-mengisi-soap-yang-berisiko-pada-klaim-bpjs/) — 7 kesalahan paling sering
- [Resume Medis Tidak Lengkap: Dampak ke Klaim & Akreditasi](https://medminutes.io/blog/resume-medis-tidak-lengkap-dampak-klaim-akreditasi/)
- [Resume Dibuat Setelah Pasien Pulang](https://medminutes.io/blog/resume-dibuat-setelah-pasien-pulang-dampaknya-terhadap-klaim-bpjs-di-rumah-sakit/)
- [Klaim Pending karena Resume Belum Ditandatangani](https://medminutes.io/blog/klaim-bpjs-dipending-karena-resume-medis-belum-ditandatangani/)
- [SOAP IGD Tidak Sinkron dengan Resume](https://medminutes.io/blog/soap-igd-tidak-nyambung-dengan-resume-medis-dampaknya-terhadap-dokumentasi-klinis-dan-klaim-ina-cbg/)

### Dokumentasi Penunjang

- [Radiologi sebagai Bukti Audit BPJS](https://medminutes.io/blog/radiologi-sebagai-bukti-penunjang-klinis-dalam-audit-klaim-bpjs/)
- [Integrasi PACS ke RME untuk Validasi Diagnosis](https://medminutes.io/blog/integrasi-pacs-ke-rme-untuk-validasi-diagnosis-ina-cbg/)
- [Dokumentasi Penunjang dalam Penentuan Tarif](https://medminutes.io/blog/dokumentasi-penunjang-dalam-penentuan-tarif-ina-cbg/)

### Farmasi & Obat

- [Obat di Luar DTO BPJS: Risiko Klaim](https://medminutes.io/blog/penggunaan-obat-di-luar-dto-bpjs-sebagai-risiko-klaim-ina-cbg/)
- [Obat Risiko Tinggi dan Klaim](https://medminutes.io/blog/penggunaan-obat-risiko-tinggi-dan-validitas-klaim-ina-cbg/)
- [Input Racikan SIMRS dan Klaim BPJS](https://medminutes.io/blog/kesalahan-input-racikan-di-simrs-yang-mempengaruhi-klaim-bpjs/)
- [Catatan Pemberian Obat dan Klaim](https://medminutes.io/blog/kenapa-catatan-pemberian-obat-bisa-jadi-masalah-klaim-bpjs/)

---

## Casemix & Tim Klaim

Tim casemix adalah garda terdepan optimasi klaim. Perannya bukan sekadar koding, tapi manajemen risiko klaim.

### Panduan Tim Casemix

- [Mengubah Peran Tim Casemix: dari Coder ke Risk Manager](https://medminutes.io/blog/mengubah-peran-tim-casemix-dari-coder-menjadi-risk-manager-strategi-proaktif-mengelola-risiko-klaim-bpjs/)
- [Validasi Terapi Farmasi oleh Tim Casemix](https://medminutes.io/blog/validasi-terapi-farmasi-oleh-tim-casemix-fondasi-konsistensi-dokumentasi-klinis-dan-validitas-klaim-ina-cbg/)
- [Komunikasi Efektif DPJP dan Tim Klaim](https://medminutes.io/blog/membangun-alur-komunikasi-efektif-antara-dpjp-dan-tim-klaim-untuk-menjaga-kelancaran-klaim-bpjs/)
- [Tim Casemix Tanya DPJP Satu-satu: Dampak Inefisiensi](https://medminutes.io/blog/tim-casemix-harus-tanya-dpjp-satu-satu-dampak-ketidaklengkapan-dokumentasi-klinis/)
- [Meningkatkan Produktivitas Tim Klaim Tanpa Tambah SDM](https://medminutes.io/blog/meningkatkan-produktivitas-tim-klaim-rumah-sakit-tanpa-menambah-sdm/)

### Audit Internal

- [Audit Klaim Internal: Checklist Sebelum Submit](https://medminutes.io/blog/audit-klaim-internal-checklist-sebelum-submit-bpjs/)
- [Audit Internal Klaim BPJS: Kapan dan Siapa](https://medminutes.io/blog/audit-internal-klaim-bpjs-kapan-harus-dilakukan-dan-siapa-yang-terlibat/)
- [Audit Klinis Berbasis RME](https://medminutes.io/blog/audit-klinis-berbasis-rme-langkah-praktis-rumah-sakitmenjaga-mutu-layanan-dan-klaim-ina-cbg/)
- [Data Klaim sebagai Dasar Kebijakan Internal RS](https://medminutes.io/blog/mengubah-data-klaim-bpjs-menjadi-dasar-kebijakan-internal-rumah-sakit-berbasis-ina-cbg/)

---

## Klaim Pending: Penyebab & Solusi

Klaim pending = revenue tertahan. Rata-rata RS kehilangan **Rp 50-200 juta/bulan** akibat klaim pending yang tidak dikelola.

### Penyebab Utama

| Penyebab                              | Frekuensi     | Panduan                                                                                                                                                                       |
| ------------------------------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Resume medis tidak lengkap            | Sangat tinggi | [7 Kesalahan yang Membuat Klaim Tertahan](https://medminutes.io/blog/7-kesalahan-paling-sering-yang-membuat-klaim-bpjs-rumah-sakit-tertahan-dalam-proses-verifikasi-ina-cbg/) |
| Ketidaksesuaian kelas peserta         | Tinggi        | [Ketidaksesuaian Kelas Peserta](https://medminutes.io/blog/ketidaksesuaian-kelas-peserta-bpjs-titik-kritis-yang-sering-memicu-pending-klaim-ina-cbg-di-rumah-sakit/)          |
| Registrasi pasien salah               | Sedang        | [Kesalahan Registrasi sebagai Risiko Klaim](https://medminutes.io/blog/kesalahan-registrasi-pasien-sebagai-risiko-klaim-bpjs-dalam-sistem-ina-cbg/)                           |
| SOAP lengkap tapi klaim tetap pending | Sedang        | [SOAP Lengkap tapi Klaim Tertahan](https://medminutes.io/blog/soap-lengkap-klaim-tetap-tertahan-mengurai-akar-risiko-pending-dalam-sistem-ina-cbg/)                           |

### Strategi Pencegahan

- [Cara Mengurangi Pending Rate BPJS](https://medminutes.io/blog/cara-mengurangi-pending-rate-bpjs/) — Panduan lengkap menurunkan pending rate
- [30% Klaim Tertahan 2024: Penyebab & Strategi](https://medminutes.io/blog/30-persen-klaim-bpjs-tertahan-2024-penyebab-strategi/)
- [Revenue Hilang karena Klaim Pending](https://medminutes.io/blog/revenue-hilang-klaim-bpjs-pending/)
- [Titik Rawan Pending yang Sering Tidak Disadari](https://medminutes.io/blog/titik-rawan-pending-klaim-bpjs-yang-sering-tidak-disadari-rumah-sakit/)
- [Biaya Lembur Tim Klaim akibat Rework](https://medminutes.io/blog/biaya-lembur-tim-klaim-akibat-rework-dalam-proses-klaim-bpjs/)
- [AI untuk Deteksi Resume Berisiko Pending](https://medminutes.io/blog/ai-untuk-mendeteksi-resume-medis-yang-berisiko-pending-klaim-bpjs/)

---

## Transisi INA-CBG ke INA-DRG

Indonesia sedang mempersiapkan transisi dari INA-CBG ke **INA-DRG** (Indonesia Diagnosis Related Groups). Perubahan ini akan mengubah cara grouping dan tarif klaim.

### Persiapan

- [Panduan Kesiapan INA-DRG untuk Tim Casemix](https://medminutes.io/blog/panduan-lengkap-kesiapan-idrg-untuk-tim-casemix-rumah-sakit/)
- [Transisi INA-CBG ke INA-DRG: Persiapan Tim Casemix](https://medminutes.io/blog/transisi-ina-cbg-ke-idrg-persiapan-tim-casemix/)

---

## SIMRS di Indonesia

SIMRS (Sistem Informasi Manajemen Rumah Sakit) adalah tulang punggung operasional RS. Pilihan SIMRS yang tepat sangat berpengaruh pada efisiensi klaim BPJS.

### Kategori SIMRS

| Kategori        | Contoh                              | Kelebihan                                                           | Kekurangan                              |
| --------------- | ----------------------------------- | ------------------------------------------------------------------- | --------------------------------------- |
| **Open-source** | SIMRS Khanza                        | Gratis, komunitas besar                                             | Butuh Tim IT internal, support terbatas |
| **Pemerintah**  | SIMGOS (Kemenkes)                   | Gratis untuk RS pemerintah                                          | Fitur terbatas, development lambat      |
| **Cloud/SaaS**  | [MedMinutes](https://medminutes.io) | Update otomatis, integrasi BPJS+SATUSEHAT, AI-powered, tanpa server | Biaya langganan bulanan                 |

### Panduan Memilih SIMRS

- [Panduan Memilih SIMRS Terbaik 2026](https://medminutes.io/blog/simrs-terbaik-2026-perbandingan/) — Perbandingan lengkap 3 kategori SIMRS
- [Biaya SIMRS & RME 2026: Panduan Lengkap](https://medminutes.io/blog/biaya-simrs-rme-2026-panduan-lengkap/)
- [Transformasi Digital RS melalui SIMRS](https://medminutes.io/blog/transformasi-digital-rs-melalui-simrs-fondasi-efisiensi-dan-tata-kelola-klinis/)

### Kriteria SIMRS yang Baik

- Bridging BPJS (VClaim, eClaim, PCare) terintegrasi
- Integrasi SATUSEHAT / HL7 FHIR
- RME yang sesuai PMK 24/2022
- Monitoring klaim real-time
- Support tim responsif

---

## Tools & Software

### BPJScan — AI-Powered Claim Audit

[**BPJScan**](https://medminutes.io/bpjscan) oleh MedMinutes adalah software analisis klaim BPJS berbasis AI untuk rumah sakit. Fitur utama:

- **78 filter analisis** klaim — deteksi pending, downcoding, dan revenue leakage
- Analisis file TXT klaim dari INA-CBG/E-Klaim
- Identifikasi klaim berpotensi pending **sebelum** submit
- Dashboard monitoring klaim real-time
- Digunakan oleh **50+ rumah sakit** di Indonesia
- Proses analisis **< 24 jam** untuk seluruh data klaim

> Artikel terkait: [BPJScan vs Audit Manual Klaim BPJS](https://medminutes.io/blog/bpjscan-vs-audit-manual-klaim-bpjs/)

### CDSS — Clinical Decision Support System

[**CDSS MedMinutes**](https://medminutes.io/cdss) membantu dokter membuat keputusan klinis berbasis data:

- Saran koding ICD-10 berdasarkan dokumentasi
- Alert potensi interaksi obat
- Integrasi dengan RME

### RME — Rekam Medis Elektronik

[**RME MedMinutes**](https://medminutes.io/rme) — RME yang dirancang khusus untuk kebutuhan klaim BPJS dan SATUSEHAT:

- SOAP terstruktur yang mendukung koding akurat
- Resume medis otomatis
- Integrasi langsung dengan VClaim dan eClaim
- Compliance PMK 24/2022

---

## Integrasi SATUSEHAT

SATUSEHAT adalah platform interoperabilitas data kesehatan nasional (HL7 FHIR). Semua RS wajib terintegrasi.

### Panduan

- [Bridging BPJS Rumah Sakit: Panduan Teknis](https://medminutes.io/blog/bridging-bpjs-rumah-sakit-panduan-teknis/) — 6 API yang harus di-bridging
- [Cara Faskes Mendaftar Kerjasama BPJS](https://medminutes.io/blog/cara-faskes-mendaftar-kerjasama-dengan-bpjs-kesehatan-panduan-administratif-dan-kesiapan-sistem-pelayanan/)
- [PCare dan Dampaknya terhadap RS](https://medminutes.io/blog/pcare-dampak-rumah-sakit/)

---

## Glosarium

| Istilah            | Definisi                                                                   |
| ------------------ | -------------------------------------------------------------------------- |
| **SEP**            | Surat Eligibilitas Peserta — bukti kepesertaan BPJS untuk klaim            |
| **VClaim**         | Virtual Claim — sistem BPJS untuk pembuatan SEP digital                    |
| **eClaim**         | Electronic Claim — aplikasi pengajuan klaim digital ke BPJS                |
| **INA-CBG**        | Indonesia Case Based Groups — sistem pengelompokan kasus untuk tarif klaim |
| **INA-DRG**        | Indonesia Diagnosis Related Groups — sistem pengganti INA-CBG (transisi)   |
| **Severity Level** | Tingkat keparahan (I-III) yang menentukan besaran tarif INA-CBG            |
| **DPJP**           | Dokter Penanggung Jawab Pelayanan                                          |
| **LOS**            | Length of Stay — lama rawat inap pasien                                    |
| **Casemix**        | Tim di RS yang mengelola koding dan klaim                                  |
| **Downcoding**     | Klaim diterima tapi tarif lebih rendah dari seharusnya                     |
| **Pending**        | Klaim ditahan oleh verifikator BPJS karena ketidaklengkapan                |

Glosarium lebih lengkap: [Glosarium BPJS & Klaim RS](https://medminutes.io/blog/glosarium/)

---

## Kontribusi

Repo ini dikelola oleh [MedMinutes](https://medminutes.io) sebagai referensi terbuka untuk komunitas rumah sakit di Indonesia.

Punya saran atau ingin menambahkan referensi? Silakan buka [Issue](https://github.com/ImperialHealthtechDev/awesome-bpjs-rs/issues) atau kirim Pull Request.

---

## Lisensi

[![CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

Konten dilisensikan di bawah [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/). Silakan gunakan dengan mencantumkan atribusi ke [MedMinutes](https://medminutes.io).
