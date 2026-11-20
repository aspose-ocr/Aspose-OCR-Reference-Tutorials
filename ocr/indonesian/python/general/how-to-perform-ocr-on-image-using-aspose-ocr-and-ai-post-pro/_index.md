---
category: general
date: 2026-09-25
description: Pelajari cara melakukan OCR pada gambar dengan Aspose OCR, memuat gambar
  untuk OCR, dan mengenali teks dari struk dalam contoh Python lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- load image for OCR
- recognize text from receipt
- Aspose OCR Python
- AI post‑processor OCR
language: id
lastmod: 2026-09-25
og_description: Lakukan OCR pada gambar menggunakan Aspose OCR di Python. Panduan
  ini menunjukkan cara memuat gambar untuk OCR dan mengenali teks dari struk dengan
  peningkatan AI.
og_image_alt: Screenshot of Python code performing OCR on an image and showing original
  vs AI‑enhanced text
og_title: Lakukan OCR pada gambar dengan Aspose OCR dan AI post‑processor – Panduan
  Python
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: Learn how to perform OCR on image with Aspose OCR, load image for OCR,
    and recognize text from receipt in a complete Python example.
  headline: How to perform OCR on image using Aspose OCR and AI post‑processor in
    Python
  type: TechArticle
tags:
- OCR
- Python
- Aspose
title: Cara melakukan OCR pada gambar menggunakan Aspose OCR dan AI post‑processor
  di Python
url: /id/python/general/how-to-perform-ocr-on-image-using-aspose-ocr-and-ai-post-pro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR pada gambar menggunakan Aspose OCR dan AI post‑processor di Python

Jika Anda perlu **perform OCR on image** file di Python, tutorial ini menunjukkan solusi lengkap yang siap dijalankan. Anda akan belajar cara **load image for OCR**, menjalankan mesin Aspose OCR, dan **recognize text from receipt** dokumen dengan post‑processing berbasis AI opsional.

Kami akan membahas setiap langkah, mulai dari menginstal SDK hingga melepaskan sumber daya, sehingga Anda dapat mengintegrasikan ekstraksi teks yang andal ke dalam aplikasi Anda sendiri tanpa melewatkan detail apa pun.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

- Python 3.8+ terinstal  
- Aspose OCR untuk Python via pip (`pip install aspose-ocr`)  
- Akses internet untuk mengunduh model AI opsional  
- Contoh gambar kwitansi (`receipt.png`) ditempatkan di direktori yang diketahui  

Tidak diperlukan layanan eksternal tambahan; kode dijalankan secara lokal dan menggunakan model gratis Qwen2‑3B‑Instruct ketika lapisan GPU tersedia.

## Langkah 1: Instal paket yang diperlukan

```bash
pip install aspose-ocr
```

Paket `aspose-ocr` berisi kelas `OcrEngine` dan post‑processor `AsposeAI` yang akan kami gunakan untuk **perform OCR on image** file.

## Langkah 2: Buat dan konfigurasikan mesin OCR – load image for OCR

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # <-- load image for OCR
```

Memanggil `load_image` memberi tahu mesin file mana yang akan dianalisis. Anda dapat mengganti path dengan file PNG, JPG, atau TIFF apa pun yang perlu **perform OCR on image**.

## Langkah 3: Siapkan AsposeAI post‑processor opsional

AI post‑processor dapat memperbaiki ejaan, meningkatkan format, atau menerapkan logika khusus setelah hasil OCR mentah dikembalikan.

```python
from aspose.ocr import AsposeAI, AsposeAIModelConfig

# Initialise the AI processor (logging is optional)
ai_processor = AsposeAI()   # AsposeAI(logging=my_logger)

# Define which model to use – it will auto‑download if missing
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20                     # use GPU layers when available
)

# Load the model configuration into the processor
ai_processor.initialize(model_config)   # implicit in many examples
```

Konfigurasi tersebut menginstruksikan processor untuk mengunduh model Qwen2 default, memungkinkan Anda untuk **perform OCR on image** dengan pemahaman bahasa tingkat tinggi.

## Langkah 4: Lampirkan fungsi post‑processing sederhana

Anda dapat menyambungkan callable apa pun yang menerima teks mentah dan mengembalikan versi yang telah diperbaiki. Berikut contoh minimal yang memperbaiki typo umum:

```python
def simple_spell_check(text, **kwargs):
    """Correct a frequent misspelling in receipt OCR results."""
    return text.replace("reciept", "receipt")

# Register the function with the AI processor
ai_processor.set_post_processor(simple_spell_check, {})
```

Karena fungsi tersebut terdaftar, setiap kali Anda memanggil `run_postprocessor`, output OCR akan melewati langkah ini.

## Langkah 5: Jalankan OCR dan tingkatkan hasil – recognize text from receipt

```python
# Perform the core OCR operation
raw_result = ocr_engine.recognize()          # <-- recognize text from receipt

# Let the AI processor improve the raw output
enhanced_result = ai_processor.run_postprocessor(raw_result)

# Display both versions
print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)
```

Pemanggilan `recognize` mengembalikan objek yang atribut `text`‑nya berisi karakter mentah yang diekstrak dari gambar kwitansi. Pemanggilan `run_postprocessor` berikutnya mengembalikan hasil baru di mana pemeriksaan ejaan kami (dan perbaikan berbasis model apa pun) telah diterapkan.

### Output yang Diharapkan

```
Original OCR : Total: $23.45\nSubtotl: $20.00\nTax: $3.45\nThank you for your reciept
AI‑enhanced  : Total: $23.45
Subtotal: $20.00
Tax: $3.45
Thank you for your receipt
```

Perhatikan bagaimana teks yang ditingkatkan AI memperbaiki typo dan menyisipkan jeda baris untuk keterbacaan—tepat apa yang Anda inginkan saat **recognize text from receipt** file.

## Langkah 6: Bersihkan sumber daya

```python
# Release memory held by the AI processor
ai_processor.free_resources()

# Dispose of the OCR engine
ocr_engine.dispose()
```

Melepaskan sumber daya sangat penting terutama saat memproses banyak gambar dalam layanan yang berjalan lama.

## Skrip lengkap yang dapat dijalankan

Menggabungkan semua bagian memberi Anda satu skrip yang dapat Anda salin, tempel, dan jalankan:

```python
# ocr_receipt.py
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# 1️⃣ Initialise OCR engine and load the image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # load image for OCR

# 2️⃣ Set up optional AI post‑processor
ai_processor = AsposeAI()
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20
)
ai_processor.initialize(model_config)

# 3️⃣ Register a simple spell‑check function
def simple_spell_check(text, **kwargs):
    return text.replace("reciept", "receipt")
ai_processor.set_post_processor(simple_spell_check, {})

# 4️⃣ Perform OCR and enhance the result
raw_result = ocr_engine.recognize()                # recognize text from receipt
enhanced_result = ai_processor.run_postprocessor(raw_result)

print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)

# 5️⃣ Release resources
ai_processor.free_resources()
ocr_engine.dispose()
```

Jalankan skrip dengan:

```bash
python ocr_receipt.py
```

Anda akan melihat output asli dan output yang ditingkatkan AI dicetak ke konsol.

## Tips profesional dan jebakan umum

- **Kualitas gambar penting** – pastikan gambar kwitansi terang dan tidak terlalu terkompresi; jika tidak, mesin OCR mungkin melewatkan karakter, mengurangi manfaat post‑processing.  
- **Ketersediaan GPU** – jika mesin Anda tidak memiliki GPU yang kompatibel, setel `gpu_layers=0` untuk memaksa inferensi CPU; model tetap akan berjalan, meskipun lebih lambat.  
- **Post‑processor khusus** – Anda dapat menghubungkan beberapa fungsi atau menggunakan model bahasa yang lebih canggih untuk memformat ulang tanggal, jumlah, atau nama vendor.  
- **Pemrosesan batch** – buat satu objek `AsposeAI` dan gunakan kembali pada banyak instance `OcrEngine` untuk menghindari pengunduhan model berulang.  

## Kesimpulan

Anda kini tahu cara **perform OCR on image** file menggunakan Aspose OCR, cara **load image for OCR**, dan cara **recognize text from receipt** dengan peningkatan berbasis AI. Dengan mengikuti langkah-langkah di atas, Anda dapat mengintegrasikan pemrosesan kwitansi yang akurat dan berkecepatan tinggi ke dalam aplikasi Python apa pun.

**Langkah selanjutnya**: jelajahi teknik post‑processing tambahan seperti normalisasi mata uang, integrasikan hasil ke dalam basis data, atau beralih ke model yang lebih besar untuk kwitansi multibahasa. Untuk kustomisasi lebih dalam, lihat dokumentasi Aspose OCR tentang paket bahasa khusus dan pra‑pemrosesan gambar lanjutan.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Konversi Gambar ke Teks: Ekstrak Teks dari Gambar Menggunakan Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar Menggunakan Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}