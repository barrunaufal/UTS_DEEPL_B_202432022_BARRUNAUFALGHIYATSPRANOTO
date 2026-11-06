# UTS Praktikum Deep Learning — Peramalan ISPU PM10 Jakarta dengan LSTM

| Keterangan | Isi |
| --- | --- |
| Nama | Barru Naufal Ghiyats Pranoto |
| NIM | 202432022 |
| Kelas | B |
| Mata Kuliah | Deep Learning |
| Dosen Pengampu | Dr. Dra. Dwina Kuswardani, M.Kom |
| Topik | Forecasting Time-Series (NIM genap) |
| Algoritma | LSTM (PyTorch) |

## Dataset

**Air Quality Index in Jakarta** — Kaggle:
https://www.kaggle.com/datasets/senadu34/air-quality-index-in-jakarta-2010-2021

Indeks Standar Pencemaran Udara (ISPU) harian dari 5 Stasiun Pemantau Kualitas Udara (SPKU) DKI Jakarta, bersumber dari Satu Data Jakarta (Januari 2010 – Februari 2025).

Model memakai kolom `pm10` dari `ispu_dki1.csv` (Stasiun DKI1 Bunderan HI) pada periode 1 Januari 2010 – 31 Desember 2021. Data tahun 2022 tidak tersedia pada seluruh file stasiun, sehingga dipakai periode kontinu sebelum 2022.

## Isi Repositori

| File | Keterangan |
| --- | --- |
| `UTS_DEEPL_B_202432022_BARRUNAUFALGHIYATSPRANOTO.ipynb` | Notebook program (PyTorch) beserta seluruh output dan grafik |
| `ispu_dki1.csv` | Data Stasiun DKI1 (Bunderan HI) — **dipakai untuk pemodelan** |
| `ispu_dki2.csv` | Data Stasiun DKI2 (Kelapa Gading) |
| `ispu_dki3.csv` | Data Stasiun DKI3 (Jagakarsa) |
| `ispu_dki4.csv` | Data Stasiun DKI4 (Lubang Buaya) |
| `ispu_dki5.csv` | Data Stasiun DKI5 (Kebon Jeruk) |
| `ispu_dki_all.csv` | Satu baris per hari dari stasiun dengan ISPU tertinggi |

## Alur Program

1. Import library
2. Pra-pemrosesan: interpolasi data kosong, normalisasi Min-Max, sliding window 30 hari → prediksi 1 hari berikutnya, pembagian data latih/uji 80:20
3. Arsitektur: 2 lapis LSTM (64 unit hidden, dropout 0,2) + lapisan Linear
4. Pelatihan: 50 epoch, Adam (learning rate 0,001), MSELoss, batch 32
5. Visualisasi: kurva loss serta perbandingan data aktual vs prediksi

## Hasil pada Data Uji (8 Agustus 2019 – 31 Desember 2021)

| Metrik | LSTM | Pembanding naif (besok = hari ini) |
| --- | --- | --- |
| MAE (ISPU) | 6,73 | 7,61 |
| RMSE (ISPU) | 8,86 | 10,12 |
| MAPE (%) | 16,49 | 17,28 |

## Cara Menjalankan

1. Buka notebook di Google Colab.
2. Pastikan `ispu_dki1.csv` dapat dibaca: upload ke panel Files Colab, atau isi `FILE_PATH` dengan URL raw file tersebut di repositori ini.
3. Pilih **Runtime → Run all**.
