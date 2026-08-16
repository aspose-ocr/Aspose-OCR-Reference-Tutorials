---
category: general
date: 2026-03-18
description: Jalankan OCR pada gambar untuk mengekstrak teks dari PNG dan menghasilkan
  PDF yang dapat dicari. Pelajari cara mengenali gambar teks dan mengonversi PNG ke
  PDF dalam hitungan menit.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: id
og_description: Jalankan OCR pada gambar untuk mengekstrak teks dari PNG, mengenali
  gambar teks, dan menghasilkan PDF yang dapat dicari. Ikuti panduan langkah demi
  langkah ini.
og_title: Jalankan OCR pada Gambar – Ekstrak Teks dari PNG dengan Cepat
tags:
- OCR
- Python
- Image Processing
title: Jalankan OCR pada Gambar – Ekstrak Teks dari PNG dengan Cepat
url: /id/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar – Ekstrak Teks dari PNG dengan Cepat

Pernah membutuhkan untuk **run OCR on image** file tetapi tidak yakin harus mulai dari mana? Mungkin Anda memiliki artikel yang dipindai disimpan sebagai `article.png` dan Anda hanya menginginkan teks polos, atau Anda memerlukan PDF yang dapat dicari untuk pengarsipan. Bagaimanapun, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan menjelaskan cara mengekstrak teks dari PNG, mengenali gambar teks, dan bahkan mengonversi PNG tersebut menjadi PDF yang dapat dicari—semua dengan beberapa baris kode.

> **Apa yang akan Anda dapatkan:** skrip lengkap yang dapat dijalankan yang memuat PNG, menjalankan OCR, menyimpan output hOCR, dan secara opsional membuat PDF yang dapat dicari. Tidak ada impor yang hilang, tidak ada jalan buntu “lihat dokumen”—hanya solusi mandiri yang dapat Anda masukkan ke dalam proyek Anda hari ini.

## Prasyarat

- **Python 3.8+** (sintaks yang digunakan di sini bekerja pada versi terbaru apa pun)
- Perpustakaan **`ocr_engine`** yang Anda gunakan (contoh mengasumsikan kelas bernama `OcrEngine`; ganti dengan Tesseract, EasyOCR, dll., jika diperlukan)
- Gambar PNG yang ingin Anda proses (misalnya `article.png` ditempatkan dalam folder yang dapat Anda referensikan)
- Izin menulis ke direktori output

Jika Anda menggunakan Tesseract di balik layar, instal dengan:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

Kemudian instal pembungkus Python:

```bash
pip install pytesseract Pillow
```

*Tip pro:* tetap perbarui perpustakaan OCR Anda—paket bahasa baru dan perbaikan kinerja sering dirilis.

## Jalankan OCR pada Gambar – Panduan Langkah‑per‑Langkah

Berikut adalah **script lengkap**. Silakan salin‑tempel ke dalam file bernama `run_ocr.py` dan jalankan dengan `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Apa yang dilakukan skrip, dalam bahasa sederhana

1. **Instantiate** mesin OCR sehingga Anda dapat mengontrol pengaturannya.
2. **Load** file PNG (`article.png`). Skrip akan berhenti lebih awal jika file tidak ada—tidak ada error `NoneType` misterius kemudian.
3. **Select** `hocr` sebagai format ekspor. Format ini mempertahankan tata letak asli, yang penting untuk mengonversi gambar menjadi PDF yang dapat dicari nanti.
4. **Run** mesin pengenalan; di sinilah proses berat terjadi.
5. **Write** XML hOCR ke `article.hocr`. Sekarang Anda memiliki representasi yang dapat dibaca mesin dari teks dan koordinatnya.
6. *(Optional)* Ganti ke `"pdf"` dan hasilkan PDF yang dapat dicari dalam satu langkah tambahan.

Output **yang diharapkan** adalah file `.hocr` ber-encoding UTF‑8 yang terlihat seperti ini (dipangkas untuk singkat):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Jika Anda meng-uncomment bagian PDF, Anda juga akan mendapatkan `article_searchable.pdf`, yang dapat Anda buka di penampil PDF apa pun dan gunakan kotak pencarian **Ctrl + F** untuk menemukan kata secara instan.

![Contoh output menjalankan OCR pada gambar](example.png "Jalankan OCR pada gambar – hasil hOCR dan PDF")

## Cara Mengekstrak Teks dari PNG Menggunakan OcrEngine

Jika yang Anda butuhkan hanya teks mentah (tanpa tata letak, tanpa PDF), Anda dapat melewatkan langkah hOCR sepenuhnya:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Mengapa memilih teks polos?* Ini ringan, sempurna untuk pengindeksan, dan bekerja dengan baik pada pipeline NLP downstream.

## Kenali Gambar Teks dan Hasilkan PDF yang Dapat Dicari

Membuat PDF yang dapat dicari adalah proses dua‑bagian:

1. **Run OCR** dengan `hocr` (seperti yang kami lakukan di atas) untuk mendapatkan informasi tata letak.
2. **Combine** PNG asli dengan hOCR menjadi PDF menggunakan pengekspor PDF milik engine.

Sebagian besar perpustakaan OCR modern (Tesseract, ABBYY, Google Vision) menyediakan ekspor `pdf` yang melakukan hal ini. Potongan kode dalam blok *Optional* pada skrip utama menunjukkan pola tersebut. Jika perpustakaan Anda tidak memiliki pengekspor PDF bawaan, Anda dapat menggunakan **`pdf2image`** + **`reportlab`** untuk menggabungkan gambar dan hOCR—beritahu saya, dan saya akan membagikan contoh tambahan singkat.

## Konversi PNG ke PDF dengan Output OCR

Kadang-kadang Anda hanya menginginkan **PDF polos** yang berisi gambar (tanpa lapisan yang dapat dicari). Itu bahkan lebih sederhana:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Gabungkan ini dengan langkah OCR jika Anda membutuhkan versi yang dapat dicari, atau pertahankan sebagai replika visual yang setia untuk keperluan arsip.

## Kesalahan Umum & Tips

| Masalah | Mengapa Terjadi | Solusi Cepat |
|-------|----------------|-----------|
| **Blurry atau PNG beresolusi rendah** | Akurasi OCR turun drastis di bawah ~300 DPI. | Perbesar dengan `Image.resize((width*2, height*2), Image.LANCZOS)` sebelum memberi ke engine. |
| **Bahasa salah** | Engine default ke bahasa Inggris; karakter non‑Inggris menjadi kacau. | Panggil `ocr_engine.setLanguage('deu')` (atau kode ISO yang sesuai) sebelum `recognize()`. |
| **Output hOCR hilang** | Beberapa engine default ke teks polos ketika `setExportFormat` tidak dipanggil. | Pastikan `setExportFormat("hocr")` dijalankan **sebelum** `recognize()`. |
| **Kesalahan izin file** | Mencoba menulis ke folder hanya-baca. | Gunakan path di dalam proyek Anda atau jalankan `os.makedirs(..., exist_ok=True)` terlebih dahulu. |
| **PDF besar menyebabkan lonjakan memori** | Pengekspor PDF menyimpan seluruh gambar di RAM. | Proses halaman dalam potongan atau gunakan penulis PDF streaming. |

*Tip pro:* selalu uji pada gambar contoh kecil sebelum memperluas ke batch ribuan. Ini menghemat jam debugging.

## Kesimpulan

Anda sekarang tahu **how to run OCR on image** file, **extract text from PNG**, **recognize text image** untuk tugas downstream, **generate a searchable PDF**, dan **convert PNG to PDF** ketika Anda membutuhkan arsip sederhana. Skrip yang disediakan adalah solusi lengkap, salin‑dan‑tempel yang langsung dapat digunakan, dan bagian opsional memungkinkan Anda menyesuaikan output sesuai alur kerja Anda.

### Apa selanjutnya?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}