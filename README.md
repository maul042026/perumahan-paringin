# 🏠 Perumahan Paringin Asri
### Website Penjualan Rumah Subsidi FLPP — PT Rusdi Rahmi

> Website marketing dan booking unit rumah subsidi pemerintah (FLPP) di Paringin, Kabupaten Balangan, Kalimantan Selatan. Data unit, stok, dan progress pembangunan terhubung langsung ke Google Sheets sehingga bisa diupdate kapan saja tanpa menyentuh kode.

🌐 **Live Site:** [https://username.github.io/perumahan-paringin-asri](https://username.github.io/perumahan-paringin-asri)

---

## ✨ Fitur Website

| Fitur | Keterangan |
|---|---|
| 📊 Data Real-time | Stok unit dan progress langsung dari Google Sheets |
| 🧮 Simulasi KPR | Kalkulator cicilan FLPP interaktif (DP, tenor, bunga) |
| 📋 Form Booking | Booking online + notifikasi email otomatis ke developer |
| 📍 Info Lokasi | Jarak ke fasilitas umum + link Google Maps |
| 📱 Responsif | Tampil bagus di HP maupun desktop |
| ❓ FAQ | Pertanyaan umum calon pembeli |

---

## 🗂️ Struktur File

```
perumahan-paringin-asri/
│
├── index.html               ← Website utama
├── google-apps-script.js    ← Kode backend (paste ke Google Apps Script)
├── PANDUAN-SETUP.md         ← Panduan lengkap setup
└── README.md                ← File ini
```

---

## ⚙️ Cara Setup

### 1. Google Sheets — Buat 3 Tab

**Tab "Units"** — data tiap tipe rumah:

| nama | tipe | harga | lb | lt | kamar_tidur | kamar_mandi | stok_tersedia | stok_total | label | fasilitas | listrik |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Tipe 36/72 | 36/72 | 166000000 | 36 | 72 | 2 | 1 | 18 | 28 | TERSEDIA | Dinding bata merah,Atap genteng metal,Lantai keramik | 1300 |
| Tipe 36/60 | 36/60 | 166000000 | 36 | 60 | 2 | 1 | 10 | 14 | POPULER | Dinding bata merah,Atap genteng metal,Lantai keramik | 1300 |

**Tab "Settings"** — pengaturan website:

| key | value |
|---|---|
| nama_proyek | Perumahan Paringin Asri |
| alamat | Jl. [Nama Jalan], Paringin, Kab. Balangan 71611 |
| whatsapp | 6281234567890 |
| email | info@perumahanparingin.com |
| gmaps_url | https://maps.google.com/?q=-2.123,115.456 |
| total_unit | 42 |
| target_serah | Q2 2025 |
| progress_konstruksi | 65 |
| progress_dokumen | 80 |

**Tab "Bookings"** — diisi otomatis sistem saat ada booking masuk:

| tanggal | nama | hp | email | pekerjaan | unit | penghasilan | catatan | status |
|---|---|---|---|---|---|---|---|---|
| *(otomatis)* | *(otomatis)* | ... | | | | | | BARU |

---

### 2. Google Apps Script — Pasang Backend

1. Di Google Sheets → klik menu **Extensions → Apps Script**
2. Hapus semua kode yang ada, lalu paste isi file `google-apps-script.js`
3. **Cari Sheet ID Anda:**

   Buka Spreadsheet di browser, lihat URL-nya:
   ```
   https://docs.google.com/spreadsheets/d/1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgVE2upms/edit
                                          ↑_________________________________________↑
                                          Ini Sheet ID — salin bagian ini saja
   ```
   > ⚠️ **Perhatian:** Sheet ID berbeda dengan URL pubhtml (`2PACX-1v...`).
   > Sheet ID yang benar ada di URL saat Anda membuka Spreadsheet biasa, bukan saat publish.

4. Tempel Sheet ID ke kode Apps Script:
   ```javascript
   const SHEET_ID = 'tempel_sheet_id_anda_di_sini';
   // Contoh:
   const SHEET_ID = '1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgVE2upms';
   ```

5. Ganti email notifikasi booking:
   ```javascript
   const emailDeveloper = 'email_anda@gmail.com';
   ```

6. **Deploy sebagai Web App:**
   - Klik **Deploy → New deployment**
   - Klik ikon ⚙️ → pilih **Web app**
   - Execute as: **Me**
   - Who has access: **Anyone**
   - Klik **Deploy** → izinkan akses jika diminta
   - **Salin URL** yang muncul (format: `https://script.google.com/macros/s/.../exec`)

---

### 3. Pasang URL ke index.html

Buka `index.html`, cari dan ganti baris ini:

```javascript
// SEBELUM (belum diisi):
const SCRIPT_URL = 'https://script.google.com/macros/s/GANTI_DENGAN_URL_ANDA/exec';

// SESUDAH (sudah diisi URL Apps Script Anda):
const SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbx7mB7PQvh.../exec';
```

Simpan file.

---

### 4. Upload ke GitHub Pages

```
1. Buat repository baru di github.com (Public)
2. Upload index.html — rename menjadi index.html jika belum
3. Settings → Pages → Source: main branch / root
4. Tunggu 1–2 menit → website online!
```

URL website: `https://[username].github.io/[nama-repo]`

---

## 🔄 Update Data Sehari-hari

Cukup buka Google Sheets dari HP — tidak perlu sentuh kode:

| Yang ingin diubah | Tab | Yang diubah |
|---|---|---|
| Ada unit terjual / booking | Units | Kurangi angka di `stok_tersedia` |
| Progress konstruksi naik | Settings | Ubah nilai `progress_konstruksi` |
| Kelengkapan dokumen | Settings | Ubah nilai `progress_dokumen` |
| Nomor WhatsApp | Settings | Ubah nilai `whatsapp` |
| Lihat booking masuk | Bookings | Semua booking tersimpan di sini |
| Tandai booking sudah diproses | Bookings | Kolom `status` → ubah ke `PROSES` atau `SELESAI` |

---

## 💰 Biaya Operasional

| Komponen | Biaya |
|---|---|
| Google Sheets + Apps Script | **Gratis** |
| GitHub Pages Hosting | **Gratis** |
| Domain .com *(opsional)* | ±Rp 150.000/tahun |
| **Total minimum** | **Rp 0/bulan** |

---

## 🛠️ Teknologi

- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **Backend/Database**: Google Sheets + Google Apps Script
- **Hosting**: GitHub Pages
- **Font**: Plus Jakarta Sans, Playfair Display (Google Fonts)

---

## ❓ Troubleshooting

**"Gagal memuat data" saat website dibuka**
- Pastikan `SCRIPT_URL` di `index.html` sudah diisi URL Apps Script yang benar
- Pastikan Apps Script di-deploy dengan akses **Anyone**
- Buka URL Apps Script langsung di browser — harus muncul data JSON

**Tidak ada notifikasi email saat booking masuk**
- Cek folder Spam di Gmail
- Pastikan email di `emailDeveloper` sudah benar di Apps Script
- Re-deploy Apps Script setelah mengubah kode

**Setelah ubah kode Apps Script, perubahan tidak muncul**
- Klik Deploy → **Manage deployments** → edit → pilih **New version** → Deploy

---

*PT Rusdi Rahmi · Paringin, Kabupaten Balangan, Kalimantan Selatan*
