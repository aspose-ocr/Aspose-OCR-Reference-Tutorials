---
category: general
date: 2026-03-28
description: Ekstrak teks dari PNG dengan cepat menggunakan Aspose OCR di Python.
  Pelajari cara mengonversi teks halaman yang dipindai dengan pengenalan gambar paralel
  di Python untuk hasil berperforma tinggi.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: id
og_description: Ekstrak teks dari PNG dengan cepat menggunakan Aspose OCR di Python.
  Panduan ini menunjukkan cara mengonversi teks halaman yang dipindai dengan pengenalan
  gambar paralel di Python, menghasilkan hasil berkecepatan tinggi.
og_title: Ekstrak Teks dari PNG – OCR Paralel Cepat dengan Python
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: Ekstrak Teks dari PNG – OCR Paralel Cepat dengan Python dan Aspose
url: /id/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari PNG – OCR Paralel Cepat dengan Python

Pernah perlu **mengekstrak teks dari PNG** tetapi menemukan OCR satu‑thread sangat lambat? Anda tidak sendirian. Baik Anda mendigitalkan tumpukan struk yang dipindai atau mengubah slide kuliah menjadi PDF yang dapat dicari, kendala biasanya terletak pada langkah OCR itu sendiri.  

Dalam tutorial ini kami akan menunjukkan solusi lengkap yang siap dijalankan untuk **mengonversi teks halaman yang dipindai** secara paralel, menggunakan mode batch asinkron Aspose OCR bersama dengan `ThreadPoolExecutor` Python. Pada akhir tutorial Anda akan dapat **recognize image text python**‑style, menangani puluhan gambar dalam sebagian kecil waktu yang dibutuhkan loop naïf.

> **Apa yang akan Anda dapatkan**  
> * Skrip fungsional penuh yang mengekstrak teks dari gambar PNG secara bersamaan.  
> * Pemahaman mengapa mode batch async mempercepat proses.  
> * Tips untuk menskalakan solusi ke beban kerja yang lebih besar.

## Apa yang Anda Butuhkan

| Prasyarat | Alasan |
|--------------|--------|
| Python 3.9+ | Sintaks modern dan petunjuk tipe. |
| `aspose-ocr` dan paket `aspose-storage` | Menyediakan mesin OCR dan pemuat gambar. |
| Folder berisi file PNG (misalnya, halaman yang dipindai) | Materi sumber yang ingin Anda proses. |
| Pengetahuan dasar tentang konkruensi Python | Berguna tetapi tidak wajib; kami akan menjelaskan semuanya. |

Anda dapat memasang pustaka Aspose dengan:

```bash
pip install aspose-ocr aspose-storage
```

> **Tips pro:** Pastikan paket Anda selalu terbaru (`pip list --outdated`) untuk mendapatkan peningkatan performa terbaru.

## Langkah 1: Inisialisasi Mesin Aspose OCR dalam Mode Batch Asinkron

Hal pertama yang kami lakukan adalah membuat instance `OcrEngine` dan mengalihkannya ke **asynchronous batch mode**. Mode ini mengantri permintaan pengenalan secara internal, memungkinkan mesin memproses banyak gambar tanpa memblokir thread Python Anda.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Mengapa async?*  
Ketika Anda memanggil `recognize` dalam mode sinkron, pemanggilan akan memblokir hingga gambar selesai diproses. Dalam mode async, mesin dapat mulai mengerjakan gambar berikutnya sementara gambar saat ini masih dalam proses decoding, sehingga I/O dan kerja CPU tumpang tindih.

## Langkah 2: Daftar File PNG yang Ingin Diproses

Di sini kami mendefinisikan kumpulan gambar. Pada proyek nyata Anda mungkin menghasilkan daftar ini secara dinamis (misalnya, `glob.glob("*.png")`), tetapi menuliskannya secara eksplisit membuat contoh mudah diikuti.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Catatan:** Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya tempat pemindaian PNG Anda berada. Jika Anda memiliki ratusan file, pertimbangkan menggunakan `os.listdir` dan memfilter untuk `.png`.

## Langkah 3: Tulis Helper yang Memuat Gambar dan Mengembalikan Teksnya

Helper ini mengabstraksi proses dua langkah memuat file melalui **Aspose Storage** dan kemudian memberikannya ke mesin OCR. Menambahkan docstring kecil membuat fungsi ini mendokumentasikan dirinya sendiri—berguna untuk pemeliharaan di masa depan.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Mengapa fungsi terpisah?*  
Ini membuat kode thread‑pool tetap bersih dan memungkinkan kami menggunakan kembali logika ini di tempat lain (misalnya, di endpoint Flask). Selain itu, memisahkan I/O memudahkan debugging—jika file tertentu gagal, Anda akan melihat nama file dalam jejak pengecualian.

## Langkah 4: Jalankan Pengakuan Gambar Paralel Python dengan Thread Pool

Sekarang kami mengimpor `ThreadPoolExecutor`. Secara default kami memulai empat pekerja, tetapi Anda dapat menyesuaikan `max_workers` berdasarkan jumlah core CPU dan ukuran kumpulan gambar.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### Bagaimana Ini Memberikan Pengakuan Gambar Paralel Python

* **ThreadPoolExecutor** membuat kumpulan thread pekerja yang masing‑masing memanggil `recognize_image`.  
* Karena mesin OCR berada dalam mode batch async, setiap thread dapat menyerahkan pekerjaan ke mesin sambil tetap responsif.  
* `as_completed` menghasilkan futures dalam urutan selesai, sehingga Anda mendapatkan hasil segera setelah siap—sempurna untuk streaming batch besar.

> **Jebakan umum:** Menggunakan `max_workers=1` menghilangkan tujuan paralelisme. Pada mesin 8‑core, `max_workers=8` sering memberikan throughput terbaik, tetapi coba beberapa nilai untuk menemukan titik optimal bagi perangkat keras Anda.

## Langkah 5: Verifikasi Output dan Tangani Kasus Tepi

Saat Anda menjalankan skrip, Anda akan melihat blok teks untuk setiap PNG, diawali dengan nama file-nya:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Jika ada gambar yang gagal (file rusak, format tidak didukung), blok `except` mencetak pesan error yang membantu alih‑alih menghentikan seluruh batch.

### Memperluas Solusi

| Skenario | Penyesuaian yang Disarankan |
|----------|-----------------------------|
| **Ribuan halaman** | Beralih ke `ProcessPoolExecutor` untuk memanfaatkan beberapa proses CPU, atau bagi daftar menjadi potongan dan proses batch secara berurutan. |
| **Format gambar berbeda (JPG, TIFF)** | Metode `storage.Image.load` secara otomatis mendeteksi format, jadi cukup tambahkan file ke `input_images`. |
| **Perlu menyimpan hasil** | Tulis `text` ke file `.txt` atau masukkan ke basis data di dalam blok `else`. |
| **Pemantauan performa** | Bungkus `recognize_image` dengan timer (`time.perf_counter`) dan log durasi per file. |

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah skrip lengkap, siap ditempatkan ke file bernama `parallel_ocr.py`. Tidak ada bagian yang hilang—semua yang Anda butuhkan ada di sini.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Simpan file, sesuaikan placeholder `YOUR_DIRECTORY`, dan jalankan:

```bash
python parallel_ocr.py
```

Anda akan melihat teks yang diekstrak untuk setiap PNG muncul di konsol, persis seperti yang ditunjukkan sebelumnya.

## Kesimpulan

Kami baru saja menunjukkan cara **mengekstrak teks dari PNG** secara efisien dengan menggabungkan mode batch async Aspose OCR dan `ThreadPoolExecutor` Python. Skrip ini mengonversi teks halaman yang dipindai secara paralel, memberi Anda cara skalabel untuk **recognize image text python**‑style tanpa menulis thread‑pool khusus dari nol.  

Jika Anda siap melangkah lebih jauh, coba:

* Menyimpan hasil ke basis data SQLite yang dapat dicari.  
* Menambahkan pra‑pemrosesan gambar (deskew, denoise) dengan OpenCV sebelum OCR.  
* Menyebarkan skrip sebagai microservice di belakang endpoint Flask atau FastAPI.

Ingat, kunci OCR berperforma tinggi bukan hanya mesin yang lebih cepat—tetapi juga cara memberi mesin kerja secara yang memaksimalkan konkruensi. Dengan pola yang ditunjukkan di sini, Anda dapat menangani puluhan bahkan ratusan pemindaian PNG dengan perubahan kode minimal.

Selamat coding, dan semoga PDF Anda selalu dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}