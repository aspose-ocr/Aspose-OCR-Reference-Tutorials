---
category: general
date: 2026-11-20
description: Lakukan OCR pada gambar dengan Aspose OCR dan kemudian ekstrak teks dari
  gambar menggunakan post‑processor AI bawaan. Pelajari alur kerja Python lengkap
  dalam hitungan menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: id
lastmod: 2026-11-20
og_description: Lakukan OCR pada gambar dengan Aspose OCR, kemudian ekstrak teks dari
  gambar melalui pemrosesan lanjutan AI. Ikuti panduan Python langkah demi langkah
  ini.
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: Lakukan OCR pada gambar dan ekstrak teks dari gambar menggunakan Aspose
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: Lakukan OCR pada gambar dan ekstrak teks dari gambar dengan Aspose
url: /id/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada gambar dan ekstrak teks dari gambar dengan Aspose

Jika Anda perlu **perform OCR on image** file dalam Python, panduan ini menunjukkan solusi lengkap end‑to‑end. Menggunakan Aspose OCR bersama dengan post‑processor Aspose AI, Anda dapat secara andal **extract text from image** file dan meningkatkan output OCR mentah dengan model bahasa ringan.

Dalam tutorial ini Anda akan:

* Siapkan mesin Aspose OCR.
* Jalankan OCR untuk **extract text from image**.
* Opsional, konfigurasikan model AI untuk post‑processing.
* Daftarkan fungsi post‑processor kustom.
* Hasilkan teks yang ditingkatkan dan bersihkan sumber daya.

Langkah‑langkah ini bekerja dengan gambar raster apa pun (PNG, JPEG, BMP) dan hanya memerlukan paket `aspose-ocr`.

## Prerequisites

Sebelum Anda memulai, pastikan Anda memiliki:

| Persyaratan | Mengapa penting |
|-------------|----------------|
| Python 3.8+ | Diperlukan oleh Aspose SDK. |
| `aspose-ocr` pip package | Menyediakan `AsposeOCR`, `AsposeAI`, dan kelas konfigurasi model. |
| An image file (e.g., `sample_image.png`) | Sumber yang akan Anda **perform OCR on image**. |
| Optional: GPU support | Jika Anda berencana menjalankan model yang lebih besar pada GPU, atur `gpu_layers` sesuai. |

Install SDK dengan:

```bash
pip install aspose-ocr
```

## Langkah 1: Lakukan OCR pada gambar

Operasi pertama adalah membaca gambar dan memperoleh teks mentah. Ini adalah langkah inti **perform OCR on image**.

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**Mengapa ini berhasil:** `AsposeOCR.recognize_image` menjalankan model optical‑character‑recognition yang telah dilatih sebelumnya dan dioptimalkan untuk kecepatan serta akurasi pada font umum. Metode ini mengembalikan string Unicode biasa, yang menjadi dasar untuk pemrosesan lebih lanjut.

> **Pro tip:** Jika gambar berisi banyak bahasa, setel `ocr_engine.language = "eng+spa"` (atau kode ISO‑639‑2 yang didukung) sebelum memanggil `recognize_image`.

## Langkah 2: Inisialisasi post‑processor AI

Aspose AI menyediakan lapisan post‑processing ringan yang dapat membersihkan kesalahan OCR, memperbaiki tanda baca, atau menerapkan logika bisnis kustom.

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**Mengapa Anda membutuhkannya:** OCR mentah sering salah mengenali karakter (mis., “0” vs “O”). Langkah AI menyempurnakan output, membuat hasil **extract text from image** lebih dapat diandalkan untuk tugas hilir seperti pengindeksan atau analitik.

## Langkah 3: (Opsional) Konfigurasikan model AI

Anda dapat mengarahkan processor ke model Hugging Face tertentu, mengaktifkan unduhan otomatis, atau memaksa eksekusi CPU. Langkah ini opsional tetapi berguna ketika Anda menginginkan perilaku deterministik.

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**Penjelasan:**  
* `allow_auto_download` menghemat Anda dari manajemen model manual.  
* `hugging_face_repo_id` memilih model; `gpt2` merupakan kompromi yang baik antara ukuran dan kualitas untuk koreksi teks pendek.  
* `gpu_layers` mengontrol berapa banyak lapisan transformer yang dijalankan di GPU; `0` memaksa eksekusi CPU murni, yang aman di semua mesin.

## Langkah 4: Daftarkan fungsi post‑processing kustom

Aspose AI memungkinkan Anda menyambungkan callable apa pun yang menerima string OCR mentah dan mengembalikan versi yang telah diubah. Berikut contoh sederhana yang mengubah semua menjadi huruf besar.

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**Kapan menyesuaikan:** Gunakan fungsi kustom ketika Anda memerlukan pembersihan khusus domain, seperti menghapus pengidentifikasi rahasia, menormalkan tanggal, atau menerapkan koreksi berbasis regex. Model AI akan dijalankan *setelah* fungsi ini, memungkinkan Anda menggabungkan aturan deterministik dengan perbaikan probabilistik.

## Langkah 5: Tingkatkan hasil OCR menggunakan post‑processor AI

Sekarang jalankan pipeline lengkap: teks OCR mentah pertama kali melewati fungsi kustom Anda, kemudian melalui model AI, dan akhirnya Anda menerima output yang telah disempurnakan.

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**Apa yang harus Anda lihat:**  
Jika gambar asli berisi “Hello world”, konsol mungkin menampilkan:

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

Dalam skenario nyata, model AI akan memperbaiki ejaan yang salah, menambahkan tanda baca yang hilang, atau memformat ulang baris, memberi Anda hasil **extract text from image** yang lebih bersih dan siap untuk penyimpanan atau analisis.

## Langkah 6: Lepaskan sumber daya saat selesai

Baik mesin OCR maupun post‑processor AI mengalokasikan sumber daya native. Membebaskan secara eksplisit menghindari kebocoran memori, terutama pada layanan yang berjalan lama.

```python
# Clean up native resources
ai_processor.free_resources()
```

Jika Anda juga menginstansiasi `ocr_engine` dengan backend berat, Anda dapat memanggil `ocr_engine.dispose()` (jika tersedia) dengan cara yang sama.

## Variasi umum dan kasus tepi

| Situasi | Penyesuaian yang direkomendasikan |
|-----------|------------------------|
| **PDF besar dengan banyak halaman** | Loop setiap halaman, panggil `recognize_image` untuk setiap halaman yang diraster, dan gabungkan hasilnya. |
| **Lingkungan dengan GPU** | Atur `model_config.gpu_layers` ke jumlah lapisan yang Anda inginkan di GPU (mis., `4`). Pastikan driver CUDA terpasang. |
| **Teks non‑Inggris** | Ubah `ocr_engine.language` ke kode bahasa yang sesuai dan, jika diperlukan, pilih model Hugging Face khusus bahasa. |
| **Pemindaian sangat berisik** | Pra‑proses gambar dengan OpenCV (hilangkan noise, threshold) sebelum memanggil `recognize_image`. |
| **Perlu mempertahankan kapitalisasi asli** | Ganti fungsi `my_post_processor` dengan no‑op atau aturan yang lebih halus alih-alih `text.upper()`. |

## Contoh kerja lengkap

Menggabungkan semuanya, berikut skrip tunggal yang dapat Anda jalankan apa adanya (ganti `YOUR_DIRECTORY/sample_image.png` dengan jalur file Anda yang sebenarnya):

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

Menjalankan skrip ini mencetak baik output OCR mentah maupun versi yang ditingkatkan AI, menunjukkan bagaimana Anda dapat **perform OCR on image** file dan secara andal **extract text from image** dalam alur kerja tunggal yang dapat direproduksi.

## Kesimpulan

Anda kini tahu cara **perform OCR on image** file dengan Aspose OCR, kemudian **extract text from image** menggunakan post‑processor AI bawaan. Tutorial ini mencakup:

* Menginisialisasi mesin OCR.
* Menjalankan OCR untuk memperoleh teks mentah.
* (Opsional) mengonfigurasi model Hugging Face ringan.
* Menambahkan sebuah

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks Gambar dengan Aspose OCR & AI – Panduan Langkah‑per‑Langkah Lengkap](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [Cara Memperbaiki Kesalahan OCR – Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Ekstrak Teks dari Gambar Python – Panduan Lengkap Aspose OCR](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}