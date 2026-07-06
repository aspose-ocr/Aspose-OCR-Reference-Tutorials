---
category: general
date: 2026-07-05
description: Ekstrak tabel dari gambar menggunakan Python OCR. Pelajari cara mengekstrak
  tabel, mengonversi gambar ke TSV, dan kuasai teknik OCR tabel gambar dengan Python.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: id
og_description: Ekstrak tabel dari gambar dengan Python OCR. Panduan ini menunjukkan
  cara mengekstrak tabel, mengonversi gambar ke TSV, dan menggunakan alat Python OCR
  untuk gambar tabel.
og_title: Ekstrak Tabel dari Gambar – Konversi Gambar ke TSV dengan Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Ekstrak Tabel dari Gambar – Konversi Gambar ke TSV dengan Python
url: /id/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Tabel dari Gambar – Konversi Gambar ke TSV dengan Python

Pernah bertanya-tanya bagaimana cara mengekstrak tabel dari gambar tanpa membuat frustasi? Dalam tutorial ini kami akan membahas **cara mengekstrak tabel** dari sebuah gambar menggunakan pustaka `aocr`, kemudian mengubah data tersebut menjadi file TSV yang rapi. Tidak ada sihir, hanya beberapa baris Python dan sedikit pemrosesan pasca‑AI.

Jika Anda pernah mencoba menyalin‑tempel tabel dari faktur yang dipindai atau tangkapan layar dan berakhir dengan hasil yang berantakan, Anda akan menghargai mengapa pendekatan berbasis OCR patut dikuasai. Pada akhir tutorial, Anda akan dapat memasukkan gambar tabel apa pun ke Python dan mendapatkan nilai yang dipisahkan tab bersih, siap untuk spreadsheet atau basis data.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut di mesin Anda:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.9+ | Paket `aocr` menargetkan runtime Python modern. |
| `aocr` library (`pip install aocr`) | Menyediakan mesin OCR dan post‑processor AI yang akan kita gunakan. |
| File gambar yang berisi tabel (PNG, JPG, dll.) | Data sumber yang akan kami ekstrak. |
| Opsional: lingkungan virtual | Menjaga dependensi terisolasi—sangat disarankan. |

Menyiapkan hal‑hal ini akan menghindarkan Anda dari gangguan di tengah panduan.

---

## Instalasi Dependensi

Pertama, mari instal alat OCR. Buka terminal dan jalankan:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Tips profesional:** Jika Anda mengalami kesalahan izin, tambahkan `--user` ke perintah `pip install` atau gunakan `pipx` untuk instalasi global.

---

## Langkah 1 – Inisialisasi Mesin OCR

Mesin adalah inti dari proses. Anggaplah sebagai “otak” yang melihat setiap piksel dan memutuskan karakter apa yang berada di mana.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Mengapa kita membuat instance mesin alih‑alih memanggil satu fungsi? Objek mesin memungkinkan kita menambahkan post‑processor khusus nanti, memberi kontrol detail atas output—penting ketika Anda membutuhkan akurasi **ocr table image python**.

---

## Langkah 2 – Menambahkan AI Post‑Processor

`aocr` dilengkapi dengan post‑processor AI ringan yang membersihkan hasil OCR mentah sambil mempertahankan batas sel. Tidak diperlukan argumen tambahan, sehingga kode tetap rapi.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Jika Anda melewatkan langkah ini, Anda masih akan mendapatkan teks mentah, tetapi struktur tabel akan berisik—bayangkan spreadsheet di mana setiap sel adalah misteri. Post‑processor melakukan pekerjaan berat menyelaraskan teks ke grid aslinya.

---

## Langkah 3 – Memuat Gambar Tabel Anda

Anda dapat memuat gambar dari jalur apa pun, tetapi untuk kejelasan kami akan merujuk ke direktori placeholder. Ganti `"YOUR_DIRECTORY/invoice_table.png"` dengan jalur sebenarnya ke file Anda.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Catatan:** `aocr.Image` secara otomatis mendeteksi format gambar dan menormalkan saluran warna, jadi Anda tidak perlu memproses file terlebih dahulu kecuali sangat rusak.

---

## Langkah 4 – Lakukan OCR Terstruktur

Sekarang mesin memindai gambar dan mengembalikan objek tabel mentah. Objek ini berisi baris, kolom, dan teks mentah untuk setiap sel.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Mengapa menggunakan `recognize_structured` alih‑alih pemanggilan `recognize` umum? Varian terstruktur berusaha menebak batas baris/kolom, memberikan hasil mirip matriks yang jauh lebih mudah dikonversi ke TSV nanti.

---

## Langkah 5 – Bersihkan Data dengan AI Post‑Processor

Menjalankan post‑processor memperbaiki output mentah: menghapus karakter asing, menggabungkan fragmen terpisah, dan memastikan teks setiap sel ter‑align dengan benar.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Jika Anda memeriksa `processed_table.table`, Anda akan melihat daftar baris, setiap baris berupa daftar objek `Cell`. Setiap `Cell` memiliki atribut `.text` yang berisi string yang telah dibersihkan.

---

## Langkah 6 – Ekspor Tabel sebagai TSV

Langkah terakhir adalah mengubah data yang telah diproses menjadi file nilai dipisahkan tab (TSV)—tepat apa yang Anda butuhkan ketika ingin **mengonversi gambar ke TSV** untuk Excel atau Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Menjalankan skrip mencetak setiap baris ke konsol (jika Anda suka) dan menulis file TSV bersih yang dapat Anda buka di program spreadsheet apa pun.

### Verifikasi Cepat

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Anda harus melihat kolom yang ter‑align rapi, seperti:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Jika output terlihat berantakan, periksa kembali kualitas gambar (ketajaman, kontras) dan pertimbangkan menyesuaikan pengaturan mesin OCR—`engine.set_config(...)` memungkinkan Anda mengatur model bahasa dan ambang kepercayaan.

---

## Menangani Kasus Pinggiran Umum

| Situasi | Solusi yang Disarankan |
|---------|------------------------|
| **Gambar miring** | Pra‑rotasi menggunakan `Pillow` (`Image.rotate`) sebelum memberikan ke `aocr`. |
| **Kontras rendah** | Terapkan equalisasi histogram (`cv2.equalizeHist`) untuk meningkatkan keterbacaan. |
| **Sel yang digabung** | Post‑process TSV untuk memisahkan sel berdasarkan delimiter yang diketahui atau gunakan flag `merge_cells=False` jika tersedia. |
| **PDF multi‑halaman** | Konversi setiap halaman menjadi gambar terlebih dahulu (`pdf2image`) dan jalankan pipeline dalam loop. |

Penyesuaian ini menjaga alur kerja **ocr table image python** Anda tetap kuat di berbagai materi sumber.

---

## Skrip Lengkap – Solusi Satu‑Pintu

Berikut adalah skrip lengkap yang siap dijalankan yang menggabungkan semua langkah yang dibahas. Simpan sebagai `extract_table.py` dan jalankan `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara mengekstrak tabel dari gambar menggunakan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Cara Mengekstrak Teks dari Gambar dengan Menyiapkan Persegi Panjang dalam OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}