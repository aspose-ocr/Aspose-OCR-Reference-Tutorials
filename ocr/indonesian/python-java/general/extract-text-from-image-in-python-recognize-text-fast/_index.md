---
category: general
date: 2026-07-05
description: Ekstrak teks dari gambar menggunakan Python OCR. Pelajari cara mengenali
  teks dari gambar, memuat gambar untuk OCR, dan mengatur bahasa OCR dalam beberapa
  baris saja.
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: id
og_description: Ekstrak teks dari gambar dengan Python OCR. Panduan ini menunjukkan
  cara mengenali teks dari gambar, memuat gambar untuk OCR, membuat mesin OCR gaya
  Python, dan mengatur bahasa OCR.
og_title: Ekstrak Teks dari Gambar dengan Python – Kenali Teks dengan Cepat
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Ekstrak Teks dari Gambar dengan Python – Kenali Teks dengan Cepat
url: /id/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Python – Kenali Teks dengan Cepat

Pernah butuh **ekstrak teks dari gambar** tetapi tidak tahu pustaka mana yang harus dipilih? Jika Anda pernah bertanya pada diri sendiri *bagaimana cara mengenali teks dari gambar* tanpa harus menggunakan alat eksternal, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan membuat sebuah mesin OCR kecil, mengarahkannya ke sebuah gambar, dan mengambil teksnya—tidak lebih, tidak kurang.

Kami akan membahas setiap langkah: **create OCR engine python**, **set OCR language**, **load image for OCR**, memicu pengenalan secara asynchronous, dan akhirnya membaca hasilnya. Pada akhir tutorial Anda akan memiliki skrip mandiri yang dapat Anda masukkan ke proyek apa pun, baik itu digitizer dokumen atau chatbot yang membaca meme.

## Apa yang Anda Butuhkan

- Python 3.8+ (kode berfungsi pada 3.10 dan yang lebih baru juga)  
- Paket `ocr` (pembungkus tipis di atas Tesseract – instal dengan `pip install ocr` atau fork pilihan Anda)  
- File gambar (`.jpg`, `.png`, dll.) yang berisi teks yang dapat dibaca  
- Sedikit kesabaran untuk bagian async (ini cepat, janji)

Itu saja—tanpa dependensi berat, tanpa build native. Jika Anda sudah memiliki Tesseract di sistem Anda, pembungkus `ocr` akan menemukannya secara otomatis.

## Langkah 1: Buat OCR Engine – Jantung Ekstraksi

Hal pertama yang harus dilakukan: Anda memerlukan objek engine yang tahu cara berkomunikasi dengan engine OCR yang mendasarinya. Anggaplah itu sebagai “otak” yang nanti akan memproses gambar.

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*Mengapa ini penting*: tanpa engine Anda tidak memiliki konteks untuk pengaturan bahasa atau kemampuan async. Kelas `OcrEngine` mengabstraksi panggilan command‑line tingkat rendah ke Tesseract, memberikan Anda API Python yang bersih.

## Langkah 2: Atur Bahasa OCR – beri tahu engine apa yang diharapkan

Jika dokumen Anda berbahasa Inggris, Anda dapat membiarkan default, tetapi sebaiknya atur secara eksplisit. Ini juga menunjukkan cara **set OCR language** untuk locale lain.

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **Pro tip**: Untuk PDF multibahasa, Anda dapat memberikan daftar seperti `[ocr.Language.ENGLISH, ocr.Language.FRENCH]`. Engine akan mencoba kedua bahasa secara otomatis.

## Langkah 3: Muat Gambar untuk OCR – bawa gambar Anda ke memori

Sekarang kita benar‑benarnya **load image for OCR**. Pembungkus mendukung lazy loading, sehingga file tidak dibaca sampai engine membutuhkannya.

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*Kasus tepi*: Jika gambar sangat besar (lebih dari 5 MB), pertimbangkan untuk mengubah ukurannya terlebih dahulu agar pengenalan lebih cepat. Anda dapat melakukannya dengan Pillow:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## Langkah 4: Mulai Pengenalan Asynchronous – jangan blok aplikasi Anda

Menjalankan OCR dapat memakan satu atau dua detik, terutama pada pemindaian besar. Metode `recognize_async` mengembalikan future yang dapat Anda periksa nanti, memungkinkan Anda **melakukan pekerjaan lain sementara OCR berjalan di latar belakang**.

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

Mengapa async? Pada server web Anda tidak ingin satu permintaan menghambat seluruh pool pekerja. Objek future memberi Anda kontrol: Anda dapat `await` di kode async atau memblokir hanya ketika Anda benar‑benar membutuhkan hasilnya.

## Langkah 5: Ambil Hasil – blok hanya bila diperlukan

Ketika Anda akhirnya membutuhkan teks, panggil `future.get()`. Panggilan ini **hanya memblokir di sini**, artinya sisa program Anda tetap responsif sampai OCR selesai.

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

Jika Anda berada dalam loop `asyncio`, Anda dapat menggunakan `await future` – pembungkus mendukung kedua gaya.

## Langkah 6: Gunakan Teks yang Dikenali – data Anda siap

Sekarang Anda memiliki objek `result`, mengambil string biasa sangat mudah. Mari cetak dan juga tunjukkan cara menuliskannya ke file.

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Output yang diharapkan** (dipotong untuk singkat):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Jika gambar tidak mengandung teks, `result.text` akan menjadi string kosong—tangani kasus tersebut dengan elegan.

## Contoh Lengkap yang Berfungsi – Semua Langkah dalam Satu Skrip

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel, sesuaikan `image_path`, dan Anda siap.

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **Catatan**: Ganti `"YOUR_DIRECTORY/large_document.jpg"` dengan path sebenarnya ke gambar Anda. Skrip ini bekerja di Windows, macOS, dan Linux selama Tesseract terinstal dan dapat diakses di `PATH` Anda.

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Karakter sampah** | Bahasa yang salah atau file data bahasa yang hilang. | Pastikan `engine.language` sesuai dengan teks dan file `.traineddata` yang bersangkutan ada di folder `tessdata` Tesseract. |
| **Performa lambat pada gambar besar** | OCR skalanya kira‑kira sebanding dengan jumlah piksel. | Ubah ukuran atau down‑sample sebelum memberi ke engine (lihat potongan kode Pillow). |
| **Future tidak pernah selesai** | File gambar rusak atau tidak dapat dibaca. | Bungkus `future.get()` dalam blok try/except dan validasi `image.is_valid()` sebelum pengenalan. |
| **Unicode loss** |  |  |

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑demi‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Ubah Gambar menjadi Teks – Lakukan OCR pada Gambar dari URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose OCR untuk .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}