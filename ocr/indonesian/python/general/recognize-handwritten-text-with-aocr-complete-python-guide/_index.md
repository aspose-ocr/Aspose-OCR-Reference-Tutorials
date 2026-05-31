---
category: general
date: 2026-05-31
description: Mengenali teks tulisan tangan dengan cepat menggunakan Aocr. Pelajari
  cara mengaktifkan add‑on tulisan tangan, memuat gambar untuk OCR, dan mengekstrak
  teks dari gambar.
draft: false
keywords:
- recognize handwritten text
- extract text from image
- load image for ocr
- handwritten text extraction
- how to enable handwritten
language: id
og_description: Mengenali teks tulisan tangan di Python menggunakan Aocr. Panduan
  ini menunjukkan cara mengaktifkan add‑on tulisan tangan, memuat gambar untuk OCR,
  dan mengekstrak teks dari gambar.
og_title: Mengenali Teks Tulisan Tangan dengan Aocr – Panduan Python Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize handwritten text quickly using Aocr. Learn how to enable
    handwritten add‑on, load image for OCR, and extract text from image.
  headline: recognize handwritten text with Aocr – Complete Python Guide
  type: TechArticle
- description: recognize handwritten text quickly using Aocr. Learn how to enable
    handwritten add‑on, load image for OCR, and extract text from image.
  name: recognize handwritten text with Aocr – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If the image contains a clear note like:'
  - name: Running the Script
    text: '```bash python handwritten_ocr.py ```'
  - name: 1. Blurry or Low‑Contrast Images
    text: 'Handwritten OCR struggles with low‑quality scans. Before feeding the image
      to Aocr, consider:'
  - name: 2. Multi‑Page PDFs
    text: Aocr works on single images. If you have a multi‑page PDF, split it into
      individual pages (e.g., using `pdf2image`) and loop over each page, feeding
      them to the same engine instance.
  - name: 3. Non‑English Handwriting
    text: The default model focuses on English characters. For other alphabets, you’ll
      need to load language‑specific models (if available) via `ocr.set_language("es")`
      or similar.
  type: HowTo
- questions:
  - answer: Absolutely. The core engine handles printed text out of the box; you can
      toggle the handwritten add‑on on or off depending on your use case.
    question: Does this work with printed text too?
  - answer: Check the image path, ensure the file exists, and verify that the handwriting
      is legible. Pre‑processing (contrast boost) often fixes empty results.
    question: What if I get an empty string?
  - answer: 'Aocr’s `recognize()` returns plain text, but the library also offers
      `recognize_with_boxes()` which yields coordinates for each detected token—useful
      for highlighting in UI. ## Conclusion We’ve just **recognize handwritten text**
      using Aocr, from installing the package to printing the final string. '
    question: Can I get bounding boxes for each word?
  type: FAQPage
tags:
- OCR
- Python
- HandwritingRecognition
title: Mengenali teks tulisan tangan dengan Aocr – Panduan Python Lengkap
url: /id/python/general/recognize-handwritten-text-with-aocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks tulisan tangan dengan Aocr – Panduan Python Lengkap

Pernah bertanya-tanya bagaimana cara **mengenali teks tulisan tangan** dalam sebuah foto tanpa membuat Anda stres? Anda bukan satu‑satunya. Baik Anda mendigitalkan catatan rapat, memproses formulir, atau sekadar bermain dengan AI untuk bersenang‑senang, mendapatkan teks bersih yang dapat dicari dari coretan dapat terasa seperti sihir.  

Kabar baiknya? Aocr membuatnya menjadi sangat mudah. Dalam tutorial ini kami akan membahas setiap langkah—*cara mengaktifkan pengenalan tulisan tangan*, *memuat gambar untuk OCR*, dan akhirnya *mengekstrak teks dari gambar* hanya dengan beberapa baris Python. Pada akhir tutorial, Anda akan memiliki skrip siap‑jalankan yang mengubah catatan tulisan tangan menjadi teks biasa.

## Apa yang Dibahas dalam Tutorial Ini

- Menginstal paket Python Aocr  
- Membuat instance mesin OCR  
- **Cara mengaktifkan pengenalan tulisan tangan** add‑on  
- Memuat *gambar untuk OCR* dengan benar (termasuk keanehan path)  
- Menjalankan mesin dan **mengekstrak teks dari gambar**  
- Kesulitan umum dan tips untuk **ekstraksi teks tulisan tangan** yang andal  

Tidak diperlukan pengalaman sebelumnya dengan Aocr, hanya setup Python dasar. Mari kita mulai.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

1. Python 3.8+ terinstal (versi terbaru apa pun sudah cukup).  
2. Akses ke terminal atau command prompt.  
3. File gambar yang berisi catatan tulisan tangan yang jelas (JPEG atau PNG).  
4. Koneksi internet untuk instalasi `pip` pertama kali.

Jika ada yang belum tersedia, hentikan dulu dan selesaikan—kalau tidak, kode akan menghasilkan error yang membingungkan.

## Langkah 1: Instal Paket Aocr

Langkah pertama: Anda memerlukan library Aocr. Library ini dipublikasikan di PyPI, jadi perintah `pip` sederhana sudah cukup.

```bash
pip install aocr
```

> **Pro tip:** Jika Anda menggunakan virtual environment (sangat disarankan), aktifkan dulu sebelum menjalankan perintah instalasi. Ini menjaga dependensi tetap rapi dan menghindari benturan versi.

## Langkah 2: Impor Modul dan Buat Instance Mesin OCR

Sekarang kita akan mengimpor library dan memulai sebuah engine. Anggap engine sebagai otak yang akan melakukan pekerjaan berat.

```python
# Step 2: Import Aocr and create the engine
import aocr

# Create an OCR engine instance – this is where the magic begins
ocr = aocr.OcrEngine()
```

Mengapa kita memerlukan sebuah instance? Objek `OcrEngine` menyimpan konfigurasi—seperti model bahasa dan add‑on—sehingga Anda dapat menyesuaikannya per proyek tanpa harus menginisialisasi ulang semuanya.

## Langkah 3: **cara mengaktifkan pengenalan tulisan tangan** Add‑on

Aocr dilengkapi dengan mesin OCR inti yang menangani teks cetak secara default. Pengenalan tulisan tangan, bagaimanapun, berada di add‑on opsional yang harus Anda aktifkan secara eksplisit.

```python
# Step 3: Enable the handwritten‑recognition add‑on
# Passing True activates the feature; False would disable it.
ocr.enable_handwritten_recognition(True)
```

> **Mengapa ini penting:** Mengaktifkan add‑on memuat jaringan saraf khusus yang dilatih pada tulisan kursif dan blok. Melewatkan langkah ini akan membuat engine memperlakukan coretan Anda sebagai noise, mengembalikan string kosong atau karakter tak terbaca.

## Langkah 4: Memuat **gambar untuk OCR** dengan Benar

Memuat gambar terdengar sederhana, tetapi penanganan path sering membuat pemula kebingungan—terutama di Windows di mana backslash berfungsi sebagai karakter escape. Gunakan raw string (`r"..."`) atau slash maju untuk menghindari bug tersembunyi.

```python
# Step 4: Load the image containing handwritten text
image_path = r"YOUR_DIRECTORY/handwritten_note.jpg"  # Replace with your actual path
ocr.load_image(image_path)
```

Jika Anda menggunakan macOS atau Linux, raw string yang sama juga berfungsi baik. Pastikan file memang ada; jika tidak, `FileNotFoundError` akan muncul.

## Langkah 5: Jalankan Engine dan **ekstrak teks dari gambar**

Setelah engine siap dan gambar telah dimuat, saatnya mengenali isinya. Metode `recognize()` mengembalikan string biasa yang berisi semua karakter yang terdeteksi.

```python
# Step 5: Perform OCR to recognize the handwritten content
result = ocr.recognize()

# Step 6: Output the recognized text
print("Recognized Handwritten Text:")
print(result)
```

### Output yang Diharapkan

Jika gambar berisi catatan jelas seperti:

```
Buy milk
Call Alice at 5pm
```

Anda akan melihat sesuatu yang serupa tercetak di konsol:

```
Recognized Handwritten Text:
Buy milk
Call Alice at 5pm
```

Variasi ejaan kecil dapat terjadi—tulisan tangan memang bersifat ambigu—tetapi struktur keseluruhan seharusnya dapat dikenali.

## Skrip Lengkap – Siap Dijalan

Berikut adalah skrip lengkap yang menggabungkan semua langkah. Salin‑tempel ke file bernama `handwritten_ocr.py`, ganti nilai `image_path`, lalu jalankan dengan `python handwritten_ocr.py`.

```python
"""
Handwritten Text Recognition with Aocr
--------------------------------------
This script demonstrates how to:
- enable the handwritten add‑on,
- load an image for OCR,
- and extract text from image.
"""

import aocr

def main():
    # 1️⃣ Create OCR engine
    ocr = aocr.OcrEngine()

    # 2️⃣ Enable handwritten recognition (the crucial add‑on)
    ocr.enable_handwritten_recognition(True)

    # 3️⃣ Load your handwritten image
    image_path = r"YOUR_DIRECTORY/handwritten_note.jpg"  # 👉 Update this line
    ocr.load_image(image_path)

    # 4️⃣ Perform recognition
    result = ocr.recognize()

    # 5️⃣ Print the extracted text
    print("\n=== Recognized Handwritten Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

### Menjalankan Skrip

```bash
python handwritten_ocr.py
```

Jika semuanya telah diatur dengan benar, Anda akan melihat teks yang diekstrak tercetak di konsol. 🎉

## Menangani Kasus Edge yang Umum

### 1. Gambar Buram atau Kontras Rendah

OCR tulisan tangan kesulitan dengan pemindaian ber kualitas rendah. Sebelum memberi gambar ke Aocr, pertimbangkan:

- Mengonversi ke grayscale (`cv2.cvtColor`)  
- Menerapkan Gaussian blur ringan untuk mengurangi noise  
- Menyesuaikan kontras dengan Pillow (`ImageEnhance.Contrast`)

Langkah pra‑pemrosesan ini dapat secara dramatis meningkatkan akurasi **ekstraksi teks tulisan tangan**.

### 2. PDF Multi‑Halaman

Aocr bekerja pada gambar tunggal. Jika Anda memiliki PDF multi‑halaman, pisahkan menjadi halaman‑halaman terpisah (misalnya dengan `pdf2image`) dan lakukan loop pada tiap halaman, memberi masing‑masing ke instance engine yang sama.

### 3. Tulisan Tangan Non‑Inggris

Model default berfokus pada karakter bahasa Inggris. Untuk alfabet lain, Anda perlu memuat model bahasa spesifik (jika tersedia) melalui `ocr.set_language("es")` atau serupa.

## Pro Tips untuk **ekstraksi teks tulisan tangan** yang Andal

- **Jaga ukuran gambar tetap wajar**: Gambar sangat besar mengonsumsi memori lebih banyak dan dapat memperlambat proses. Ubah ukuran menjadi lebar sekitar ~1200 px sambil mempertahankan rasio aspek.  
- **Hindari teks yang diputar**: Aocr mengharapkan teks dalam posisi tegak. Gunakan `ocr.rotate_image(angle)` bila catatan Anda miring.  
- **Pemrosesan batch**: Saat menangani puluhan catatan, gunakan kembali instance `OcrEngine` yang sama—inisialisasi ulang memakan biaya yang cukup tinggi.

## Pertanyaan yang Sering Diajukan

**T: Apakah ini juga bekerja dengan teks cetak?**  
J: Tentu saja. Mesin inti menangani teks cetak secara default; Anda dapat menyalakan atau mematikan add‑on tulisan tangan sesuai kebutuhan.

**T: Mengapa saya mendapatkan string kosong?**  
J: Periksa path gambar, pastikan file ada, dan pastikan tulisan tangan dapat dibaca. Pra‑pemrosesan (peningkatan kontras) sering memperbaiki hasil kosong.

**T: Bisakah saya mendapatkan bounding box untuk tiap kata?**  
J: `recognize()` mengembalikan teks biasa, tetapi library juga menyediakan `recognize_with_boxes()` yang menghasilkan koordinat untuk tiap token yang terdeteksi—berguna untuk menyorot di UI.

## Kesimpulan

Kita baru saja **mengenali teks tulisan tangan** menggunakan Aocr, mulai dari instalasi paket hingga mencetak string akhir. Dengan mengikuti langkah‑langkah—**cara mengaktifkan pengenalan tulisan tangan** add‑on, memuat *gambar untuk OCR* dengan tepat, dan akhirnya *mengekstrak teks dari gambar*—Anda kini memiliki fondasi kuat untuk proyek apa pun yang memerlukan **ekstraksi teks tulisan tangan**.  

Selanjutnya, coba proses batch catatan, bereksperimen dengan pra‑pemrosesan gambar, atau jelajahi API bounding‑box untuk output yang lebih kaya. Kemungkinannya tak terbatas, dan dengan desain Aocr yang fleksibel, mengubah coretan menjadi data yang dapat dicari tidak lagi menjadi sakit kepala.

Punya pertanyaan lebih lanjut atau ingin berbagi hasil? Tinggalkan komentar di bawah, dan selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}