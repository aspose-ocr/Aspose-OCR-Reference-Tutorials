---
category: general
date: 2026-01-12
description: Tutorial OCR Python yang menunjukkan cara mengekstrak teks tabel dari
  gambar. Pelajari cara membaca tabel dari gambar dan mengekstrak teks yang dipilih
  dengan Aspose OCR.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: id
og_description: Tutorial OCR Python yang mengajarkan cara mengekstrak teks tabel dari
  gambar, membaca tabel dari gambar, dan mengekstrak teks terpilih menggunakan Aspose
  OCR.
og_title: 'Tutorial OCR Python: Ekstrak Teks Tabel dari Gambar'
tags:
- OCR
- Python
- AsposeOCR
title: 'Tutorial OCR Python: Ekstrak Teks Tabel dari Gambar'
url: /id/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial OCR Python: Ekstrak Teks Tabel dari Gambar

Pernah membutuhkan **python ocr tutorial** yang benar‑benar menunjukkan cara mengambil tabel dari formulir yang dipindai? Anda tidak sendirian. Kebanyakan tutorial berhenti pada ekstraksi teks umum, meninggalkan Anda menebak cara mengisolasi grid data rapi yang Anda butuhkan.  

Dalam panduan ini kami akan membahas skenario dunia nyata: membaca tabel dari gambar, mengekstrak hanya teks terpilih yang Anda perlukan, dan akhirnya mencetak hasilnya. Sepanjang jalan kami akan menyelipkan tips tentang **cara mengekstrak tabel** secara andal, sehingga Anda tidak perlu menciptakan kembali roda setiap kali.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan Aspose OCR untuk Python.  
- Cara mendefinisikan wilayah persegi panjang yang berisi tabel.  
- Langkah‑langkah tepat untuk **mengekstrak teks tabel** dan **membaca tabel dari gambar**.  
- Tips menangani banyak bahasa atau tata letak tabel yang tidak teratur.  
- Skrip lengkap yang dapat dijalankan dan langsung Anda gunakan dalam proyek hari ini.

**Prasyarat**  
- Python 3.8 atau lebih baru.  
- Familiaritas dasar dengan konsep OCR (tidak memerlukan keahlian mendalam).  
- Gambar PNG atau JPEG yang berisi tabel jelas (kami sebut `form_with_table.png`).  

Jika Anda sudah memiliki semua itu, mari mulai—tanpa basa‑basi, hanya kode yang dapat langsung dipakai.

![python ocr tutorial example of table region](table_region_example.png){alt="contoh tutorial ocr python yang menunjukkan wilayah tabel"}

## Langkah 1: Instal dan Impor Aspose OCR

Langkah pertama: Anda memerlukan pustaka Aspose OCR. Paketnya ada di PyPI, jadi satu perintah `pip` sudah cukup.

```bash
pip install aspose-ocr
```

Sekarang impor modul dan helper apa pun yang Anda perlukan.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Pro tip:* Simpan dependensi Anda dalam file `requirements.txt`. Ini memudahkan reproduksi lingkungan.

## Langkah 2: Inisialisasi Mesin OCR (Inti Tutorial OCR Python)

Membuat mesin adalah inti dari setiap **python ocr tutorial**. Di sini kami juga menetapkan bahasa default ke Inggris—silakan ganti nanti bila perlu.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

Mengapa mengatur bahasa? Akurasi OCR dapat meningkat drastis ketika mesin tahu karakter apa yang diharapkan. Jika Anda menangani formulir multibahasa, Anda dapat menetapkan daftar bahasa atau menimpa per wilayah (lihat nanti).

## Langkah 3: Muat Gambar Anda

Aspose OCR bekerja dengan sebagian besar format gambar umum. Cukup arahkan ke jalur file, dan Anda akan mendapatkan objek `Image` yang siap diproses.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Kasus khusus:* Gambar besar (lebih dari 5 MB) dapat memperlambat proses. Pertimbangkan untuk mengubah ukuran atau mengompresnya sebelum OCR jika kinerja menjadi masalah.

## Langkah 4: Definisikan Wilayah Tabel (Baca Tabel dari Gambar)

Sekarang bagian yang menyenangkan: memberi tahu mesin *di mana* tabel berada. Anda menyediakan `OcrRegion` dengan `Rectangle` (x, y, lebar, tinggi). Koordinatnya berbasis piksel, jadi Anda mungkin perlu bereksperimen sedikit.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

Mengapa memakai wilayah? Dengan membatasi OCR pada area tabel, kami **mengekstrak teks terpilih** lebih cepat dan menghindari noise dari label atau grafik di sekitarnya. Ini juga meningkatkan akurasi karena mesin dapat fokus pada tata letak yang seragam.

## Langkah 5: Jalankan OCR pada Wilayah yang Didefinisikan

Setelah wilayah ditetapkan, panggil `process_region`. Metode ini mengembalikan objek `OcrResult` yang berisi teks mentah, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

Jika Anda perlu mengekstrak beberapa tabel, cukup ulangi Langkah 4‑5 dengan persegi panjang yang berbeda.

## Langkah 6: Keluarkan Teks Tabel yang Diekstrak

Akhirnya, cetak—atau simpan—representasi teks tabel. Aspose OCR mengembalikan teks polos dengan jeda baris yang biasanya selaras dengan baris tabel, sehingga pasca‑pemrosesan menjadi mudah.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Output yang diharapkan** (contoh):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

Anda kini dapat mengalirkan string ini ke parser `csv`, DataFrame pandas, atau pipeline analitik lainnya.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip lengkap yang dapat Anda jalankan segera. Ganti `YOUR_DIRECTORY/form_with_table.png` dengan jalur sebenarnya ke gambar Anda.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

Jalankan skrip dengan `python extract_table.py`. Jika semuanya cocok, Anda akan melihat tabel tercetak di konsol.

## Pertanyaan Umum & Penanganan Kasus Khusus

**Bagaimana jika tabel tidak berbentuk persegi panjang sempurna?**  
Anda dapat membagi tabel menjadi beberapa wilayah yang tumpang tindih atau menggunakan persegi panjang yang lebih besar mencakup seluruh area, lalu melakukan pasca‑pemrosesan teks (misalnya, memisahkan berdasarkan jeda baris).

**Bisakah saya mengekstrak hanya kolom tertentu?**  
Setelah Anda memiliki teks tabel lengkap, gunakan `csv` atau `pandas` di Python untuk memotong kolom yang Anda butuhkan. Langkah OCR sendiri mengembalikan semua yang berada dalam persegi panjang.

**Bagaimana cara menangani tabel non‑Inggris?**  
Setel `ocr_engine.language` (atau `region.language`) ke enum yang sesuai, seperti `ocr.Language.FRENCH` atau gabungkan beberapa bahasa menggunakan `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

**Apakah ada cara mendapatkan kotak pembatas untuk setiap sel?**  
Aspose OCR dapat mengembalikan `region_result.words` di mana setiap kata menyertakan kotak pembatas. Anda perlu memetakan kotak‑kotak tersebut kembali ke grid—berguna untuk analisis tata letak lanjutan.

## Tips untuk Akurasi Lebih Baik

- **Bersihkan gambar**: Binarisasi atau tingkatkan kontras sebelum memberi ke OCR. Pustaka seperti Pillow dapat membantu.  
- **Hindari artefak kompresi**: Simpan hasil pemindaian sebagai PNG bila memungkinkan.  
- **Perhatikan DPI**: 300 dpi adalah titik optimal; nilai lebih rendah dapat menyebabkan karakter terlewat.  
- **Uji ukuran persegi panjang yang berbeda**: Persegi panjang sedikit lebih besar sering menangkap karakter stray yang sebenarnya bagian dari tabel.

## Langkah Selanjutnya

Setelah Anda menguasai **cara mengekstrak tabel** dengan Aspose OCR, Anda dapat menjelajahi:

- Mengonversi teks yang diekstrak menjadi file CSV dengan modul `csv` Python.  
- Memasukkan data ke dalam **pandas** DataFrame untuk analisis.  
- Menggunakan OCR untuk membaca formulir tulisan tangan (memerlukan mesin berbeda atau pelatihan tambahan).  
- Mengotomatiskan pemrosesan batch puluhan formulir yang dipindai menggunakan loop `for` sederhana.

Setiap ekstensi ini dibangun di atas konsep inti yang dibahas dalam **python ocr tutorial** ini, sehingga Anda siap untuk menskalakan solusi.

---

*Selamat coding! Jika Anda menemui kendala, tinggalkan komentar di bawah—saya akan dengan senang hati membantu menyempurnakan proses ekstraksi Anda.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}