---
category: general
date: 2026-06-06
description: Lakukan OCR pada gambar menggunakan Aspose OCR dan model Hugging Face.
  Pelajari cara mengunduh model Hugging Face, mengekstrak teks dari faktur, dan membebaskan
  sumber daya GPU.
draft: false
keywords:
- perform OCR on image
- download Hugging Face model
- extract text from invoice
- free GPU resources
- load image for OCR
language: id
og_description: Lakukan OCR pada gambar menggunakan Aspose OCR dan model Hugging Face.
  Tutorial ini menunjukkan cara mengunduh model, mengekstrak teks dari faktur, dan
  membebaskan sumber daya GPU.
og_title: Lakukan OCR pada Gambar dengan Aspose OCR & LLM – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Perform OCR on image using Aspose OCR and a Hugging Face model. Learn
    how to download Hugging Face model, extract text from invoice, and free GPU resources.
  headline: Perform OCR on Image with Aspose OCR & LLM – Complete Guide
  type: TechArticle
tags:
- OCR
- Aspose
- Python
- AI
- HuggingFace
title: Lakukan OCR pada Gambar dengan Aspose OCR & LLM – Panduan Lengkap
url: /id/python/general/perform-ocr-on-image-with-aspose-ocr-llm-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar dengan Aspose OCR & LLM – Panduan Lengkap

Pernah ingin **perform OCR on image** file tetapi merasa terjebak pada pertanyaan “dari mana saya harus memulai?”? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika pertama kali menangani otomasi dokumen. Kabar baiknya, dengan Aspose OCR dan LLM ringan dari Hugging Face, Anda dapat mengubah pemindaian mentah faktur menjadi teks bersih yang dapat dicari hanya dalam beberapa baris Python.

Dalam tutorial ini kami akan membahas semua yang Anda perlukan: mulai dari **loading image for OCR**, hingga **downloading the Hugging Face model**, hingga **extracting text from invoice** data, dan akhirnya **free GPU resources** agar aplikasi Anda tetap ringan. Pada akhir tutorial Anda akan memiliki skrip mandiri yang dapat Anda masukkan ke proyek mana pun.

---

## Apa yang Akan Anda Pelajari

- Cara **perform OCR on image** menggunakan `OcrEngine` milik Aspose.
- Langkah tepat untuk **download Hugging Face model** secara otomatis.
- Teknik **extract text from invoice** dari PDF atau PNG dengan pemrosesan lanjutan berbasis AI.
- Praktik terbaik untuk **free GPU resources** setelah inferensi.
- Tips **load image for OCR** secara efisien dan menghindari jebakan umum.

Tidak diperlukan dokumentasi eksternal—semua yang Anda butuhkan ada di sini, lengkap dengan kode, penjelasan, dan output yang diharapkan.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

| Requirement | Reason |
|-------------|--------|
| Python 3.9+ | Sintaks modern dan type hints |
| `asposeocr` package (`pip install asposeocr`) | Mesin OCR inti |
| Akses ke GPU (opsional tetapi direkomendasikan) | Mempercepat post‑processor LLM |
| Gambar faktur (`sample_invoice.png`) | Kasus uji dunia nyata |

Jika ada yang belum terpasang, instal sekarang; skrip juga akan **download Hugging Face model** secara otomatis, jadi Anda tidak perlu mencari file secara manual.

---

## Langkah 1: Perform OCR on Image – Buat Engine

Hal pertama yang harus Anda lakukan adalah memulai engine OCR Aspose. Anggap saja ini seperti membuka kanvas kosong di mana gambar nanti akan diubah menjadi teks.

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

> **Mengapa ini penting:** `OcrEngine` mengabstraksi semua pra‑pemrosesan gambar tingkat rendah, sehingga Anda dapat fokus pada alur kerja tingkat tinggi. Engine ini juga menyediakan metode `set_post_processor` yang nantinya akan menghubungkan LLM untuk output yang lebih cerdas.

---

## Langkah 2: Load Image for OCR – Pilih File yang Tepat

Setelah engine ada, kita perlu **load image for OCR**. Aspose mendukung PNG, JPG, TIFF, dan beberapa format lainnya. Pastikan path bersifat absolut atau relatif terhadap lokasi skrip Anda.

```python
# Step 2: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Tip:** Jika gambar Anda berukuran besar, pertimbangkan untuk mengubah ukurannya terlebih dahulu guna mengurangi tekanan memori. Engine OCR dapat menangani pemindaian resolusi tinggi, tetapi gambar 300 DPI biasanya merupakan titik optimal untuk faktur.

---

## Langkah 3: Perform Raw OCR dan Lihat Teks yang Diekstrak

Dengan gambar sudah dimuat, kita akhirnya dapat **perform OCR on image** dan melihat apa yang dihasilkan oleh engine mentah. Langkah ini memberi kita baseline sebelum menambahkan sentuhan AI.

```python
# Step 3: Run the built‑in OCR and capture raw results
raw_result = engine.recognize()
print("Raw text:")
print(raw_result.text)
```

**Output yang diharapkan (dipotong):**

```
Raw text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Output mentah sering kali berisi pemisah baris, karakter yang salah dikenali, atau bidang yang hilang—itulah mengapa kita akan menambahkan model bahasa pada langkah berikutnya.

---

## Langkah 4: Download Hugging Face Model – Konfigurasikan Post‑Processor LLM

Inilah saat **download Hugging Face model** menjadi sorotan. Aspose AI dapat secara otomatis mengambil model dari hub Hugging Face jika belum ada di disk. Kita akan menggunakan model Qwen2.5‑3B‑Instruct‑GGUF, yang menyeimbangkan akurasi dan jejak memori.

```python
# Step 4: Set up the AI model configuration
ai_cfg = AsposeAIModelConfig(
    allow_auto_download="true",               # automatically fetch model if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",         # int8 quantization cuts RAM usage dramatically
    gpu_layers=20,                            # first 20 layers run on GPU, rest on CPU
    directory_model_path="YOUR_DIRECTORY/asp_ocr_models"
)
```

> **Mengapa ini berhasil:** `allow_auto_download` menghilangkan kebutuhan mengunduh file `.gguf` secara manual. Kuantisasi (`int8`) mengurangi ukuran model menjadi sekitar 3 GB, membuatnya dapat dijalankan pada kebanyakan GPU konsumen. Sesuaikan `gpu_layers` berdasarkan perangkat keras Anda—lebih banyak lapisan di GPU = inferensi lebih cepat.

---

## Langkah 5: Extract Text from Invoice Menggunakan Post‑Processing AI‑Enhanced

Sekarang kita mengaitkan LLM ke engine OCR dan menjalankan **post‑processor** yang membersihkan output mentah, memperbaiki kesalahan OCR, serta memformat bidang faktur dengan rapi.

```python
# Step 5: Initialize the AI engine and bind it to the OCR engine
ai_engine = AsposeAI()
ai_engine.initialize(ai_cfg)                 # implicit when using set_post_processor in newer versions
engine.set_post_processor(ai_engine)

# Run the AI‑enhanced post‑processor
enhanced_result = engine.run_postprocessor(raw_result)
print("\nEnhanced text:")
print(enhanced_result.text)
```

**Contoh output yang ditingkatkan:**

```
Enhanced text:
Invoice Number: 12345
Date: 2024-04-01
Bill To: Acme Corp.
Amount Due: $1,250.00
Status: Paid
```

> **Apa yang terjadi?** LLM mengenali bahwa “Invoice #12345” seharusnya “Invoice Number: 12345”, memperbaiki format tanggal, dan bahkan menebak bidang “Bill To” yang terlewat oleh engine mentah. Inilah inti dari otomatisasi **extract text from invoice**.

---

## Langkah 6: Free GPU Resources – Bersihkan Setelah Pemrosesan

Jika Anda menjalankan ini dalam layanan yang berjalan lama (misalnya API Flask), Anda harus **free GPU resources** setelah setiap inferensi untuk menghindari crash karena kehabisan memori. Aspose AI menyediakan metode sederhana untuk itu.

```python
# Step 6: Release GPU memory and dispose of the engine
ai_engine.free_resources()   # frees GPU layers and model tensors
engine.dispose()             # cleans up internal buffers
```

> **Pro tip:** Panggil `free_resources()` di dalam blok `finally:` jika Anda membungkus panggilan OCR dalam `try/except`. Hal ini menjamin pembersihan bahkan ketika terjadi pengecualian.

---

## Langkah 7: Skrip Lengkap – Gabungkan Semua

Berikut adalah skrip lengkap yang siap dijalankan. Salin‑tempel, sesuaikan path, dan Anda siap.

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Load image for OCR
engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# 3️⃣ Raw OCR
raw_result = engine.recognize()
print("Raw text:")
print(raw_result.text)

# 4️⃣ Download Hugging Face model (auto‑download enabled)
ai_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    directory_model_path="YOUR_DIRECTORY/asp_ocr_models"
)

# 5️⃣ Attach AI post‑processor and enhance text
ai_engine = AsposeAI()
ai_engine.initialize(ai_cfg)          # optional in newer versions
engine.set_post_processor(ai_engine)

enhanced_result = engine.run_postprocessor(raw_result)
print("\nEnhanced text:")
print(enhanced_result.text)

# 6️⃣ Free GPU resources
ai_engine.free_resources()
engine.dispose()
```

Jalankan skrip dan saksikan transformasi dari OCR berisik menjadi data faktur yang bersih dan terstruktur. 🎉

---

## Pertanyaan Umum & Kasus Edge

| Question | Answer |
|----------|--------|
| **What if the model fails to download?** | Ensure your machine has internet access and that the `hugging_face_repo_id` is correct. You can also manually download the

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}