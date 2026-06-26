---
category: general
date: 2026-06-25
description: Cara melakukan OCR dengan Aspose OCR Python – pelajari cara memuat OCR
  gambar, memproses OCR gambar, dan mengekstrak hasil JSON dalam hitungan menit.
draft: false
keywords:
- how to perform OCR
- aspose OCR python
- load image OCR
- process image OCR
language: id
og_description: Cara melakukan OCR dengan Aspose OCR Python. Ikuti panduan ini untuk
  memuat OCR gambar, memproses OCR gambar, dan mengurai output JSON dengan mudah.
og_title: Cara Melakukan OCR dengan Aspose OCR Python
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  headline: How to Perform OCR with Aspose OCR Python
  type: TechArticle
- description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  name: How to Perform OCR with Aspose OCR Python
  steps:
  - name: Creating an OCR engine instance.
    text: Creating an OCR engine instance.
  - name: Loading an image for OCR.
    text: Loading an image for OCR.
  - name: Processing the image OCR.
    text: Processing the image OCR.
  - name: Converting the result to JSON.
    text: Converting the result to JSON.
  - name: Parsing and printing useful information.
    text: Parsing and printing useful information.
  - name: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
    text: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
  - name: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
    text: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
  - name: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
    text: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Cara Melakukan OCR dengan Aspose OCR Python
url: /id/python-java/general/how-to-perform-ocr-with-aspose-ocr-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR dengan Aspose OCR Python

Pernah bertanya‑tanya **bagaimana melakukan OCR** pada kwitansi, faktur, atau dokumen ter‑scan menggunakan Python? Anda tidak sendirian. Dalam banyak proyek dunia nyata, mengekstrak teks dari gambar adalah langkah pertama menuju otomatisasi, analitik, atau pengarsipan.  

Kabar baiknya? Dengan **Aspose OCR Python** Anda dapat memuat OCR gambar, memproses OCR gambar, dan mendapatkan payload JSON yang rapi hanya dalam beberapa baris kode. Di bawah ini Anda akan melihat skrip lengkap yang siap dijalankan, plus penjelasan di balik setiap langkah sehingga Anda benar‑benar memahami *mengapa* kode terlihat seperti itu.

## Apa yang Dibahas dalam Tutorial Ini

- Menyiapkan mesin Aspose OCR di Python  
- **Load image OCR** dengan benar, menangani format umum seperti TIFF, PNG, dan JPEG  
- **Process image OCR** dan mengonversi hasilnya ke JSON  
- Mengurai JSON untuk mengambil informasi berguna (kata, skor kepercayaan, dll.)  
- Tips untuk pemecahan masalah, penanganan kasus tepi, dan ide langkah selanjutnya  

Tidak diperlukan pengalaman sebelumnya dengan Aspose; cukup lingkungan Python 3 yang berfungsi dan file gambar yang ingin Anda baca.

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.8+ | Aspose OCR’s wheels target modern interpreters |
| `aspose-ocr` package (`pip install aspose-ocr`) | Perpustakaan inti yang melakukan pekerjaan berat |
| Sebuah gambar contoh (misalnya `receipt.tif`) | Kita memerlukan sesuatu untuk dimasukkan ke mesin |
| Pengetahuan dasar `json` | Kita akan mengurai output OCR menjadi dict Python |

> **Pro tip:** Jika Anda menggunakan Windows, jalankan command prompt sebagai Administrator saat menginstal paket untuk menghindari masalah izin.

---

## Cara Melakukan OCR dengan Aspose OCR Python

Berikut adalah **skrip lengkap** yang dapat Anda salin‑tempel ke file bernama `ocr_demo.py`. Skrip ini berisi semuanya—dari impor hingga output akhir—sehingga Anda dapat menjalankannya langsung.

```python
#!/usr/bin/env python3
"""
How to Perform OCR with Aspose OCR Python

This script demonstrates:
1. Creating an OCR engine instance.
2. Loading an image for OCR.
3. Processing the image OCR.
4. Converting the result to JSON.
5. Parsing and printing useful information.
"""

import json
import aspose.ocr as ocr
import os
import sys

# ----------------------------------------------------------------------
# Step 1: Create an OCR engine instance
# ----------------------------------------------------------------------
# The engine holds configuration (language, recognition mode, etc.).
# For most cases the defaults work fine, but you can tweak them later.
engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Step 2: Load image OCR
# ----------------------------------------------------------------------
# Aspose can read many formats; here we use a TIFF because receipts often
# come as multi‑page scans. Adjust the path to point at your own file.
image_path = os.path.join("YOUR_DIRECTORY", "receipt.tif")
if not os.path.isfile(image_path):
    sys.stderr.write(f"❌ Image not found: {image_path}\n")
    sys.exit(1)

# The Image.load method decodes the file into an in‑memory object.
image = ocr.Image.load(image_path)

# ----------------------------------------------------------------------
# Step 3: Process image OCR
# ----------------------------------------------------------------------
# The recognize() call runs the OCR engine on the supplied image.
# It returns an OcrResult object that we can later serialize.
result = engine.recognize(image)

# ----------------------------------------------------------------------
# Step 4: Convert the recognition result to JSON
# ----------------------------------------------------------------------
# Aspose gives us a handy to_json() method; we then feed the string
# into Python's json module for a native dict.
json_payload = result.to_json()
parsed = json.loads(json_payload)

# ----------------------------------------------------------------------
# Step 5: Inspect the parsed data
# ----------------------------------------------------------------------
# The structure contains keys like "words", "lines", and "pages".
# We'll print a few samples to prove it works.
print("\n🔎 JSON keys:", list(parsed.keys()))
if parsed.get("words"):
    print("First word entry:", parsed["words"][0])
else:
    print("⚠️ No words detected – check image quality or language settings.")
```

### Output yang Diharapkan

Saat Anda menjalankan `python ocr_demo.py` (dengan asumsi gambar ada dan dapat dibaca), Anda akan melihat sesuatu yang mirip dengan:

```
🔎 JSON keys: ['pages', 'lines', 'words', 'language', 'confidence']
First word entry: {'text': 'Total', 'confidence': 0.98, 'rectangle': {...}}
```

Konten tepatnya bervariasi tergantung gambar sumber, tetapi keberadaan array `"words"` menegaskan bahwa **process image OCR** berhasil.

---

## Load Image OCR – Tips & Kesalahan Umum

1. **Format file penting** – TIFF bekerja sangat baik untuk dokumen ter‑scan, PNG biasanya lebih baik untuk screenshot, dan JPEG untuk foto.  
2. **Resolusi** – Aspose OCR memberikan hasil terbaik dengan 300 dpi atau lebih. Jika Anda melihat skor kepercayaan rendah, pertimbangkan untuk meningkatkan resolusi gambar sebelum memuatnya.  
3. **File multi‑halaman** – Jika TIFF Anda berisi beberapa halaman, `image = ocr.Image.load(path)` akan menghasilkan sebuah stack; Anda dapat mengiterasi dengan `for page in image.pages:` dan memanggil `engine.recognize(page)` untuk tiap halaman.

> **Mengapa langkah ini krusial:** Memuat gambar dengan benar memastikan mesin OCR menerima data piksel yang bersih. Gambar yang rusak atau format yang tidak didukung akan menyebabkan `engine.recognize` melempar pengecualian, menghentikan alur kerja Anda.

---

## Process Image OCR – Opsi Lanjutan

Aspose OCR menyediakan beberapa properti pada objek `OcrEngine`:

| Properti | Kasus penggunaan |
|----------|-------------------|
| `engine.language = ocr.Language.English` | Memaksa bahasa Inggris ketika gambar berisi skrip campuran |
| `engine.recognition_mode = ocr.RecognitionMode.TextDetection` | Lebih cepat, tetapi kurang akurat; cocok untuk pratinjau cepat |
| `engine.auto_rotate = True` | Secara otomatis memperbaiki halaman yang diputar (berguna untuk kwitansi) |

Anda dapat mengatur properti ini sebelum langkah 3 untuk menyempurnakan fase **process image OCR**. Contohnya:

```python
engine.language = ocr.Language.English
engine.auto_rotate = True
```

---

## Memahami Output Aspose OCR Python

Payload JSON mengikuti skema yang dapat diprediksi:

- **pages** – Daftar objek halaman, masing‑masing dengan dimensi dan info rotasi.  
- **lines** – Kata‑kata yang dikelompokkan pada baseline yang sama. Berguna untuk merekonstruksi paragraf.  
- **words** – Objek kata individual yang berisi `text`, `confidence`, dan `rectangle` dengan koordinat.  
- **language** – Kode bahasa yang terdeteksi (misalnya "en").  
- **confidence** – Kepercayaan keseluruhan untuk seluruh dokumen.

Mengetahui struktur ini memungkinkan Anda mengekstrak tepat apa yang Anda butuhkan. Misalnya, untuk mengambil semua kata dengan confidence < 0.9 (potensi kesalahan OCR), Anda dapat menambahkan:

```python
low_confidence = [w for w in parsed["words"] if w["confidence"] < 0.9]
print("Potentially mis‑read words:", low_confidence)
```

---

## Kasus Tepi & Cara Menanganinya

| Situasi | Penanganan yang disarankan |
|---------|----------------------------|
| **Hasil kosong** (tidak ada kata) | Periksa kualitas gambar, pastikan bahasa yang tepat telah disetel, dan mungkin tingkatkan DPI. |
| **PDF multi‑halaman** | Konversi halaman PDF ke gambar terlebih dahulu (misalnya menggunakan `pdf2image`) lalu beri setiap halaman ke mesin OCR. |
| **Skrip non‑Latin** | Instal paket bahasa tambahan via `engine.add_language(ocr.Language.ChineseSimplified)`. |
| **File besar** | Proses secara bertahap; gunakan kembali instance `OcrEngine` yang sama untuk menghindari alokasi memori berlebih. |

---

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabung)

Berikut versi ringkas yang dapat Anda letakkan di notebook Jupyter atau skrip. Skrip ini mencakup penanganan error, pengaturan opsional, dan mencetak ringkasan yang rapi.

```python
import json, os, sys, aspose.ocr as ocr

def perform_ocr(image_path: str):
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Create engine and tweak settings (optional)
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English   # ensures English detection
    engine.auto_rotate = True                # correct rotated scans

    # Load and recognize
    image = ocr.Image.load(image_path)
    result = engine.recognize(image)

    # Convert to JSON and parse
    parsed = json.loads(result.to_json())
    return parsed

if __name__ == "__main__":
    img = os.path.join("YOUR_DIRECTORY", "receipt.tif")
    try:
        data = perform_ocr(img)
        print("\n🔎 JSON keys:", list(data.keys()))
        print("First word:", data["words"][0] if data.get("words") else "No words")
    except Exception as exc:
        sys.stderr.write(f"❗ OCR failed: {exc}\n")
```

Menjalankan ini akan memberikan output ringkas yang sama seperti sebelumnya,

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}