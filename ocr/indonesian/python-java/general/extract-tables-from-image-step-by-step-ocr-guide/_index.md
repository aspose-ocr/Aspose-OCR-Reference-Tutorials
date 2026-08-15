---
category: general
date: 2026-03-26
description: Ekstrak tabel dari gambar dan konversi gambar menjadi spreadsheet menggunakan
  Python OCR. Pelajari cara memuat gambar untuk OCR, membaca tabel, dan mengekstrak
  data tabel.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: id
og_description: Ekstrak tabel dari gambar dengan Python OCR. Panduan ini menunjukkan
  cara memuat gambar untuk OCR, membaca tabel, dan mengubahnya menjadi spreadsheet.
og_title: Ekstrak Tabel dari Gambar – Tutorial OCR Lengkap
tags:
- OCR
- Python
- Data Extraction
title: Ekstrak Tabel dari Gambar – Panduan OCR Langkah demi Langkah
url: /id/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Tabel dari Gambar – Tutorial OCR Lengkap

Pernahkah Anda perlu **extract tables from image** tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika PDF atau tangkapan layar berisi data tabel yang harus menjadi baris dan kolom yang dapat diedit. Kabar baik? Beberapa baris kode Python, dipadukan dengan mesin OCR yang solid, dapat mengubah gambar itu menjadi spreadsheet yang dapat digunakan dalam hitungan detik.

Dalam tutorial ini kami akan menjelaskan cara memuat gambar untuk OCR, menjalankan mesin pengenalan, dan mengekstrak setiap baris tabel satu per satu. Pada akhir tutorial Anda akan dapat **convert image to spreadsheet**, dan Anda juga akan melihat cara **ocr read tables** dan **ocr extract table data** untuk pemrosesan lanjutan. Tidak ada keajaiban tersembunyi, hanya kode yang jelas dan dapat dijalankan yang dapat Anda masukkan ke dalam proyek Anda hari ini.

---

## Apa yang Anda Butuhkan

Sebelum kita menyelam lebih dalam, pastikan Anda memiliki hal‑hal berikut:

- **Python 3.9+** – rilis stabil terbaru paling cocok.
- Perpustakaan **`ocr`** (atau SDK OCR kompatibel apa pun yang menyediakan `OcrEngine`, `Image`, dan metode terkait tabel). Instal dengan `pip install ocr‑sdk` (ganti dengan nama paket yang sebenarnya).
- Sebuah file gambar (`.png`, `.jpg`, dll.) yang berisi tabel yang tercetak jelas.  
- Opsional: **pandas** jika Anda ingin menulis data yang diekstrak langsung ke file CSV atau Excel (`pip install pandas`).

Sudah siap? Bagus—mari kita mulai.

## Langkah 1: Impor SDK OCR dan Siapkan Lingkungan Anda

Langkah pertama: kita perlu mengimpor kelas OCR ke dalam skrip kita dan menyiapkan pembantu kecil yang nanti akan mengubah data tabel mentah menjadi DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Why this matters:** Mengimpor `ocr` memberi kita akses ke `OcrEngine`, `Imaging.Image`, dan objek tabel yang akan kita iterasi. `pandas` tidak diperlukan untuk ekstraksi, tetapi mempermudah bagian “convert image to spreadsheet”.

## Langkah 2: Muat Gambar yang Ingin Diproses

Sekarang kita benar‑benarnya **load image for OCR**. SDK mengharapkan objek `Image`, jadi kita akan membungkus jalur file kita dengan metode pembantu `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Pro tip:** Simpan file gambar Anda dalam folder khusus (`assets/` atau `data/`) dan gunakan jalur relatif. Dengan begitu skrip tetap portabel di berbagai mesin.

## Langkah 3: Jalankan Proses Pengenalan

Dengan gambar terlampir, kita akhirnya dapat memberi tahu mesin untuk **ocr read tables**. Pemanggilan `recognize()` mengembalikan objek hasil yang berisi semua yang ditemukan mesin—blok teks, baris, dan, yang paling penting bagi kami, tabel.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Why we check:** Beberapa gambar mungkin berisik atau batas tabel samar, sehingga mesin tidak mendeteksinya. Mencatat peringatan memberi Anda umpan balik awal tanpa menghentikan skrip.

## Langkah 4: Ekstrak Baris dan Sel Setiap Tabel

Inilah tempat keajaiban sebenarnya terjadi. Kami akan mengiterasi setiap tabel yang terdeteksi, mengambil setiap baris, lalu teks setiap sel. List comprehension internal membuat kode ringkas, namun kami tetap akan menjelaskan alurnya.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**What’s going on?**  

- `enumerate(..., start=1)` memberikan nomor tabel yang ramah untuk pencatatan.  
- `row_obj.get_cells()` mengembalikan setiap objek sel; `cell.get_text()` mengambil string yang didekode OCR.  
- Kami menyimpan baris dalam `rows_data`, lalu menyerahkannya ke `pandas.DataFrame` yang secara otomatis menyelaraskan kolom.  
- Blok `print` mencerminkan **essential output** yang ditampilkan dalam cuplikan asli, sehingga Anda dapat memverifikasi hasil secara langsung.

**Edge case handling:** Jika sebuah baris memiliki jumlah sel yang berbeda dari yang lain, `pandas` akan mengisi tempat yang kosong dengan `NaN`. Anda dapat membersihkan DataFrame nanti dengan `df.fillna('')` jika lebih suka string kosong.

## Langkah 5: Simpan Tabel yang Diekstrak ke Spreadsheet

Sekarang kita memiliki daftar DataFrames, mengubahnya menjadi buku kerja Excel (atau file CSV) sangat mudah. Ini memenuhi tujuan “convert image to spreadsheet”.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Why Excel?** Kebanyakan pengguna bisnis menyukai `.xlsx`. Jika Anda lebih suka CSV, ganti loop dengan `df.to_csv(f"table_{idx}.csv", index=False)`.

## Skrip Lengkap, Siap‑Jalankan

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel dan jalankan.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Expected console output** (asumsi tabel sederhana 2×3):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

Dan Anda akan menemukan `extracted_tables.xlsx` di folder skrip, setiap tabel pada lembar terpisah.

## Pertanyaan yang Sering Diajukan & Tips

| Pertanyaan | Jawaban |
|------------|---------|
| **Bisakah saya menggunakan perpustakaan OCR yang berbeda?** | Tentu saja. Polanya tetap sama: muat gambar → kenali → iterasi pada `get_tables()`. Cukup ganti impor dan nama objek. |
| **Bagaimana jika gambar saya berisik?** | Lakukan pra‑pemrosesan dengan OpenCV (thresholding, deskew) sebelum memberi ke mesin OCR. Reduksi noise sering meningkatkan akurasi **ocr extract table data**. |
| **Apakah saya perlu menginstal `openpyxl`?** | Ya, `pandas` menggunakannya di balik layar untuk output Excel. Instal dengan `pip install openpyxl`. |
| **Bagaimana cara menangani sel yang digabung?** | Beberapa SDK menyediakan `cell.is_merged()`; Anda dapat mendeteksi dan menyebarkan nilai ke seluruh rentang yang digabung secara manual. |
| **Apakah ada cara untuk mengekstrak hanya tabel tertentu?** | Filter dengan `table_obj.get_confidence()` atau dengan memeriksa kata kunci header sebelum memproses. |

## Penutup

Anda kini memiliki solusi lengkap end‑to‑end untuk **extract tables from image**, mengonversi hasil menjadi spreadsheet yang rapi, dan bahkan menangani beberapa tabel dalam satu gambar. Skrip ini menunjukkan cara **load image for OCR**, **ocr read tables**, dan **ocr extract table data** sambil tetap fleksibel untuk variasi dunia nyata.

Apa selanjutnya? Coba beri mesin OCR halaman PDF yang dirender sebagai gambar, atau bereksperimen dengan bahasa dan font yang berbeda. Anda juga dapat mengalirkan DataFrames langsung ke basis data atau alat pelaporan—imajinasi Anda adalah batasnya.

Jika Anda menemukan panduan ini bermanfaat, silakan bagikan, beri bintang pada repositori yang menyimpan SDK, atau tinggalkan komentar dengan trik Anda sendiri. Selamat coding, semoga tabel Anda selalu terurai dengan sempurna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}