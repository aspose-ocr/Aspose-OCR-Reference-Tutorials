---
category: general
date: 2026-06-25
description: Pemrosesan OCR batch di Python menjadi mudah. Pelajari cara mengekstrak
  teks dari kumpulan gambar dan kuasai ekstraksi teks gambar batch dengan thread paralel.
draft: false
keywords:
- batch OCR processing
- extract text from image batch
- batch image text extraction
language: id
og_description: Pemrosesan OCR batch dalam Python memungkinkan Anda mengekstrak teks
  dari kumpulan gambar dengan cepat. Tutorial ini membimbing Anda melalui OCR paralel
  dengan contoh kode yang jelas.
og_title: Pemrosesan OCR Batch di Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  headline: Batch OCR Processing in Python – Complete Programming Guide
  type: TechArticle
- description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  name: Batch OCR Processing in Python – Complete Programming Guide
  steps:
  - name: Missing or Corrupt Images
    text: If an image can’t be opened, most OCR libraries raise an exception that
      aborts the whole batch. Wrap the call in a `try/except` inside the batch function
      or filter out problematic files beforehand (see the sanity check in Step 1).
  - name: Language & DPI Settings
    text: For multilingual documents, pass a `langs` parameter (e.g., `langs=['en',
      'de']`). If your scans are low‑resolution, consider pre‑processing with `Pillow`
      to upscale to 300 DPI before OCR—this often boosts accuracy.
  - name: Memory Constraints
    text: 'Eight threads can eat RAM, especially with large images. If you hit memory
      errors, lower `max_threads` or process the list in smaller chunks:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Pemrosesan OCR Batch di Python – Panduan Pemrograman Lengkap
url: /id/python-java/general/batch-ocr-processing-in-python-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pemrosesan OCR Batch di Python – Panduan Pemrograman Lengkap

Pernah membutuhkan **batch OCR processing** tetapi tidak yakin cara menjalankannya secara efisien pada puluhan halaman yang dipindai? Anda tidak sendirian—para pengembang sering menemui kendala ketika mencoba mengekstrak teks dari batch gambar tanpa membuat CPU mereka kehabisan daya.  

Dalam panduan ini kami akan menunjukkan cara sederhana untuk **extract text from image batch** menggunakan mesin OCR Python, menjalankan pekerjaan pada hingga delapan thread, dan akhirnya melihat berapa banyak karakter yang dihasilkan oleh setiap gambar. Pada akhir tutorial Anda akan memiliki skrip yang dapat digunakan kembali untuk menangani **batch image text extraction** seperti seorang profesional.

## Apa yang Dibahas dalam Tutorial Ini

Kami akan melangkah melalui tiga langkah praktis:

1. Membuat daftar file gambar yang ingin Anda kenali.  
2. Menjalankan mesin OCR secara paralel dengan `max_threads=8`.  
3. Mengulang hasil dan mencetak ringkasan singkat.

Tanpa layanan eksternal, tanpa pustaka yang tidak dikenal—hanya Python biasa dan pembungkus OCR tipikal (misalnya, `ocr` dari `easyocr` atau pembungkus khusus). Jika Anda sudah memiliki Python 3.8+ dan paket OCR terpasang, Anda siap untuk menyalin‑tempel dan menjalankannya.

---

## Langkah 1: Siapkan Daftar File Gambar untuk Pemrosesan OCR Batch

Hal pertama yang Anda perlukan adalah kumpulan jalur gambar. Anggaplah ini sebagai daftar belanja untuk mesin OCR; setiap entri mengarah ke file PNG, JPEG, atau TIFF yang berisi teks yang ingin Anda baca.

```python
# Step 1: Prepare a list of image files to be recognized
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png",
    "YOUR_DIRECTORY/page4.png",
    "YOUR_DIRECTORY/page5.png"
]

# Quick sanity check – make sure the files exist
import os
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"These files are missing: {missing}")
```

**Mengapa ini penting:**  
Membuat daftar di awal memungkinkan mesin OCR bekerja dalam mode batch sejati. Ini juga memberi Anda satu tempat untuk menambah atau menghapus file tanpa menyentuh logika pemrosesan nanti. Pemeriksaan kelayakan mencegah kegagalan “file tidak ditemukan” yang menyebalkan di tengah proses panjang.

---

## Langkah 2: Jalankan OCR pada Batch dengan Thread Paralel (Extract Text from Image Batch)

Sekarang kami menyerahkan daftar tersebut ke mesin OCR. Sebagian besar pembungkus OCR modern menyediakan metode `recognize_batch` yang menerima argumen `max_threads`. Dengan mengaturnya ke `8` kami memberi tahu pustaka untuk memulai delapan thread pekerja, yang pada CPU quad‑core dengan hyper‑threading dapat secara dramatis mengurangi waktu pemrosesan.

```python
# Step 2: Run OCR on the batch, allowing up to 8 parallel threads
# Assuming `ocr` is a module that provides OcrEngine with recognize_batch()
import ocr

batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# batch_results is a list of Result objects, each with a .text attribute
```

**Mengapa paralelisme membantu:**  
OCR bersifat intensif CPU; setiap gambar diproses melalui jaringan saraf atau mesin lama. Menjalankannya satu per satu dapat sangat lambat, terutama untuk pemindaian resolusi tinggi. Thread paralel membuat semua core sibuk, mengubah pekerjaan 5‑menit menjadi 1‑menit pada perangkat keras tipikal.

**Tip:** Jika Anda menggunakan `easyocr`, pemanggilan terlihat seperti `reader.readtext(image_path, detail=0)` di dalam loop. Abstraksi `recognize_batch` kami menyembunyikan kompleksitas itu, tetapi Anda selalu dapat menggantinya dengan `ThreadPoolExecutor` Anda sendiri jika pustaka tidak menyediakan dukungan batch.

---

## Langkah 3: Iterasi Hasil dan Ringkas Ekstraksi Teks Gambar Batch

Setelah OCR selesai, Anda akan memiliki daftar objek hasil. Mari gabungkan jalur file asli dengan output OCR yang bersesuaian dan cetak satu baris rapi untuk setiap gambar yang menunjukkan berapa banyak karakter yang dikenali.

```python
# Step 3: Iterate through the results and display character counts
for file_path, result in zip(image_files, batch_results):
    # result.text holds the raw extracted string
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Apa yang akan Anda lihat:**  

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

**Mengapa langkah ini berguna:**  
Hitungan karakter cepat memberi tahu Anda sekilas apakah sebuah gambar diproses dengan benar. Hitungan yang secara tak terduga rendah dapat menandakan pemindaian yang buram, pengaturan bahasa yang salah, atau file yang rusak—masalah yang dapat Anda selesaikan sebelum melanjutkan ke analisis lanjutan.

---

## Bonus: Menangani Kasus Tepi dan Kesalahan Umum

### Gambar Hilang atau Rusak  
Jika sebuah gambar tidak dapat dibuka, sebagian besar pustaka OCR akan melemparkan pengecualian yang menghentikan seluruh batch. Bungkus pemanggilan dalam `try/except` di dalam fungsi batch atau saring file bermasalah sebelumnya (lihat pemeriksaan kelayakan pada Langkah 1).

### Pengaturan Bahasa & DPI  
Untuk dokumen multibahasa, berikan parameter `langs` (mis., `langs=['en', 'de']`). Jika pemindaian Anda beresolusi rendah, pertimbangkan pra‑pemrosesan dengan `Pillow` untuk meningkatkan ke 300 DPI sebelum OCR—ini sering meningkatkan akurasi.

### Kendala Memori  
Delapan thread dapat menghabiskan RAM, terutama dengan gambar besar. Jika Anda mengalami kesalahan memori, turunkan `max_threads` atau proses daftar dalam potongan yang lebih kecil:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(image_files, 3):  # process three images at a time
    results = ocr.OcrEngine.recognize_batch(chunk, max_threads=3)
    # handle results...
```

---

## Skrip Lengkap yang Berfungsi

Menggabungkan semuanya, berikut contoh lengkap yang siap dijalankan. Ganti `"YOUR_DIRECTORY"` dengan jalur yang berisi file PNG Anda dan pastikan modul `ocr` telah terpasang.

```python
#!/usr/bin/env python3
"""
Batch OCR Processing Script
Extracts text from an image batch using parallel threads and prints character counts.
"""

import os
import ocr  # Replace with your OCR library import, e.g., from easyocr import Reader

# -------------------------------------------------
# Step 1: Define the list of image files
# -------------------------------------------------
image_dir = "YOUR_DIRECTORY"
image_files = [
    os.path.join(image_dir, f"page{i}.png") for i in range(1, 6)
]

# Verify that all files exist
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"Missing image files: {missing}")

# -------------------------------------------------
# Step 2: Run OCR in parallel (max 8 threads)
# -------------------------------------------------
# The OcrEngine is a placeholder – adapt to your library's API
batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# -------------------------------------------------
# Step 3: Report how many characters each image yielded
# -------------------------------------------------
for file_path, result in zip(image_files, batch_results):
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Output yang diharapkan** (angka Anda akan berbeda):

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

Jalankan skrip dengan `python batch_ocr.py` dan saksikan terminal menampilkan statistik singkat.

---

## Gambaran Visual

![Diagram alur pemrosesan OCR batch](image-placeholder.png "Diagram yang menggambarkan langkah‑langkah pemrosesan OCR batch")

*Image alt text:* *Diagram alur pemrosesan OCR batch yang menunjukkan pembuatan daftar file, eksekusi OCR paralel, dan rangkuman hasil.*

---

## Kesimpulan

Anda kini memiliki fondasi yang kuat untuk **batch OCR processing** di Python. Dengan menyiapkan daftar gambar yang bersih, memanfaatkan thread paralel untuk **extract text from image batch**, dan merangkum hasilnya, Anda dapat mengubah tugas manual yang melelahkan menjadi alur kerja yang cepat dan dapat diulang.  

Dari sini Anda mungkin:

- Simpan setiap `result.text` ke file `.txt` untuk NLP downstream.  
- Gabungkan hitungan karakter dengan skor kepercayaan untuk menyaring halaman berkualitas rendah.  
- Integrasikan skrip ke dalam alur kerja ingest dokumen yang lebih besar, mungkin memasok indeks pencarian.

Apakah Anda sedang mendigitalkan arsip, membangun aplikasi pemindaian struk, atau menyiapkan data pelatihan untuk model bahasa, konsep yang dibahas di sini dapat diskalakan ke ratusan atau ribuan file dengan sedikit penyesuaian.

Ada pertanyaan tentang pengaturan bahasa, pra‑pemrosesan gambar, atau penyebaran di cloud? Tinggalkan komentar atau lihat tutorial terkait tentang *Python image preprocessing* dan *asynchronous OCR with asyncio*. Selamat coding!

---

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara Batch OCR Gambar dengan Daftar di Aspose.OCR untuk .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}