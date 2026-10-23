# 🛍️ Analisis Perilaku Belanja Online Orang Indonesia di E-Commerce (Tokopedia)

**Produk Terlaris & Pengaruh Promo** — sebuah analisis data eksploratif dengan Python.

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-2.x-150458?logo=pandas&logoColor=white)
![Status](https://img.shields.io/badge/status-tahap%201%20%E2%80%94%20persiapan-yellow)

> **Catatan:** README ini akan dilengkapi pada Tahap 5 (temuan utama + grafik).
> Bagian yang sudah final ditandai ✅, bagian yang masih dikerjakan ditandai 🚧.

---

## 📌 Latar Belakang

E-commerce sudah jadi bagian sehari-hari orang Indonesia. Setiap Harbolnas, 11.11, dan 12.12,
halaman utama marketplace dipenuhi banner diskon. Tapi pertanyaannya:

> Apakah diskon besar benar-benar membuat produk lebih laku? Kategori apa yang paling
> "cinta promo", dan kategori apa yang pembelinya justru cuek?

Proyek ini menjawab pertanyaan tersebut memakai data produk Tokopedia yang tersedia publik,
dilengkapi data minat pencarian Google Trends untuk melihat pola musiman.

**Untuk siapa analisis ini?** Penjual online dan tim marketing yang ingin tahu di mana
anggaran promo paling efektif dibelanjakan — dan di mana justru sia-sia.

---

## ❓ Pertanyaan Bisnis

| # | Pertanyaan | Dijawab dengan |
|---|---|---|
| 1 | Kategori produk apa yang paling banyak terjual? | Total & rata-rata `terjual` per kategori |
| 2 | Di rentang harga berapa produk paling laku? | Kelompok harga vs median terjual |
| 3 | Seberapa besar pengaruh diskon terhadap penjualan? (10% vs 50%) | Median per kelompok diskon + korelasi Spearman |
| 4 | Seberapa besar pengaruh rating terhadap penjualan? | Scatter/box per kelompok rating + korelasi Spearman |
| 5 | Kategori mana yang paling sensitif terhadap promo? | Selisih median (berdiskon vs tidak) per kategori |
| 6 | Bagaimana tren minat saat tanggal kembar & Harbolnas? | Google Trends Indonesia, 5 tahun |

---

## 🗃️ Sumber Data

| Dataset | Isi | Tahun | Lisensi | Link |
|---|---|---|---|---|
| **Tokopedia Product and Review Dataset** | 5.553 produk, 24 kategori, `count_sold`, `price`, `discounted_price`, `rating_average`, `is_official` | 2025 | CC BY-NC 4.0 | [Kaggle](https://www.kaggle.com/datasets/musabiam/tokopedia-product-and-review-dataset) |
| **Indonesia E-Commerce Dataset: Tokopedia Listings** | 29.519 produk, 9 kolom, `Terjual`, `Diskon (%)`, `Rating` | 2025/2026 | Apache 2.0 | [Kaggle](https://www.kaggle.com/datasets/pandaa12/indonesia-e-commerce-dataset-tokopedia-listings) |
| **Google Trends** (via `pytrends`) | Indeks minat pencarian, `geo='ID'` | 2020–2025 | Syarat layanan Google | [trends.google.com](https://trends.google.com) |

🚧 **Dataset final yang dipakai:** *menunggu pilihan (Tahap 1).*

---

## 🧪 Metodologi (ringkas)

1. **Data cleaning** — konversi `"1rb+ terjual"` → `1000`, `"Rp1.000.000"` → `1000000`,
   hapus duplikat, tangani nilai kosong, dan tangani outlier secara hati-hati (bukan asal buang).
2. **Feature engineering** — kolom turunan: persentase diskon, kelompok harga, kelompok diskon,
   kelompok rating.
3. **Analisis** — statistik deskriptif + **median** (bukan hanya rata-rata, karena distribusi
   penjualan sangat miring) + **korelasi Spearman** (mengukur hubungan antar-peringkat,
   tahan terhadap outlier).
4. **Visualisasi** — bar chart, box plot, scatter, line chart tren.

### ⚠️ Batasan yang diakui sejak awal

- **`jumlah terjual` adalah proxy**, bukan laporan penjualan resmi. Tokopedia hanya
  menampilkan angka kasar ("1rb+ terjual").
- **Korelasi ≠ sebab-akibat.** Produk berdiskon yang laku bisa berarti diskon menarik pembeli,
  *atau* penjual mendiskon produk yang memang sudah laku.
- **Snapshot, bukan time series.** Data produk adalah potret satu waktu, sehingga tidak bisa
  menunjukkan perubahan perilaku dari bulan ke bulan. Kebutuhan tren ditutup dengan Google Trends.
- **Google Trends = minat pencarian (0–100), bukan jumlah pembeli.**
- Tidak ada scraping ke Tokopedia; hanya dataset publik dan Google Trends.

---

## 📁 Struktur Repo

```
.
├── notebook/
│   └── Tokopedia_Ecommerce_Analysis.ipynb   # notebook utama (Colab-ready)
├── data/
│   ├── raw/                                 # data mentah (tidak di-commit)
│   └── processed/                           # data bersih hasil cleaning
├── images/                                  # grafik untuk README
├── requirements.txt
└── README.md
```

---

## ▶️ Cara Menjalankan

**Paling mudah — buka di Google Colab:**

1. Buka `notebook/Tokopedia_Ecommerce_Analysis.ipynb`
2. Klik badge "Open in Colab" (ditambahkan pada Tahap 5)
3. Unduh dataset dari tautan di atas, lalu unggah ke Colab (panduan ada di dalam notebook)

**Secara lokal:**

```bash
git clone https://github.com/imanuelrpt/indonesia-ecommerce-behavior-analysis.git
cd indonesia-ecommerce-behavior-analysis
pip install -r requirements.txt
jupyter notebook notebook/Tokopedia_Ecommerce_Analysis.ipynb
```

---

## 👤 Penulis

**Imanuel R.**
[GitHub](https://github.com/imanuelrpt) · *tambahkan link LinkedIn*

---

## 📄 Lisensi & Atribusi

Kode di repo ini bebas dipakai untuk pembelajaran. Dataset tetap milik pemiliknya
masing-masing dan mengikuti lisensi yang tertera di tabel Sumber Data.
