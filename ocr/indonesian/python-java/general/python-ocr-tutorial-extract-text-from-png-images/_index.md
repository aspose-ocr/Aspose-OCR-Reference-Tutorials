---
category: general
date: 2026-06-25
description: Tutorial OCR Python yang menunjukkan cara mengekstrak teks dari file
  PNG, membaca gambar teks, dan mengenali teks gambar menggunakan mesin sederhana
  yang bebas lisensi.
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: id
og_description: Tutorial OCR Python mengajarkan Anda cara memuat gambar untuk OCR,
  mengekstrak teks dari file PNG, dan mengenali teks gambar hanya dengan beberapa
  baris kode.
og_title: Tutorial OCR Python – Ekstrak Teks dari PNG
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'Tutorial OCR Python: Ekstrak Teks dari Gambar PNG'
url: /id/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial OCR Python – Ekstrak Teks dari Gambar PNG

Pernah bertanya-tanya bagaimana **python ocr tutorial** dapat mengubah tangkapan layar struk menjadi teks yang dapat diedit? Anda tidak sendirian. Dalam banyak proyek dunia nyata kami perlu *read text image* file dengan cepat, dan melakukannya sendiri lebih baik daripada menyalin‑tempel dari GUI setiap kali.  

Dalam panduan ini kami akan membahas contoh langsung yang **extracts text PNG** file, menunjukkan cara *load image for OCR*, dan akhirnya mencetak hasil *recognize image text* — semuanya dengan mesin OCR gratis, hanya untuk evaluasi. Tanpa kunci lisensi, tanpa ketergantungan berat—hanya Python biasa dan beberapa paket kecil.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mengimpor pustaka OCR ringan.
- Langkah tepat untuk **load image for OCR** dan menangani jebakan umum.
- Cara **read text image** file dengan kualitas beragam.
- Tips meningkatkan akurasi saat Anda **extract text png** file.
- Cara menampilkan string yang dikenali dan secara opsional menuliskannya ke disk.

### Prasyarat

- Python 3.8 atau lebih baru (pustaka ini bekerja dengan 3.7+ tetapi 3.8+ disarankan).
- Familiaritas dasar dengan pip dan lingkungan virtual.
- File gambar bernama `sample.png` (atau PNG apa pun yang ingin Anda uji) disimpan di folder yang dapat Anda referensikan.

Jika ada yang terdengar tidak familiar, jeda sejenak dan siapkan—percaya saya, hasilnya sepadan.

---

## Tutorial OCR Python – Menyiapkan Mesin

Hal pertama yang harus dilakukan: kita membutuhkan objek mesin OCR. Pustaka yang akan kami gunakan adalah pembungkus kecil di atas mesin OCR native yang langsung dapat digunakan untuk evaluasi. Tidak memerlukan kunci lisensi, yang membuat *python ocr tutorial* sempurna untuk prototipe cepat.

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**Mengapa ini penting:** Membuat mesin mengisolasi runtime OCR dari sisa kode Anda, memungkinkan Anda menggunakannya kembali untuk banyak gambar tanpa menginisialisasi ulang sumber daya berat setiap kali.

---

## Memuat Gambar untuk OCR – Membaca File PNG

Sekarang mesin sudah ada, kita harus *load image for OCR*. Metode `Image.load` pada pustaka menerima path dan secara otomatis mendekode PNG, JPEG, BMP, serta beberapa format lain.

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Tip pro:** Jika PNG Anda mengandung saluran alfa, pustaka akan menghapusnya secara otomatis. Namun, untuk hasil terbaik pada tugas *read text image*, pertahankan gambar dalam skala abu‑abu—ini mengurangi noise dan mempercepat pengenalan.

---

## Mengenali Teks Gambar – Menjalankan Mesin OCR

Dengan objek gambar siap, kita akhirnya dapat **recognize image text**. Ini adalah inti dari *python ocr tutorial* dan hanya memerlukan satu baris kode.

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**Apa yang terjadi di balik layar?** Mesin menjalankan serangkaian filter pra‑pemrosesan (deskew, binarisasi) sebelum memasukkan bitmap ke jaringan saraf yang dilatih pada jutaan karakter. Itulah mengapa Anda sering mendapatkan output yang sangat akurat bahkan pada PNG beresolusi rendah.

---

## Tampilkan dan Simpan Teks yang Diekstrak

Mendapatkan hasil memang bagus, tetapi Anda mungkin ingin melihatnya atau menyimpannya di suatu tempat. Objek `result` menyediakan atribut `text` yang berisi output string biasa.

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Output yang diharapkan** (asumsi `sample.png` berisi “Hello, OCR!”):

```
Eval-mode result: Hello, OCR!
```

Jika Anda mendapatkan sampah alih-alih karakter yang dapat dibaca, periksa bagian berikut untuk perbaikan umum.

---

## Menangani Masalah Umum Saat Anda Ekstrak Teks PNG

Bahkan mesin OCR terbaik pun mengalami kesulitan pada gambar tertentu. Berikut adalah hambatan umum dan cara mengatasinya.

### 1. Kontras Rendah atau Latar Belakang Gelap

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. Garis Teks Miring

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. Karakter Non‑Inggris

Jika PNG Anda berisi huruf beraksen atau skrip non‑Latin, inisialisasi mesin dengan paket bahasa yang sesuai:

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. Gambar Sangat Besar

Memproses PNG 4000×3000 dapat lambat. Turunkan skala sambil mempertahankan keterbacaan:

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

Penyesuaian ini merupakan bagian dari *python ocr tutorial* yang kuat dan bekerja di luar skenario jalur bahagia.

---

## Skrip Lengkap – Solusi Satu‑File

Berikut adalah skrip lengkap yang siap dijalankan yang menggabungkan semua langkah dan perbaikan opsional yang dibahas. Salin‑tempel ke dalam `ocr_extract.py` dan jalankan `python ocr_extract.py`.

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**Jalankan:**  
```bash
python ocr_extract.py ./sample.png
```

Anda akan melihat string yang dikenali dicetak dan file `sample_extracted.txt` dibuat di samping gambar.

---

## Gambaran Visual

![Python OCR tutorial – load image for OCR and extract text from PNG](/images/python-ocr-flow.png)

*Alt text:* *Diagram tutorial OCR Python yang menunjukkan alur dari memuat gambar untuk OCR hingga mengekstrak teks PNG.*

Diagram menggambarkan progresi linier dari **load image for OCR** → **recognize image text** → **extract text PNG** dan menyoroti dimana Anda dapat menyisipkan langkah pra‑pemrosesan.

---

## Kesimpulan

Kami baru saja menyelesaikan **python ocr tutorial** yang menunjukkan cara *load image for OCR*, *recognize image text*, dan akhirnya **extract text png** file dengan hanya beberapa perintah Python. Skrip ini berfungsi penuh, menangani kasus tepi umum, dan dapat diperluas untuk pemrosesan batch atau dukungan multibahasa.

Siap untuk tantangan berikutnya? Coba beri mesin PDF yang dikonversi menjadi gambar, bereksperimen dengan paket bahasa yang berbeda, atau integrasikan langkah OCR ke dalam API Flask sehingga aplikasi web Anda dapat membaca tangkapan layar yang diunggah secara langsung. Kemungkinan otomatisasi *read text image* hampir tak terbatas.

Ada pertanyaan atau gambar sulit yang tidak dapat Anda pecahkan? Tinggalkan komentar di bawah, dan mari kita selesaikan bersama. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}