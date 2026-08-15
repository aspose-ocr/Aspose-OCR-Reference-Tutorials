---
category: general
date: 2026-03-26
description: cara melakukan OCR batch secara efisien menggunakan Python—pelajari cara
  mengekstrak teks dari gambar dan konversi OCR PDF dengan pemrosesan paralel.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: id
og_description: cara melakukan batch OCR secara efisien—panduan langkah demi langkah
  untuk mengekstrak teks dari gambar, konversi OCR PDF, dan pemrosesan batch OCR menggunakan
  Python.
og_title: 'Cara batch OCR: ekstraksi teks paralel cepat'
tags:
- OCR
- Python
- Parallel Computing
title: 'cara melakukan OCR batch: ekstraksi teks paralel cepat'
url: /id/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara melakukan batch ocr: ekstraksi teks paralel cepat

Pernah bertanya-tanya **cara melakukan batch ocr** ketika Anda memiliki puluhan halaman yang dipindai, tangkapan layar, dan PDF yang berserakan? Anda bukan satu-satunya—sebagian besar pengembang mengalami hal yang sama: memproses setiap file satu per satu menjadi bottleneck yang menyakitkan.  

Kabar baiknya, Anda dapat memulai beberapa thread pekerja, memberi mereka semua file Anda, dan menyaksikan mesin OCR memproses batch secara paralel. Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan **extract text from images**, melakukan **pdf ocr conversion**, dan memanfaatkan **parallel ocr processing** untuk kecepatan.

> **Apa yang akan Anda dapatkan**  
> * Skrip Python yang berfungsi penuh yang memproses daftar campuran file PNG, TIFF, PDF, dan JPG sekaligus.  
> * Pemahaman mengapa thread pool mempercepat tugas OCR yang I/O‑bound.  
> * Tips untuk menangani kesalahan, PDF besar, dan jumlah thread kustom.  

## Prasyarat

Sebelum kita menyelam lebih dalam, pastikan Anda memiliki:

| Persyaratan | Alasan |
|-------------|--------|
| Python 3.8+ | Sintaks modern & `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | Menyediakan `OcrBatchProcessor` dan objek hasil |
| A handful of sample files (PNG, TIFF, PDF, JPG) | Untuk melihat **extract text from images** dalam aksi |
| Basic familiarity with threads (optional) | Bermanfaat tetapi tidak wajib |

Jika Anda belum menginstal paket `ocr`, jalankan:

```bash
pip install ocr-lib   # replace with the actual package name
```

Sekarang lingkungan sudah siap, mari kita uraikan masalahnya.

## Langkah 1: Impor helper dan buat instance batch processor

Hal pertama yang kita butuhkan adalah tempat untuk mengumpulkan semua pekerjaan OCR. Kelas `OcrBatchProcessor` melakukan hal itu—menempatkan item kerja dalam antrian dan mengembalikan daftar objek `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Mengapa ini penting*: Mengimpor `as_completed` memungkinkan kita merespons setiap pekerjaan yang selesai secara instan, alih-alih menunggu file paling lambat. Ini adalah inti dari **batch ocr processing**.

## Langkah 2: Sesuaikan pool pekerja untuk eksekusi paralel

Secara default processor mungkin menggunakan satu thread, yang menghilangkan tujuan batching. Kami secara eksplisit meminta empat pekerja—silakan tingkatkan angka ini sesuai jumlah core CPU yang Anda miliki.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Tip pro*: Untuk tugas I/O‑bound seperti OCR, Anda sering mendapatkan hasil yang berkurang setelah `CPU cores * 2`. Uji beberapa nilai dan pilih titik optimal.

## Langkah 3: Antrikan setiap file yang ingin Anda OCR

Di sini kami menambahkan campuran file gambar dan PDF. Metode `add` hanya mencatat path; pekerjaan sebenarnya tidak akan dimulai sampai kami mengirim batch.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Jika Anda perlu memproses seluruh folder, loop `glob` singkat dapat menyelesaikannya:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Langkah 4: Jalankan pekerjaan dan kumpulkan futures

Memanggil `submit_all` memberi lampu hijau pada processor. Ini mengembalikan daftar objek `Future`—anggaplah mereka sebagai placeholder untuk hasil yang akan muncul nanti.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

Pada titik ini mesin OCR sedang sibuk di latar belakang, setiap thread memproses sebuah file.

## Langkah 5: Ambil hasil segera setelah selesai

Dengan menggunakan `as_completed` kami mengiterasi futures sesuai urutan selesai, bukan urutan kami mengirimnya. Ini membuat skrip kami responsif, terutama ketika beberapa PDF memakan waktu lebih lama dibanding PNG sederhana.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Output yang diharapkan** (dipotong untuk singkatnya):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Setiap blok sesuai dengan representasi teks biasa dari file asli. Jika Anda melakukan **pdf ocr conversion**, teks akan mencakup semua yang dapat diuraikan mesin OCR dari setiap halaman.

## Menangani Kasus Edge & Kesalahan Umum

| Situasi | Hal yang perlu diwaspadai | Perbaikan cepat |
|-----------|-------------------|-----------|
| Gambar rusak | `future.result()` menghasilkan `OSError` | Bungkus dengan `try/except` (lihat kode di atas) |
| PDF sangat besar ( > 100 MB ) | Tekanan memori, thread lebih lambat | Tingkatkan `thread_count` secara moderat atau bagi PDF menjadi bab terlebih dahulu |
| Dokumen multibahasa | Model OCR default mungkin salah deteksi | Berikan petunjuk bahasa ke `OcrBatchProcessor` jika perpustakaan mendukungnya |
| Perlu mempertahankan tata letak | `get_text()` biasa kehilangan kolom | Gunakan `ocr_result.get_hocr()` atau metode serupa yang memperhatikan tata letak |

### Tip pro: Jumlah thread kustom berdasarkan tipe file

Jika Anda tahu sebagian besar beban kerja Anda adalah PDF, Anda dapat mengalokasikan lebih banyak thread untuk itu dan lebih sedikit untuk PNG kecil. Beberapa perpustakaan memungkinkan Anda memberikan `priority` per‑job; jika tidak, Anda dapat membuat dua batch terpisah—satu untuk gambar, satu untuk PDF—dan menjalankannya secara bersamaan.

## Gambaran Visual (opsional)

![how to batch ocr workflow diagram](https://example.com/ocr-workflow.png "how to batch ocr workflow")

*Diagram ini menggambarkan alur dari penemuan file → pembuatan batch → eksekusi paralel → agregasi hasil.*

## Skrip Lengkap yang Dapat Anda Salin‑Tempel

Berikut adalah seluruh program, siap dimasukkan ke file `.py`. Ini mencakup semua potongan kode di atas, plus helper kecil yang secara otomatis menemukan file yang didukung dalam sebuah direktori.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Simpan ini sebagai `batch_ocr.py`, arahkan ke folder yang berisi pemindaian Anda, dan saksikan konsol terisi dengan teks yang diekstrak.  

### Mengapa ini berhasil

* **Thread pool** – OCR sebagian besar menunggu I/O disk dan panggilan mesin eksternal, sehingga banyak thread menjaga CPU tetap sibuk.  
* **`as_completed`** – Anda mendapatkan hasil segera setelah siap, yang ideal untuk umpan balik UI atau pipeline streaming.  
* **Isolasi error** – Satu file buruk tidak akan menjatuhkan seluruh batch; blok `try/except` mengisolasi kegagalan.

## Kesimpulan

Singkatnya, Anda kini tahu **cara melakukan batch ocr** menggunakan `concurrent.futures` Python bersama perpustakaan OCR yang mendukung pemrosesan batch. Dengan mengonfigurasi thread pool yang sederhana, mengantrikan setiap file yang didukung, dan mengambil hasil saat selesai, Anda memperoleh **parallel ocr processing** yang cepat tanpa mengorbankan keandalan.  

Dari sini Anda dapat:

* Menghubungkan output ke indeks pencarian untuk pengambilan dokumen cepat.  
* Memperluas skrip untuk menulis setiap hasil ke file `.txt` di samping yang asli.  
* Mengganti thread pool bawaan dengan `asyncio` jika perpustakaan OCR Anda menawarkan API async.  

Terus bereksperimen—ganti dengan Tesseract, Azure Cognitive Services, atau Google Vision, dan Anda akan melihat pola yang sama berlaku. Selamat mencoba OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}