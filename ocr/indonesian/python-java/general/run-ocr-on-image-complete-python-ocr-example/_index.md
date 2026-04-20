---
category: general
date: 2026-03-18
description: Jalankan OCR pada gambar dengan cepat menggunakan Python. Pelajari cara
  mengenali teks dari PNG, memuat gambar untuk OCR, dan mengekstrak kata‑kata dari
  gambar dalam panduan langkah demi langkah.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: id
og_description: Jalankan OCR pada gambar menggunakan Python. Tutorial ini menunjukkan
  cara mengenali teks dari PNG, memuat gambar untuk OCR, dan mengekstrak kata‑kata
  dari gambar dengan contoh kode lengkap.
og_title: Jalankan OCR pada Gambar – Panduan Python
tags:
- OCR
- Python
- Image Processing
title: Jalankan OCR pada Gambar – Contoh Lengkap OCR dengan Python
url: /id/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar – Contoh Python OCR Lengkap

Pernahkah Anda perlu **run OCR on image** file tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian; banyak pengembang mengalami kebuntuan saat pertama kali menangani ekstraksi teks dari dokumen yang dipindai. Dalam tutorial ini kami akan membahas **Python OCR example** yang memungkinkan Anda **recognize text from PNG** file, **load image for OCR**, dan **extract words from image** dengan skor kepercayaan—semua dalam beberapa baris kode.

Kami akan membahas semua yang Anda butuhkan: pustaka yang diperlukan, cara menyiapkan mesin, mengapa setiap langkah penting, dan seperti apa outputnya. Pada akhir tutorial, Anda akan dapat menyalin potongan kode ini ke dalam proyek Anda sendiri dan mulai mengekstrak teks dari gambar apa pun secara instan. Tanpa basa-basi, hanya solusi praktis yang dapat dijalankan.

## Apa yang Anda Butuhkan

- Python 3.8 atau lebih baru terpasang  
- Paket `ocrengine` (atau pustaka apa pun yang menyediakan kelas `OcrEngine`). Anda dapat menginstalnya via `pip install ocrengine` – sesuaikan nama jika Anda menggunakan pustaka OCR lain seperti `pytesseract`.  
- File gambar (PNG, JPG, dll.) yang ingin Anda proses – untuk panduan ini kami akan menggunakan `invoice.png`.  

Itu saja. Tanpa dependensi berat, tanpa layanan eksternal, hanya Python murni.

![contoh run OCR pada gambar – faktur yang dipindai sedang diproses](/images/run-ocr-on-image.png)

*Alt text: contoh run OCR pada gambar – faktur yang dipindai sedang diproses*

## Langkah 1 – Instal dan Impor Pustaka OCR

Pertama-tama, mari kita dapatkan mesin OCR ke dalam lingkungan kita dan mengimpornya. Jika Anda menggunakan paket hipotetik `ocrengine`, impor terlihat seperti ini:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Why this matters:** Mengimpor kelas yang tepat memberi Anda akses ke metode yang akan kami panggil nanti, seperti `setImageFromFile` dan `recognize`. Jika Anda melewatkan langkah ini, Python akan mengeluarkan `ModuleNotFoundError`, dan Anda akan terhenti sebelum bahkan memuat gambar.

## Langkah 2 – Buat Instance Mesin OCR

Sekarang pustaka sudah siap, kita memerlukan objek mesin yang akan menyimpan konfigurasi dan status untuk proses pengenalan.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Pro tip:* Beberapa mesin OCR memungkinkan Anda menyesuaikan model bahasa atau pengaturan DPI pada titik ini. Untuk **python OCR example** dasar, nilai default sudah cukup, tetapi jika Anda menangani pemindaian beresolusi rendah, pertimbangkan untuk menyesuaikannya di sini.

## Langkah 3 – Muat Gambar yang Ingin Diproses

Langkah logis berikutnya adalah **load image for OCR**. Anda mengarahkan mesin ke jalur file PNG (atau format lain yang didukung) yang ingin Anda analisis.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**What’s happening under the hood?** Mesin membaca data piksel, mengubahnya menjadi format yang dapat dipahami algoritma pengenalan, dan menyimpannya secara internal. Jika jalur file salah, Anda akan mendapatkan `FileNotFoundError`, jadi periksa kembali apakah gambar tersebut ada.

## Langkah 4 – Jalankan Algoritma Pengenalan

Dengan gambar yang dimuat, akhirnya kami **run OCR on image** untuk mengekstrak konten teks.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

Pada titik ini mesin memindai bitmap, menerapkan pencocokan pola, dan mengembalikan objek yang berisi setiap kata yang terdeteksi, baris, dan metrik kepercayaan.

## Langkah 5 – Iterasi Kata yang Dikenali dan Tampilkan Kepercayaan

Bagian paling berguna dari alur kerja OCR apa pun adalah melihat **the confidence** untuk setiap token yang diekstrak. Ini memberi tahu Anda seberapa yakin mesin tentang setiap kata, memungkinkan Anda menyaring hasil dengan kepercayaan rendah jika diperlukan.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Expected output** (sample):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Anda sekarang dapat melihat tepat **what words were extracted from the image** dan seberapa dapat diandalkan setiap deteksi. Ini adalah inti dari setiap pipeline **extract words from image**.

## Menangani Kasus Tepi Umum

### Bagaimana Jika Gambar Berwarna Grayscale?

Beberapa mesin OCR bekerja lebih baik dengan gambar berwarna. Jika Anda memperhatikan kepercayaan rendah secara keseluruhan, coba ubah PNG menjadi versi hitam‑putih dengan kontras lebih tinggi sebelum memberi makan ke mesin. Pillow dapat membantu:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Menangani Banyak Bahasa

Jika dokumen Anda berisi bahasa Inggris dan Spanyol, Anda ingin **recognize text from PNG** menggunakan model multibahasa. Sebagian besar mesin memungkinkan Anda mengatur daftar bahasa saat inisialisasi:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Menyaring Kata‑Kata dengan Kepercayaan Rendah

Kadang-kadang Anda hanya membutuhkan kata dengan kepercayaan di atas, misalnya, 90 %. Filter cepat terlihat seperti ini:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Skrip Lengkap, Siap‑Jalankan

Menggabungkan semuanya, berikut satu skrip yang dapat Anda salin‑tempel dan jalankan segera (cukup ganti jalur ke PNG Anda).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Jalankan dengan:

```bash
python run_ocr_on_image.py
```

Anda akan melihat daftar kata dan persentase kepercayaan tercetak di konsol, persis seperti yang ditunjukkan sebelumnya.

## Pertanyaan yang Sering Diajukan

**Apakah ini bekerja dengan file JPG atau TIFF?**  
Tentu saja. Metode `setImageFromFile` menerima format apa pun yang dapat didekode oleh pustaka dasar, sehingga Anda dapat **run OCR on image** file tipe JPG, TIFF, BMP, dll.

**Bisakah saya memproses banyak gambar dalam loop?**  
Tentu saja. Bungkus langkah pemuatan dan pengenalan di dalam loop `for` atas daftar jalur file. Hanya ingat untuk menginisialisasi ulang mesin jika pustaka memerlukan instance baru per gambar.

**Bagaimana jika saya membutuhkan teks dalam satu string alih‑alih per‑kata?**  
Sebagian besar objek hasil OCR menyediakan metode `getText()` yang mengembalikan seluruh dokumen. Contoh:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Langkah Selanjutnya dan Topik Terkait

Sekarang Anda tahu cara **run OCR on image**, pertimbangkan untuk menjelajahi:

- **Post‑processing**: Gunakan ekspresi reguler untuk membersihkan tanggal, jumlah, atau ID yang diekstrak dari faktur.  
- **Batch processing**: Gabungkan skrip dengan `os.listdir()` untuk menangani seluruh folder dokumen yang dipindai.  
- **Alternative libraries**: `pytesseract` adalah opsi open‑source yang populer; alur kerjanya serupa—cukup ganti pemanggilan mesin.  
- **Exporting results**: Tulis kata yang diekstrak dan skor kepercayaan ke CSV untuk analisis lebih lanjut.

Setiap ekstensi ini dibangun langsung di atas fondasi yang kami buat di sini, memungkinkan Anda mengubah data OCR mentah menjadi informasi yang dapat ditindaklanjuti.

---

### TL;DR

Kami telah menunjukkan **python OCR example** yang ringkas yang mendemonstrasikan cara **load image for OCR**, **run OCR on image**, dan **extract words from image** sambil melaporkan kepercayaan. Skrip lengkap siap dijalankan, dan Anda kini memiliki pengetahuan untuk menyesuaikannya ke proyek apa pun yang membutuhkan **recognize text from PNG** (atau format lain). Cobalah, sesuaikan ambang kepercayaan, dan saksikan aplikasi Anda menjadi sadar teks dalam hitungan menit. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}