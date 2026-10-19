---
category: general
date: 2026-03-18
description: Ekstrak teks dari PNG menggunakan Python dan Aspose OCR. Pelajari cara
  memuat gambar untuk OCR, menjalankan OCR pada banyak file, dan melakukan OCR batch
  gambar dengan pengenalan gambar paralel.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: id
og_description: Ekstrak teks dari PNG dengan Aspose OCR di Python. Tutorial ini menunjukkan
  cara memuat gambar untuk OCR, memproses OCR pada banyak file, dan menjalankan batch
  OCR gambar menggunakan pengenalan gambar paralel.
og_title: Ekstrak teks dari PNG – Panduan OCR Paralel
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Ekstrak teks dari PNG – Panduan OCR Paralel untuk Pengakuan Gambar Batch
url: /id/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak teks dari PNG – Panduan OCR Paralel untuk Pengolahan Gambar Batch

Pernahkah Anda perlu **mengekstrak teks dari PNG** tetapi terjebak pada titik di mana satu gambar membutuhkan waktu lama untuk diproses? Anda tidak sendirian. Dalam banyak proyek dunia nyata—seperti pemindai faktur, digitalisasi struk, atau alat arsip—kecepatan sangat penting, dan memproses setiap PNG satu per satu tidak cukup.  

Dalam panduan ini kami akan menjelaskan solusi lengkap yang siap dijalankan yang **memuat gambar untuk OCR**, menjalankan **ocr multiple files** dalam pola **batch OCR images**, dan memanfaatkan **parallel image recognition** dengan modul `threading` Python. Pada akhir panduan Anda akan memiliki skrip yang mengekstrak teks dari sejumlah PNG dalam hitungan detik, bukan menit.

## Apa yang Anda Butuhkan

- Python 3.8 atau lebih baru (sintaks yang ditunjukkan juga berfungsi pada 3.10+).  
- Paket Aspose OCR untuk Java/Python (`aspose-ocr`). Anda dapat menginstalnya melalui `pip`.  
- Sebuah folder berisi beberapa file PNG yang ingin Anda proses.  
- Jumlah RAM yang cukup—setiap thread menyimpan instance mesin OCR yang kecil, sehingga bahkan laptop dapat menjalankan puluhan pekerja.

Tidak ada layanan eksternal, tidak ada kunci cloud, dan tidak ada file konfigurasi misterius. Hanya kode Python murni yang dapat Anda salin‑tempel dan jalankan.

## Mengapa mengekstrak teks dari PNG secara paralel?

Memproses PNG bersifat CPU‑bound: mesin OCR menjalankan serangkaian algoritma analisis gambar yang memproses data piksel. Ketika Anda memiliki sepuluh, dua puluh, atau seratus gambar, total waktu eksekusi pada dasarnya adalah jumlah dari masing‑masing proses.  

Dengan membuat thread untuk setiap file, kita membiarkan sistem operasi menjadwalkan pekerjaan berat CPU tersebut secara bersamaan. Pada mesin multi‑core hal ini sering memotong setengah—atau bahkan seperempat—waktu nyata. Trade‑off‑nya adalah jejak memori yang sedikit lebih tinggi, tetapi untuk kebanyakan pekerjaan batch peningkatan kecepatan sangat berharga.

> **Tip pro:** Jika Anda menangani ratusan megabyte gambar, pertimbangkan menggunakan `concurrent.futures.ProcessPoolExecutor` alih‑alih `threading`. Proses memberikan paralelisme sejati pada interpreter CPython yang terikat GIL, dengan biaya sedikit overhead tambahan.

## Langkah 1: Instal Aspose OCR untuk Python

Langkah pertama—mari kita pasang pustaka OCR ke sistem Anda.

```bash
pip install aspose-ocr
```

Baris tunggal itu mengunduh biner Aspose OCR terbaru beserta binding Python-nya. Jika Anda mengalami kesalahan izin, coba tambahkan `--user` atau gunakan lingkungan virtual.

## Langkah 2: Muat gambar untuk OCR – fungsi pekerja

Sekarang kita mendefinisikan rutin inti yang akan dijalankan di setiap thread. Ia **memuat gambar untuk OCR**, menjalankan proses pengenalan, dan mencetak pratinjau teks yang diekstrak.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

Beberapa hal yang perlu diperhatikan:

- **Mengapa `OcrEngine` baru per thread?** Mesin menyimpan buffer internal; berbagi satu instance dapat menyebabkan kondisi balapan dan output yang berantakan.  
- **Mengapa menghapus baris baru?** Saat kita mencatat ke konsol, ini menjaga baris tetap rapi.  
- **Penanganan error?** Pada produksi Anda akan membungkus kode dengan `try/except` dan mungkin mencatat ke file—sesuatu yang akan kami bahas nanti.

## Langkah 3: Daftar file PNG yang ingin diproses

Anda dapat menuliskan daftar secara manual, tetapi pendekatan yang lebih fleksibel adalah memindai direktori. Di bawah ini kami menuliskan tiga file secara manual untuk kejelasan; ganti path dengan folder Anda sendiri.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Jika Anda lebih suka penemuan otomatis:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Penyesuaian kecil itu memungkinkan Anda **mengekstrak teks dari PNG** secara massal tanpa harus mengubah kode sumber setiap kali.

## Langkah 4: Siapkan ocr multiple files dengan batch OCR images

Sekarang kami membuat thread untuk setiap gambar. Ini adalah inti dari pola **batch OCR images**.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

List comprehension membuat kode tetap ringkas, dan setiap objek `Thread` menyimpan fungsi target serta argumennya (`image_path`).  

> **Catatan samping:** Modul `threading` Python menggunakan thread OS native, jadi pada laptop 4‑core Anda biasanya akan melihat hingga empat thread yang benar‑benar berjalan sekaligus; sisanya akan dijadwalkan saat inti menjadi bebas.

## Langkah 5: Jalankan pengenalan gambar paralel

Meluncurkan pekerja sangat sederhana: iterasi daftar dan panggil `start()`. Setelah itu kami menunggu setiap thread selesai menggunakan `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Setelah skrip selesai, Anda akan melihat serangkaian baris seperti:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Output tersebut mengonfirmasi setiap PNG telah diproses dan teks yang diekstrak tersedia untuk penanganan lebih lanjut (misalnya, menyimpan ke basis data atau memasukkannya ke pipeline NLP).

## Langkah 6: Verifikasi hasil dan tangani kasus tepi

### Memeriksa hasil kosong

Kadang gambar terlalu berisik, atau mesin OCR gagal mendeteksi karakter apa pun. Pemeriksaan cepat dapat menyelamatkan Anda dari kesalahan di tahap selanjutnya.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Membatasi jumlah thread bersamaan

Jika Anda menjalankan ini pada VM dengan sumber daya terbatas, membuat ratusan thread dapat membebani penjadwal. Anda dapat membatasi konkurensi dengan semaphore:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Menyimpan hasil ke file

Alih‑alih mencetak, Anda mungkin menginginkan CSV dengan nama file dan teks yang diekstrak:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Pastikan membuka CSV **sekali** di luar fungsi thread untuk menghindari kondisi balapan; penulis modul `csv` aman untuk thread pada penulisan sederhana.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip tunggal yang dapat Anda letakkan dalam file bernama `batch_ocr.py` dan jalankan:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}