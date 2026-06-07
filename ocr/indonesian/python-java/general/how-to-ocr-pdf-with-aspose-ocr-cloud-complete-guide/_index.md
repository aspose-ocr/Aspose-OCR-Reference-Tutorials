---
category: general
date: 2026-06-06
description: Cara melakukan OCR PDF menggunakan Aspose OCR Cloud. Pelajari cara mengekstrak
  teks dari PDF, mengonversi halaman PDF ke PNG, dan menyimpan gambar halaman PDF
  dengan Python.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: id
og_description: Cara OCR PDF dengan Aspose OCR Cloud. Panduan ini menunjukkan cara
  mengekstrak teks biasa dari PDF, mengonversi halaman PDF ke PNG, dan menyimpan gambar
  halaman PDF.
og_title: Cara OCR PDF dengan Aspose OCR Cloud – Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Cara OCR PDF dengan Aspose OCR Cloud – Panduan Lengkap
url: /id/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR PDF dengan Aspose OCR Cloud – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara OCR PDF** tanpa harus berurusan dengan alat desktop yang berat? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika mereka membutuhkan cara cepat dan programatis untuk mengambil teks dari dokumen yang dipindai. Kabar baiknya? Dengan Aspose OCR Cloud Anda dapat **mengekstrak teks dari PDF**, mengubah setiap halaman menjadi PNG, dan bahkan **menyimpan gambar halaman PDF** untuk penggunaan nanti, semuanya dari skrip Python yang rapi.

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui: mulai dari menginstal SDK, melisensikan engine, dan mengenali PDF multi‑halaman, hingga mengekstrak teks biasa, mengonversi halaman ke PNG, dan menyimpan gambar-gambar tersebut ke disk. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke proyek mana pun yang membutuhkan kemampuan **how to OCR PDF**.

## Apa yang Anda Butuhkan

- **Python 3.8+** (kode ini juga berfungsi pada 3.10 dan yang lebih baru)  
- Akun Aspose OCR Cloud – Anda akan mendapatkan file lisensi percobaan gratis (`Aspose.OCR.lic`)  
- Paket `asposeocrcloud` (`pip install asposeocrcloud`)  
- PDF yang dipindai dan multi‑halaman yang ingin Anda proses  

Itu saja. Tidak ada binary tambahan, tidak ada dependensi native, hanya Python murni.

## Cara OCR PDF – Penyiapan dan Lisensi

Sebelum Anda dapat memanggil metode OCR apa pun, Anda harus memberi tahu SDK siapa Anda. Aspose menggunakan file lisensi ringan yang Anda tempatkan di lokasi yang dapat diakses oleh skrip Anda.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Pro tip:* Jika Anda melewatkan langkah lisensi, SDK tetap akan berfungsi tetapi akan menambahkan watermark kecil pada gambar output. Tidak ideal untuk produksi.

## Langkah 2: Instal Aspose OCR Cloud Python SDK

Buka terminal dan jalankan:

```bash
pip install asposeocrcloud
```

Paket ini mengunduh semua dependensi yang diperlukan (requests, pillow, dll.) sehingga Anda tidak perlu mencari apa pun lagi.

## Langkah 3: Buat Engine OCR dan Pilih Bahasa

Engine adalah inti dari operasi. Anda dapat menentukan bahasa apa pun yang didukung oleh Aspose; Bahasa Inggris bekerja untuk kebanyakan kasus.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Mengapa mengatur bahasa? Karena engine OCR menggunakan kamus khusus bahasa untuk meningkatkan akurasi. Jika Anda memproses PDF berbahasa Prancis, cukup ganti `ENGLISH` dengan `FRENCH`.

## Langkah 4: Arahkan ke PDF Multi‑Halaman Anda

Berikan engine path lengkap ke file yang ingin Anda proses. Path relatif dapat digunakan selama dapat diresolusikan dari direktori kerja skrip.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Pastikan file dapat dibaca; jika tidak, Anda akan melihat `FileNotFoundError`.

## Langkah 5: Jalankan OCR – Anda Mendapatkan Daftar Hasil

Memanggil `recognize_pdf` mengembalikan sebuah daftar di mana setiap elemen sesuai dengan satu halaman dari PDF sumber.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Setiap `OcrResult` berisi dua properti berguna:

* `text` – representasi teks biasa dari halaman (bagus untuk **extract plain text pdf**)
* `image` – objek `Image` Pillow dari halaman yang dirender (sempurna untuk **convert pdf page png**)

## Langkah 6: Ekstrak Teks dari PDF dan Konversi Halaman ke PNG

Sekarang kita mengulangi hasil, mencetak teks yang diekstrak, dan menyimpan versi PNG dari setiap halaman.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Output Konsol yang Diharapkan

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Anda juga akan menemukan `page_1.png`, `page_2.png`, … berada di `YOUR_DIRECTORY`. Itu adalah gambar halaman yang dirasterisasi yang dapat Anda masukkan ke pipeline pemrosesan gambar selanjutnya.

## Langkah 7: Simpan Gambar Halaman PDF (Pemrosesan Pasca Opsional)

Jika Anda hanya membutuhkan gambar dan bukan teks, Anda dapat melewatkan baris `print(res.text)`. Sebaliknya, jika Anda ingin menyimpan teks dalam file `.txt` terpisah, cukup tambahkan penulisan kecil berikut:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Penambahan kecil ini menunjukkan betapa mudahnya **save PDF page images** sambil juga menyimpan konten yang diekstrak.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip lengkap yang dapat Anda salin‑tempel ke `ocr_pdf.py`:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Jalankan dengan:

```bash
python ocr_pdf.py
```

Anda akan melihat dump konsol dari teks setiap halaman dan serangkaian file PNG

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Mengenali Teks PDF – Operasi OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Mengonversi Gambar ke PDF C# – Simpan Hasil OCR Multi‑halaman](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}