---
category: general
date: 2026-06-22
description: Pelajari cara melakukan OCR pada file PDF di Python, mengekstrak teks
  dari PDF, dan mengonversi PDF ke teks menggunakan pendekatan berbasis aliran. Langkah
  sederhana untuk memproses PDF yang dipindai.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: id
og_description: Bagaimana cara OCR file PDF di Python? Ikuti panduan ini untuk mengekstrak
  teks dari PDF, mengonversi PDF ke teks, dan memproses PDF yang dipindai menggunakan
  stream.
og_title: Cara OCR PDF di Python – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Cara OCR PDF di Python – Panduan Lengkap untuk Mengekstrak Teks dari PDF
url: /id/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR PDF di Python – Panduan Lengkap untuk Mengekstrak Teks dari PDF

Pernah bertanya-tanya **bagaimana cara OCR PDF** tanpa harus berurusan dengan alat desktop yang berat? Anda bukan satu-satunya. Dalam banyak proyek dunia nyata—seperti otomatisasi faktur atau mendigitalisasi pemindaian arsip—Anda memerlukan cara yang andal untuk mengubah PDF yang dipindai menjadi teks yang dapat dicari dan diedit.

Di tutorial ini kami akan membahas contoh bersih end‑to‑end yang **mengekstrak teks dari PDF** menggunakan mesin OCR Python yang ringan. Pada akhir tutorial Anda akan tahu persis cara **mengonversi PDF ke teks**, cara **memuat PDF dari stream**, dan cara **memproses PDF yang dipindai** secara efisien. Tidak ada keajaiban, hanya kode Python biasa yang dapat Anda masukkan ke dalam proyek Anda hari ini.

## Apa yang Akan Anda Pelajari

- Menginstal dan mengonfigurasi pustaka OCR Python yang memahami input PDF.  
- Mengaktifkan mode pengenalan PDF dan mengatur format output menjadi teks biasa.  
- Memuat PDF multi‑halaman dari aliran file (pola klasik “load pdf from stream”).  
- Menjalankan OCR pada semua halaman dan mengambil konten teksnya.  
- Mencetak atau menyimpan hasil untuk pemrosesan selanjutnya.

**Prasyarat**  
- Python 3.8+ terinstal di mesin Anda.  
- Familiaritas dasar dengan pip dan lingkungan virtual.  
- File PDF yang dipindai (bernama `multipage.pdf` dalam contoh) ditempatkan di direktori yang diketahui.

Jika ada yang terdengar tidak familiar, jangan khawatir—setiap langkah dijelaskan dengan bahasa sederhana, dan kami akan menyediakan perintah tepat yang Anda perlukan.

---

## Langkah 1: Instal Mesin OCR (cara OCR PDF)

Pertama-tama—Anda memerlukan mesin OCR yang dapat menangani input PDF. Untuk panduan ini kami akan menggunakan paket hipotetik `ocr` (API-nya meniru SDK komersial populer, tetapi pola yang sama bekerja dengan Tesseract‑OCR, ABBYY, atau Google Vision bila dibungkus dengan tepat).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** Jika Anda menggunakan Windows dan mengalami kesalahan izin, coba `pip install --user ocr` sebagai gantinya.

Setelah paket terinstal, Anda dapat mengimpornya dalam skrip Anda dan membuat instance mesin—ini adalah inti dari **cara OCR PDF**.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Objek `OcrEngine` menyimpan semua pengaturan yang akan kami ubah nanti, seperti bahasa, DPI, dan—yang penting—mode PDF.

## Langkah 2: Aktifkan Pengenalan PDF dan Pilih Output (ekstrak teks dari PDF)

Secara default banyak SDK OCR mengasumsikan Anda memberi mereka gambar. Untuk membuat mesin memperlakukan aliran masuk sebagai PDF, kami mengaktifkan flag pengenalan PDF dan meminta output teks biasa.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

Mengapa harus menentukan format output? Karena beberapa mesin dapat mengembalikan PDF dengan lapisan teks tersembunyi, PDF yang dapat dicari, atau JSON dengan kotak pembatas. Untuk kebanyakan pipeline ekstraksi data, **mengekstrak teks dari PDF** sebagai string biasa adalah format downstream yang paling bersih.

## Langkah 3: Muat PDF dari Aliran File (load PDF from stream)

Memuat PDF dari aliran adalah pola yang efisien memori—Anda menghindari memuat seluruh file ke RAM sekaligus. Ini sangat berguna saat menangani dokumen multi‑halaman yang besar.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **Bagaimana jika file berada di S3 atau bucket cloud lainnya?**  
> Cukup ganti `from_file` dengan metode yang menerima buffer byte (mis., `ImageStream.from_bytes(s3_object.read())`). Sisanya tetap sama.

## Langkah 4: Jalankan OCR pada Semua Halaman (proses PDF yang dipindai)

Sekarang pekerjaan berat dimulai. Mesin akan iterasi melalui setiap halaman, menjalankan mesin pengenalan, dan mengembalikan daftar objek halaman—masing‑masing menampilkan konten teksnya.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

Di balik layar, pustaka OCR mendekompresi setiap halaman PDF, merasternya pada DPI yang dikonfigurasi, dan memberi bitmap ke model jaringan sarafnya. Hasilnya? Sekumpulan objek `Page` siap untuk diekstrak.

## Langkah 5: Ambil dan Tampilkan Teks yang Diakui (konversi PDF ke teks)

Akhirnya, kami mengulangi halaman yang dikembalikan dan mencetak teks yang diakui. Inilah saat **konversi PDF ke teks** benar‑benar terjadi.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Output yang Diharapkan

Jika `multipage.pdf` berisi tiga halaman yang dipindai, Anda akan melihat sesuatu seperti:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

Perhatikan pemisahan bersih antar halaman—berguna jika Anda perlu menyimpan teks setiap halaman dalam basis data atau mengirimkannya ke model NLP selanjutnya.

## Menangani Kasus Tepi Umum

### 1. PDF dengan Lapisan Gambar dan Teks Campuran

Beberapa PDF sudah memiliki lapisan teks tersembunyi (mis., diekspor dari Word). Jika Anda ingin mesin OCR **mengabaikan teks yang ada** dan memproses ulang gambar, atur:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. File Besar Melebihi Batas Memori

Saat bekerja dengan PDF berukuran gigabyte, pertimbangkan memproses dalam potongan:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Dukungan Bahasa dan Font

Jika dokumen yang dipindai dalam bahasa Prancis atau mengandung karakter khusus, beri tahu mesin model bahasa mana yang akan digunakan:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## Skrip Lengkap – Siap Dijalan

Berikut contoh lengkap yang dapat dijalankan yang menggabungkan semua bagian. Simpan sebagai `ocr_pdf.py` dan jalankan `python ocr_pdf.py`.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**Menjalankan skrip** akan mencetak teks setiap halaman ke konsol, persis seperti yang ditunjukkan pada bagian “Output yang Diharapkan”. Dari sini Anda dapat mengarahkan output ke file:

```bash
python ocr_pdf.py > extracted_text.txt
```

## Kesimpulan

Kami baru saja membahas **cara OCR PDF** di Python dari awal hingga akhir. Dengan mengonfigurasi mesin, memuat dokumen melalui aliran, dan mengiterasi setiap halaman yang diakui, Anda dapat **mengekstrak teks dari PDF**, **mengonversi PDF ke teks**, dan **memproses PDF yang dipindai** hanya dengan beberapa baris kode. Pendekatan ini dapat diskalakan dari faktur dua‑halaman kecil hingga arsip ratusan halaman yang besar.

Apa selanjutnya? Cobalah mengirimkan string yang diekstrak ke indeks pencarian, rangkuman model bahasa, atau pipeline validasi data. Anda juga dapat bereksperimen dengan format output seperti JSON untuk mempertahankan metadata posisi untuk analisis dokumen lanjutan.

Ada pertanyaan tentang menangani PDF terenkripsi atau mengintegrasikan dengan penyimpanan cloud? Tinggalkan komentar di bawah—selamat coding! 

![Diagram yang menunjukkan alur kerja OCR PDF – cara OCR PDF, memuat PDF dari stream, mengenali halaman, dan mengekstrak teks](ocr-pdf-workflow.png "diagram alur kerja OCR PDF")

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cara Mengekstrak Teks dari Gambar Menggunakan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Cara Mengekstrak Teks dari Arsip ZIP Menggunakan Aspose.OCR untuk .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}