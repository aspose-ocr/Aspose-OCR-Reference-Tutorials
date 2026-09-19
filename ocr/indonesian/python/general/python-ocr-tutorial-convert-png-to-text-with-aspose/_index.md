---
category: general
date: 2026-09-19
description: Tutorial OCR Python menunjukkan cara mengonversi PNG menjadi teks menggunakan
  Aspose OCR. Pelajari ekstraksi teks OCR dengan Python dan ekstrak teks dari gambar
  yang dipindai.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- python OCR tutorial
- convert PNG to text
- OCR text extraction python
- extract text image python
- extract text scanned image
language: id
lastmod: 2026-09-19
og_description: Tutorial OCR Python memandu Anda melalui proses mengubah PNG menjadi
  teks menggunakan Aspose OCR. Kuasai ekstraksi teks OCR dengan Python dan ekstrak
  teks dari gambar yang dipindai.
og_image_alt: Screenshot of Python OCR code extracting text from a PNG image
og_title: Tutorial OCR Python – mengonversi PNG ke teks dengan Aspose
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  headline: 'Python OCR tutorial: convert PNG to text with Aspose'
  type: TechArticle
- description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  name: 'Python OCR tutorial: convert PNG to text with Aspose'
  steps:
  - name: Expected output
    text: 'If `sample.png` contains the sentence “Hello, world!”, the console will
      show:'
  - name: 1. Non‑PNG formats
    text: Even though this tutorial focuses on **convert PNG to text**, you might
      receive JPEG or TIFF files. The same code works; just change the file extension
      in `load_image`.
  - name: 2. Low‑resolution images
    text: 'OCR accuracy drops below 150 dpi. If you encounter poor results, upscale
      the image first using Pillow:'
  - name: 3. Extracting text from a scanned image with multiple languages
    text: 'Set a comma‑separated list of language codes:'
  - name: 4. Large documents
    text: 'Processing many pages in a single run can exhaust memory. Process each
      page individually:'
  type: HowTo
tags:
- python
- OCR
- image processing
title: 'Tutorial OCR Python: mengonversi PNG ke teks dengan Aspose'
url: /id/python/general/python-ocr-tutorial-convert-png-to-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial OCR Python: mengonversi PNG ke teks dengan Aspose

Jika Anda membutuhkan **python OCR tutorial** yang mengubah gambar PNG menjadi teks yang dapat diedit, panduan ini memberikan solusi lengkap yang siap dijalankan. Anda akan melihat cara menginstal pustaka Aspose OCR, memuat gambar, menjalankan mesin pengenalan, dan mencetak hasilnya—semua dalam beberapa langkah singkat.

Memindai dokumen dan mengekstrak teksnya dapat terasa merepotkan, terutama ketika Anda harus mengelola format gambar dan pengaturan bahasa. Tutorial ini menghilangkan dugaan dengan menunjukkan secara tepat metode mana yang harus dipanggil dan mengapa penting, sehingga Anda dapat fokus mengintegrasikan OCR ke dalam aplikasi Anda.

Anda juga akan belajar cara **convert PNG to text**, menangani jebakan umum, dan menyesuaikan kode untuk tipe gambar lain seperti JPEG atau TIFF. Pada akhir tutorial, Anda akan dapat mengekstrak teks dari gambar hasil pemindaian apa pun dengan percaya diri.

## Prerequisites

* Python 3.8 atau yang lebih baru terinstal.
* Koneksi internet untuk mengunduh paket Aspose OCR.
* Gambar PNG (atau format yang didukung) yang berisi teks yang dapat dibaca.

Anda **tidak** memerlukan mesin OCR terpisah atau binari eksternal—Aspose OCR menyatukan semua yang Anda butuhkan.

## Langkah 1: Instal paket Aspose OCR

Langkah pertama adalah menambahkan pustaka ke lingkungan Anda. Aspose menyediakan paket pure‑Python yang dapat diinstal melalui pip.

```bash
pip install aspose-ocr
```

**Tip profesional:** Gunakan lingkungan virtual (`python -m venv venv`) untuk menjaga dependensi terisolasi dari proyek lain.

Menginstal paket membuat modul `aspose.ocr` tersedia, yang berisi kelas `OcrEngine` yang digunakan sepanjang tutorial ini.

## Langkah 2: Impor kelas OCR engine

Setelah paket tersedia, impor kelas yang menggerakkan proses pengenalan.

```python
# Step 2: Import the OCR engine class
from aspose.ocr import OcrEngine
```

`OcrEngine` mengenkapsulasi semua logika untuk memuat gambar, mengonfigurasi bahasa, dan mengekstrak teks. Mengimpornya di bagian atas mengikuti praktik Python standar dan menjaga skrip tetap rapi.

## Langkah 3: Buat instance dari OCR engine

Membuat instance memberi Anda mesin baru dengan pengaturan default. Anda dapat menyesuaikan properti seperti bahasa atau pra‑pemrosesan gambar nanti.

```python
# Step 3: Create an instance of the OCR engine
engine = OcrEngine()
```

Objek `engine` baru mewakili satu sesi OCR. Menggunakan kembali instance yang sama untuk beberapa gambar dapat meningkatkan kinerja karena sumber daya internal di‑cache.

## Langkah 4: Muat gambar yang ingin diproses

Tentukan jalur ke file PNG yang ingin Anda konversi. Metode `load_image` menerima format apa pun yang didukung Aspose OCR, sehingga Anda juga dapat memberikan file JPEG, BMP, atau TIFF.

```python
# Step 4: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample.png")
```

Jika file tidak ditemukan, `load_image` akan mengeluarkan `FileNotFoundError`. Bungkus pemanggilan dalam blok try/except untuk kode produksi guna memberikan pesan error yang ramah.

## Langkah 5: Lakukan OCR untuk mengekstrak teks dari gambar

Memanggil `recognize` menjalankan pipeline pengenalan dan mengembalikan string yang diekstrak. Metode ini secara otomatis menangani analisis tata letak, segmentasi karakter, dan deteksi bahasa (default adalah English).

```python
# Step 5: Perform OCR to extract text from the image
text = engine.recognize()
```

Anda dapat mengubah bahasa sebelum memanggil `recognize`:

```python
engine.language = "fr"   # for French text
```

Fleksibilitas ini berguna ketika Anda membutuhkan **OCR text extraction python** untuk dokumen multibahasa.

## Langkah 6: Output teks yang dikenali

Akhirnya, cetak atau simpan hasilnya. Untuk pemeriksaan cepat, `print` menampilkan string mentah di konsol.

```python
# Step 6: Output the recognized text
print(text)
```

### Output yang diharapkan

Jika `sample.png` berisi kalimat “Hello, world!”, konsol akan menampilkan:

```
Hello, world!
```

Output mungkin menyertakan pemisah baris atau spasi ekstra tergantung pada tata letak asli. Anda dapat memproses string tersebut dengan `str.strip()` atau ekspresi reguler untuk membersihkannya.

## Menangani kasus tepi umum

### 1. Format non‑PNG

Meskipun tutorial ini berfokus pada **convert PNG to text**, Anda mungkin menerima file JPEG atau TIFF. Kode yang sama berfungsi; cukup ubah ekstensi file di `load_image`.

```python
engine.load_image("scanned_page.tiff")
```

### 2. Gambar beresolusi rendah

Akurasi OCR menurun di bawah 150 dpi. Jika Anda mendapatkan hasil yang buruk, tingkatkan ukuran gambar terlebih dahulu menggunakan Pillow:

```python
from PIL import Image

img = Image.open("sample.png")
high_res = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
high_res.save("sample_high_res.png")
engine.load_image("sample_high_res.png")
```

### 3. Mengekstrak teks dari gambar hasil pemindaian dengan banyak bahasa

Atur daftar kode bahasa yang dipisahkan koma:

```python
engine.language = "en,es,de"
```

Aspose OCR akan mencoba mengenali karakter dari semua bahasa yang terdaftar.

### 4. Dokumen besar

Memproses banyak halaman dalam satu kali jalan dapat menghabiskan memori. Proses setiap halaman secara terpisah:

```python
for page_path in ["page1.png", "page2.png", "page3.png"]:
    engine.load_image(page_path)
    print(engine.recognize())
```

## Skrip lengkap yang dapat dijalankan

Menggabungkan semua langkah menghasilkan program mandiri yang dapat Anda salin, tempel, dan jalankan.

```python
# python_ocr_tutorial.py
# Complete script for extracting text from a PNG image using Aspose OCR

# Install the library first:
# pip install aspose-ocr

from aspose.ocr import OcrEngine

def extract_text(image_path: str) -> str:
    """
    Loads an image and returns the recognized text.
    Parameters:
        image_path: Path to the PNG (or other supported) image.
    Returns:
        Recognized text as a string.
    """
    engine = OcrEngine()          # Create OCR engine instance
    engine.load_image(image_path) # Load the target image
    return engine.recognize()     # Perform OCR and return result

if __name__ == "__main__":
    # Replace with the actual path to your image
    path = "YOUR_DIRECTORY/sample.png"
    try:
        result = extract_text(path)
        print("=== Recognized Text ===")
        print(result)
    except Exception as e:
        print(f"Error during OCR processing: {e}")
```

Jalankan skrip dengan:

```bash
python python_ocr_tutorial.py
```

Anda akan melihat teks yang diekstrak dicetak ke konsol.

## Kesimpulan

Tutorial **python OCR** ini menunjukkan cara **convert PNG to text** menggunakan Aspose OCR, mencakup instalasi, pemuatan gambar, pengenalan, dan penanganan output. Anda kini memiliki pola yang dapat diandalkan untuk **OCR text extraction python**, dan Anda dapat menyesuaikan kode untuk **extract text image python** dari dokumen hasil pemindaian apa pun.

Dari sini, pertimbangkan:

* Mengintegrasikan skrip ke dalam layanan web (misalnya, Flask) untuk menyediakan OCR sebagai API.
* Menyimpan teks yang diekstrak dalam basis data untuk arsip yang dapat dicari.
* Bereksperimen dengan pengaturan bahasa yang berbeda untuk menangani pemindaian multibahasa.

Selamat coding, dan nikmati mengubah gambar menjadi teks yang dapat dicari dan diedit!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Konversi Gambar ke Teks: Ekstrak Teks dari Gambar Menggunakan Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Tutorial OCR Python: Ekstrak Teks Tabel dari Gambar](/ocr/english/python-java/general/python-ocr-tutorial-extract-table-text-from-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}