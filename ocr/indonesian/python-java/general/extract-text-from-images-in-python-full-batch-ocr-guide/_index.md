---
category: general
date: 2026-06-19
description: Ekstrak teks dari gambar di Python dengan mesin OCR sederhana. Pelajari
  cara mengonversi gambar yang dipindai menjadi teks, mengenali teks dari foto, dan
  menampilkan daftar file gambar di Python secara efisien.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: id
og_description: Ekstrak teks dari gambar di Python menggunakan mesin OCR ringan. Panduan
  ini menunjukkan cara mengonversi gambar yang dipindai menjadi teks, mengenali teks
  dari foto, dan menampilkan daftar file gambar di Python dalam beberapa langkah.
og_title: Ekstrak Teks dari Gambar di Python – Panduan OCR Batch Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Ekstrak Teks dari Gambar dengan Python – Panduan OCR Batch Lengkap
url: /id/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Python – Panduan OCR Batch Lengkap

Pernah membutuhkan untuk **extract text from images** tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—para pengembang terus-menerus menghadapi tantangan mengubah PDF yang dipindai, kwitansi yang difoto, atau screenshot menjadi teks yang dapat dicari. Dalam tutorial ini kami akan membahas contoh lengkap yang siap‑jalan yang menunjukkan cara **convert scanned images to text**, mengenali teks dari gambar, dan bahkan **list image files python**‑style. Pada akhir Anda akan memiliki skrip yang dapat digunakan kembali yang memproses seluruh folder sekaligus.

Kami akan membahas semua yang Anda butuhkan: pustaka yang diperlukan, mengapa setiap langkah penting, penanganan kasus tepi, dan sedikit pemecahan masalah. Tidak perlu mencari dokumentasi eksternal; kode di bawah ini berdiri sendiri, dan penjelasannya menjawab “bagaimana” *dan* “mengapa”. Buka IDE favorit Anda, dan mari kita mulai.

---

## Apa yang Akan Anda Bangun

- Inisialisasi mesin OCR (kami akan menggunakan paket `ocr` untuk ilustrasi).
- Pindai sebuah direktori dan **list image files python**‑style, menyaring PNG, JPG, dan TIFF.
- Jalankan operasi **batch OCR** pada semua gambar yang ditemukan.
- Cetak teks yang diekstrak untuk setiap file, dengan label yang jelas.

> **Pro tip:** Jika Anda belum menginstal pustaka `ocr`, Anda dapat menggantinya dengan `pytesseract` dengan beberapa perubahan kecil—logika inti tetap sama.

---

## Prasyarat

- Python 3.8+ (skrip ini menggunakan f‑strings dan type hints).
- Sebuah pustaka OCR yang menyediakan `OcrEngine` dengan `recognize_batch`. Untuk panduan ini kami mengasumsikan paket `ocr` fiktif, tetapi pola ini bekerja dengan pustaka nyata.
- Sebuah folder yang berisi file gambar yang ingin Anda proses (`.png`, `.jpg`, `.tif`).

---

## Langkah 1 – Instal & Impor Modul yang Diperlukan

Pertama, pastikan paket OCR tersedia. Jika Anda menggunakan pustaka nyata seperti `pytesseract`, ganti impor sesuai.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Why this matters:** Mengimpor `os` memberi kita penanganan path lintas‑platform, sementara `typing.List` membantu dengan autocomplete IDE dan membuat kode tahan masa depan.

---

## Langkah 2 – **Extract Text from Images**: Inisialisasi Mesin OCR

Membuat mesin adalah langkah pertama menuju pekerjaan OCR apa pun. Kami juga mengatur bahasa ke auto‑detect sehingga mesin dapat menangani dokumen dengan bahasa campuran.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Explanation:** Dengan membungkus pembuatan mesin dalam sebuah fungsi, kami menjaga kode tetap modular. Jika nanti Anda perlu menyesuaikan DPI atau mode OCR, Anda hanya mengedit satu tempat ini.

---

## Langkah 3 – **List Image Files Python**: Kumpulkan File dari Direktori

Sekarang kita perlu menemukan setiap gambar yang ingin diproses. List comprehension di bawah ini mencerminkan pola “list image files python” yang umum.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Edge case handling:** Fungsi ini mengabaikan sub‑folder (Anda dapat menambahkan rekursi nanti) dan secara otomatis menyaring file tersembunyi karena biasanya tidak berakhiran ekstensi yang didukung.

---

## Langkah 4 – **Convert Scanned Images to Text**: Jalankan Batch OCR

Sebagian besar pustaka OCR menyediakan metode batch yang jauh lebih cepat dibandingkan memproses satu gambar sekaligus. Berikut cara memanggilnya.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Why batch?** Mengirim semua gambar sekaligus mengurangi overhead (mis., memuat model OCR berulang kali) dan sering menghasilkan pemanfaatan CPU/GPU yang lebih baik.

---

## Langkah 5 – **Recognize Text from Pictures**: Tampilkan Hasil

Akhirnya, kami mengiterasi nama file yang dipasangkan dengan hasil OCR, mencetak header bersih untuk setiap gambar.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Tip:** `strip()` menghapus spasi kosong di awal/akhir yang sering ditambahkan OCR.

---

## Script Lengkap – Gabungkan Semua

Berikut adalah program lengkap yang dapat dijalankan. Simpan sebagai `batch_ocr.py` dan jalankan `python batch_ocr.py <your_folder>`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Output yang Diharapkan

Dengan asumsi folder berisi `invoice1.png` dan `receipt.jpg`, Anda mungkin melihat:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

Setiap blok jelas berlabel, membuat pemrosesan selanjutnya (mis., menyimpan ke basis data) menjadi sederhana.

---

## Menangani Kendala Umum

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Tidak ada teks muncul** | Bahasa OCR tidak terdeteksi atau gambar terlalu kontras rendah. | Paksa bahasa (`engine.language = ocr.Language.English`) atau pra‑proses gambar (tingkatkan kontras). |
| **Kesalahan memori pada batch besar** | Mesin mencoba memuat semua gambar sekaligus. | Bagi `image_files` menjadi potongan (`batch_size = 20`) dan panggil `recognize_batch` berulang kali. |
| **Format file tidak didukung** | Anda menambahkan `.gif` atau `.bmp`. | Perluas tuple `supported_exts` atau konversi gambar ke PNG/JPG terlebih dahulu. |
| **Unicode rusak** | OCR mengembalikan bytes alih-alih string. | Pastikan pustaka OCR mengeluarkan Unicode (`result.text.decode('utf‑8')` jika diperlukan). |

---

## Memperluas Alur Kerja

Sekarang Anda dapat **extract text from images**, pertimbangkan langkah selanjutnya berikut:

- **Export to CSV** – Tulis setiap nama file dan teks yang diekstrak ke spreadsheet untuk analisis.
- **Parallel processing** – Gunakan `concurrent.futures.ThreadPoolExecutor` untuk menangani beberapa batch secara bersamaan.
- **Integrate with cloud OCR** – Ganti mesin lokal dengan Google Vision atau Azure OCR untuk akurasi lebih tinggi pada tata letak kompleks.
- **Add image preprocessing** – Pustaka seperti Pillow atau OpenCV dapat memperbaiki kemiringan, mengurangi noise, atau melakukan threshold pada gambar sebelum OCR, meningkatkan hasil.

Semua ide ini secara alami melibatkan fungsi inti yang sama yang telah kami buat, jadi Anda tidak perlu memulai dari nol.

---

## Kesimpulan

Kami baru saja membahas solusi lengkap untuk **extract text from images** dengan Python, mencakup semua hal mulai dari **list image files python** hingga **recognize text from pictures** dan akhirnya **convert scanned images to text** dalam batch yang rapi. Skrip ini sengaja sederhana namun cukup fleksibel untuk menjadi fondasi proyek yang lebih besar—apakah Anda mendigitalkan kwitansi, membangun arsip yang dapat dicari, atau menggerakkan pipeline ekstraksi data.

Cobalah, sesuaikan langkah pra‑proses, dan saksikan akurasi OCR Anda meningkat. Jika Anda menemui kendala, tinjau kembali tabel “Menangani Kendala Umum”; kebanyakan masalah dapat diselesaikan dengan perubahan konfigurasi kecil.

Siap untuk tantangan berikutnya? Coba tambahkan langkah konversi PDF‑ke‑gambar menggunakan `pdf2image`, lalu masukkan gambar tersebut langsung ke pipeline yang sama. Langit adalah batasnya ketika Anda menggabungkan OCR dengan ekosistem Python yang kaya.

Selamat coding, dan semoga teks Anda selalu terbaca!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}