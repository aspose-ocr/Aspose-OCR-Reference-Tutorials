---
category: general
date: 2026-07-05
description: Bagaimana menggunakan OCR di Python untuk mengonversi TIFF menjadi teks
  dengan cepat. Pelajari langkah‑langkah pustaka OCR Python untuk mengekstrak teks
  dari gambar TIFF dan membangun mesin OCR Python.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: id
og_description: Bagaimana cara menggunakan OCR di Python? Panduan ini menunjukkan
  langkah demi langkah cara mengonversi TIFF menjadi teks menggunakan mesin OCR Python
  dan perpustakaan OCR Python.
og_title: Cara Menggunakan OCR di Python – Ekstraksi Teks TIFF Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Cara Menggunakan OCR di Python – Ekstrak Teks dari TIFF
url: /id/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di Python – Ekstrak Teks dari TIFF

Pernah bertanya-tanya **bagaimana cara menggunakan OCR di Python** untuk mengubah buku yang dipindai menjadi teks yang dapat diedit? Anda bukan satu-satunya—pengembang, peneliti, dan hobiist semua mengalami kendala ini saat menangani gambar TIFF multi‑halaman. Kabar baiknya? Dengan **ocr library python** Anda dapat menjalankan mesin OCR kecil, mengarahkannya ke file TIFF, dan mendapatkan teks bersih yang dapat dicari dalam hitungan detik.

Dalam tutorial ini kami akan membahas semua yang Anda perlukan: menginstal paket yang tepat, memuat TIFF multi‑halaman, menjalankan mesin OCR, dan akhirnya mencetak isi setiap halaman. Pada akhir tutorial Anda akan dapat **mengonversi TIFF ke teks** dan **mengekstrak teks dari TIFF** tanpa meninggalkan lingkungan Python Anda.

## Prasyarat

- Python 3.9 atau lebih baru (contoh diuji pada 3.11)
- Versi terbaru dari pustaka `ocr` (atau `python ocr engine` kompatibel lain yang Anda sukai)
- File TIFF multi‑halaman yang ingin Anda proses (kami akan menyebutnya `scanned_book.tif`)
- Familiaritas dasar dengan skrip Python dan lingkungan virtual

Tidak diperlukan alat eksternal yang berat—hanya pip dan beberapa baris kode.

## Instal OCR Library Python

Pertama-tama: Anda memerlukan backend OCR yang solid. Untuk panduan ini kami akan menggunakan paket fiktif `ocr` yang dilengkapi dengan API tingkat‑tinggi yang sederhana, namun pola yang sama dapat diterapkan pada pembungkus berbasis Tesseract seperti `pytesseract` atau SDK komersial.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** Jika Anda menggunakan Windows dan paket tersebut bergantung pada binary native, pastikan Anda telah menginstal Visual C++ redistributable yang sesuai. Installer biasanya akan memberi peringatan jika ada yang kurang.

## Cara Menggunakan OCR Engine di Python

Sekarang pustaka sudah siap, mari jalankan mesin OCR dan arahkan ke file TIFF kita. Cuplikan kode berikut membuat instance engine, mengatur bahasa ke Bahasa Inggris, dan menyiapkannya untuk pemrosesan multi‑halaman.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Mengapa mengatur bahasa?**  
Sebagian besar mesin OCR menggunakan model bahasa untuk meningkatkan akurasi. Jika Anda melewatkan langkah ini, mesin akan kembali ke model generik yang mungkin salah mengenali tanda baca atau karakter khusus.

## Memuat Gambar TIFF Multi‑Page

Langkah selanjutnya adalah memuat dokumen yang dipindai. Helper `ocr.Image.load` memahami tumpukan TIFF secara langsung, mengembalikan objek yang mewakili setiap halaman secara internal.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Edge case:** Jika TIFF Anda menggunakan kompresi (CCITT Group 4, LZW, dll.) dan pustaka mengeluarkan error, coba konversi ke versi tidak terkompresi dengan ImageMagick terlebih dahulu:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Lakukan OCR pada Semua Halaman – Konversi TIFF ke Teks

Dengan objek gambar di tangan, engine kini dapat memproses semua halaman sekaligus. Metode ini mengembalikan daftar di mana setiap elemen berisi hasil OCR untuk satu halaman.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Apa yang terjadi di balik layar?**  
Fungsi `recognize_multi_page` mengiterasi setiap halaman yang diraster, menjalankan pengenalan jaringan saraf, dan mengemas output teks polos bersama skor kepercayaan. Ini pada dasarnya operasi batch yang menghemat Anda dari menulis loop manual.

## Iterasi Hasil – Ekstrak Teks dari TIFF

Akhirnya, kami menampilkan teks yang dikenali. Anda dapat menulis output ke file `.txt` terpisah, mengirimnya ke basis data, atau memasukkannya ke indeks pencarian—sesuai alur kerja Anda.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Output yang Diharapkan

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Setiap string `result.text` berisi output OCR mentah untuk halaman tersebut. Jika Anda memerlukan pelestarian jeda baris, sebagian besar engine menyediakan `result.lines` sebagai daftar string.

## Menangani File TIFF Besar – Tips & Trik

Memproses TIFF 500‑halaman dapat menguras memori. Berikut beberapa strategi agar tetap lancar:

1. **Chunk halaman** – Alih-alih `recognize_multi_page`, panggil `engine.recognize(page)` di dalam generator yang menghasilkan satu halaman pada satu waktu.
2. **Sesuaikan DPI** – Menurunkan resolusi gambar (mis., dari 300 DPI ke 200 DPI) mengurangi beban CPU sementara hampir tidak memengaruhi akurasi untuk kebanyakan teks cetak.
3. **Paralelisasi** – Jika OCR engine Anda thread‑safe, buat `concurrent.futures.ThreadPoolExecutor` untuk menjalankan pengenalan pada beberapa halaman secara bersamaan.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Simpan Teks yang Diekstrak ke File

Sebagian besar pipeline dunia nyata memerlukan penyimpanan persisten. Di bawah ini cara singkat untuk menuliskan teks setiap halaman ke file masing‑masing, mempertahankan urutan halaman.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Sekarang Anda memiliki direktori bersih berisi file `.txt` siap untuk diindeks atau diproses lebih lanjut dengan NLP.

## Pratinjau Gambar – Cara Menggunakan Hasil OCR Secara Visual

Jika Anda ingin melihat overlay OCR pada gambar asli (berguna untuk debugging), banyak pustaka memungkinkan Anda menggambar bounding box. Berikut contoh singkat menggunakan Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Cara menggunakan OCR di Python – overlay OCR pada halaman TIFF](ocr_overlay_example.png)

*Alt text:* Cara menggunakan OCR di Python – overlay visual teks yang dikenali pada halaman TIFF.

## Kesalahan Umum dan Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| Karakter rusak | Model bahasa salah | Atur `engine.language` ke enum yang tepat |
| Halaman hilang | Kompresi TIFF tidak didukung | Konversi ke TIFF tidak terkompresi terlebih dahulu |
| Performa lambat | DPI tinggi + pemrosesan satu‑thread | Kurangi DPI atau aktifkan multi‑threading |
| Output kosong | Gambar terlalu gelap/kontras rendah | Pra‑proses dengan peningkatan kontras (`opencv` atau `Pillow`) |

Menangani hal‑hal ini sejak awal menghemat Anda berjam‑jam debugging di kemudian hari.

## Langkah Selanjutnya – Melampaui Ekstraksi Dasar

Sekarang Anda telah menguasai dasar **bagaimana cara menggunakan OCR di Python**, pertimbangkan untuk mengeksplorasi:

- **Pembuatan PDF** – Gabungkan teks yang diekstrak dengan `reportlab` untuk membangun PDF yang dapat dicari.
- **Deteksi bahasa** – Auto‑switch `engine.language` menggunakan `langdetect`.
- **Ekstraksi data terstruktur** – Gunakan regular expression atau spaCy untuk mengambil tanggal, nama, atau tabel dari teks mentah.
- **Backend OCR alternatif** – Ganti `ocr` dengan `pytesseract` atau `easyocr` jika Anda memerlukan dukungan multibahasa.

Setiap topik ini secara alami terhubung kembali ke kata kunci sekunder **ocr library python**, **convert tiff to text**, **extract text from tiff**, dan **python ocr engine**, memberi Anda fondasi kuat untuk proyek yang lebih maju.

---

### Kesimpulan

Kami telah membahas **bagaimana cara menggunakan OCR di Python** mulai dari instalasi hingga pemrosesan multi‑halaman, menunjukkan secara tepat cara **mengonversi TIFF ke teks** dan **mengekstrak teks dari TIFF** menggunakan **python OCR engine** yang sederhana. Contoh lengkap yang dapat dijalankan di atas seharusnya bekerja langsung untuk kebanyakan file TIFF standar, dan tips yang diberikan akan membantu Anda menskalakan ke dokumen yang lebih besar atau mengintegrasikan OCR ke dalam pipeline yang lebih luas.

Cobalah dengan buku yang Anda pindai, kwitansi, atau gambar arsip Anda—lalu eksperimen dengan ide‑ide tingkat lanjutan yang tercantum di bagian “Langkah Selanjutnya”. Selamat coding, semoga hasil OCR Anda selalu akurat!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara mengekstrak teks dari tiff dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Cara Melakukan Ekstraksi Teks Gambar dari Stream Menggunakan Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}