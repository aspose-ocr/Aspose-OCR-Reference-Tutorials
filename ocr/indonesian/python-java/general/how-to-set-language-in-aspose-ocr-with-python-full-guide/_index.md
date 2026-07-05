---
category: general
date: 2026-07-05
description: Cara mengatur bahasa di Aspose OCR menggunakan Python. Pelajari cara
  menggunakan OCR, cara mengekstrak teks dari gambar PNG, dan mengonversi gambar ke
  teks dengan Python dalam hitungan menit.
draft: false
keywords:
- how to set language
- how to use ocr
- how to extract text
- extract text png
- image to text python
language: id
og_description: Cara mengatur bahasa di Aspose OCR menggunakan Python. Panduan ini
  menunjukkan cara menggunakan OCR, mengekstrak teks dari file PNG, dan melakukan
  konversi gambar ke teks dengan Python.
og_title: Cara Mengatur Bahasa di Aspose OCR dengan Python – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to set language in Aspose OCR using Python. Learn how to use OCR,
    how to extract text from PNG images, and convert image to text python in minutes.
  headline: How to Set Language in Aspose OCR with Python – Full Guide
  type: TechArticle
- description: How to set language in Aspose OCR using Python. Learn how to use OCR,
    how to extract text from PNG images, and convert image to text python in minutes.
  name: How to Set Language in Aspose OCR with Python – Full Guide
  steps:
  - name: Alternative Language Options
    text: 'If your image contains **Cyrillic** or **Arabic**, just swap the enum:'
  - name: Expected Output
    text: 'Assuming `input.png` contains the phrase “Hello, World!” you’ll see:'
  - name: 1. Blurry Images Yield Garbage
    text: '- **Solution:** Pre‑process the image (increase contrast, sharpen). Aspose
      OCR offers built‑in filters, e.g., `engine.image_preprocessing = ocr.ImagePreprocessing.AUTO`.'
  - name: 2. Wrong Language Produces Missing Accents
    text: '- **Solution:** Double‑check that you called `engine.language = ocr.Language.LATIN_EXTENDED`
      **before** calling `recognize`. Changing the language after recognition has
      no effect.'
  - name: 3. License Not Found → Evaluation Watermark
    text: '- **Solution:** Verify the path to `Aspose.OCR.Java.lic`. Use an absolute
      path or `os.path.join(os.getcwd(), "license", "Aspose.OCR.Java.lic")` to avoid
      relative‑path surprises.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Cara Mengatur Bahasa di Aspose OCR dengan Python – Panduan Lengkap
url: /id/python-java/general/how-to-set-language-in-aspose-ocr-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengatur Bahasa di Aspose OCR dengan Python – Panduan Lengkap

Mengatur bahasa di Aspose OCR menggunakan Python sering menjadi langkah pertama untuk mendapatkan hasil yang akurat. Dalam tutorial ini kami akan memandu Anda cara mengatur bahasa, cara menggunakan OCR, dan cara mengekstrak teks dari gambar PNG—semua dalam satu skrip yang dapat dijalankan.

Jika Anda pernah menatap screenshot yang buram dan bertanya-tanya apakah Anda dapat mengubahnya menjadi teks yang dapat diedit secara ajaib, Anda berada di tempat yang tepat. Kami akan membahas segala hal mulai dari lisensi perpustakaan hingga mencetak teks yang dikenali, dan kami akan menyisipkan tips praktis agar Anda tidak terjebak pada jebakan umum.

## Prasyarat — Apa yang Anda Butuhkan Sebelum Memulai

- **Python 3.8+** (versi terbaru apa pun dapat digunakan)
- **pip** untuk menginstal paket `aspose-ocr`
- **File lisensi Aspose OCR** (opsional tetapi disarankan untuk produksi)
- **Gambar PNG** yang berisi teks yang ingin Anda baca  
  (kami akan menyebutnya `input.png` sepanjang tutorial)

Tidak ada kerangka kerja berat, tidak ada akrobatik Docker—hanya Python biasa dan perpustakaan Aspose OCR.

## Langkah 1: Instal dan Lisensikan Aspose OCR

Pertama-tama, Anda memerlukan perpustakaan ini di mesin Anda. Buka terminal dan jalankan:

```bash
pip install aspose-ocr
```

Jika Anda memiliki lisensi, letakkan `Aspose.OCR.Java.lic` (ya, lisensi Java dapat digunakan untuk Python) di tempat yang aman dan muat dengan cara berikut:

```python
import asposeocr as ocr

# Load your Aspose OCR license (optional but removes evaluation limits)
ocr.License().set_license("YOUR_DIRECTORY/Aspose.OCR.Java.lic")
```

> **Pro tip:** Simpan file lisensi di luar folder kontrol sumber Anda untuk menghindari commit tidak sengaja.

## Langkah 2: Buat Instance Mesin OCR

Sekarang kita memulai mesin yang akan melakukan pekerjaan berat.

```python
# Create an OCR engine instance
engine = ocr.OcrEngine()
```

Objek `engine` adalah gerbang Anda ke semua fitur OCR yang disediakan Aspose—pengenalan, pemilihan bahasa, pra‑pemrosesan gambar, apa saja.

## Langkah 3: Cara Mengatur Bahasa — Mengonfigurasi Latin Extended

Di sinilah kata kunci utama bersinar. Untuk mencapai akurasi terbaik Anda harus memberi tahu mesin set bahasa apa yang diharapkan. Aspose OCR mendukung puluhan bahasa, tetapi untuk banyak teks Eropa Barat Anda akan menginginkan **Latin Extended**.

```python
# How to set language: configure the engine to recognize Latin Extended characters
engine.language = ocr.Language.LATIN_EXTENDED
```

Mengapa ini penting? Mengatur bahasa mempersempit set karakter yang dicari mesin, secara dramatis mengurangi hasil positif palsu. Jika Anda melewatkan langkah ini, Anda mungkin mendapatkan output yang berantakan, terutama dengan karakter beraksen.

### Opsi Bahasa Alternatif

Jika gambar Anda berisi **Cyrillic** atau **Arabic**, cukup ganti enum:

```python
engine.language = ocr.Language.CYRILLIC      # For Russian, Bulgarian, etc.
engine.language = ocr.Language.ARABIC        # For Arabic script
```

Anda bahkan dapat menggabungkan beberapa bahasa dengan mengirimkan daftar, tetapi ingat bahwa setiap bahasa tambahan sedikit memperlambat pemrosesan.

## Langkah 4: Muat Gambar yang Ingin Anda Konversi (Ekstrak Teks PNG)

Bagian selanjutnya dari puzzle adalah memberi mesin bitmap. Aspose OCR dapat membaca banyak format, tetapi kami akan fokus pada **PNG** karena bersifat lossless dan banyak digunakan.

```python
# Load the image that contains the text you want to recognize
image = ocr.Image.load("YOUR_DIRECTORY/input.png")
```

Jika Anda bertanya-tanya cara mengekstrak teks dari **PNG** yang berada di web, Anda dapat mengunduhnya terlebih dahulu menggunakan `requests` dan kemudian mengirimkan byte array ke `ocr.Image.from_bytes()`.

```python
import requests
response = requests.get("https://example.com/sample.png")
image = ocr.Image.from_bytes(response.content)
```

## Langkah 5: Lakukan OCR dan Cetak Hasilnya (Cara Menggunakan OCR)

Sekarang tiba saatnya—jalankan mesin dan ambil teksnya.

```python
# Perform OCR and output the recognised text
result = engine.recognize(image)

print("Recognised text:")
print(result.text)
```

Properti `result.text` menyimpan output konversi **image to text python**. Ini adalah string biasa, sehingga Anda dapat menuliskannya ke file, mengirimkannya ke chatbot, atau bahkan menjalankan analisis sentimen.

### Output yang Diharapkan

Dengan asumsi `input.png` berisi frasa “Hello, World!” Anda akan melihat:

```
Recognised text:
Hello, World!
```

Jika gambar berisi beberapa baris, mereka akan dipisahkan oleh karakter baris baru (`\n`). Anda dapat memisahkannya dengan `result.text.splitlines()` untuk pemrosesan lebih lanjut.

## Langkah 6: Kesalahan Umum dan Cara Memperbaikinya

### 1. Gambar Buram Menghasilkan Sampah

- **Solusi:** Pra‑proses gambar (tingkatkan kontras, tajamkan). Aspose OCR menawarkan filter bawaan, misalnya `engine.image_preprocessing = ocr.ImagePreprocessing.AUTO`.

### 2. Bahasa Salah Menghasilkan Aksen Hilang

- **Solusi:** Periksa kembali bahwa Anda memanggil `engine.language = ocr.Language.LATIN_EXTENDED` **sebelum** memanggil `recognize`. Mengubah bahasa setelah pengenalan tidak berpengaruh.

### 3. Lisensi Tidak Ditemukan → Watermark Evaluasi

- **Solusi:** Verifikasi jalur ke `Aspose.OCR.Java.lic`. Gunakan jalur absolut atau `os.path.join(os.getcwd(), "license", "Aspose.OCR.Java.lic")` untuk menghindari kejutan jalur relatif.

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabungkan)

Berikut adalah skrip lengkap yang dapat Anda salin‑tempel ke `ocr_demo.py` dan jalankan:

```python
import asposeocr as ocr
import os

# -------------------------------------------------
# 1️⃣ Load license (optional)
# -------------------------------------------------
license_path = os.path.join("YOUR_DIRECTORY", "Aspose.OCR.Java.lic")
if os.path.exists(license_path):
    ocr.License().set_license(license_path)
    print("License loaded successfully.")
else:
    print("License not found – running in evaluation mode.")

# -------------------------------------------------
# 2️⃣ Create OCR engine
# -------------------------------------------------
engine = ocr.OcrEngine()

# -------------------------------------------------
# 3️⃣ How to set language – Latin Extended for accented chars
# -------------------------------------------------
engine.language = ocr.Language.LATIN_EXTENDED

# -------------------------------------------------
# 4️⃣ Load PNG image (extract text png)
# -------------------------------------------------
image_path = os.path.join("YOUR_DIRECTORY", "input.png")
image = ocr.Image.load(image_path)

# -------------------------------------------------
# 5️⃣ Perform OCR – how to use OCR
# -------------------------------------------------
result = engine.recognize(image)

# -------------------------------------------------
# 6️⃣ Output – how to extract text / image to text python
# -------------------------------------------------
print("\n--- Recognised text ---")
print(result.text)
```

Simpan file, ganti `YOUR_DIRECTORY` dengan folder yang sebenarnya, dan jalankan:

```bash
python ocr_demo.py
```

Anda akan melihat teks yang dikenali dicetak ke konsol.

## Bonus: Menyimpan Output ke File Teks

Jika Anda lebih suka file yang persisten daripada output konsol:

```python
output_path = os.path.join("YOUR_DIRECTORY", "output.txt")
with open(output_path, "w", encoding="utf-8") as f:
    f.write(result.text)
print(f"Text saved to {output_path}")
```

Sekarang Anda telah menyelesaikan **cara mengatur bahasa**, **cara menggunakan OCR**, dan **cara mengekstrak teks** dari PNG—semua dalam Python.

---

## Kesimpulan

Kami baru saja mendemonstrasikan **cara mengatur bahasa** di Aspose OCR dengan Python, menunjukkan **cara menggunakan OCR** untuk membaca gambar, dan menjelaskan **cara mengekstrak teks** dari file PNG—pada dasarnya mengubah gambar menjadi teks yang dapat diedit menggunakan teknik **image to text python**. Skrip lengkap siap dijalankan, dan Anda dapat menyesuaikannya untuk bahasa lain atau format gambar hanya dengan mengubah satu baris.

Siap untuk langkah selanjutnya? Coba proses sekumpulan gambar dalam loop, bereksperimen dengan pengaturan bahasa yang berbeda, atau integrasikan output ke dalam pipeline pemrosesan dokumen yang lebih besar. Langit adalah batasnya setelah Anda menguasai dasar-dasarnya.

Ada pertanyaan tentang bahasa tertentu atau membutuhkan bantuan debugging gambar yang sulit? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}