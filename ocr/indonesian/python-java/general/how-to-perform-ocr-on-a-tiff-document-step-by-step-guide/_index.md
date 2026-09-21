---
category: general
date: 2026-01-12
description: Cara melakukan OCR dengan cepat dan akurat. Pelajari cara menjalankan
  OCR pada dokumen, mengekstrak teks dari TIFF, memuat gambar untuk OCR, dan mengatur
  bahasa OCR di Python.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: id
og_description: Cara melakukan OCR di Python. Tutorial ini menunjukkan cara menjalankan
  OCR pada dokumen, mengekstrak teks dari tiff, memuat gambar untuk OCR, dan mengatur
  bahasa OCR.
og_title: Cara Melakukan OCR pada Dokumen TIFF – Panduan Lengkap
tags:
- OCR
- Python
- Image Processing
title: Cara Melakukan OCR pada Dokumen TIFF – Panduan Langkah demi Langkah
url: /id/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR pada Dokumen TIFF – Panduan Lengkap

Pernah bertanya-tanya **bagaimana melakukan OCR** pada file TIFF yang dipindai tanpa menghabiskan berjam‑jam mencari pustaka yang tepat? Anda tidak sendirian. Banyak pengembang menemui kendala ketika harus mengekstrak teks dari gambar TIFF, terutama ketika kinerja dan pengaturan bahasa penting.

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui: mulai dari menginstal paket OCR, memuat gambar untuk OCR, mengatur bahasa OCR, hingga akhirnya **menjalankan OCR pada dokumen** dan mendapatkan teks bersih. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang dapat Anda sisipkan ke proyek mana pun.

> **Tip pro:** Meskipun contoh ini menggunakan modul `ocr` generik, konsep yang sama berlaku untuk Tesseract, EasyOCR, atau mesin OCR modern apa pun yang menyediakan API Python.

---

## Apa yang Anda Butuhkan

- Python 3.8+ (versi terbaru apa pun)
- Pustaka OCR yang menyediakan kelas `OcrEngine` (contoh menggunakan paket fiktif `ocr`; ganti dengan paket yang Anda pakai)
- File TIFF multi‑halaman yang ingin diproses (kami sebut `big_document.tif`)
- Mesin dengan setidaknya 4 core CPU jika Anda berencana mengatur jumlah thread

Tanpa layanan eksternal, tanpa kunci cloud—hanya kode lokal yang berjalan dalam hitungan detik.

---

![contoh cara melakukan ocr](/images/ocr-example.png "cara melakukan OCR pada dokumen TIFF")

*Teks alt gambar: cara melakukan OCR pada dokumen TIFF – pratinjau teks yang diekstrak.*

---

## Langkah 1: Instal dan Impor Pustaka OCR

Hal pertama yang harus dilakukan: dapatkan pustaka ke mesin Anda. Kebanyakan paket OCR tersedia di PyPI, jadi cukup `pip install` saja.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Sekarang impor kelas‑kelas yang Anda perlukan. Jika Anda menggunakan Tesseract, baris impor akan berbeda, tetapi sisa kode tetap sama.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Mengapa ini penting:* Mengimpor simbol yang tepat di awal mencegah bentrok namespace di kemudian hari dan membuat skrip lebih mudah dibaca.

---

## Langkah 2: Buat dan Konfigurasikan Mesin OCR (Set OCR Language)

Mengonfigurasi mesin adalah tempat Anda **mengatur bahasa OCR** untuk pengenalan yang akurat. Bahasa Inggris adalah default, tetapi Anda dapat beralih ke Prancis, Jerman, atau bahkan mode multibahasa dengan satu baris kode.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Mengapa 4 thread?** Kebanyakan laptop modern memiliki setidaknya empat core, dan membatasi jumlah thread mencegah proses OCR memonopoli seluruh mesin—terutama berguna saat skrip dijalankan di server bersama.

Jika Anda memerlukan bahasa lain, cukup ganti `ocr.Language.ENGLISH` dengan `ocr.Language.FRENCH`, `ocr.Language.SPANISH`, dll.

---

## Langkah 3: Muat Gambar untuk OCR (Load Image for OCR)

Sekarang kita **memuat gambar untuk OCR**. Metode `Image.load` membaca file TIFF ke memori, menangani dokumen multi‑halaman secara otomatis.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Kasus tepi:* Jika file sangat besar, Anda mungkin kehabisan RAM. Dalam situasi tersebut, pertimbangkan memuat satu halaman pada satu waktu dengan `Image.load_page(page_number)` (jika pustaka mendukungnya).

---

## Langkah 4: Jalankan OCR pada Dokumen

Dengan mesin siap dan gambar sudah dimuat, saatnya **menjalankan OCR pada dokumen**. Metode `process` melakukan pekerjaan berat dan mengembalikan objek hasil.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Di balik layar mesin membagi gambar menjadi blok‑blok teks, menjalankan model pengenalan, dan menyatukan hasilnya. Pemanggilan ini bersifat blocking, artinya skrip menunggu hingga seluruh TIFF selesai diproses—ideal untuk pekerjaan batch.

---

## Langkah 5: Ekstrak Teks dari TIFF dan Verifikasi Output

Akhirnya, kita **mengekstrak teks dari TIFF** dengan mengakses atribut `text` dari hasil. Mari cetak 200 karakter pertama sebagai pemeriksaan cepat.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Output yang diharapkan (contoh):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Jika Anda memerlukan teks lengkap, cukup gunakan `ocr_result.text`. Untuk pemrosesan lanjutan, Anda mungkin ingin menuliskannya ke file `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Contoh Skrip Lengkap yang Siap Jalankan

Menggabungkan semuanya, berikut skrip siap‑jalankan. Ganti nama paket placeholder dengan paket yang sebenarnya Anda instal.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Jalankan skrip dengan:

```bash
python ocr_tiff_example.py
```

Anda akan melihat pratinjau tercetak di konsol dan sebuah file bernama `extracted_text.txt` yang berisi transkripsi lengkap.

---

## Pertanyaan Umum & Kasus Tepi

- **Bagaimana jika TIFF berisi banyak halaman?**  
  Kebanyakan mesin OCR memperlakukan setiap halaman sebagai gambar terpisah secara internal. `ocr_result.text` akan berisi baris baru di antara halaman. Jika Anda memerlukan penanganan per‑halaman, iterasikan dengan `Image.load_page(page_number)`.

- **Bisakah saya memproses PNG atau JPEG alih‑alih TIFF?**  
  Tentu saja. Metode `Image.load` biasanya menerima format apa pun yang didukung oleh Pillow atau pustaka di bawahnya. Cukup ubah ekstensi file.

- **Teks saya berantakan—apakah saya harus mengubah bahasa?**  
  Ya. Langkah **set OCR language** sangat penting untuk dokumen non‑Inggris. Pastikan paket bahasa sudah terpasang (misalnya `tesseract‑lang‑fra` untuk bahasa Prancis).

- **Kehabisan memori?**  
  Kurangi `set_memory_limit` atau proses halaman satu‑per‑satu. Beberapa mesin juga memungkinkan Anda menurunkan skala gambar sebelum pengenalan.

---

## Kesimpulan

Itulah panduan singkat dan lengkap tentang **cara melakukan OCR** pada file TIFF menggunakan Python. Kami telah membahas semua mulai dari instalasi pustaka, konfigurasi mesin (termasuk **set OCR language**), **load image for OCR**, **run OCR on document**, hingga **extract text from tiff**.  

Silakan bereksperimen: ubah jumlah thread, ganti bahasa, atau alirkan output OCR ke pipeline pemrosesan bahasa alami. Langit adalah batasnya setelah Anda menguasai dasar‑dasarnya.

Masih ada pertanyaan? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}