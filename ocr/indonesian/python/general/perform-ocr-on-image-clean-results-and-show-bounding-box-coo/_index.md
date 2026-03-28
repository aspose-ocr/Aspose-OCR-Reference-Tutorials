---
category: general
date: 2026-03-28
description: Lakukan OCR pada gambar dan dapatkan teks bersih dengan koordinat kotak
  pembatas. Pelajari cara mengekstrak OCR, membersihkan OCR, dan menampilkan hasil
  langkah demi langkah.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: id
og_description: Lakukan OCR pada gambar, bersihkan outputnya, dan tampilkan koordinat
  kotak pembatas dalam tutorial singkat.
og_title: Lakukan OCR pada Gambar – Hasil Bersih dan Kotak Pembatas
tags:
- OCR
- Computer Vision
- Python
title: Lakukan OCR pada Gambar – Bersihkan Hasil dan Tampilkan Koordinat Kotak Pembatas
url: /id/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar – Bersihkan Hasil dan Tampilkan Koordinat Bounding Box

Pernahkah Anda perlu **melakukan OCR pada gambar** tetapi terus mendapatkan teks yang berantakan dan tidak yakin di mana setiap kata berada pada gambar? Anda tidak sendirian. Dalam banyak proyek—digitalisasi faktur, pemindaian struk, atau ekstraksi teks sederhana—mendapatkan output OCR mentah hanyalah rintangan pertama. Kabar baiknya? Anda dapat membersihkan output tersebut dan langsung melihat koordinat bounding box setiap wilayah tanpa menulis banyak kode boilerplate.

Dalam panduan ini kami akan menjelaskan **cara mengekstrak OCR**, menjalankan post‑processor **cara membersihkan OCR**, dan akhirnya **menampilkan koordinat bounding box** untuk setiap wilayah yang telah dibersihkan. Pada akhir panduan Anda akan memiliki satu skrip yang dapat dijalankan yang mengubah foto buram menjadi teks terstruktur yang rapi siap untuk pemrosesan selanjutnya.

## Apa yang Anda Butuhkan

- Python 3.9+ (sintaks di bawah bekerja pada 3.8 dan lebih baru)
- Mesin OCR yang mendukung `recognize(..., return_structured=True)` – misalnya, pustaka fiktif `engine` yang digunakan dalam contoh. Ganti dengan Tesseract, EasyOCR, atau SDK apa pun yang mengembalikan data wilayah.
- Familiaritas dasar dengan fungsi dan loop Python
- File gambar yang ingin Anda pindai (PNG, JPG, dll.)

> **Tips Pro:** Jika Anda menggunakan Tesseract, fungsi `pytesseract.image_to_data` sudah memberikan bounding box. Anda dapat membungkus hasilnya dalam adaptor kecil yang meniru API `engine.recognize` yang ditunjukkan di bawah.

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Teks alternatif: diagram yang menunjukkan cara melakukan OCR pada gambar dan memvisualisasikan koordinat bounding box*

## Langkah 1 – Lakukan OCR pada Gambar dan Dapatkan Wilayah Terstruktur

Hal pertama adalah meminta mesin OCR untuk mengembalikan tidak hanya teks biasa tetapi daftar terstruktur dari wilayah teks. Daftar ini berisi string mentah dan persegi panjang yang mengelilinginya.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Mengapa ini penting:**  
Ketika Anda hanya meminta teks biasa, Anda kehilangan konteks spasial. Data terstruktur memungkinkan Anda kemudian **menampilkan koordinat bounding box**, menyelaraskan teks dengan tabel, atau memberikan lokasi yang tepat ke model selanjutnya.

## Langkah 2 – Cara Membersihkan Output OCR dengan Post‑Processor

Mesin OCR hebat dalam mengenali karakter, tetapi sering meninggalkan spasi berlebih, artefak pemutusan baris, atau simbol yang salah dikenali. Post‑processor menormalkan teks, memperbaiki kesalahan OCR umum, dan memangkas spasi kosong.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Jika Anda membuat pembersih sendiri, pertimbangkan:

- Menghapus karakter non‑ASCII (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Menggabungkan beberapa spasi menjadi satu spasi
- Menggunakan pemeriksa ejaan seperti `pyspellchecker` untuk typo yang jelas

**Mengapa Anda harus peduli:**  
String yang rapi membuat pencarian, pengindeksan, dan pipeline NLP selanjutnya jauh lebih dapat diandalkan. Dengan kata lain, **cara membersihkan OCR** sering menjadi perbedaan antara dataset yang dapat digunakan dan sakit kepala.

## Langkah 3 – Tampilkan Koordinat Bounding Box untuk Setiap Wilayah yang Dibersihkan

Sekarang teks sudah rapi, kami mengiterasi setiap wilayah, mencetak persegi panjangnya dan string yang telah dibersihkan. Ini adalah bagian di mana kami akhirnya **menampilkan koordinat bounding box**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Contoh output**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Anda sekarang dapat memasukkan koordinat tersebut ke dalam pustaka gambar (mis., OpenCV) untuk menambahkan kotak pada gambar asli, atau menyimpannya dalam basis data untuk kueri di kemudian hari.

## Skrip Lengkap, Siap‑Jalankan

Berikut adalah program lengkap yang menggabungkan ketiga langkah. Ganti pemanggilan placeholder `engine` dengan SDK OCR Anda yang sebenarnya.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Cara Menjalankan

```bash
python perform_ocr.py sample_invoice.jpg
```

Anda akan melihat daftar bounding box yang dipasangkan dengan teks yang telah dibersihkan, persis seperti contoh output di atas.

## Pertanyaan yang Sering Diajukan & Kasus Tepi

| Question | Answer |
|----------|--------|
| **Bagaimana jika mesin OCR tidak mendukung `return_structured`?** | Tulislah wrapper tipis yang mengonversi output mentah mesin (biasanya daftar kata dengan koordinat) menjadi objek dengan atribut `text` dan `bounding_box`. |
| **Apakah saya dapat memperoleh skor kepercayaan?** | Banyak SDK menampilkan metrik kepercayaan per wilayah. Tambahkan ke pernyataan print: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Bagaimana menangani teks yang diputar?** | Pra‑proses gambar dengan `cv2.minAreaRect` milik OpenCV untuk meluruskan sebelum memanggil `recognize`. |
| **Bagaimana jika saya membutuhkan output dalam format JSON?** | Serialisasikan `processed_result.regions` dengan `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Apakah ada cara untuk memvisualisasikan kotak?** | Gunakan OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` di dalam loop, lalu `cv2.imwrite("annotated.jpg", img)`. |

## Kesimpulan

Anda baru saja mempelajari **cara melakukan OCR pada gambar**, membersihkan output mentah, dan **menampilkan koordinat bounding box** untuk setiap wilayah. Alur tiga langkah—recognize → post‑process → iterate—adalah pola yang dapat digunakan kembali yang dapat Anda masukkan ke dalam proyek Python apa pun yang membutuhkan ekstraksi teks yang dapat diandalkan.

### Apa Selanjutnya?

- **Jelajahi berbagai back‑end OCR** (Tesseract, EasyOCR, Google Vision) dan bandingkan akurasi.
- **Integrasikan dengan basis data** untuk menyimpan data wilayah untuk arsip yang dapat dicari.
- **Tambahkan deteksi bahasa** untuk mengarahkan setiap wilayah melalui pemeriksa ejaan yang sesuai.
- **Tumpangkan kotak pada gambar asli** untuk verifikasi visual (lihat cuplikan OpenCV di atas).

Jika Anda menemukan keanehan, ingat bahwa kemenangan terbesar datang dari langkah post‑processing yang solid; string yang bersih jauh lebih mudah dikerjakan daripada dump karakter mentah.

Selamat coding, dan semoga pipeline OCR Anda selalu rapi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}