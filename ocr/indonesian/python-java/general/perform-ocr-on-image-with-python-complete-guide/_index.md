---
category: general
date: 2026-07-05
description: Lakukan OCR pada gambar di Python dengan cepat. Pelajari cara memuat
  gambar untuk OCR, mengekstrak teks dari formulir yang dipindai, dan menggunakan
  OCR untuk mengenali gambar di Python.
draft: false
keywords:
- perform OCR on image
- load image for OCR
- how to use OCR Python
- extract text from scanned form
- OCR recognize image Python
language: id
og_description: Lakukan OCR pada gambar di Python. Tutorial ini menunjukkan cara memuat
  gambar untuk OCR, mengekstrak teks dari formulir yang dipindai, dan menggunakan
  OCR untuk mengenali gambar di Python.
og_title: Lakukan OCR pada Gambar dengan Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image in Python quickly. Learn how to load image for
    OCR, extract text from scanned form, and use OCR recognize image Python.
  headline: Perform OCR on Image with Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Lakukan OCR pada Gambar dengan Python – Panduan Lengkap
url: /id/python-java/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar dengan Python – Panduan Lengkap

Pernah membutuhkan untuk **perform OCR on image** file tetapi tidak yakin harus mulai dari mana di Python? Anda tidak sendirian. Baik Anda mendigitalkan kwitansi, mengambil data dari formulir survei yang berisik, atau sekadar mengubah PDF yang dipindai menjadi teks yang dapat dicari, kemampuan mengekstrak teks dari formulir yang dipindai adalah masalah harian bagi banyak pengembang.

Dalam tutorial ini kami akan membimbing Anda melalui **how to use OCR Python** library langkah demi langkah, mulai dari memuat gambar hingga menampilkan hasil yang sudah difilter. Pada akhir tutorial Anda akan tahu persis cara **load image for OCR**, mengonfigurasi ambang kepercayaan, dan memanggil metode **OCR recognize image Python** yang sebenarnya melakukan pekerjaan berat.

> **What you’ll get:** skrip siap‑jalankan yang memuat gambar, menjalankan OCR, dan mencetak teks bersih yang difilter berdasarkan kepercayaan. Tanpa referensi yang samar, tanpa impor yang hilang—hanya solusi lengkap yang dapat disalin‑tempel.

---

## Apa yang Anda Butuhkan

* Python 3.9 atau lebih baru terpasang (kode juga berfungsi pada 3.10+).  
* Paket OCR yang mengikuti API `ocr` yang digunakan di bawah – misalnya, library fiktif `simple-ocr` atau pembungkus apa pun yang mengekspor `OcrEngine`, `Language`, dan `Image`.  
* File gambar (`.png`, `.jpg`, dll.) yang berisi teks yang ingin Anda ekstrak.  
* Terminal atau IDE tempat Anda dapat menjalankan satu skrip Python.

Jika Anda sudah memiliki semuanya, bagus—mari kita mulai.

---

## Lakukan OCR pada Gambar – Menyiapkan Engine

Hal pertama yang harus Anda lakukan adalah membuat instance engine OCR. Anggap engine sebagai otak di balik operasi; ia tahu cara menafsirkan piksel dan mengubahnya menjadi karakter.

```python
# Import the OCR library – replace `ocr` with your actual package name
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Mengapa ini penting:* tanpa engine tidak ada yang dapat diproses. Objek `OcrEngine` menyimpan semua konfigurasi yang akan Anda sesuaikan nanti, seperti bahasa dan ambang kepercayaan.

---

## Muat Gambar untuk OCR – Menyiapkan Formulir yang Dipindai

Sekarang engine sudah ada, kita perlu **load image for OCR**. Metode `Image.load()` dari library membaca file dari disk dan mengubahnya menjadi representasi internal yang dapat dipahami engine.

```python
# Step 2: Load the image you want to process
# Replace the path with the actual location of your noisy form
image_path = "YOUR_DIRECTORY/noisy_form.png"
image = ocr.Image.load(image_path)
```

> **Tip:** Jika Anda menangani PDF, konversi setiap halaman menjadi gambar terlebih dahulu (mis., menggunakan `pdf2image`). Engine OCR hanya menerima gambar raster.

---

## Cara Menggunakan OCR Python – Mengonfigurasi Bahasa dan Kepercayaan

Sebagian besar engine OCR mendukung banyak bahasa dan memungkinkan Anda memfilter karakter dengan kepercayaan rendah. Menetapkan parameter ini lebih awal memastikan Anda hanya mendapatkan teks yang dapat diandalkan.

```python
# Step 3: Choose language and set a confidence threshold
engine.language = ocr.Language.ENGLISH          # you can switch to FR, DE, etc.
engine.min_confidence = 85                     # accept only characters >85 % confidence
```

*Mengapa 85 %?* Pada praktiknya, ambang sekitar 80‑90 % menghilangkan sebagian besar sampah sambil mempertahankan teks yang baik. Silakan sesuaikan berdasarkan kualitas pemindaian Anda.

---

## Ekstrak Teks dari Formulir yang Dipindai – Mengenali Gambar

Dengan engine siap dan gambar sudah dimuat, saatnya sebenarnya **perform OCR on image**. Metode `recognize()` mengembalikan objek hasil yang berisi teks yang diekstrak dan, opsional, data kotak pembatas.

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

Jika library mendukungnya, `result` juga dapat menampilkan `result.confidences` (daftar skor kepercayaan per karakter) dan `result.words` (objek kata terstruktur). Untuk panduan ini kami akan fokus pada output teks biasa.

---

## OCR Recognize Image Python – Menampilkan Hasil yang Difilter

Akhirnya, mari cetak teks yang difilter. Simbol dengan kepercayaan rendah muncul sebagai tanda tanya (`?`) karena kami mengatur `min_confidence` ke 85 %.

```python
# Step 5: Show the filtered text
print("Filtered text:")
print(result.text)
```

### Output yang Diharapkan

```
Filtered text:
Name: John Doe
Date: 2023‑04‑15
Amount: $123.45
Signature: ?
```

Perhatikan bagaimana tanda tangan yang tidak terbaca berubah menjadi `?`. Itulah tepatnya fungsi filter kepercayaan—menjaga output tetap rapi untuk pemrosesan selanjutnya.

---

## Kesalahan Umum dan Tips Pro

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Output kosong** | Gambar terlalu gelap atau beresolusi rendah. | Pra‑proses dengan OpenCV: tingkatkan kontras, ubah ukuran menjadi ≥300 dpi. |
| **Karakter sampah** | Bahasa yang dipilih salah. | Setel `engine.language` agar sesuai dengan dokumen (mis., `ocr.Language.FRENCH`). |
| **Terlalu banyak simbol `?`** | Ambang kepercayaan terlalu tinggi. | Turunkan `engine.min_confidence` ke 70‑80 % untuk pemindaian yang berisik. |
| **Kesalahan Unicode** | Output berisi karakter non‑ASCII tetapi pengkodean konsol salah. | Jalankan `python -X utf8` atau setel `PYTHONIOENCODING=utf-8`. |

**Pro tip:** Jika Anda perlu mengekstrak tabel, jalankan proses kedua dengan engine OCR yang sadar tata letak (seperti `--psm 6` pada Tesseract) setelah Anda memfilter teks mentah.

---

## Skrip Lengkap – Siap Dijalan

Berikut adalah skrip lengkap yang berdiri sendiri yang menggabungkan setiap langkah yang dibahas. Simpan sebagai `perform_ocr.py`, sesuaikan jalur gambar, dan jalankan `python perform_ocr.py`.

```python
# perform_ocr.py
# -------------------------------------------------
# Complete Python script to perform OCR on image,
# load image for OCR, configure engine, and display
# filtered results. Works with any OCR library that
# follows the simple `ocr` API shown here.
# -------------------------------------------------

import ocr  # Replace with your actual OCR package name

def main():
    # 1️⃣ Create the engine
    engine = ocr.OcrEngine()

    # 2️⃣ Configure language and confidence
    engine.language = ocr.Language.ENGLISH
    engine.min_confidence = 85  # Only keep chars >85 % confidence

    # 3️⃣ Load the image (adjust the path)
    image_path = "YOUR_DIRECTORY/noisy_form.png"
    image = ocr.Image.load(image_path)

    # 4️⃣ Recognize the text
    result = engine.recognize(image)

    # 5️⃣ Print the filtered output
    print("Filtered text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

Jalankan, dan Anda akan melihat teks yang difilter dicetak ke konsol—tepat seperti yang dijanjikan oleh langkah **extract text from scanned form**.

---

## Apa Selanjutnya?

Sekarang Anda tahu cara **perform OCR on image** dan **extract text from scanned form**, Anda mungkin ingin menjelajahi:

* **Batch processing** – iterasi melalui direktori gambar untuk menghasilkan CSV hasil.  
* **Post‑processing** – gunakan regex atau spaCy untuk mengekstrak bidang seperti tanggal, jumlah, atau ID.  
* **Integrations** – alirkan output OCR ke basis data, Google Sheets, atau REST API.  

Semua ide ini secara alami melibatkan fungsi inti yang sama yang kami bahas: memuat gambar, mengonfigurasi engine, dan memanggil metode **OCR recognize image Python**.

---

## Kesimpulan

Kami telah membahas contoh lengkap yang siap produksi tentang cara **perform OCR on image** menggunakan Python. Dari **load image for OCR** hingga mengonfigurasi bahasa, mengatur ambang kepercayaan, dan akhirnya **extract text from scanned form**, setiap langkah dijelaskan dengan kode dan penjelasan yang jelas. Anda kini memiliki fondasi yang kuat untuk menangani skenario yang lebih kompleks—baik itu pekerjaan batch, dukungan multi‑bahasa, atau ekstraksi tabel.

Jalankan skrip, sesuaikan ambang, dan saksikan dokumen Anda menjadi dapat dicari dalam hitungan menit. Ada pertanyaan atau formulir sulit yang tidak mau bekerja? Tinggalkan komentar di bawah, dan mari kita selesaikan bersama. Selamat coding! 

![Perform OCR on image example](example.png "Perform OCR on image")

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara Menggunakan AspOCR: Filter Pra‑proses Gambar OCR untuk .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}