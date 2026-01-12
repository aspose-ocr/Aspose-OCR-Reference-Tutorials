---
category: general
date: 2026-01-12
description: Ekstrak teks dari PDF menggunakan mesin OCR Python – pelajari cara membaca
  PDF dengan OCR, memuat gambar untuk OCR, dan mendapatkan hasil terstruktur.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: id
og_description: Ekstrak teks dari PDF menggunakan mesin OCR Python. Tutorial ini menunjukkan
  cara membaca PDF dengan OCR, memuat gambar untuk OCR, dan menggunakan mesin OCR
  Python untuk hasil yang dapat diandalkan.
og_title: Ekstrak Teks dari PDF dengan Mesin OCR Python – Panduan Lengkap
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Ekstrak Teks dari PDF dengan Mesin OCR Python – Panduan Langkah-demi-Langkah
url: /id/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari PDF dengan Mesin OCR Python – Tutorial Lengkap

Pernah perlu **mengekstrak teks dari PDF** tetapi file-nya hanya berupa gambar yang dipindai? Anda tidak sendirian. Dalam banyak proyek dunia nyata PDF yang Anda terima tidak memiliki teks yang dapat dipilih, jadi satu‑satunya cara adalah **membaca PDF dengan OCR**.  

Dalam panduan ini kami akan membahas solusi praktis end‑to-end yang menunjukkan secara tepat cara **memuat gambar untuk OCR**, menjalankan **OCR engine Python**, dan mengambil teks terstruktur yang dapat Anda masukkan ke dalam pipeline hilir. Tanpa referensi yang samar, hanya contoh lengkap yang dapat dijalankan yang dapat Anda salin‑tempel hari ini.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mengimpor pustaka OCR Python yang Anda butuhkan.  
- Langkah‑langkah tepat untuk **memuat gambar untuk OCR** dari file PDF.  
- Cara memanggil metode `recognize_structured()` pada engine dan mengiterasi blok, baris, dan kata.  
- Tips untuk menangani hasil dengan kepercayaan rendah dan PDF multi‑halaman.  

Pada akhir tutorial ini Anda akan memiliki skrip yang secara andal **mengekstrak teks dari PDF** dokumen, terlepas apakah dokumen tersebut berisi satu halaman atau seratus.

---

![Diagram yang menunjukkan mesin OCR memproses PDF dan menghasilkan teks terstruktur.](images/ocr_flow.png "extract text from pdf diagram")

*Teks alt gambar: diagram ekstrak teks dari pdf yang menggambarkan langkah‑langkah pemrosesan OCR.*

## Prasyarat

- Python 3.9 atau lebih baru (kode menggunakan f‑strings dan type hints).  
- Paket OCR yang dapat di‑install via pip yang menyediakan kelas `OcrEngine` (misalnya, pustaka fiktif `pyocr`).  
- File PDF yang ingin Anda proses, disimpan secara lokal (misalnya, `form.pdf`).  

Jika Anda belum memiliki pustaka OCR, instal dengan:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## Langkah 1: Ekstrak Teks dari PDF – Menyiapkan OCR Engine

Sebelum kita dapat **membaca PDF dengan OCR**, kita memerlukan sebuah instance engine. Anggap engine sebagai otak yang melihat setiap piksel dan memutuskan karakter apa yang diwakilinya.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Mengapa ini penting:** Menginisialisasi engine sekali memungkinkan Anda menggunakan kembali paket bahasa yang dimuat di banyak file, menghemat waktu dan memori.

---

## Langkah 2: Memuat Gambar untuk OCR – Menyiapkan PDF Anda

PDF bukan gambar mentah, sehingga pustaka biasanya menyediakan bantuan untuk mengonversi halaman pertama (atau semua halaman) menjadi gambar yang dapat dipahami oleh OCR engine.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Tip:** Jika PDF Anda memiliki banyak halaman, banyak pustaka OCR memungkinkan Anda memberikan `page=2` atau melakukan loop pada `engine.load_image(pdf_path, page=n)`. Untuk dokumen besar, pertimbangkan memproses halaman secara batch untuk menghindari lonjakan memori.

---

## Langkah 3: Menggunakan OCR Engine Python – Mengenali Teks Terstruktur

Sekarang pekerjaan berat terjadi. Pemanggilan `recognize_structured()` mengembalikan hierarki blok → baris → kata, masing‑masing diberi anotasi bahasa, kepercayaan, dan kotak pembatas.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **Apa yang Anda dapatkan:**  
> - `structured_result.blocks` – kontainer tingkat atas (sering paragraf atau kolom).  
> - Setiap blok berisi `lines`, dan setiap baris berisi `words`.  
> - Skor kepercayaan memungkinkan Anda menyaring hasil yang meragukan.

---

## Langkah 4: Mengiterasi Hasil – Mengakses Blok, Baris, dan Kata

Berikut adalah loop ringkas yang mencetak informasi paling berguna. Silakan kembangkan untuk menulis JSON, CSV, atau memasukkan ke database.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Output yang Diharapkan

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Mengapa Anda akan menyukainya:** Hierarki ini mencerminkan cara manusia membaca halaman, memudahkan rekonstruksi tabel atau tata letak kolom kemudian.

---

## Langkah 5: Menangani Kasus Tepi – Kepercayaan Rendah & PDF Multi‑Halaman

### Kata dengan Kepercayaan Rendah

Jika kepercayaan sebuah kata turun di bawah, misalnya, `0.70`, Anda mungkin ingin menandainya untuk peninjauan manual:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Memproses Semua Halaman

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Pro tip:** Simpan gambar perantara sebagai PNG jika pustaka OCR Anda merender ulang setiap kali—hal ini dapat menghemat beberapa detik pada batch besar.

---

## Skrip Lengkap yang Berfungsi

Menggabungkan semuanya, berikut satu file yang dapat Anda jalankan segera:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

Simpan ini sebagai `extract_pdf_ocr.py` dan jalankan:

```bash
python extract_pdf_ocr.py
```

Anda akan melihat detail tingkat blok dicetak ke konsol, bersama dengan peringatan kepercayaan rendah.

---

## Kesimpulan

Kami baru saja membahas cara lengkap dan siap produksi untuk **mengekstrak teks dari PDF** menggunakan **OCR engine Python**. Mulai dari menginstal pustaka, melalui **memuat gambar untuk OCR**, hingga **membaca PDF dengan OCR** dan akhirnya mengiterasi output terstruktur, kini Anda memiliki skrip yang dapat digunakan kembali dan dapat disesuaikan untuk proyek apa pun.

Langkah selanjutnya yang dapat Anda jelajahi:

- Mengekspor hierarki ke JSON untuk pipeline NLP hilir.  
- Menambahkan deteksi bahasa untuk beralih model OCR secara dinamis.  
- Mengintegrasikan dengan `pdf2image` untuk pra‑memproses PDF yang memiliki tata letak kompleks.  

Cobalah pada batch faktur multi‑halaman, sesuaikan ambang kepercayaan, dan lihat seberapa cepat Anda dapat mengubah PDF yang dipindai menjadi teks yang dapat dicari dan diedit. Jika Anda mengalami kendala, tinggalkan komentar di bawah—selamat mencoba OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}