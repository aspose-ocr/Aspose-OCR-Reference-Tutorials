---
category: general
date: 2026-06-06
description: Cara melakukan OCR PDF menggunakan Python, mengekstrak teks dari PDF,
  mengonversi teks PDF yang dipindai, dan mengubah bahasa OCR hanya dalam beberapa
  baris kode.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: id
og_description: 'Cara OCR PDF dengan Python: panduan praktis yang menunjukkan cara
  mengekstrak teks dari PDF, mengonversi teks PDF yang dipindai, dan mengubah bahasa
  OCR dengan mudah.'
og_title: Cara OCR PDF dengan Python – Tutorial Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Cara OCR PDF di Python – Panduan Lengkap Langkah demi Langkah
url: /id/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR PDF di Python – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya-tanya **bagaimana cara OCR PDF** tanpa harus membayar alat SaaS yang mahal? Anda bukan satu-satunya. Baik Anda sedang mendigitalkan buku lama, mengambil data dari faktur, atau hanya membutuhkan teks yang dapat dicari dari laporan yang dipindai, menguasai PDF OCR di Python dapat menghemat berjam‑jam penyalinan manual.

Dalam tutorial ini kami akan membahas contoh singkat dan berfungsi yang **mengekstrak teks dari PDF**, menunjukkan cara **mengonversi teks PDF yang dipindai** menjadi string yang dapat diedit, dan bahkan mendemonstrasikan cara **mengubah bahasa OCR** jika dokumen Anda bukan dalam bahasa Inggris. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke dalam proyek apa pun.

## Prasyarat & Penyiapan

Sebelum kita mulai, pastikan Anda memiliki:

- Python 3.8+ terinstal (kode ini bekerja pada 3.9, 3.10, dan yang lebih baru)
- Paket `ocr` yang menyediakan kelas `OcrEngine` (Anda dapat menginstalnya via `pip install ocr-lib` – ganti dengan nama paket sebenarnya yang Anda gunakan)
- File PDF yang ingin Anda proses; untuk demo kami akan menggunakan `high_res_book.pdf` yang ditempatkan di folder bernama `YOUR_DIRECTORY`

Jika Anda menggunakan lingkungan virtual (sangat disarankan), aktifkan terlebih dahulu:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Pro tip:** Simpan file PDF Anda di dalam direktori `data/` khusus untuk menghindari masalah terkait jalur di kemudian hari.

## Langkah 1: Buat Instance OCR Engine (Cara OCR PDF – Inisialisasi)

Hal pertama yang harus Anda lakukan ketika ingin **melakukan OCR pada PDF** adalah menginstansiasi engine. Anggap engine sebagai otak yang akan membaca setiap halaman, menafsirkan glyph, dan memberikan kembali teks polos.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

Mengapa ini penting: tanpa engine Anda tidak memiliki konteks untuk pengaturan bahasa, opsi rendering, atau penanganan PDF. Objek `OcrEngine` menyimpan semua default tersebut dan memungkinkan Anda menyesuaikannya nanti.

## Langkah 2: Atur Bahasa Pengakuan (Ubah Bahasa OCR)

Sebagian besar perpustakaan OCR default ke bahasa Inggris, tetapi bagaimana jika dokumen Anda dalam bahasa Prancis, Jerman, atau bahkan Jepang? Mengubah bahasa semudah memanggil `set_recognition_language`. Ini memenuhi persyaratan **change OCR language** dan memastikan akurasi yang lebih tinggi.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Mengapa Anda mungkin memerlukannya:** Arsip multibahasa sering berisi halaman dengan bahasa campuran. Mengganti bahasa secara dinamis mencegah kesalahan pengenalan karakter seperti “ß” atau “ñ”.

## Langkah 3: Konfigurasikan Opsi Rendering PDF (Konversi Teks PDF yang Dipindai Secara Efektif)

Saat menangani PDF yang dipindai, resolusi dan mode warna sangat memengaruhi kualitas OCR. Rendering pada 300 DPI dalam skala abu‑abu adalah titik optimal untuk kebanyakan dokumen—cukup tinggi untuk menangkap detail namun cukup rendah untuk menjaga penggunaan memori tetap wajar.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

Pemanggilan berantai mungkin terlihat mewah, tetapi sebenarnya hanyalah API fluida yang mengembalikan objek opsi yang sama setiap kali. Jika Anda membutuhkan warna (misalnya, untuk diagram berwarna), ganti `"grayscale"` dengan `"color"`.

## Langkah 4: Kenali PDF dan Ambil Teks Halaman Pertama (Ekstrak Teks dari PDF)

Sekarang tiba pada inti **bagaimana cara OCR PDF**: memberikan engine jalur file dan mengambil teks yang dikenali. Metode ini mengembalikan daftar hasil per halaman; setiap hasil berisi atribut `text`.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

Jika Anda membutuhkan seluruh dokumen, iterasikan `results`:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### Bagaimana Jika PDF Terenkripsi?

Beberapa PDF dilindungi kata sandi. Dalam kasus itu Anda dapat mengirimkan kata sandi ke `recognize_pdf`:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

Engine akan mendekripsi secara langsung sebelum melakukan OCR—tidak diperlukan langkah tambahan.

## Langkah 5: Pemrosesan Pasca Teks yang Diekstrak (Penyetelan Halus Ekstrak Teks dari PDF)

Output OCR mentah sering berisi pemutusan baris, spasi berlebih, atau karakter yang terkadang salah dikenali. Rutinitas pembersihan cepat membuat string yang diekstrak siap untuk pemrosesan lanjutan (pengindeksan pencarian, penyimpanan basis data, dll.).

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

Anda kini dapat dengan aman **mengekstrak teks dari PDF** dan memasukkannya ke dalam pipeline NLP apa pun, mesin pencari, atau operasi sederhana `open(...).write()`.

## Bonus: Pemrosesan Batch Banyak PDF (Skala Perform OCR pada PDF)

Jika Anda memiliki folder penuh PDF yang dipindai, bungkus logika dalam sebuah loop:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

Potongan kode ini menunjukkan cara **perform OCR on PDF** secara massal, kebutuhan umum untuk proyek digitalisasi.

## Output yang Diharapkan

Menjalankan contoh satu‑halaman (Langkah 4) seharusnya mencetak sesuatu seperti:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

Jika Anda memproses buku multi‑halaman, konsol akan menampilkan teks bersih setiap halaman, dan skrip batch akan meninggalkan file `.txt` di samping setiap PDF.

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Gejala | Solusi |
|-------|----------|-----|
| PDF sumber beresolusi rendah | Karakter kacau, kata hilang | Tingkatkan DPI (`set_dpi(400)` atau lebih tinggi) |
| Pengaturan bahasa salah | Banyak simbol tidak dikenal, terutama karakter beraksen | Gunakan `engine.set_recognition_language(ocr.Language.FRENCH)` atau enum yang sesuai |
| PDF besar menyebabkan error memori | `MemoryError` atau crash setelah beberapa halaman | Proses halaman secara bertahap (`engine.recognize_pdf(..., max_pages=10)`) |
| Font hilang di PDF | Output kosong untuk halaman tertentu | Pastikan PDF memang berisi gambar raster; beberapa PDF hanya vektor dan memerlukan penanganan berbeda |

## Ilustrasi Gambar

Berikut adalah visual cepat dari alur kerja. Teks alt sengaja dibuat SEO‑friendly.

![diagram alur kerja cara OCR PDF yang menunjukkan inisialisasi engine, pengaturan bahasa, opsi rendering, pengenalan, dan ekstraksi teks](/images/ocr-workflow.png)

*Diagram ini tidak diperlukan agar kode berjalan, tetapi membantu pembelajar visual melihat di mana setiap langkah berada.*

## Kesimpulan

Kami telah membahas **bagaimana cara OCR PDF** di Python dari awal hingga akhir: membuat OCR engine, **mengubah bahasa OCR**, mengonfigurasi rendering untuk **mengonversi teks PDF yang dipindai**, dan akhirnya **mengekstrak teks dari PDF** untuk penggunaan lebih lanjut. Contoh lengkap yang dapat dijalankan siap disisipkan ke dalam proyek apa pun, dan skrip batch opsional menunjukkan cara menskalakan solusi.

Selanjutnya, Anda mungkin ingin mengeksplorasi:

- Menambahkan **perform OCR on PDF** untuk arsip multibahasa dengan melakukan loop pada daftar bahasa.
- Mengintegrasikan teks yang diekstrak dengan Elasticsearch untuk pencarian full‑text.
- Menggunakan OCR untuk membuat PDF yang dapat dicari dengan menyematkan lapisan teks kembali ke file asli (banyak perpustakaan menyediakan metode `save_as_searchable_pdf`).

Silakan bereksperimen, mengubah pengaturan DPI, atau beralih ke backend OCR yang berbeda. Dasar-dasarnya tetap sama, dan Anda kini memiliki fondasi yang kuat untuk dibangun.

Selamat coding, dan semoga dokumen yang dipindai akhirnya menjadi dapat dicari!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}