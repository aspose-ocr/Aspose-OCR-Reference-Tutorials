---
category: general
date: 2026-01-12
description: Cara melakukan OCR gambar secara batch dengan cepat dan mengekstrak teks
  dari file JPEG menggunakan Python. Pelajari pemrosesan batch langkah demi langkah
  dengan contoh lengkap yang dapat dijalankan.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: id
og_description: Cara melakukan OCR gambar secara batch dan mengekstrak teks dari file
  JPEG. Panduan ini membawa Anda melalui solusi Python lengkap yang siap dijalankan.
og_title: Cara Memproses OCR Gambar Secara Batch – Tutorial Python Cepat
tags:
- OCR
- Python
- image processing
title: Cara Memproses OCR Gambar Secara Batch – Panduan Cepat untuk Mengekstrak Teks
  dari File JPEG
url: /id/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR Gambar – Panduan Cepat untuk Mengekstrak Teks dari File JPEG

Pernah bertanya-tanya **bagaimana cara batch OCR gambar** tanpa menulis skrip terpisah untuk setiap file? Anda tidak sendirian. Dalam banyak proyek—pemindaian faktur, digitalisasi arsip, atau moderasi konten—kita perlu mengambil teks dari puluhan atau ratusan file JPEG sekaligus. Kabar baiknya, Anda dapat melakukannya dengan hanya beberapa baris Python, dan Anda akan memiliki mesin yang dapat dipakai ulang yang dapat dimasukkan ke dalam pipeline apa pun.

Dalam tutorial ini kami akan menunjukkan **bagaimana cara batch OCR gambar**, kemudian membahas cara mengekstrak teks dari file JPEG, menangani kasus tepi, dan memverifikasi output. Pada akhir tutorial Anda akan memiliki skrip mandiri yang dapat dijalankan pada folder gambar apa pun, dan Anda akan memahami mengapa pemrosesan batch penting untuk kinerja dan pemeliharaan.

## Apa yang Akan Anda Pelajari

- Menyiapkan mesin OCR sederhana dan mengkonfigurasinya untuk bahasa Inggris.
- Mengumpulkan semua file JPEG dari sebuah direktori dengan `pathlib`.
- Memanggil mesin OCR sekali untuk memproses seluruh batch.
- Menampilkan pratinjau teks yang dikenali untuk setiap gambar.
- Tips menangani batch besar, bahasa berbeda, dan jebakan umum.

**Prasyarat**: Python 3.8+, pustaka `ocr` (atau pembungkus kompatibel lainnya), dan folder berisi gambar JPEG yang ingin Anda analisis. Tidak diperlukan layanan eksternal—semua berjalan secara lokal.

---

## Langkah 1: Inisialisasi Mesin OCR – Inti dari Cara Batch OCR Gambar

Sebelum kita dapat **batch OCR gambar**, kita memerlukan mesin yang tahu cara membaca teks. Pada kebanyakan pustaka Anda membuat objek mesin, secara opsional mengatur bahasa, dan kemudian menggunakannya kembali untuk setiap file.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Mengapa ini penting*: Menginisialisasi mesin sekali menghindari beban memuat model bahasa berulang-ulang. Ini juga memberi Anda satu tempat untuk menyesuaikan pengaturan (misalnya DPI, whitelist karakter) yang akan berlaku untuk seluruh batch.

> **Pro tip**: Jika Anda berencana memproses dokumen multibahasa, ubah `ocr.Language.ENGLISH` menjadi `ocr.Language.MULTI` atau muat beberapa paket bahasa sebelum batch dimulai.

---

## Langkah 2: Kumpulkan Semua File JPEG – Bagian “Ekstrak Teks dari File JPEG”

Setelah mesin siap, kita perlu memberi tahu mesin gambar mana yang akan diproses. Menggunakan `pathlib` membuat kode menjadi platform‑independen dan ringkas.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Mengapa ini penting*: Dengan mengumpulkan daftar file terlebih dahulu, kita dapat memberi seluruh koleksi ke mesin OCR dalam satu panggilan—tepat seperti apa yang dimaksud dengan **cara batch OCR gambar**. Jika Anda memiliki sub‑folder, Anda dapat mengubah `glob("**/*.jpg")` menjadi pencarian rekursif.

> **Kasus tepi**: Jika gambar Anda memiliki ekstensi campuran (`.jpeg`, `.JPG`), perpanjang pola glob: `image_dir.rglob("*.[jJ][pP][eE]?g")`.

---

## Langkah 3: Proses Seluruh Batch dalam Satu Panggilan – Kekuatan Sebenarnya dari Batch OCR

Sebagian besar pustaka OCR modern menyediakan metode `process_batch` (atau nama serupa) yang menerima iterable berisi jalur file. Inilah inti dari **cara batch OCR gambar** secara efisien.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Mengapa ini penting*: Satu panggilan batch mengurangi jumlah transisi Python‑to‑C, menjaga model bahasa tetap terload di memori, dan sering memungkinkan paralelisasi internal. Hasilnya adalah daftar objek—masing‑masing berisi teks yang dikenali dan skor kepercayaan.

> **Catatan kinerja**: Untuk batch sangat besar (ribuan gambar), pertimbangkan membagi daftar menjadi potongan‑potongan lebih kecil (misalnya 200 file) untuk menghindari konsumsi memori berlebih.

---

## Langkah 4: Tampilkan Pratinjau Teks yang Diekstrak – Validasi Cepat

Setelah batch selesai, berguna untuk melihat beberapa karakter pertama dari setiap hasil. Ini membantu Anda memastikan OCR memang mengekstrak teks dari file JPEG Anda.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Mengapa ini penting*: Pratinjau singkat memungkinkan Anda menemukan kegagalan jelas (misalnya output kosong, karakter kacau) tanpa membuka setiap file. Jika Anda melihat masalah sistematis, Anda dapat menyesuaikan pengaturan mesin dan menjalankan ulang batch.

> **Jebakan umum**: Lupa menghapus karakter newline dapat membuat pratinjau terlihat berantakan. Baris `replace("\n", " ")` membersihkannya.

---

## Contoh Lengkap yang Berfungsi – Semua Langkah Digabungkan

Berikut adalah skrip lengkap yang dapat Anda salin‑tempel, sesuaikan jalur direktori, dan jalankan. Skrip ini mendemonstrasikan seluruh alur kerja **cara batch OCR gambar** dari awal hingga akhir.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Output yang diharapkan** (contoh):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

Jika pratinjau menampilkan teks yang bermakna, Anda telah berhasil **mengekstrak teks dari file JPEG** menggunakan pendekatan batch.

---

## Menangani Batch Besar dan Skenario Lanjutan

### Membagi Beban Kerja Besar
Saat menangani ribuan gambar, memori dapat menjadi bottleneck. Bagi daftar menjadi potongan‑potongan lebih kecil:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Mengganti Bahasa
Jika dokumen Anda berbahasa Prancis atau Spanyol, ubah bahasa sebelum batch:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Menyimpan Hasil ke Disk
Alih‑alih mencetak, Anda mungkin ingin menulis setiap hasil OCR ke file `.txt`:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Kesimpulan

Anda kini tahu **bagaimana cara batch OCR gambar** dan secara andal **mengekstrak teks dari file JPEG** menggunakan skrip Python yang ringkas. Dengan menginisialisasi mesin sekali, mengumpulkan semua jalur JPEG, memprosesnya dalam satu batch, dan meninjau output, Anda memperoleh kecepatan dan kesederhanaan. Dari sini Anda dapat memperluas alur kerja—menambah dukungan multibahasa, menyimpan hasil ke basis data, atau mengintegrasikan skrip ke dalam pipeline pemrosesan dokumen yang lebih besar.

Siap untuk langkah berikutnya? Coba ganti pustaka `ocr` dengan Tesseract, bereksperimen dengan pra‑pemrosesan gambar (thresholding, resizing), atau alirkan teks yang diekstrak ke model pemrosesan bahasa alami untuk kategorisasi otomatis. Langit adalah batasnya, dan Anda kini memiliki fondasi yang kuat untuk dibangun.

Selamat coding, semoga batch OCR Anda selalu bebas error!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}