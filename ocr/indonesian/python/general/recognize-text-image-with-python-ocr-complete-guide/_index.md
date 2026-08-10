---
category: general
date: 2026-06-28
description: Pelajari cara mengenali gambar teks menggunakan Python OCR, mengekstrak
  file PNG teks, dan mencetak teks yang dikenali dengan penanganan kesalahan yang
  kuat.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: id
og_description: Tutorial langkah demi langkah untuk mengenali gambar teks dalam Python,
  mengekstrak teks PNG, dan mencetak teks yang dikenali dengan aman.
og_title: Mengenali gambar teks dengan Python OCR – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Mengenali gambar teks dengan Python OCR – Panduan Lengkap
url: /id/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali gambar teks dengan Python OCR – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **recognize text image** dalam skrip Python tanpa harus mengimpor kerangka kerja yang berat? Anda tidak sendirian. Banyak pengembang membutuhkan cara cepat untuk *load image OCR* sebuah tangkapan layar, kwitansi yang dipindai, atau PNG sederhana dan mendapatkan teksnya kembali.  

Dalam tutorial ini kami akan menyiapkan mesin OCR minimal, menambahkan logger khusus, **load image OCR**, menjalankan **process image OCR**, dan akhirnya **print recognized text**. Pada akhir tutorial Anda akan memiliki skrip mandiri yang juga dapat **extract text png** file sesuai permintaan.

## Apa yang Akan Anda Dapatkan

- Sebuah potongan kode Python yang berfungsi penuh yang membuat mesin OCR, mencatat setiap langkah, dan menangani kegagalan dengan elegan.  
- Penjelasan jelas tentang *why* setiap baris penting—sehingga Anda dapat menyesuaikan kode ke Tesseract, EasyOCR, atau backend lainnya.  
- Tips untuk jebakan umum (font yang hilang, PNG yang rusak) dan cara men-debug-nya.  

### Prasyarat

- Python 3.8+ terinstal  
- Sebuah perpustakaan OCR yang menyediakan kelas `OcrEngine` (contoh menggunakan API fiktif namun tipikal; ganti dengan `pytesseract`, `easyocr`, dll.).  
- Sebuah gambar PNG yang ingin Anda analisis, disimpan sebagai `input.png` dalam folder yang Anda kontrol.  

> **Pro tip:** Jika Anda menggunakan `pytesseract`, instal biner Tesseract sistem terlebih dahulu (`sudo apt install tesseract-ocr` di Linux) dan kemudian `pip install pytesseract pillow`.

---

## ## Recognize Text Image: Menyiapkan Logger

Logger yang baik adalah pahlawan tak dikenal dalam setiap pipeline OCR. Ia memberi tahu Anda *when* mesin dimulai, *what* file yang dibuka, dan *why* mungkin gagal.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Mengapa ini penting:*  
Logger memisahkan output diagnostik dari inti OCR, memudahkan pengalihan log ke file, layanan pemantauan, atau bahkan UI di kemudian hari.  

---

## ## Load Image OCR: Memberi Mesin PNG

Sebelum mesin dapat **process image OCR**, ia membutuhkan objek gambar yang tepat. Kebanyakan perpustakaan menerima instance Pillow `Image`.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Poin penting:*  

- **load image ocr** – `Image.from_file` menyembunyikan detail decoding PNG.  
- Jaga agar path dapat dikonfigurasi; hard‑coding membuat skrip rapuh.  
- Panggilan logger mengonfirmasi gambar berhasil dibaca, yang berguna ketika file hilang atau rusak.  

---

## ## Process Image OCR: Mengenali Teks

Sekarang pekerjaan berat dimulai. Mesin memindai bitmap, menerapkan jaringan saraf atau heuristiknya, dan menghasilkan string Unicode.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Mengapa kami membungkusnya dalam `try/except`:*  
OCR dapat gagal pada PNG beresolusi rendah, ruang warna yang tidak didukung, atau data bahasa yang hilang. Menangkap `OcrException` memungkinkan Anda **print recognized text** hanya ketika memang ada, menghindari jejak tumpukan yang membingungkan bagi pengguna akhir.  

---

## ## Print Recognized Text & Extract Text PNG

Jika pengenalan berhasil, kami menampilkan hasilnya dan opsional menuliskannya ke file `.txt` yang meniru nama PNG asli.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*Apa yang Anda dapatkan:*  

- **print recognized text** – umpan balik visual langsung di terminal.  
- File `.txt` berdampingan yang secara efektif **extract text png** untuk pemrosesan lanjutan (pengindeksan pencarian, entri data, dll.).  

---

## ## Kasus Pinggiran Umum & Cara Menanganinya

| Situasi | Gejala | Solusi |
|-----------|---------|-----|
| PNG hanya dalam skala abu-abu | OCR mengembalikan string kosong | Konversi ke RGB (`Image.convert("RGB")`) sebelum memberi ke mesin. |
| Bahasa tidak didukung | `OcrException` dengan kode `LANG_NOT_FOUND` | Instal paket bahasa (mis., `tesseract‑lang‑fra` untuk bahasa Prancis) dan set `ocr_engine.language = "fra"`. |
| Gambar sangat besar ( > 5 MB ) | Pengenalan lambat atau error memori | Ukur ulang dengan `image.thumbnail((2000, 2000))` sebelum `set_image`. |
| Karakter tak terduga | Output kacau | Pastikan gambar benar-benar PNG; beberapa file menyamar sebagai PNG padahal sebenarnya JPEG. Gunakan `Image.verify()` untuk memvalidasi. |

---

## ## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Output konsol yang diharapkan (jalur sukses):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

Jika ada yang salah, Anda akan melihat baris `[ERROR]` yang jelas dengan alasannya, berkat logger khusus.

---

## ## Langkah Selanjutnya & Topik Terkait

- **extract text png** dari batch: bungkus skrip dalam loop `for` yang menelusuri pohon direktori.  
- **process image ocr** dengan pra‑pemrosesan (deskew, peningkatan kontras) menggunakan OpenCV sebelum memberi ke mesin.  
- Beralih ke layanan OCR cloud (Google Vision, Azure Read) dengan mengganti implementasi `OcrEngine`—kode di sekitarnya tetap sama.  
- Pelajari cara **print recognized text** ke PDF menggunakan `reportlab` untuk pembuatan laporan otomatis.  

---

## Kesimpulan

Kami baru saja menelusuri cara yang ringkas dan siap produksi untuk **recognize text image** dalam Python, mulai dari memuat PNG hingga **print recognized text** dan menyimpan hasilnya. Dengan menyisipkan logger kecil, menangani pengecualian, dan opsional menyimpan output, skrip ini siap untuk eksperimen cepat maupun integrasi ke pipeline yang lebih besar.

Cobalah dengan tangkapan layar Anda sendiri, bereksperimen dengan pra‑pemrosesan gambar, dan Anda akan segera mengekstrak teks dari PNG apa pun yang Anda gunakan. Ada pertanyaan? Tinggalkan komentar—selamat OCRing!  

![contoh mengenali gambar teks](placeholder.png)


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara Melakukan Ekstraksi Teks Gambar dari Stream Menggunakan Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Konversi Gambar ke Teks – Lakukan OCR pada Gambar dari URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}