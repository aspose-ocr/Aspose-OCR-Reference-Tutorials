---
category: general
date: 2026-06-28
description: Cara melakukan OCR batch menggunakan Python. Pelajari cara OCR banyak
  gambar, mengekstrak teks dari PNG, dan mengubah gambar menjadi teks dengan tutorial
  OCR Python lengkap.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: id
og_description: Cara melakukan OCR batch di Python dijelaskan dalam kalimat pertama.
  Ikuti tutorial OCR Python ini untuk mengekstrak teks dari file PNG secara efisien.
og_title: Cara Batch OCR di Python – Panduan Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Cara Melakukan OCR Batch di Python – Panduan Lengkap Langkah demi Langkah
url: /id/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di Python – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya-tanya **bagaimana cara batch OCR** pada tumpukan halaman yang dipindai tanpa menulis loop yang memblokir UI Anda? Anda tidak sendirian. Memproses puluhan file PNG satu‑per‑satu bisa terasa seperti menunggu cat mengering, terutama ketika setiap gambar memerlukan satu atau dua detik untuk didekode.  

Dalam tutorial ini kami akan menunjukkan cara bersih dan non‑blocking untuk **OCR banyak gambar** sekaligus, **mengekstrak teks dari PNG** file, dan **mengonversi gambar ke teks** menggunakan mesin OCR Python modern. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang dapat Anda masukkan ke proyek apa pun – sempurna untuk *python ocr tutorial* cepat atau pekerjaan batch produksi.

## Apa yang Akan Anda Bangun

- Menginisialisasi mesin OCR dan mengatur bahasanya ke Latin (atau bahasa apa pun yang Anda butuhkan).  
- Memberi daftar jalur gambar (PNG dalam contoh kami) ke mesin.  
- Menjalankan operasi batch yang mengembalikan objek mirip Future.  
- Mengambil semua hasil secara bersamaan dengan thread pool, sehingga thread utama tetap bebas.  
- Mencetak teks yang dikenali untuk setiap halaman, dipisahkan dengan rapi.

Tidak ada sihir tersembunyi, hanya Python biasa dan perpustakaan OCR pihak ketiga (kami akan menggunakan paket fiktif `pyocr` untuk ilustrasi).  

**Prasyarat**  
- Python 3.8+ terpasang.  
- Familiaritas dasar dengan fungsi Python dan `concurrent.futures`.  
- Akses ke perpustakaan OCR yang menyediakan kelas `OcrEngine` (misalnya, `pip install pyocr`).  

Jika Anda belum memiliki salah satu dari itu, dapatkan sekarang – lebih mudah daripada yang Anda kira.

---

## Cara Batch OCR di Python – Konsep Inti

Sebelum kita masuk ke kode, mari jawab “mengapa” di balik setiap langkah.

1. **Mengapa mengatur bahasa?**  
   Akurasi OCR melambung ketika mesin tahu karakter apa yang diharapkan. Latin cocok untuk Inggris, Prancis, Spanyol, dll. Ganti ke `Language.Japanese` atau `Language.Arabic` bila diperlukan.

2. **Mengapa menggunakan operasi batch?**  
   Panggilan batch memungkinkan mesin menjadwalkan pekerjaan secara internal, seringkali memanfaatkan thread native atau akselerasi GPU. Ia mengembalikan handle yang dapat Anda query nanti, sehingga Anda tidak terblokir saat tiap gambar diproses.

3. **Mengapa ThreadPoolExecutor?**  
   Objek Future yang kita terima bersifat *lazy* – ia hanya mulai menarik hasil ketika diminta. Dengan memberikan thread pool ke `getAll`, kita biarkan Python mengambil teks tiap halaman secara paralel, memotong waktu eksekusi secara signifikan.

4. **Mengapa enumerate hasil?**  
   Urutan hasil cocok dengan urutan jalur input, sehingga kita dapat memberi label nomor halaman dengan aman.

Memahami “mengapa” ini membantu Anda menyesuaikan pola ke perpustakaan lain atau dataset yang lebih besar.

---

## Langkah 1: Instal dan Impor Paket yang Diperlukan

Pertama, pastikan perpustakaan OCR terinstal. Contoh ini menggunakan paket generik `pyocr`; ganti dengan perpustakaan yang Anda pilih (mis. `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Sekarang impor semua yang diperlukan.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Pro tip:** Menggunakan `Path` dari `pathlib` membuat skrip Anda bersifat OS‑agnostic dan lebih mudah dibaca.

---

## Langkah 2: Buat Mesin OCR dan Atur Bahasa

Membuat mesin sangat mudah. Kami akan mengunci ke Latin untuk demo ini.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

Pemanggilan `setLanguage` bersifat opsional untuk beberapa mesin, tetapi merupakan kebiasaan yang baik. Ini memberi tahu model OCR untuk fokus pada set karakter yang Anda butuhkan, meningkatkan kecepatan dan akurasi.

---

## Langkah 3: Daftar File Gambar yang Akan Diproses (Extract Text from PNG)

Kumpulkan semua file PNG yang ingin Anda konversi. Menggunakan `Path.glob` berarti Anda dapat menaruh seluruh folder tanpa mengubah skrip.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Mengapa ini penting:** Dengan menyortir daftar, kami menjamin urutan deterministik, yang kemudian menyelaraskan setiap hasil dengan nomor halaman yang tepat.

---

## Langkah 4: Jalankan Operasi Batch OCR (Convert Image to Text)

Sekarang kami menyerahkan daftar ke mesin. Metode ini mengembalikan kontainer mirip Future yang akan kami polling nanti.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Di balik layar mesin mungkin memulai thread pekerja sendiri atau bahkan pipeline GPU. Yang penting bagi kami adalah memiliki handle (`batch_future`) yang tahu cara mengambil hasil individual.

---

## Langkah 5: Ambil Semua Hasil Secara Bersamaan (OCR Multiple Images)

Di sinilah kita benar‑benar *batch* pekerjaan. Dengan memberikan `ThreadPoolExecutor` ke `getAll`, teks tiap halaman diambil di thread masing‑masing.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Anda dapat menyesuaikan `max_workers` berdasarkan jumlah core CPU atau rekomendasi perpustakaan OCR. Lebih banyak pekerja ≠ selalu lebih cepat – perhatikan penggunaan CPU Anda.

---

## Langkah 6: Tampilkan Teks yang Dikenali (Python OCR Tutorial Finale)

Akhirnya, cetak teks tiap halaman. Objek `Result` menyediakan `getText()` – sesuaikan jika perpustakaan Anda memakai nama metode berbeda.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Output yang diharapkan (contoh)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Jika ada gambar yang gagal, kebanyakan mesin mengembalikan string kosong atau melempar exception – Anda dapat membungkus loop dalam blok `try/except` untuk menangani kasus tepi dengan elegan.

---

## Skrip Lengkap – Siap Dijalan

Berikut adalah skrip lengkap yang berdiri sendiri. Salin‑tempel ke file bernama `batch_ocr.py`, sesuaikan `YOUR_DIRECTORY`, dan jalankan `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Simpan, jalankan, dan saksikan konsol terisi teks yang diekstrak. Sederhana, cepat, dan sepenuhnya asynchronous.

---

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Tidak ada output** – string kosong | Mesin OCR tidak menemukan teks (gambar terlalu berisik) | Praproses gambar: binarisasi, deskew, atau tingkatkan DPI |
| **`FileNotFoundError`** | Jalur direktori salah atau file PNG tidak ada | Periksa kembali `YOUR_DIRECTORY` dan pastikan file berakhiran `.png` |
| **Penggunaan CPU tinggi** | `max_workers` terlalu tinggi untuk mesin Anda | Kurangi `max_workers` atau aktifkan akselerasi GPU bila didukung |
| **Karakter Unicode kacau** | Mesin default ke bahasa lain | Panggil `engine.setLanguage(Language.Latin)` (atau yang sesuai) sebelum batch OCR |

Menangani hal‑hal ini sejak awal menghemat berjam‑jam debugging.

---

## Memperluas Tutorial – Langkah Selanjutnya

- **OCR banyak gambar** dalam format lain (JPEG, TIFF) – cukup ubah pola glob.  
- **Extract text from PNG** dan masukkan ke indeks pencarian (mis. Elasticsearch).  
- **Convert image to text** untuk pembuatan PDF menggunakan `reportlab` atau `PyPDF2`.  
- **Paralelisasi lintas mesin** dengan `multiprocessing` atau antrian tugas seperti Celery untuk dataset masif.  

Masing‑masing topik ini berkembang secara alami dari **python ocr tutorial** yang baru saja Anda selesaikan.

---

## Kesimpulan

Kami telah membahas **cara batch OCR** sekumpulan file PNG, mendemonstrasikan kekuatan API berorientasi batch, dan menunjukkan cara **extract text from PNG** dengan pendekatan thread‑pooled. Skrip lengkap di atas siap produksi, dan Anda kini memiliki fondasi kuat untuk proyek Python yang berat OCR.

Cobalah, ubah pengaturan bahasa, bahkan ganti `pyocr` dengan `pytesseract` – pola tetap sama. Punya pertanyaan atau ingin berbagi kasus penggunaan menarik? Tinggalkan komentar, dan mari terus berdiskusi.

*Selamat coding!*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}