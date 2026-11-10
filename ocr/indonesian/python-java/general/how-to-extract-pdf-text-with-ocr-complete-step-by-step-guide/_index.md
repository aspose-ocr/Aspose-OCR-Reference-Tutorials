---
category: general
date: 2026-03-26
description: Cara mengekstrak teks PDF menggunakan OCR. Pelajari cara memuat PDF sebagai
  gambar, mengenali teks PDF, dan mengekstrak teks dari PDF dengan contoh Python sederhana.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: id
og_description: Cara mengekstrak teks PDF menggunakan OCR. Panduan ini menunjukkan
  cara memuat PDF sebagai gambar, mengenali teks PDF, dan mengekstrak teks dari PDF
  menggunakan Python.
og_title: Cara Mengekstrak Teks PDF dengan OCR – Tutorial Lengkap
tags:
- OCR
- Python
- PDF processing
title: Cara Mengekstrak Teks PDF dengan OCR – Panduan Lengkap Langkah demi Langkah
url: /id/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekstrak Teks PDF dengan OCR – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya-tanya **cara mengekstrak PDF** yang sebenarnya hanya gambar hasil pemindaian? Anda tidak sendirian—banyak pengembang menemui hal ini ketika mereka membutuhkan konten yang dapat dicari tetapi hanya memiliki PDF berupa gambar. Kabar baik? Beberapa baris kode dan perpustakaan OCR yang solid dapat mengubah PDF bergambar itu menjadi teks biasa dalam sekejap.  

Dalam tutorial ini kami akan membahas **cara menggunakan OCR** untuk memuat PDF sebagai gambar, mengenali teks PDF, dan akhirnya **mengekstrak teks dari PDF** dengan panjang berapa pun. Pada akhir tutorial Anda akan memiliki skrip yang dapat dijalankan, penjelasan jelas setiap langkah, serta beberapa tips untuk menghindari jebakan umum.

## Apa yang Anda Butuhkan

- Python 3.9 atau lebih baru (kode ini juga berfungsi pada 3.10+)  
- Paket Python `ocr` (atau perpustakaan OCR kompatibel apa pun yang menyediakan `OcrEngine`, `OcrEngineMode`, dan `Imaging.Image`)  
- PDF multi‑halaman yang ingin Anda proses (untuk demo kita akan menyebutnya `multi_page.pdf`)  
- Pemahaman dasar tentang lingkungan virtual (opsional tetapi disarankan)

> **Pro tip:** Jika Anda menggunakan Windows, pertimbangkan untuk memakai Anaconda Prompt; pada macOS/Linux, perintah sederhana `python -m venv venv && source venv/bin/activate` sudah cukup.

## Langkah 1: Instalasi Perpustakaan OCR

Pertama, dapatkan paket OCR dari PyPI. Contoh di bawah menggunakan paket fiktif `ocr` yang meniru API yang ditunjukkan dalam cuplikan kode, tetapi sebagian besar perpustakaan dunia nyata (seperti `pytesseract` + `pdf2image`) mengikuti pola yang sama.

```bash
pip install ocr
```

Jika Anda menggunakan mesin yang berbeda, ganti `ocr` dengan nama yang sesuai (misalnya, `pip install pytesseract pdf2image`).

## Langkah 2: Inisialisasi Mesin OCR

Membuat instance mesin adalah fondasi **cara mengekstrak PDF**. Anggap mesin sebagai otak yang akan menafsirkan piksel di setiap halaman PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Mengapa ini penting:** `set_engine_mode` memungkinkan Anda menukar kecepatan dengan akurasi. `DEFAULT` adalah pilihan seimbang; jika Anda membutuhkan presisi lebih tinggi, beralihlah ke `HIGH_ACCURACY` (jika perpustakaan mendukungnya).

## Langkah 3: Muat PDF sebagai Objek Gambar

OCR bekerja pada gambar, bukan kontainer PDF, jadi kita harus mengonversi PDF menjadi representasi gambar terlebih dahulu. Metode `Imaging.Image.load` menangani PDF multi‑halaman secara otomatis.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Kasus tepi:** Beberapa perpustakaan hanya menerima gambar satu‑halaman. Dalam skenario itu, Anda harus melakukan loop pada setiap halaman menggunakan `pdf2image.convert_from_path`. Panggilan `load` kami mengabstraksi hal itu, menjadikan **memuat pdf sebagai gambar** satu baris kode.

## Langkah 4: Kenali Teks pada Semua Halaman

Sekarang masuk ke inti **mengenali teks PDF**. Mesin memindai setiap halaman, mengembalikan daftar objek hasil—satu per halaman.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Setiap `page_result` berisi metode seperti `get_text()` (teks polos) dan `get_confidence()` (metrik kualitas opsional).  

> **Tip:** Jika Anda hanya membutuhkan halaman pertama, panggil `recognize(pdf_image[0])` alih‑alih pembantu multi‑halaman.

## Langkah 5: Iterasi Hasil dan Keluarkan Teks yang Diekstrak

Akhirnya, kami melakukan loop pada hasil, mencetak teks setiap halaman. Ini menyelesaikan alur kerja **mengekstrak teks dari PDF**.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Output yang Diharapkan

Jika `multi_page.pdf` berisi tiga halaman dengan kata “Hello”, “World”, dan “Python”, Anda akan melihat:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

Itu saja—PDF Anda kini sepenuhnya dapat dicari dan teksnya siap untuk diproses lebih lanjut (pengindeksan, analisis sentimen, apa saja yang Anda butuhkan).

## Langkah 6: Menangani Kendala Umum

| Masalah | Mengapa Terjadi | Perbaikan Cepat |
|---------|----------------|-----------------|
| **Output kosong** | Halaman PDF dipindai dengan DPI rendah, sehingga karakter tidak dapat dibedakan. | Perbesar gambar sebelum OCR: `pdf_image = pdf_image.resize(300)` (300 DPI adalah titik optimal). |
| **Karakter sampah** | Alfabet non‑Latin memerlukan paket bahasa. | Muat model bahasa yang sesuai: `ocr_engine.load_language('spa')` untuk bahasa Spanyol, dll. |
| **Memori meluap pada PDF besar** | Memuat semua halaman sekaligus mengonsumsi RAM. | Proses halaman dalam batch: `for img in pdf_image.split(batch=10): …` (pseudo‑code). |
| **Performa lambat** | Menggunakan `DEFAULT` pada dokumen besar dapat terasa lambat. | Beralih ke mode `FAST` atau jalankan OCR secara paralel menggunakan `concurrent.futures`. |

## Bonus: Menyimpan Teks yang Diekstrak ke File

Sebagian besar alur kerja dunia nyata memerlukan teks yang disimpan. Berikut helper kecil yang menulis semuanya ke `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Sekarang Anda dapat memasukkan `output.txt` ke mesin pencari, basis data, atau model NLP apa pun.

## Menggabungkan Semua – Skrip Lengkap

Di bawah ini adalah program lengkap yang siap dijalankan. Salin‑tempel, sesuaikan jalur file, dan Anda siap mulai.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Jalankan:

```bash
python extract_pdf_ocr.py
```

Anda akan melihat konten setiap halaman dicetak ke konsol, diikuti dengan konfirmasi bahwa file `extracted_text.txt` telah dibuat.

## Kesimpulan

Kami telah membahas **cara mengekstrak PDF** dari dokumen yang hanya berisi gambar menggunakan mesin OCR, mulai dari instalasi perpustakaan hingga menangani hasil multi‑halaman dan menyimpan output. Anda kini tahu **cara menggunakan OCR**, cara **memuat PDF sebagai gambar**, dan cara **mengenali teks PDF** dengan andal.  

Langkah selanjutnya? Coba ganti mode mesin default ke pengaturan akurasi tinggi, bereksperimen dengan paket bahasa untuk PDF multibahasa, atau alirkan teks yang diekstrak ke indeks pencarian teks penuh seperti Elasticsearch. Langit adalah batasnya setelah Anda menguasai dasar‑dasar mengekstrak teks dari file PDF.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="diagram alur cara mengekstrak pdf"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}