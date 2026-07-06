---
category: general
date: 2026-06-19
description: Lakukan OCR pada gambar menggunakan pustaka OCR Python. Pelajari cara
  mendeteksi teks dari gambar, mengenali teks dari JPEG, dan mengekstrak teks dari
  gambar yang dipindai secara efisien.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: id
og_description: Lakukan OCR pada gambar dengan Python dan ekstrak teks dari file yang
  dipindai. Panduan ini memandu Anda melalui proses memuat gambar, memperbaiki kemiringan,
  dan mengenali teks langkah demi langkah.
og_title: Lakukan OCR pada Gambar di Python – Panduan Ekstraksi Teks Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Lakukan OCR pada Gambar di Python – Panduan Ekstraksi Teks Lengkap
url: /id/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar di Python – Panduan Ekstraksi Teks Lengkap

Pernah perlu **melakukan OCR pada file gambar** tetapi terhambat karena kodenya terlihat misterius? Anda tidak sendirian. Baik Anda mengubah tumpukan struk yang dipindai menjadi PDF yang dapat dicari atau mengekstrak keterangan dari JPEG untuk proyek data‑science, kemampuan mengenali teks dari JPEG dan format lainnya adalah keterampilan yang wajib dimiliki oleh setiap pengembang saat ini.

Dalam tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan cara **mendeteksi teks dari file gambar**, **mengekstrak teks dari dokumen gambar yang dipindai**, dan bahkan **memuat gambar untuk OCR** hanya dalam beberapa baris kode. Pada akhir tutorial, Anda akan memiliki potongan kode siap produksi yang dapat Anda sisipkan ke dalam proyek Anda—tanpa impor yang hilang, tanpa shortcut “lihat dokumen”.

## Apa yang Akan Anda Bangun

- Skrip Python kecil yang membuat mesin OCR, mengaktifkan auto‑deskew, memuat JPEG (atau format lain yang didukung), dan mencetak teks yang dikenali.
- Penjelasan **mengapa** setiap pengaturan penting, bukan hanya **bagaimana** menuliskannya.
- Tips untuk menangani PDF multi‑halaman, bahasa non‑Inggris, dan jebakan umum seperti pemindaian yang buram.

### Prasyarat

- Python 3.8+ terpasang (contoh menggunakan paket `ocr` yang tersedia via `pip install ocr-lib` – ganti dengan nama pustaka Anda yang sebenarnya).
- Familiaritas dasar dengan fungsi Python dan lingkungan virtual.
- File gambar (JPEG, PNG, TIFF) yang ingin Anda proses; kami akan menggunakan `skewed_page.jpg` sebagai placeholder.

> **Pro tip:** Jika Anda menggunakan Windows, jalankan terminal Anda sebagai Administrator saat menginstal pustaka OCR untuk menghindari masalah izin.

---

## Lakukan OCR pada Gambar – Penyiapan dan Konfigurasi

Hal pertama yang Anda butuhkan adalah instance mesin OCR yang bersih. Anggap saja ini sebagai otak di balik operasi; tanpa konfigurasi yang tepat, bahkan gambar paling tajam pun akan menghasilkan teks yang tidak dapat dibaca.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Mengapa ini penting:**  
Menetapkan `engine.language` mempersempit set karakter yang diharapkan mesin OCR, secara dramatis meningkatkan akurasi. Jika Anda melewatkannya, mesin akan menebak, sering kali salah membaca kata sederhana.

---

## Aktifkan Deskew Otomatis – Memperbaiki Pemindaian yang Miring

Halaman yang dipindai jarang sekali benar‑benar datar. Kemiringan sedikit dapat mengacaukan segmentasi karakter, mengubah “Hello” menjadi “H3llo”. Flag `auto_deskew` melakukan pekerjaan berat untuk Anda.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Kasus khusus:** Jika Anda tahu gambar Anda sudah lurus, menonaktifkan deskew dapat menghemat beberapa milidetik waktu pemrosesan—berguna saat menangani ribuan halaman dalam pekerjaan batch.

---

## Muat Gambar untuk OCR – Mendukung JPEG, PNG, TIFF

Sekarang kita benar‑benar **memuat gambar untuk OCR**. Metode `ocr.Image.load` fleksibel; ia menerima path ke format raster apa pun yang didukung.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Mengapa langkah ini krusial:** Pustaka membaca file ke dalam bitmap internal, menerapkan konversi ruang warna bila diperlukan. Melewatkan langkah ini dan mengirim aliran byte mentah akan memunculkan `FileNotFoundError` atau, lebih buruk, menghasilkan hasil kosong secara diam‑diam.

Jika Anda perlu **mengenali teks dari file JPEG** secara khusus, pastikan ekstensi file adalah `.jpeg` atau `.jpg`. Pemanggilan yang sama juga bekerja untuk PNG (`.png`) atau TIFF (`.tif`) tanpa modifikasi.

---

## Lakukan OCR pada Gambar – Menjalankan Mesin

Dengan mesin yang sudah dipersiapkan dan gambar berada di memori, saatnya **melakukan OCR pada data gambar**. Satu baris ini melakukan semua pekerjaan berat: pra‑pemrosesan, segmentasi, klasifikasi, dan penyusunan teks.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**Apa yang terjadi di balik layar?**  
- Mesin menerapkan transformasi deskew (jika diaktifkan).  
- Ia menjalankan jaringan saraf atau backend Tesseract untuk mengidentifikasi karakter.  
- Akhirnya, ia menyatukan karakter menjadi kata dan baris, mengembalikan objek `result` yang kaya.

---

## Ekstrak Teks dari Gambar yang Dipindai – Tampilkan Hasilnya

Langkah terakhir adalah **mengekstrak teks dari gambar yang dipindai** dan menampilkannya. Atribut `result.text` berisi representasi teks polos.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

Contoh output biasanya seperti ini:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

Jika mesin OCR gagal menemukan karakter apa pun, `result.text` akan menjadi string kosong. Dalam kasus tersebut, periksa kembali kualitas gambar atau pertimbangkan menyesuaikan properti `engine.confidence_threshold` (jika pustaka Anda mendukungnya).

---

## Menangani Variasi Umum

### Mengenali Teks dari JPEG vs PNG

Kedua format didukung, tetapi kompresi JPEG dapat menimbulkan artefak yang membingungkan mesin. Jika Anda sering melihat kesalahan pengenalan, coba konversi JPEG ke PNG terlebih dahulu:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Mendeteksi Teks dari Gambar dengan Banyak Bahasa

Jika dokumen Anda mencampur Bahasa Inggris dan Spanyol, atur mode multibahasa:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

Mesin kemudian akan mempertimbangkan kedua alfabet selama proses pengenalan.

### Ekstrak Teks dari PDF yang Dipindai

Untuk PDF, Anda harus meraster setiap halaman menjadi gambar terlebih dahulu. Pustaka seperti `pdf2image` mempermudah proses ini:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Contoh Lengkap yang Berfungsi

Berikut adalah skrip lengkap yang dapat Anda salin‑tempel ke dalam file `ocr_demo.py`. Skrip ini mencakup penanganan error dan helper kecil untuk mengukur waktu eksekusi.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Output yang diharapkan** (asumsi pemindaian jelas):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menjalankannya di server tanpa tampilan (headless)?**  
J: Tentu saja. Pustaka berfungsi tanpa GUI; pastikan binari native yang diperlukan (misalnya Tesseract) terinstal di server.

**T: Bagaimana jika gambar blur?**  
J: Pertimbangkan menambahkan filter penajaman sebelum `engine.recognize`. Banyak pustaka OCR menyediakan `image_preprocessing.sharpen = True` atau Anda dapat menggunakan `cv2.GaussianBlur` dari OpenCV secara terbalik.

**T: Apakah skrip ini mendukung pemrosesan batch?**  
J: Ya. Bungkus `perform_ocr` dalam loop yang iterasi daftar path file,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}