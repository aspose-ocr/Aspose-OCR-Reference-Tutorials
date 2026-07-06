---
category: general
date: 2026-06-16
description: Mengenali teks dari gambar menggunakan mesin OCR Python – pelajari cara
  mengekstrak teks dari struk dan meningkatkan akurasi OCR dalam hitungan menit.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- improve ocr accuracy
- python ocr tutorial
- image preprocessing for OCR
language: id
og_description: Mengenali teks dari gambar dengan cepat. Panduan ini menunjukkan cara
  mengekstrak teks dari struk dan meningkatkan akurasi OCR menggunakan Python.
og_title: Mengenali teks dari gambar dengan Python OCR – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  headline: recognize text from image with Python OCR – Complete Guide
  type: TechArticle
- description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  name: recognize text from image with Python OCR – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - A sample receipt image (JPEG or PNG) that you want to
      process. - The `ocr` package (the example uses a fictional `ocr` module for
      illustration; replace it with `pytesseract`, `easyocr`, or any library t'
  - name: Expected Output
    text: 'Running the script on a typical grocery receipt yields something like:'
  - name: H3 – Crop to the Receipt Region
    text: 'If your image contains a lot of background (e.g., a photo of a desk), crop
      it first:'
  - name: H3 – Use a Custom Language Pack
    text: 'For receipts that contain foreign characters (e.g., “€” or “¥”), load the
      appropriate language data:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Mengenali teks dari gambar dengan Python OCR – Panduan Lengkap
url: /id/python-java/general/recognize-text-from-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali Teks dari Gambar dengan Python OCR – Panduan Lengkap

Pernah perlu **mengenali teks dari gambar** tetapi hasilnya terlihat seperti omong kosong? Anda tidak sendirian. Dalam banyak skenario usaha kecil—misalnya memindai struk, mendigitalkan faktur, atau mengambil data dari kartu identitas—mendapatkan output yang bersih dan dapat diandalkan adalah perbedaan antara alur kerja yang lancar dan sakit kepala.

Dalam tutorial ini kami akan membimbing Anda melalui cara praktis untuk **mengenali teks dari gambar** menggunakan pustaka Python OCR yang ringan. Kami juga akan menunjukkan cara **mengekstrak teks dari struk** dan berbagi trik untuk **meningkatkan akurasi OCR** tanpa membeli perangkat lunak mahal. Siap? Mari kita mulai.

## Apa yang Akan Anda Bangun

Pada akhir panduan ini Anda akan memiliki skrip siap‑jalankan yang:

1. Membuat instance mesin OCR.  
2. Mengaktifkan pra‑pemrosesan cerdas (deskew, despeckle, binarization).  
3. Memuat gambar struk yang berisik.  
4. Menjalankan pipeline pengenalan secara otomatis.  
5. Mencetak teks bersih yang dapat dicari ke konsol.

Tanpa layanan eksternal, tanpa kunci API tersembunyi—hanya kode Python murni yang dapat Anda sesuaikan untuk proyek apa pun.

### Prasyarat

- Python 3.8+ terpasang di mesin Anda.  
- Familiaritas dasar dengan pip dan lingkungan virtual.  
- Gambar contoh struk (JPEG atau PNG) yang ingin Anda proses.  
- Paket `ocr` (contoh menggunakan modul fiktif `ocr` untuk ilustrasi; ganti dengan `pytesseract`, `easyocr`, atau pustaka lain yang menawarkan API serupa).

> **Pro tip:** Jika Anda menemukan dependensi yang hilang, instal dengan `pip install ocr` (atau nama paket yang sebenarnya) sebelum melanjutkan.

## Langkah 1 – Mengenali Teks dari Gambar: Siapkan Mesin

Pertama-tama. Kita membutuhkan objek yang tahu cara membaca data piksel dan mengubahnya menjadi karakter. Anggap mesin sebagai otak operasi; semua hal lain memberi informasi kepadanya.

```python
import ocr  # Replace with your actual OCR library import

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Mengapa membuat mesin secara manual? Beberapa pustaka memungkinkan Anda memanggil satu fungsi, tetapi instance eksplisit memberi kontrol halus atas pra‑pemrosesan—tepat apa yang kita butuhkan untuk **meningkatkan akurasi OCR** nanti.

## Langkah 2 – Mengekstrak Teks dari Struk: Aktifkan Pra‑Pemrosesan

Struk yang dipindai dengan kamera ponsel jarang sempurna. Bisa sedikit miring, berdebu, atau terkena pencahayaan tidak merata. Mengaktifkan pra‑pemrosesan melakukan pekerjaan berat sebelum mesin bahkan melihat huruf.

```python
# Step 2: Enable preprocessing to improve recognition quality
preprocess = engine.preprocessing
preprocess.deskew = True        # Auto‑rotate slightly tilted pages
preprocess.despeckle = True     # Remove isolated noise pixels
preprocess.binarization = True  # Convert image to pure black‑white
```

*Deskew* meluruskan halaman, *despeckle* menghapus bintik‑bintik, dan *binarization* memaksa setiap piksel menjadi hitam atau putih. Tiga flag ini saja dapat **meningkatkan akurasi OCR** sebesar 20‑30 % pada struk yang berisik.

## Langkah 3 – Muat Gambar yang Ingin Anda Kenali

Sekarang kami mengarahkan mesin ke file yang sebenarnya. Jalur dapat berupa absolut atau relatif; pastikan gambar ada.

```python
# Step 3: Load the scanned receipt image
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")
```

Jika Anda bertanya-tanya apakah mesin mendukung PDF atau TIFF multi‑halaman, kebanyakan pustaka modern melakukannya—cek dokumentasinya. Untuk JPEG satu halaman, baris di atas sudah cukup.

## Langkah 4 – Jalankan OCR – Mesin Menyelesaikan Sisanya

Dengan pra‑pemrosesan yang dikonfigurasi dan gambar yang dimuat, panggilan berikutnya melakukan semuanya: mempraproses, menjalankan algoritma pengenalan, dan mengembalikan objek hasil.

```python
# Step 4: Run OCR – the configured preprocessing is applied automatically
ocr_result = engine.recognize()
```

Di balik layar mesin mungkin menggunakan Tesseract, jaringan saraf, atau mesin proprietari. Anda tidak perlu tahu detail internalnya; Anda cukup mendapatkan hasil yang bersih.

## Langkah 5 – Keluarkan Teks yang Dikenali

Akhirnya, kami mengambil teks polos dari hasil dan mencetaknya. Dalam aplikasi nyata Anda bisa menulisnya ke basis data, file CSV, atau bahkan mengirimnya ke pipeline analitik selanjutnya.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Output yang Diharapkan

Menjalankan skrip pada struk belanjaan umum menghasilkan sesuatu seperti:

```
WALMART STORE #1234
123 Main St.
Anytown, USA

Date: 06/15/2026   Time: 14:32
Cashier: J. Doe

Item                Qty   Price
---------------------------------
Milk                1     2.99
Bread               2     5.48
Eggs                1     3.20
---------------------------------
Subtotal                    11.67
Tax                         0.93
Total                       12.60
```

Jika output terlihat berantakan, periksa kembali bahwa flag pra‑pemrosesan aktif dan gambar tidak terlalu gelap. Menyetel ambang binarisasi (beberapa pustaka memungkinkan nilai kustom) dapat **meningkatkan akurasi OCR** lebih jauh.

## Lanjutan: Penyempurnaan untuk Mengekstrak Teks dari Struk Lebih Cepat

Meskipun alur lima langkah ini bekerja untuk kebanyakan kasus, Anda mungkin ingin mempercepat proses ketika menangani ratusan struk setiap malam. Berikut beberapa penyesuaian opsional:

### H3 – Potong ke Area Resi

Jika gambar Anda mengandung banyak latar belakang (misalnya foto meja), potong dulu:

```python
engine.image = engine.image.crop((50, 200, 800, 1200))  # left, top, right, bottom
```

### H3 – Gunakan Paket Bahasa Kustom

Untuk struk yang mengandung karakter asing (misalnya “€” atau “¥”), muat data bahasa yang sesuai:

```python
engine.set_language('eng+deu+fra')  # English, German, French
```

Kedua trik ini membantu mesin **mengenali teks dari gambar** dengan lebih dapat diandalkan, terutama ketika materi sumber bervariasi.

## Kesalahan Umum dan Cara Menghindarinya

- **Font Hilang:** Beberapa mesin OCR memerlukan file font untuk font struk khusus. Instal paket bahasa yang tepat.  
- **Terlalu Banyak Noise:** Bahkan dengan `despeckle=True`, pemindaian yang sangat berbutir masih dapat membingungkan mesin. Filter manual cepat di Pillow (`Image.filter(ImageFilter.MedianFilter)`) dapat membantu.  
- **DPI Tidak Tepat:** Mesin OCR mengasumsikan sekitar 300 dpi. Jika gambar Anda lebih rendah, ubah ukurannya terlebih dahulu: `engine.image = engine.image.resize((width*2, height*2))`.

Menangani masalah ini secara langsung **meningkatkan akurasi OCR** tanpa harus menggunakan layanan pihak ketiga yang mahal.

## Skrip Lengkap – Siap Dijalan

Berikut adalah program Python lengkap yang dapat dijalankan dan mencakup semua yang telah dibahas. Simpan sebagai `receipt_ocr.py` dan jalankan dengan `python receipt_ocr.py`.

```python
import ocr  # Replace with the actual library you use

def main():
    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Enable preprocessing steps
    preprocess = engine.preprocessing
    preprocess.deskew = True
    preprocess.despeckle = True
    preprocess.binarization = True

    # Load the receipt image (change the path to your file)
    engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")

    # Optional: crop out unnecessary background
    # engine.image = engine.image.crop((50, 200, 800, 1200))

    # Run the recognition pipeline
    result = engine.recognize()

    # Print the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

Menjalankan skrip ini akan **mengenali teks dari gambar** dan mencetak blok data struk yang diformat dengan rapi. Silakan sesuaikan koordinat pemotongan, pengaturan bahasa, atau flag pra‑pemrosesan agar cocok dengan tata letak struk Anda.

## Kesimpulan

Kami baru saja membahas cara sederhana untuk **mengenali teks dari gambar** menggunakan Python, menunjukkan cara **mengekstrak teks dari struk**, dan mengeksplorasi beberapa tip praktis untuk **meningkatkan akurasi OCR**. Ide dasarnya sederhana: siapkan mesin OCR, aktifkan pra‑pemrosesan cerdas, beri gambar bersih, dan biarkan pustaka melakukan pekerjaan berat.

Langkah selanjutnya? Coba proses batch struk dalam loop, simpan tiap hasil ke CSV, atau hubungkan output ke sistem pembukuan. Anda juga dapat bereksperimen dengan pustaka OCR berbasis deep‑learning seperti `easyocr` untuk akurasi lebih tinggi pada font yang kompleks.

Punya pertanyaan tentang format struk tertentu atau ingin tahu cara menangani PDF multi‑halaman? Tinggalkan komentar di bawah, dan selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}