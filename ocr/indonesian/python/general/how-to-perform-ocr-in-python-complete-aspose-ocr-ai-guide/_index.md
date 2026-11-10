---
category: general
date: 2026-06-25
description: Pelajari cara melakukan OCR dengan Python dan temukan cara terbaik memuat
  gambar untuk OCR, kemudian tingkatkan akurasi dengan pemrosesan pasca Aspose AI.
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: id
og_description: Bagaimana melakukan OCR dengan Python? Ikuti panduan ini untuk memuat
  gambar untuk OCR, menjalankan pengenalan dasar, dan meningkatkan hasil dengan pemrosesan
  pasca Aspose AI.
og_title: Cara Melakukan OCR di Python – Tutorial Lengkap Aspose OCR & AI
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Cara Melakukan OCR di Python – Panduan Lengkap Aspose OCR & AI
url: /id/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di Python – Panduan Lengkap Aspose OCR & AI

Pernah bertanya-tanya **bagaimana melakukan OCR** di Python tanpa harus berurusan dengan trik‑trik gambar tingkat rendah? Anda tidak sendirian. Dalam tutorial ini kami akan membahas cara memuat gambar untuk OCR, mengekstrak teks biasa, dan kemudian memoles output dengan post‑processor AI Aspose. Pada akhir tutorial Anda akan memiliki skrip siap pakai yang mengubah pemindaian berisik menjadi teks bersih yang dapat dicari—tanpa layanan tambahan.

Kami akan membahas semuanya mulai dari menginstal SDK hingga membebaskan sumber daya dalam aplikasi yang berjalan lama. Jika Anda pernah mencoba **load image for OCR** dan mendapatkan hasil yang berantakan, panduan ini adalah antidotnya. Anda akan melihat mengapa menggabungkan OCR tradisional dengan model bahasa menghasilkan hasil yang tampak seperti diketik oleh manusia.

## Prasyarat

- Python 3.9 atau lebih baru (kode menggunakan type hints yang tidak disukai interpreter lama)
- Lisensi Aspose OCR yang aktif atau percobaan gratis (edisi komunitas cukup untuk evaluasi)
- GPU dengan setidaknya 4 GB VRAM jika Anda ingin mempercepat model AI (opsional tapi bagus)
- Contoh gambar, misalnya `sample_invoice.png`, ditempatkan di lokasi yang dapat Anda referensikan

Jika ada yang terdengar tidak familiar, jangan panik—menginstal SDK hanya satu baris, dan pengaturan GPU dapat dimatikan nanti.

## Langkah 1: Instal Aspose OCR dan Dependensi

Buka terminal dan jalankan:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

Paket pertama memberi Anda `aspose.ocr`, paket kedua menambahkan utilitas post‑processor AI. Kedua‑nya adalah wheel Python murni, jadi Anda tidak perlu mengompilasi apa pun sendiri.

## Langkah 2: Muat Gambar untuk OCR dan Inisialisasi Engine

Sekarang kami akan **load image for OCR** menggunakan `OcrEngine` milik Aspose. Anggap ini seperti menyerahkan selembar kertas kepada petugas yang sangat teliti yang membaca setiap karakter.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **Mengapa ini penting:** Panggilan `load_image` adalah jembatan antara sistem file Anda dan engine OCR. Jika path salah, Anda akan mendapatkan `FileNotFoundError` sebelum pengenalan apa pun dimulai. Selalu periksa kembali pemisah direktori, terutama di Windows vs. macOS/Linux.

## Langkah 3: Siapkan Post‑Processor AI Aspose

Aspose AI dapat mengunduh model bahasa dari Hugging Face, menyimpannya secara lokal, dan menjalankan inferensi pada GPU Anda (atau CPU). Di bawah ini kami mengonfigurasi model ringan 3‑miliar‑parameter yang cocok untuk kebanyakan laptop modern.

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **Tip:** Jika Anda berada di mesin hanya CPU, setel `gpu_layers = 0`. Model tetap akan berjalan, hanya sedikit lebih lambat. Kuantisasi `int8` menjaga jejak memori tetap kecil sambil mempertahankan sebagian besar akurasi model.

## Langkah 4: Daftarkan Post‑Processor Kustom

Model AI membutuhkan prompt yang memberi tahu apa yang harus dilakukan. Di sini kami memintanya bertindak seperti proof‑reader OCR, memperbaiki kesalahan ejaan, menggabungkan kata yang terputus, dan menghapus artefak.

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **Mengapa processor kustom?** Post‑processor default mungkin menambahkan penjelasan atau format tambahan yang tidak Anda perlukan. Dengan menyediakan fungsi kami sendiri, kami menjaga output tetap hanya teks yang telah dibersihkan, yang sempurna untuk pengindeksan downstream atau penyimpanan basis data.

## Langkah 5: Jalankan Pipeline OCR yang Ditingkatkan AI

Sekarang kami memasukkan output OCR mentah ke lapisan AI. Engine akan memanggil `correction_processor` kami, yang pada gilirannya berkomunikasi dengan model bahasa.

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

Anda akan melihat peningkatan yang nyata: karakter yang hilang dipulihkan, kesalahan umum OCR seperti “0” vs “O” diperbaiki, dan pemisahan baris menjadi lebih logis.

## Langkah 6: Pembersihan – Membebaskan Sumber Daya

Jika Anda berencana menjalankan ini di dalam layanan web atau daemon yang berjalan lama, membebaskan memori GPU sangat penting. Lupa memanggil `free_resources` dapat menyebabkan crash “out‑of‑memory” setelah beberapa ratus permintaan.

```python
ocr_ai.free_resources()
```

Itu saja—pipeline OCR lengkap Anda kini siap produksi.

## Ringkasan Skrip Lengkap

Berikut adalah contoh lengkap yang dapat dijalankan. Salin‑tempel ke file bernama `ocr_with_ai.py`, sesuaikan path gambar, dan jalankan `python ocr_with_ai.py`.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### Output yang Diharapkan

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

Perhatikan bagaimana “Inv0ice” menjadi “Invoice” dan huruf “O” yang terlepas setelah jumlah menghilang. Itulah AI yang melakukan keajaibannya.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya tidak memiliki GPU?

Setel `model_config.gpu_layers = 0` dan opsional tingkatkan `model_config.context_size` menjadi 2048 untuk performa CPU yang lebih baik. Model akan berjalan lebih lambat, tetapi Anda tetap mendapatkan kualitas koreksi yang sama.

### Gambar saya diputar—apakah `load_image` akan menanganinya?

Aspose OCR secara otomatis mendeteksi orientasi, tetapi untuk pemindaian yang sangat miring Anda mungkin ingin memutar terlebih dahulu menggunakan Pillow:

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### Bagaimana cara memproses banyak file dalam sebuah folder?

Bungkus seluruh pipeline dalam loop `for` dan simpan setiap `enhanced_text` dalam daftar atau tulis langsung ke CSV. Ingat untuk memanggil `ocr_ai.free_resources()` **sekali** setelah loop, bukan setelah setiap file—menginisialisasi ulang model berulang‑ulang akan membuang-buang sumber daya.

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### Bisakah saya mengganti model bahasa?

Tentu saja. Cukup ubah `model_config.hugging_face_repo_id` ke model GGUF‑compatible apa pun di Hugging Face (misalnya `Meta/Llama-3.2-1B-Instruct-GGUF`). Pertahankan pengaturan kuantisasi konsisten dengan perangkat keras Anda.

## Tips Pro & Jebakan

- **Pro tip:** Setel `temperature=0.0` untuk koreksi deterministik. Temperatur yang lebih tinggi dapat memperkenalkan perubahan kreatif namun tidak tepat.
- **Waspadai:** Dokumen yang sangat panjang (> 5000 karakter). Jendela konteks model terbatas pada 1024 token dalam contoh; bagi teks menjadi paragraf sebelum mengirimnya ke AI.
- **Catatan keamanan:** Jika Anda menjalankan ini di lingkungan yang diatur, pastikan URL unduhan model masuk dalam whitelist. Flag `allow_auto_download` dapat

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}