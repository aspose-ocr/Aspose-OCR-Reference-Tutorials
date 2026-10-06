---
category: general
date: 2026-01-02
description: Pelajari cara mengoreksi kemiringan gambar dan meningkatkan kontras gambar
  untuk mendapatkan teks biasa dengan cepat. Termasuk kode Python langkah demi langkah
  serta tips untuk mengekstrak teks.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: id
og_description: Cara mengoreksi kemiringan gambar dan meningkatkan kontras untuk mendapatkan
  teks biasa. Contoh Python lengkap dengan ekstraksi tabel dan percepatan GPU.
og_title: Cara Mengoreksi Kemiringan Gambar – Tutorial OCR GPU Lengkap
tags:
- OCR
- Python
- Image Processing
title: Cara Mengoreksi Kemiringan Gambar – Panduan OCR yang Dipercepat GPU
url: /id/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengoreksi Kemiringan Gambar – Panduan OCR Berakselerasi GPU

Pernah bertanya-tanya **bagaimana cara mengoreksi kemiringan gambar** ketika kwitansi Anda datang dengan sudut yang aneh? Anda tidak sendirian; foto yang miring dapat mengubah kwitansi yang seharusnya mudah dibaca menjadi berantakan. Kabar baiknya, dengan beberapa baris Python Anda dapat melakukan auto‑deskew, meningkatkan kontras, dan mengekstrak teks bersih—tanpa perlu Photoshop manual.  

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang tidak hanya **bagaimana cara mengoreksi kemiringan gambar** tetapi juga menunjukkan **cara meningkatkan kontras**, cara **mengambil teks polos**, dan bahkan **cara mengekstrak teks** dari tabel yang ditemukan oleh mesin OCR. Pada akhir tutorial Anda akan memiliki skrip mandiri yang dapat Anda masukkan ke dalam proyek apa pun.

## Apa yang Anda Butuhkan

- Python 3.9+ terpasang (kode menggunakan type hints, jadi interpreter terbaru membantu)
- Pustaka `ocr` yang menyediakan `OcrEngine`, `EngineMode`, `ImageProcessingOptions`, dan `OcrResult` (pasang via `pip install ocr‑sdk` – ganti dengan nama paket yang sebenarnya Anda gunakan)
- GPU dengan driver yang kompatibel jika Anda menginginkan percepatan kecepatan (opsional tetapi disarankan)
- File gambar yang sedikit diputar atau berkontras rendah, misalnya `receipt_skewed.jpg`

> **Tip pro:** Jika Anda tidak memiliki GPU, cukup ubah `EngineMode.GPU` menjadi `EngineMode.CPU` dan skrip tetap berfungsi—hanya sedikit lebih lambat.

## Implementasi Langkah‑per‑Langkah

Di bawah ini kami memecah solusi menjadi bagian‑bagian logis. Setiap bagian memiliki **H2** deskriptif yang mengandung kata kunci utama *bagaimana cara mengoreksi kemiringan gambar* atau salah satu kata kunci sekunder. Kode lengkap, berkomentar, dan siap dijalankan.

### Cara Mengoreksi Kemiringan Gambar dengan OCR Berakselerasi GPU

Hal pertama yang kami lakukan adalah memberi tahu mesin OCR untuk berjalan di GPU dan mengaktifkan fitur auto‑deskew. Auto‑deskew menganalisis geometri gambar dan memutarnya kembali ke posisi tegak.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Mengapa ini penting:** Akselerasi GPU dapat memotong waktu pemrosesan dari detik menjadi milidetik, yang sangat penting ketika Anda menangani puluhan kwitansi per menit.

### Tingkatkan Kontras Gambar untuk Pengenalan yang Lebih Baik

Kwitansi dengan kontras rendah adalah mimpi buruk bagi sistem OCR mana pun. Dengan meningkatkan kontras, kami memberi mesin tepi yang lebih jelas untuk diproses.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Cara meningkatkan kontras:** Metode `set_contrast_boost` menerima persentase; 30 % adalah nilai default yang aman dan bekerja untuk kebanyakan kwitansi yang dipindai. Jika gambar Anda sangat gelap, naikkan menjadi 50 % atau bereksperimen.

### Dapatkan Teks Polos dari Gambar yang Diproses

Sekarang gambar sudah lurus dan terang, kami memberikannya ke mesin dan meminta hasil teks polos.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Output yang diharapkan** (dipotong untuk singkatnya):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Cara mendapatkan teks polos:** Metode `get_text()` menghilangkan semua informasi tata letak dan mengembalikan string bersih, yang kemudian dapat Anda simpan di basis data, kirim ke API, atau masukkan ke analitik selanjutnya.

### Cara Mengekstrak Teks dari Tabel yang Terdeteksi

Seringkali kwitansi berisi data tabel (item, kuantitas, harga). SDK OCR dapat mendeteksi tabel dan memungkinkan Anda mengiterasi baris dan sel.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Contoh output tabel**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Mengapa mengekstrak tabel:** Data terstruktur memudahkan perhitungan total, pembuatan laporan, atau integrasi ke perangkat lunak akuntansi.

### Skrip Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip yang dapat Anda salin‑tempel ke dalam `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Jalankan dengan:

```bash
python deskew_and_ocr.py
```

Anda akan melihat teks yang telah dibersihkan dan tabel yang terdeteksi dicetak ke konsol.

## Kasus Tepi Umum & Cara Menanganinya

| Situasi | Apa yang Harus Dilakukan |
|-----------|------------|
| **Gambar terbalik** | Tingkatkan kepercayaan `set_auto_deskew(True)` dengan juga memanggil `set_rotation_correction(True)` jika SDK menyediakannya. |
| **Peningkatan kontras membuat gambar terlalu terang** | Kurangi persentase yang diberikan ke `set_contrast_boost` (mis., 15 %). |
| **GPU tidak tersedia** | Ganti `EngineMode.GPU` menjadi `EngineMode.CPU`; sisa pipeline tetap tidak berubah. |
| **Tabel tidak terdeteksi** | Coba pemindaian dengan resolusi lebih tinggi atau aktifkan `set_table_detection(True)` jika perpustakaan menyediakannya. |

## Langkah Selanjutnya: Dari Teks Polos ke Data Terstruktur

Sekarang Anda tahu **cara mengoreksi kemiringan gambar**, **cara meningkatkan kontras**, dan **cara mendapatkan teks polos**, Anda mungkin ingin:

- Mengurai teks polos dengan ekspresi reguler untuk mengekstrak pasangan kunci‑nilai (mis., `total`, `date`).
- Menyimpan hasil ke basis data SQLite atau PostgreSQL untuk pelaporan nanti.
- Menyambungkan skrip ke fungsi serverless (AWS Lambda, Azure Functions) untuk memproses unggahan secara otomatis.

Semua ekstensi tersebut dibangun di atas fondasi yang sama yang telah kami bahas di sini.

## Kesimpulan

Kami telah membahas **cara mengoreksi kemiringan gambar** menggunakan mesin OCR berakselerasi GPU, mendemonstrasikan **cara meningkatkan kontras** untuk pengenalan yang lebih tajam, menunjukkan secara tepat **cara mendapatkan teks polos**, dan bahkan membahas **cara mengekstrak teks** dari tabel. Skrip lengkap yang dapat dijalankan mengikat semuanya, sehingga Anda dapat memasukkannya ke dalam proyek Python apa pun dan mulai menarik data bersih dari foto yang miring dan berkontras rendah segera.

Cobalah dengan beberapa kwitansi Anda sendiri, sesuaikan tingkat kontras, dan biarkan OCR melakukan pekerjaan berat. Jika Anda menemukan keanehan, tinjau kembali tabel kasus tepi di atas—sebagian besar masalah hanya memerlukan penyesuaian kecil.

Selamat coding, semoga gambar Anda selalu lurus dan terang!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}