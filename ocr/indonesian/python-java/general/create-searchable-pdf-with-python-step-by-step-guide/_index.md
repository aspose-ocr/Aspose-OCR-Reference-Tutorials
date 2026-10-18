---
category: general
date: 2026-05-31
description: Buat PDF yang dapat dicari dari gambar hasil pemindaian menggunakan Python
  OCR. Pelajari cara mengonversi PDF gambar hasil pemindaian, mengonversi TIFF ke
  PDF, dan menambahkan lapisan teks OCR dalam hitungan menit.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: id
og_description: Buat PDF yang dapat dicari secara instan. Panduan ini menunjukkan
  cara menjalankan OCR, mengonversi PDF gambar yang dipindai, dan menambahkan lapisan
  teks OCR menggunakan satu skrip Python.
og_title: Buat PDF yang Dapat Dicari dengan Python – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Buat PDF yang Dapat Dicari dengan Python – Panduan Langkah demi Langkah
url: /id/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dengan Python – Panduan Langkah‑ demi‑Langkah

Pernah bertanya-tanya bagaimana cara **create searchable PDF** dari halaman yang dipindai tanpa harus menggunakan puluhan alat? Anda tidak sendirian. Dalam banyak alur kerja kantor, sebuah TIFF atau JPEG yang dipindai ditempatkan di drive bersama, dan orang berikutnya harus menyalin‑tempel teks secara manual—menyakitkan, rawan kesalahan, dan membuang waktu.  

Dalam tutorial ini kami akan membahas solusi yang bersih dan programatis yang memungkinkan Anda **convert scanned image PDF**, **convert TIFF to PDF**, dan **add OCR text layer** sekaligus. Pada akhir tutorial Anda akan memiliki skrip siap‑pakai yang menjalankan OCR, menyematkan teks tersembunyi, dan menghasilkan PDF yang dapat dicari yang dapat Anda indeks, cari, atau bagikan dengan percaya diri.

## Apa yang Anda Butuhkan

- Python 3.9+ (versi terbaru apa pun dapat digunakan)
- `aspose-ocr` dan `aspose-pdf` packages (diinstal via `pip install aspose-ocr aspose-pdf`)
- File gambar yang dipindai (`.tif`, `.png`, `.jpg`, atau bahkan halaman PDF yang hanya berupa gambar)
- Jumlah RAM yang cukup (mesin OCR ringan; bahkan laptop dapat menangani)

> **Pro tip:** Jika Anda menggunakan Windows, cara termudah untuk mendapatkan paket-paket tersebut adalah menjalankan perintah di jendela PowerShell yang dijalankan dengan hak istimewa.

```bash
pip install aspose-ocr aspose-pdf
```

Sekarang prasyarat sudah selesai, mari kita selami kode.

## Langkah 1: Buat Instance OCR Engine – *create searchable pdf*

Hal pertama yang kita lakukan adalah memulai OCR engine. Anggaplah ini sebagai otak yang akan membaca setiap piksel dan mengubahnya menjadi karakter.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Why this matters:** Menginisialisasi engine hanya sekali menjaga penggunaan memori tetap rendah. Jika Anda memanggil `OcrEngine()` di dalam loop untuk setiap halaman, Anda akan cepat kehabisan sumber daya.

## Langkah 2: Muat Gambar yang Dipindai – *convert tiff to pdf* & *convert scanned image pdf*

Selanjutnya, arahkan engine ke file yang ingin Anda proses. API menerima gambar raster apa pun, jadi TIFF bekerja sama baiknya dengan JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Jika Anda memiliki PDF yang hanya berisi gambar yang dipindai, Anda masih dapat menggunakan `load_image` karena Aspose akan mengekstrak halaman pertama secara otomatis.

## Langkah 3: Siapkan PDF Save Options – *add OCR text layer*

Di sini kami mengonfigurasi tampilan PDF akhir. Flag penting adalah `create_searchable_pdf`; mengaturnya ke `True` memberi tahu perpustakaan untuk menyematkan lapisan teks tak terlihat yang mencerminkan konten visual.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **What the text layer does:** Saat Anda membuka file hasil di Adobe Reader dan mencoba memilih teks, Anda akan melihat karakter tersembunyi. Mesin pencari juga dapat mengindeksnya—sempurna untuk kepatuhan atau pengarsipan.

## Langkah 4: Jalankan OCR dan Simpan – *how to run OCR* dalam satu panggilan

Sekarang keajaiban terjadi. Satu pemanggilan metode menjalankan mesin pengenalan dan menulis PDF yang dapat dicari ke disk.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

Metode `recognize` mengembalikan objek status yang dapat Anda periksa untuk kesalahan, tetapi untuk kebanyakan skenario sederhana pemanggilan sederhana di atas sudah cukup.

### Output yang Diharapkan

Menjalankan skrip mencetak:

```
PDF saved as searchable PDF.
```

Jika Anda membuka `scanned_page_searchable.pdf` Anda akan melihat dapat memilih teks, menyalin‑tempelnya, dan bahkan menjalankan pencarian `Ctrl+F`. Itu adalah ciri khas alur kerja **create searchable pdf**.

## Skrip Lengkap yang Berfungsi

Berikut adalah skrip lengkap yang siap dijalankan. Cukup ganti jalur placeholder dengan lokasi file Anda yang sebenarnya.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Simpan ini sebagai `create_searchable_pdf.py` dan jalankan:

```bash
python create_searchable_pdf.py
```

## Pertanyaan Umum & Kasus Tepi

### 1️⃣ Bisakah saya memproses PDF multi‑halaman?

Ya. Gunakan `ocr_engine.load_image("file.pdf")` lalu lakukan loop pada setiap halaman dengan `ocr_engine.recognize(pdf_save_options, page_number)`. Perpustakaan secara otomatis akan menghasilkan PDF yang dapat dicari multi‑halaman.

### 2️⃣ Bagaimana jika file sumber saya adalah TIFF resolusi tinggi (300 dpi+)?

DPI yang lebih tinggi menghasilkan akurasi OCR yang lebih baik tetapi juga penggunaan memori yang lebih besar. Jika Anda mengalami `MemoryError`, turunkan resolusi gambar terlebih dahulu:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Bagaimana cara mengubah bahasa OCR?

Set properti `language` pada engine sebelum memuat gambar:

```python
ocr_engine.language = "fra"   # French
```

Daftar lengkap kode bahasa yang didukung terdapat di dokumentasi Aspose.

### 4️⃣ Bagaimana jika saya perlu mempertahankan kualitas gambar asli?

Kelas `PdfSaveOptions` memiliki properti `compression`. Atur ke `PdfCompression.None` untuk mempertahankan data raster persis seperti semula.

```python
pdf_save_options.compression = "None"
```

## Tips untuk Penyebaran Siap‑Produksi

- **Batch processing:** Bungkus logika inti dalam fungsi yang menerima daftar jalur file. Catat setiap keberhasilan/kegagalan ke CSV untuk jejak audit.
- **Parallelism:** Gunakan `concurrent.futures.ThreadPoolExecutor` untuk menjalankan OCR pada banyak core. Ingat setiap thread memerlukan instance `OcrEngine` masing‑masing.
- **Security:** Jika Anda menangani dokumen sensitif, jalankan skrip di lingkungan sandbox dan hapus file sementara segera setelah diproses.

## Kesimpulan

Anda sekarang tahu cara **create searchable PDF** dari gambar yang dipindai menggunakan skrip Python yang ringkas. Dengan menginisialisasi OCR engine, memuat TIFF (atau raster apa pun), mengonfigurasi `PdfSaveOptions` untuk **add OCR text layer**, dan akhirnya memanggil `recognize`, seluruh pipeline **convert scanned image pdf** dan **convert TIFF to PDF** menjadi satu perintah yang dapat diulang.

Langkah selanjutnya? Coba sambungkan skrip ini dengan file‑watcher sehingga setiap pemindaian baru yang ditempatkan di folder secara otomatis menjadi dapat dicari. Atau bereksperimen dengan berbagai bahasa OCR untuk mendukung arsip multibahasa. Tidak ada batasan ketika Anda menggabungkan OCR dengan pembuatan PDF.

Ada pertanyaan lebih lanjut tentang **how to run OCR** di bahasa atau kerangka kerja lain? Tinggalkan komentar di bawah, dan selamat coding! 

![Diagram showing the flow from scanned image → OCR engine → searchable PDF (create searchable pdf)](searchable-pdf-flow.png "Create searchable pdf flow diagram")


## Apa yang Harus Anda Pelajari Selanjutnya?

- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Konversi Gambar ke PDF C# – Simpan Hasil OCR Multi‑halaman](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}