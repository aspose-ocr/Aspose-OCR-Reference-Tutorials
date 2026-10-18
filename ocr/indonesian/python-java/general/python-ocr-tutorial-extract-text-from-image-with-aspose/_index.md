---
category: general
date: 2026-03-26
description: 'Tutorial OCR Python: pelajari cara mengekstrak teks dari gambar, memuat
  gambar untuk OCR, dan mengenali teks dari struk menggunakan Aspose OCR dalam beberapa
  langkah saja.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: id
og_description: 'Tutorial OCR Python: pelajari cara cepat mengekstrak teks dari gambar,
  memuat gambar untuk OCR, dan mengenali teks dari struk dengan Aspise OCR.'
og_title: Tutorial OCR Python – Ekstrak Teks dari Gambar
tags:
- OCR
- Aspose
- Python
title: Tutorial OCR Python – Ekstrak Teks dari Gambar dengan Aspose
url: /id/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial OCR Python – Ekstrak Teks dari Gambar dengan Aspose

Pernah bertanya-tanya bagaimana cara mengambil teks dari kwitansi yang buram atau formulir yang dipindai tanpa menghabiskan berjam‑jam menulis regex khusus? Anda tidak sendirian. Dalam **python ocr tutorial** ini kami akan membahas cara memuat gambar untuk OCR, melakukan OCR di Python, dan akhirnya mengenali teks dari file kwitansi menggunakan perpustakaan Aspose OCR.  

Pada akhir panduan ini Anda akan memiliki skrip siap‑jalankan yang membaca format gambar apa pun yang didukung, mengekstrak konten teks, dan mencetaknya ke konsol. Tanpa layanan eksternal, tanpa kunci API—hanya Python murni dan mesin OCR yang kuat.  

## Apa yang Anda Butuhkan

- Python 3.8 atau lebih baru (kode menggunakan type hints, jadi interpreter terbaru lebih baik)
- Paket `asposeocrjava` yang diinstal melalui `pip install aspose-ocr`
- Gambar contoh – misalnya `receipt_noisy.jpg` yang berisi kwitansi toko tipikal
- (Opsional) Lingkungan virtual untuk menjaga ketergantungan tetap rapi

Jika Anda sudah mencentang semua kotak tersebut, kita dapat langsung melompat ke kode.  

## Langkah 1: Instal dan Impor Kelas Aspose OCR

Pertama, pastikan paket Aspose OCR tersedia. Kemudian impor kelas‑kelas yang kita perlukan.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Mengapa ini penting:** Mengimpor hanya simbol yang diperlukan menjaga namespace tetap bersih dan memberi sinyal kepada interpreter bagian perpustakaan mana yang sebenarnya kita gunakan. Ini juga mempersingkat baris kode selanjutnya, membuat tutorial lebih mudah diikuti.

> **Pro tip:** Jika Anda menggunakan notebook Jupyter, tambahkan `!` di depan baris instalasi untuk menjalankannya dalam sel.

## Langkah 2: Buat Engine OCR dan Aktifkan Mode Deep‑Learning

Aspose menawarkan beberapa mode engine. Untuk kebanyakan kwitansi dunia nyata, model deep‑learning memberikan akurasi tertinggi, terutama pada pemindaian yang berisik.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Mengapa deep‑learning?** OCR berbasis aturan tradisional dapat kesulitan pada karakter dengan kontras rendah atau terdistorsi. Model deep‑learning, yang dilatih pada jutaan glyph, beradaptasi lebih baik dengan variasi—tepat apa yang Anda butuhkan ketika Anda *perform OCR in Python* pada kwitansi yang diambil dengan kamera ponsel.

## Langkah 3: Muat Gambar untuk OCR

Sekarang kita benar‑benarnya **load image for OCR**. Aspose.Imaging mendukung PNG, JPEG, BMP, TIFF, dan lainnya, sehingga Anda dapat menunjukkannya ke hampir semua gambar dokumen.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Kesalahan umum:** Lupa menetapkan gambar pada engine menghasilkan `NullReferenceException` saat runtime. Selalu panggil `set_image` setelah memuat file.

## Langkah 4: Lakukan OCR dan Ekstrak Teks

Dengan engine yang siap dan gambar terlampir, kita akhirnya dapat **perform OCR in Python** dan mengambil hasil teks.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

Metode `recognize()` mengembalikan objek `OcrResult` yang berisi tidak hanya teks mentah tetapi juga skor kepercayaan, bounding box, dan informasi bahasa. Untuk kasus penggunaan **extract text from image** yang cepat, kita hanya membutuhkan `get_text()`.

## Langkah 5: Tampilkan Teks yang Dikenali

Mari lihat apa yang sebenarnya dibaca engine dari kwitansi.

```python
print("Recognized text:\n", recognized_text)
```

Output tipikal terlihat seperti:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Jika output berisi karakter yang kacau, pertimbangkan pra‑pemrosesan gambar (mis., meningkatkan kontras atau menerapkan filter deskew) sebelum memuatnya ke engine OCR. Aspose.Imaging menawarkan rangkaian lengkap alat peningkatan gambar yang dapat Anda rangkai bersama.

## Menangani Kasus Pinggir & Tips untuk Akurasi Lebih Baik

### 1. Menangani Kwitansi yang Sangat Berisik
Jika kwitansi sangat ternoda, Anda mungkin ingin beralih ke mode `OcrEngineMode.HIGH_SPEED` untuk proses yang lebih cepat, meskipun kurang akurat, kemudian jalankan proses kedua dalam `DEEP_LEARNING` pada gambar yang sudah dibersihkan.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Menentukan Bahasa
Secara default Aspose mencoba mendeteksi bahasa secara otomatis. Untuk kwitansi berbahasa Inggris Anda dapat mengunci bahasa tersebut:

```python
ocr_engine.set_language("eng")
```

### 3. Manajemen Memori
Saat memproses banyak gambar dalam loop, lepaskan sumber daya secara eksplisit:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. Menyimpan Hasil OCR ke File
Kadang‑kadang Anda memerlukan teks yang diekstrak disimpan untuk analisis selanjutnya.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Contoh Lengkap yang Berfungsi

Berikut adalah skrip lengkap yang menggabungkan semuanya. Salin‑tempel ke dalam file bernama `receipt_ocr.py`, sesuaikan jalur gambar, dan jalankan `python receipt_ocr.py`.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

Menjalankan skrip akan menampilkan isi kwitansi di konsol Anda dan juga membuat `receipt_output.txt` dengan data yang sama.

![tutorial ocr python – contoh output kwitansi](https://example.com/receipt_output.png "contoh tutorial ocr python")

*Teks alt gambar:* **tutorial ocr python – contoh output kwitansi**

## Ringkasan & Langkah Selanjutnya

Kami baru saja melewati **python ocr tutorial** yang menunjukkan cara **load image for OCR**, **perform OCR in Python**, dan akhirnya **recognize text from receipt** file menggunakan Aspose. Poin pentingnya adalah:

- Pilih mode engine yang tepat (deep‑learning untuk akurasi)
- Selalu lampirkan gambar sebelum memanggil `recognize()`
- Gunakan objek `OcrResult` untuk mengambil teks bersih, lalu menyimpan atau memprosesnya sesuai kebutuhan

Apa selanjutnya? Pertimbangkan menggabungkan filter Aspose Imaging untuk meningkatkan pemindaian berkontras rendah, atau mengintegrasikan skrip ke dalam API Flask sehingga Anda dapat mengunggah kwitansi melalui formulir web. Anda juga dapat mengeksplorasi mengekspor data OCR ke CSV untuk otomatisasi akuntansi.

Ada pertanyaan tentang penanganan PDF multi‑halaman atau skrip non‑Latin? Tinggalkan komentar—senang membantu!  

**Siap meningkatkan otomatisasi dokumen Anda?** Ambil kode, coba dengan gambar berbeda, dan biarkan engine OCR melakukan pekerjaan berat. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}