---
category: general
date: 2026-01-12
description: Cara melakukan OCR dan mengonversi gambar menjadi teks dengan cepat.
  Pelajari cara mengenali karakter khusus, mengekstrak teks dari gambar, dan memuat
  gambar untuk OCR dengan contoh Python lengkap.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: id
og_description: Cara melakukan OCR di Python, mengonversi gambar menjadi teks, dan
  mengenali karakter khusus. Ikuti panduan praktis ini untuk mengekstrak teks dari
  gambar.
og_title: Cara Melakukan OCR di Python – Tutorial Lengkap
tags:
- OCR
- Python
- Image Processing
title: Cara Melakukan OCR di Python – Panduan Langkah demi Langkah
url: /id/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di Python – Panduan Langkah‑demi‑Langkah

Pernahkah Anda perlu **perform OCR** pada screenshot yang berisi karakter Latin dan Cyrillic? Anda tidak sendirian. Dalam banyak proyek—baik itu mendigitalkan kwitansi, mengindeks dokumen multibahasa, atau membangun arsip yang dapat dicari—**how to perform OCR** dengan cepat menjadi pertanyaan utama.  

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan cara **convert image to text**, **recognize special characters**, dan **extract text from image** menggunakan pustaka Python sederhana. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang memuat gambar untuk OCR, menangani konten multibahasa, dan mencetak hasilnya.

## Apa yang Anda Butuhkan

- Python 3.8+ terinstal di mesin Anda.  
- Paket `ocr` (atau pustaka OCR kompatibel lainnya) terinstal via `pip install ocr`.  
- File gambar (`multilingual.png`) yang berisi glyph Latin dan Cyrillic.  
- Editor teks dasar atau IDE—VS Code, PyCharm, atau bahkan Notepad sederhana sudah cukup.  

Jika Anda tidak memiliki paket `ocr`, Anda dapat menggantinya dengan `pytesseract` dengan beberapa perubahan kecil; konsep dasarnya tetap sama.

## Langkah 1: Instal dan Impor Pustaka OCR

Pertama, mari siapkan mesin OCR. Kami akan mengimpor pustaka, membuat instance mesin, dan mengkonfigurasinya untuk dukungan multibahasa.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Mengapa ini penting:**  
Membuat mesin adalah fondasi—tanpa itu Anda tidak dapat **load image for OCR** nanti. Mengaktifkan paket bahasa memastikan mesin dapat mengidentifikasi karakter seperti “Ŀ”, “Ҕ”, dan “Ǣ” dengan benar. Jika Anda melewatkan langkah ini, Anda akan mendapatkan output yang berantakan untuk skrip non‑Latin.

## Langkah 2: Muat Gambar yang Mengandung Teks Multibahasa

Sekarang kami mengarahkan mesin ke file yang ingin diproses. Path dapat bersifat absolut atau relatif; pastikan itu mengarah ke gambar yang dapat dibaca.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![how to perform OCR example](/images/ocr-example.png "how to perform OCR on a multilingual image")

**Mengapa ini penting:**  
Pemanggilan `load_image` membaca data piksel ke memori, menyiapkannya untuk algoritma OCR. Jika gambar besar, mesin mungkin secara otomatis menurunkan resolusinya; Anda dapat menyesuaikannya nanti dengan `engine.set_max_resolution(3000)` untuk pemindaian resolusi tinggi.

## Langkah 3: Jalankan Proses Pengenalan

Dengan mesin yang siap dan gambar yang dimuat, kita akhirnya dapat mengekstrak konten teks.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Mengapa ini penting:**  
`recognize()` menjalankan jaringan saraf yang berat di belakang layar. Ia mengembalikan objek yang berisi teks mentah, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya untuk debugging visual.

## Langkah 4: Keluarkan Teks yang Diakui

Mari lihat apa yang ditemukan mesin. Kami akan mencetak teks ke konsol, tetapi Anda juga dapat menuliskannya ke file atau basis data.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Output yang Diharapkan

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Jika Anda melihat sesuatu yang serupa, selamat—Anda telah berhasil **convert image to text** dan **recognize special characters**.

## Menangani Kendala Umum

Bahkan dengan skrip yang sederhana, Anda mungkin menemui beberapa kendala. Berikut beberapa tips praktis dari pengalaman saya.

### 1. Paket Bahasa Hilang

Jika Anda mendapatkan tanda tanya (`?`) alih-alih huruf Cyrillic, periksa kembali bahwa paket bahasa telah terinstal. Untuk banyak mesin OCR Anda perlu mengunduh file `.traineddata` yang sesuai dan menaruhnya di folder `tessdata` mesin.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Kualitas Gambar Rendah

Gambar yang buram atau kontras rendah menghasilkan skor kepercayaan yang rendah. Pralakukan gambar dengan OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. File Besar dan Penggunaan Memori

Memproses foto 10 MB dapat meningkatkan penggunaan memori. Gunakan `engine.set_max_image_size(2000)` untuk membatasi resolusi, atau bagi gambar menjadi ubin dan OCR setiap ubin secara terpisah.

### 4. Menangkap Bounding Boxes

Jika Anda perlu menyorot di mana setiap kata muncul (berguna untuk overlay UI), akses `result.boxes`:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Skrip Lengkap – Eksekusi Satu‑Klik

Menggabungkan semuanya, berikut satu file yang dapat Anda jalankan sebagai `python ocr_demo.py`. Ia mencakup penanganan error, pra‑pemrosesan opsional, dan komentar untuk kejelasan.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Jalankan dengan:

```bash
python ocr_demo.py path/to/multilingual.png
```

Anda akan melihat output yang sama seperti sebelumnya, mengonfirmasi bahwa Anda telah berhasil **extract text from image**.

## Kesimpulan

Kami telah membahas **how to perform OCR** di Python dari awal hingga akhir: menginstal pustaka, memuat gambar, mengenali konten multibahasa, dan menangani kasus tepi paling umum. Dengan mengikuti panduan ini Anda kini dapat **convert image to text**, **recognize special characters**, dan **extract text from image** dalam proyek Anda sendiri—tidak lagi transkripsi manual.

Apa selanjutnya? Cobalah bereksperimen dengan:

- Menambahkan lebih banyak paket bahasa (misalnya `spa` untuk bahasa Spanyol).  
- Mengekspor hasil ke JSON untuk pemrosesan lanjutan.  
- Mengintegrasikan langkah OCR ke dalam API Flask sehingga layanan lain dapat memanggilnya.  

Jika Anda menemui keanehan apa pun, komunitas di sekitar kebanyakan pustaka OCR aktif—cari “ocr library language pack installation” atau tinggalkan komentar di bawah. Selamat coding, dan nikmati mengubah gambar menjadi teks yang dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}