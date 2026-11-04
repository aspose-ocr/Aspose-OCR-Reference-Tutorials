---
category: general
date: 2026-01-12
description: cara mengatur bahasa di Aspose OCR Python dan mengekstrak teks dari gambar
  menggunakan kamus khusus. tutorial langkah demi langkah untuk pengembang.
draft: false
keywords:
- how to set language
- extract text from image
- how to extract text
- how to add dictionary
- how to process image
language: id
og_description: cara mengatur bahasa di Aspose OCR Python dan mengekstrak teks dari
  gambar dengan kamus khusus. pelajari alur kerja lengkap dalam hitungan menit.
og_title: cara mengatur bahasa di Aspose OCR Python – Panduan Lengkap
tags:
- OCR
- Python
- Aspose
- Image Processing
title: cara mengatur bahasa di Aspose OCR Python – Panduan Lengkap
url: /id/python-java/general/how-to-set-language-in-aspose-ocr-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara mengatur bahasa di Aspose OCR Python – Panduan Lengkap

Pernah bertanya-tanya **cara mengatur bahasa** saat menggunakan Aspose OCR di Python? Anda tidak sendirian—banyak pengembang mengalami masalah ini ketika model bahasa Inggris default tidak mengenali kode produk, nomor seri, atau teks multibahasa. Kabar baiknya, solusinya sederhana namun kuat. Dalam tutorial ini kami akan membahas cara mengonfigurasi bahasa, menambahkan kamus khusus, mengekstrak teks dari gambar, dan akhirnya memproses gambar untuk hasil OCR terbaik.

Kami akan mencakup semua yang perlu Anda ketahui: mulai dari menginstal pustaka hingga menjalankan contoh lengkap yang mencetak teks yang diekstrak. Pada akhir tutorial Anda akan dapat **mengekstrak teks dari file gambar** dengan percaya diri, bahkan ketika kontennya mencakup kode tidak biasa atau bahasa campuran.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* Python 3.8+ terinstal (kode menggunakan f‑strings, jadi versi lebih lama tidak akan berfungsi).
* Lisensi Aspose OCR untuk Python yang aktif atau kunci percobaan gratis.
* Paket `asposeocr` terinstal melalui `pip install asposeocr`.
* Gambar contoh (`product_label.png`) yang berisi teks yang ingin Anda baca.

Jika semua sudah ada, bagus—mari lanjutkan. Jika belum, dapatkan percobaan gratis dari situs web Aspose dan jalankan perintah instalasi; hanya memerlukan satu menit.

## Langkah 1: Impor modul Aspose OCR

Hal pertama yang harus Anda lakukan adalah membawa kelas OCR ke dalam skrip Anda. Ini adalah fondasi untuk **cara mengatur bahasa** selanjutnya.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr
```

> **Pro tip:** Simpan semua impor di bagian atas file. Ini membuat skrip lebih mudah dipindai, terutama ketika Anda kembali ke kode nanti.

## Langkah 2: Cara mengatur bahasa

Secara default, Aspose OCR mengasumsikan bahasa Inggris. Jika gambar Anda berisi bahasa Prancis, Jerman, atau bahasa lain, Anda perlu memberi tahu mesin bahasa mana yang akan digunakan. Di sinilah kata kunci utama berperan.

```python
# Step 2: Create an OCR engine and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # change to ocr.Language.FRENCH, etc.
```

Mengapa ini penting? Mesin OCR mengandalkan model karakter spesifik bahasa. Menyediakan bahasa yang tepat meningkatkan akurasi secara dramatis—terutama untuk karakter beraksen atau ligatur khusus bahasa.

> **Catatan:** Jika Anda perlu mendukung beberapa bahasa secara bersamaan, Anda dapat memberikan daftar seperti `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

## Langkah 3: Cara menambahkan kamus (kata‑kata yang didefinisikan pengguna)

Kadang‑kadang mesin OCR salah membaca kode produk seperti “AB‑1234”. Anda dapat meningkatkan kepercayaan dengan memberi kamus khusus. Ini secara langsung menjawab **cara menambahkan kamus** di Aspose OCR.

```python
# Step 3: Supply product codes that must be recognized with higher confidence
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])
```

Mesin memperlakukan kata‑kata ini sebagai “dikenal” dan akan memberi prioritas pada mereka dibandingkan karakter yang mirip. Ini sangat berguna untuk nomor SKU, kode seri, atau merek yang tidak termasuk dalam bahasa alami.

## Langkah 4: Cara memproses gambar

Setelah mesin dikonfigurasi, Anda perlu memuat gambar yang ingin dianalisis. Ini menjawab **cara memproses gambar** dengan cara yang bersih dan dapat diulang.

```python
# Step 4: Load the image containing the product label
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")
```

Jika Anda bekerja dengan PDF, Anda dapat mengonversi setiap halaman menjadi gambar terlebih dahulu—Aspose OCR mendukung hal itu secara langsung.

## Langkah 5: Cara mengekstrak teks dari gambar

Dengan semua pengaturan selesai, langkah terakhir adalah menjalankan OCR dan mengambil teksnya. Inilah inti dari **cara mengekstrak teks** dari sebuah gambar.

```python
# Step 5: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)

# Step 6: Print the extracted text
print(ocr_result.text)
```

Saat Anda menjalankan skrip, Anda akan melihat sesuatu seperti:

```
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

Jika output terlihat berantakan, periksa kembali bahwa Anda telah mengatur bahasa yang benar dan kamus khusus Anda berisi string yang tepat.

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut skrip lengkap yang dapat Anda salin‑tempel ke dalam file bernama `extract_label.py`. Pastikan mengganti `YOUR_DIRECTORY` dengan jalur sebenarnya ke gambar Anda.

```python
import asposeocr as ocr

# Create OCR engine and set language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # Change if needed

# Add custom dictionary entries
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])

# Load the target image
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")

# Perform OCR
ocr_result = ocr_engine.process(image)

# Output the result
print("=== OCR Extraction Result ===")
print(ocr_result.text)
```

### Output yang Diharapkan

```
=== OCR Extraction Result ===
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

Jika Anda melihat kode yang tepat yang Anda tambahkan ke kamus, berarti Anda telah berhasil menguasai **cara mengatur bahasa**, **cara menambahkan kamus**, dan **cara mengekstrak teks dari gambar** menggunakan Aspose OCR.

## Menangani Kasus Edge Umum

| Situasi | Apa yang Harus Dilakukan |
|-----------|------------|
| **Gambar blur** | Lakukan pra‑pemrosesan dengan `ocr.Image.apply_filter()` untuk menajamkan sebelum memanggil `process()`. |
| **Beberapa bahasa dalam satu gambar** | Atur `ocr_engine.language = ocr.Language.ENGLISH | ocr.Language.SPANISH`. |
| **PDF besar** | Loop melalui setiap halaman, konversi ke `ocr.Image`, dan panggil `process()` per halaman. |
| **Karakter tak terduga** | Tambahkan ke daftar kata‑kata yang didefinisikan pengguna; Aspose OCR memperlakukannya sebagai token berkepercayaan tinggi. |

Tips ini menjaga pipeline OCR Anda tetap kuat, bahkan ketika input tidak sempurna.

## Referensi Visual

![cara mengatur bahasa dalam contoh Aspose OCR](image.png "Tangkapan layar yang menunjukkan cara mengatur bahasa dalam contoh Aspose OCR Python")

*Alt text:* **cara mengatur bahasa** tangkapan layar yang menggambarkan penetapan properti bahasa di IDE Python.

## Kesimpulan

Anda kini tahu **cara mengatur bahasa** di Aspose OCR Python, cara **menambahkan kamus** entri, dan langkah‑langkah tepat untuk **mengekstrak teks dari gambar** serta **memproses gambar** untuk hasil optimal. Contoh lengkap di atas dapat dimasukkan ke proyek apa pun, disesuaikan untuk bahasa berbeda, dan diperluas untuk pemrosesan batch atau input PDF.

Siap untuk tantangan berikutnya? Coba ganti `ocr.Language.ENGLISH` dengan `ocr.Language.FRENCH` dan amati peningkatan akurasi pada label berbahasa Prancis. Atau bereksperimen dengan metode `set_user_defined_words` untuk memasukkan seluruh katalog produk—mesin OCR Anda akan memperlakukan setiap entri sebagai kecocokan berkepercayaan tinggi.

Selamat coding, semoga hasil OCR Anda selalu jernih!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}