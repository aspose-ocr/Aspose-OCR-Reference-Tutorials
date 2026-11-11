---
category: general
date: 2026-07-05
description: Ubah PDF menjadi teks menggunakan Python OCR. Pelajari cara mengekstrak
  teks dari PDF, melakukan pemrosesan OCR batch, dan memuat PDF untuk OCR dalam beberapa
  langkah mudah.
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: id
og_description: Ubah PDF menjadi teks dengan cepat. Tutorial ini menunjukkan cara
  mengekstrak teks dari PDF, menjalankan pemrosesan OCR batch, dan mengenali file
  PDF yang dipindai menggunakan Python.
og_title: Konversi PDF ke Teks dengan OCR Python – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Ubah PDF menjadi Teks dengan OCR Python – Panduan Lengkap
url: /id/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi PDF ke Teks dengan Python OCR – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **mengonversi PDF ke teks** tanpa susah payah? Mungkin Anda memiliki tumpukan kontrak, faktur, atau makalah penelitian yang dipindai dan membutuhkan versi teks polos untuk pengindeksan atau analisis. Kabar baiknya, beberapa baris Python saja dapat melakukan pekerjaan berat tersebut untuk Anda.

Dalam tutorial ini kami akan membahas solusi praktis yang tidak hanya **mengonversi pdf ke teks**, tetapi juga menunjukkan cara **mengekstrak teks dari pdf**, menyiapkan **pemrosesan OCR batch**, dan **memuat pdf untuk OCR** dengan benar. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang dapat **mengenali pdf yang dipindai** dalam satu langkah.

## Apa yang Akan Anda Pelajari

- Menginstal dan mengonfigurasi pustaka OCR Python (kami akan menggunakan paket `ocr` generik untuk ilustrasi).  
- Memuat PDF multi‑halaman dan memberikannya ke mesin OCR.  
- Mengiterasi hasil untuk mencetak atau menyimpan teks yang diekstrak.  
- Menangani kasus tepi umum seperti file besar, PDF terenkripsi, dan dokumen berbahasa campuran.  

Tanpa alat GUI berat, tanpa penyalinan manual—hanya kode murni yang dapat Anda masukkan ke dalam pipeline CI atau utilitas desktop.

![Mengonversi PDF ke Teks menggunakan Python OCR](https://example.com/images/convert-pdf-to-text.png "Mengonversi PDF ke Teks menggunakan Python OCR")

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.9+ | Sintaks modern, petunjuk tipe, dan kinerja lebih baik. |
| pustaka `ocr` (atau pembungkus di atas Tesseract) | Menyediakan kelas `OcrEngine`, `Language`, dan `Image` yang digunakan dalam contoh. |
| PDF multi‑halaman yang dipindai (misalnya `contract.pdf`) | Ini adalah sumber yang akan Anda **memuat pdf untuk OCR**. |
| Familiaritas dasar dengan baris perintah | Untuk menginstal paket dan menjalankan skrip. |

Jika Anda menggunakan Tesseract di balik layar, instal melalui manajer paket OS Anda (`apt-get install tesseract-ocr` di Linux, `brew install tesseract` di macOS). Kemudian tambahkan pembungkus Python:

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## Langkah 1: Buat Mesin OCR dan Atur Bahasa Pengenalan

Pertama, kita memerlukan instance mesin OCR. Menetapkan bahasa ke Bahasa Inggris adalah default umum, tetapi Anda dapat beralih ke bahasa lain yang didukung nanti.

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**Mengapa ini penting:** Mesin adalah otak yang menafsirkan data piksel. Dengan secara eksplisit mendefinisikan `engine.language`, Anda menghindari beban deteksi bahasa pada setiap halaman, yang secara signifikan mempercepat **pemrosesan OCR batch**.

## Langkah 2: Muat Dokumen PDF untuk OCR

Sekarang kita membawa PDF ke memori. Metode `ocr.Image.load` dapat menerima jalur file dan mengembalikan objek yang dipahami mesin.

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**Tip profesional:** Jika PDF Anda dilindungi kata sandi, kebanyakan pustaka memungkinkan Anda menyertakan argumen `password`. Menangani hal ini di awal mencegah kesalahan “tidak dapat membuka file” yang membingungkan nanti.

## Langkah 3: Jalankan OCR pada Semua Halaman – Mengenali PDF yang Dipindai dalam Satu Panggilan

Menjalankan OCR halaman‑per‑halaman dapat lambat, terutama untuk dokumen besar. Metode `recognize_multi_page` melakukan **pemrosesan OCR batch** secara internal, menggunakan beberapa thread bila memungkinkan.

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**Apa yang terjadi di balik layar?** Mesin mengalirkan setiap halaman ke mesin OCR yang mendasarinya (seperti Tesseract), mengumpulkan teks, dan membungkusnya dalam `OcrResult`. Pendekatan ini mengurangi overhead I/O dan memberi Anda cara bersih untuk **mengekstrak teks dari pdf** nanti.

## Langkah 4: Iterasi Hasil dan Keluarkan Teks yang Dikenali

Akhirnya, kita melintasi setiap `OcrResult` dan mencetak teksnya. Anda juga dapat menulis setiap halaman ke file `.txt` terpisah atau menggabungkannya menjadi satu dokumen.

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**Mengapa menggunakan enumerate?** Dengan `enumerate(..., start=1)` Anda mendapatkan nomor halaman yang mudah dibaca manusia, yang berguna saat Anda perlu merujuk ke bagian tertentu dari PDF asli.

### Output yang Diharapkan

Menjalankan skrip pada kontrak 3‑halaman mungkin menghasilkan:

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

Jika sebuah halaman tidak mengandung teks yang dapat dikenali, `result.text` yang bersangkutan akan menjadi string kosong—sempurna untuk mendeteksi halaman kosong atau hanya gambar.

## Menangani PDF Besar dan Kendala Memori

Memproses PDF 500‑halaman dapat menghabiskan RAM jika Anda memuat semuanya sekaligus. Berikut dua strategi:

1. **Pemuatan Berpotongan** – Beberapa pustaka memungkinkan Anda memuat rentang halaman:

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **Streaming ke Disk** – Tulis teks setiap halaman langsung ke file alih‑alih menyimpan seluruh daftar di memori.

Kedua teknik ini menjaga alur kerja **mengonversi pdf ke teks** Anda tetap skalabel.

## Menangani Kesalahan dan Kasus Tepi

- **PDF terenkripsi** – Berikan kata sandi ke `Image.load`:

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **Bahasa Campuran** – Ganti bahasa per halaman jika Anda mendeteksi skrip yang berbeda:

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **Pemindaian Resolusi Rendah** – Praproses gambar dengan pustaka seperti `Pillow` untuk meningkatkan kontras sebelum OCR. Ini dapat secara dramatis meningkatkan kualitas langkah **mengenali pdf yang dipindai**.

## Skrip Lengkap: Mengonversi PDF ke Teks dalam Satu Jalankan

Berikut adalah skrip lengkap, siap‑eksekusi, yang menggabungkan semua bagian. Simpan sebagai `pdf_to_text.py` dan jalankan `python pdf_to_text.py`.

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**Menjalankan skrip** akan membuat folder `output` yang berisi `page_1.txt`, `page_2.txt`, dll., secara efektif **mengekstrak teks dari pdf** dalam format terstruktur.

## Menguji Solusi

1. **Pemeriksaan Kesehatan** – Buka file `.txt` yang dihasilkan dan pastikan beberapa baris pertama cocok dengan header dokumen asli.  
2. **Uji Performa** – Ukur waktu skrip pada PDF 100‑halaman menggunakan perintah `time`. Jika memakan waktu lebih lama dari yang diharapkan, pertimbangkan mengaktifkan flag multithreading pustaka (sering `engine.set_threads(4)`).  
3. **Jaminan Kualitas** – Bandingkan output OCR dengan kutipan yang diketik manual menggunakan alat diff. Targetkan akurasi karakter >95 % untuk pemindaian bersih.

## Langkah Selanjutnya dan Topik Terkait

- **Meningkatkan Akurasi**: Bereksperimen dengan `engine.dpi = 300` atau terapkan praproses gambar (deskew, denoise) sebelum OCR.  
- **PDF yang Dapat Dicari**: Gunakan pustaka PDF (seperti `PyPDF2` atau `pdfplumber`) untuk menyematkan teks yang diekstrak kembali ke PDF asli, menjadikannya dapat dicari.  
- **Pemrosesan Bahasa Alami**: Salurkan teks yang diekstrak ke spaCy atau NLTK untuk ekstraksi entitas, analisis sentimen, atau penandaan kata kunci.  
- **Pipeline Otomatisasi**: Gabungkan skrip ini dengan `watchdog` untuk memantau folder dan secara otomatis **mengonversi pdf ke teks** setiap kali file baru muncul.

Dengan menguasai pola‑pola ini, Anda akan dapat


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang erat dengan teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Mengenali Teks PDF – Operasi OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/)
- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cara Mengekstrak Teks dari Arsip ZIP Menggunakan Aspose.OCR untuk .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}