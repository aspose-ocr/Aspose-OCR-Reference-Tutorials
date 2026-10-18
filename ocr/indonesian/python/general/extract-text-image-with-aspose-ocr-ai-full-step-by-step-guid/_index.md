---
category: general
date: 2026-06-25
description: Ekstrak teks gambar menggunakan Aspose OCR dan AI. Pelajari cara memuat
  OCR gambar, meningkatkan akurasi OCR, memperbaiki kesalahan OCR, dan membebaskan
  sumber daya AI secara efisien.
draft: false
keywords:
- extract text image
- free ai resources
- improve ocr accuracy
- load image ocr
- correct OCR errors
language: id
og_description: Ekstrak teks gambar menggunakan Aspose OCR dan AI. Tutorial ini menunjukkan
  cara memuat OCR gambar, meningkatkan akurasi OCR, memperbaiki kesalahan OCR, dan
  membebaskan sumber daya AI.
og_title: Ekstrak Teks Gambar dengan Aspose OCR & AI – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text image using Aspose OCR and AI. Learn to load image OCR,
    improve OCR accuracy, correct OCR errors, and free AI resources efficiently.
  headline: Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide
  type: TechArticle
- description: Extract text image using Aspose OCR and AI. Learn to load image OCR,
    improve OCR accuracy, correct OCR errors, and free AI resources efficiently.
  name: Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide
  steps:
  - name: Import Aspose OCR and AI Modules
    text: 'We start by pulling in the two namespaces we’ll need: the core OCR engine
      and the AI helper that hosts the LLM.'
  - name: Create and Configure the OCR Engine (Enable GPU)
    text: Turning on GPU accelerates the pixel‑analysis phase, which can shave seconds
      off large batches.
  - name: Load the Image That Contains the Text to Be Recognized
    text: This is where we **load image OCR**. The path can be absolute or relative;
      just make sure the file exists.
  - name: Perform OCR and Obtain the Raw Extracted Text
    text: Now we actually **extract text image** content. The `recognize()` call returns
      a raw string, often riddled with line breaks and mis‑read characters.
  - name: Set Up the AI Post‑Processor (Auto‑Download Qwen2.5‑3B Model)
    text: We instantiate `AsposeAI`, configure it to pull the Qwen model from Hugging
      Face, and allocate GPU layers for inference.
  - name: Define a Simple Correction Function
    text: The function receives the raw OCR string, builds a prompt, and asks the
      model to proof‑read it. Temperature `0.0` forces deterministic output, which
      is ideal for correction tasks.
  - name: Attach the Correction Function and Clean the Raw OCR Result
    text: We bind `fix` as a post‑processor, then let the AI run over the `raw_text`.
      The result lands in `cleaned_text`.
  - name: Display the Corrected Text
    text: A quick `print` lets you verify that the pipeline succeeded.
  - name: Release AI Resources When Done
    text: Finally, we **free AI resources**. This call unloads the model from GPU
      memory, preventing leaks in long‑running services.
  type: HowTo
tags:
- OCR
- AI
- Aspose
title: Ekstrak Teks Gambar dengan Aspose OCR & AI – Panduan Langkah-demi-Langkah Lengkap
url: /id/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks Gambar dengan Aspose OCR & AI – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya‑tanya bagaimana cara **extract text image** tanpa menghabiskan banyak biaya pada layanan cloud? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika output OCR mentah terlihat berantakan, terutama pada pemindaian yang berisik.  

Dalam panduan ini kami akan membimbing Anda melalui contoh lengkap yang siap dijalankan yang menunjukkan cara **load image OCR**, meningkatkan kualitas untuk **improve OCR accuracy**, secara otomatis **correct OCR errors**, dan akhirnya **free AI resources** sehingga aplikasi Anda tetap ringan.

Anda akan selesai dengan string bersih yang dapat langsung Anda masukkan ke basis data, indeks pencarian, atau pipeline NLP apa pun. Tidak ada tautan misterius ke dokumen eksternal—semua yang Anda butuhkan ada di sini.

## Apa yang Akan Anda Bangun

- Muat file gambar dan jalankan Aspose OCR untuk mendapatkan teks mentah.  
- Sambungkan LLM pada perangkat (model Qwen2.5‑3B) ke dalam pipeline OCR sebagai post‑processor.  
- Gunakan prompt kecil untuk memeriksa dan memperbaiki output OCR.  
- Lepaskan model dan memori GPU dengan satu panggilan.  

Pada akhir Anda akan memiliki pola solid yang dapat Anda gunakan kembali untuk faktur, kwitansi, kontrak yang dipindai, atau bitmap apa pun yang berisi karakter yang dapat dibaca.

---

## Prerequisites

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.9+ | Sintaks modern dan petunjuk tipe. |
| `aspose-ocr` package | Menyediakan kelas `OcrEngine`. |
| GPU dengan CUDA (opsional) | Mengaktifkan `ocr_engine.use_gpu = True` untuk pengenalan lebih cepat. |
| Koneksi internet (run pertama) | Memungkinkan model Qwen diunduh otomatis. |
| Familiaritas dasar dengan fungsi | Diperlukan untuk melampirkan callback koreksi. |

Install the libraries with:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

> **Tip pro:** Jika Anda berada di mesin hanya CPU, cukup lewati baris `use_gpu`; kode akan kembali dengan lancar.

---

## Ekstrak Teks Gambar dengan Aspose OCR dan AI

Berikut adalah skrip lengkap, dibagi menjadi sembilan langkah logis. Setiap langkah diperkenalkan dengan penjelasan singkat, diikuti oleh kode tepat yang dapat Anda salin‑tempel.

### Step 1: Import Aspose OCR and AI Modules

Kami memulai dengan mengimpor dua namespace yang diperlukan: mesin OCR inti dan pembantu AI yang menyimpan LLM.

```python
# Step 1: Import Aspose OCR and AI modules
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai
```

> **Mengapa?** Menjaga impor bersama membuat skrip mudah diaudit dan menghindari ketergantungan tersembunyi di kemudian hari.

### Step 2: Create and Configure the OCR Engine (Enable GPU)

Mengaktifkan GPU mempercepat fase analisis piksel, yang dapat mengurangi beberapa detik pada batch besar.

```python
# Step 2: Create and configure the OCR engine (enable GPU for faster processing)
ocr_engine = aocr.OcrEngine()
ocr_engine.use_gpu = True   # Set to False if you lack a compatible GPU
```

> **Catatan:** Flag `use_gpu` aman untuk diubah; mesin akan secara otomatis mendeteksi ketersediaan CUDA.

### Step 3: Load the Image That Contains the Text to Be Recognized

Di sinilah kami **load image OCR**. Path dapat absolut atau relatif; pastikan file tersebut ada.

```python
# Step 3: Load the image that contains the text to be recognized
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

> **Jebakan umum:** Memberikan path yang salah akan memunculkan `FileNotFoundError`. Periksa kembali ejaan, terutama pada sistem file yang sensitif huruf besar/kecil.

### Step 4: Perform OCR and Obtain the Raw Extracted Text

Sekarang kami benar‑benarnya **extract text image** konten. Pemanggilan `recognize()` mengembalikan string mentah, sering kali penuh dengan pemisah baris dan karakter yang salah dibaca.

```python
# Step 4: Perform OCR and obtain the raw extracted text
raw_text = ocr_engine.recognize()
```

Jika Anda mencetak `raw_text` pada titik ini, Anda akan melihat sesuatu seperti:

```
Th1s is a s4mple test.
```

Perhatikan “1” menggantikan “i” dan “4” menggantikan “e”. Di situlah post‑processor AI bersinar.

### Step 5: Set Up the AI Post‑Processor (Auto‑Download Qwen2.5‑3B Model)

Kami menginstansiasi `AsposeAI`, mengkonfigurasinya untuk mengambil model Qwen dari Hugging Face, dan mengalokasikan lapisan GPU untuk inferensi.

```python
# Step 5: Set up the AI post‑processor (auto‑download Qwen2.5‑3B model)
ai_processor = aocr_ai.AsposeAI()
model_cfg = aocr_ai.AsposeAIModelConfig()
model_cfg.allow_auto_download = "true"
model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_cfg.gpu_layers = 20               # Adjust based on your GPU VRAM
ai_processor.initialize(model_cfg)
```

> **Mengapa model ini?** Qwen2.5‑3B‑Instruct cukup kecil untuk dijalankan pada GPU kelas menengah namun cukup kuat untuk memahami prompt proofreading, menjadikannya sempurna untuk **improve OCR accuracy** tanpa membengkaknya memori.

### Step 6: Define a Simple Correction Function

Fungsi ini menerima string OCR mentah, membangun prompt, dan meminta model untuk memeriksa. Temperatur `0.0` memaksa output deterministik, yang ideal untuk tugas koreksi.

```python
# Step 6: Define a simple correction function that asks the model to proof‑read the OCR output
def fix(text, _):
    prompt = f"Proof‑read and correct the OCR text:\n\n{text}"
    return ai_processor.run_inference(prompt, temperature=0.0, max_new_tokens=512)
```

> **Cara kerjanya:** LLM melihat teks tepat dan mengembalikan versi bersih, pada dasarnya berfungsi sebagai pemeriksa ejaan pintar yang juga memperbaiki anomali pemisah baris.

### Step 7: Attach the Correction Function and Clean the Raw OCR Result

Kami mengikat `fix` sebagai post‑processor, lalu membiarkan AI memproses `raw_text`. Hasilnya disimpan di `cleaned_text`.

```python
# Step 7: Attach the correction function as a post‑processor and clean the raw OCR result
ai_processor.set_post_processor(fix, None)
cleaned_text = ai_processor.run_postprocessor(raw_text)
```

Pada titik ini `cleaned_text` seharusnya berisi:

```
This is a simple test.
```

### Step 8: Display the Corrected Text

Sebuah `print` cepat memungkinkan Anda memverifikasi bahwa pipeline berhasil.

```python
# Step 8: Display the corrected text
print("Cleaned text:\n", cleaned_text)
```

Output konsol akan terlihat seperti:

```
Cleaned text:
 This is a simple test.
```

### Step 9: Release AI Resources When Done

Akhirnya, kami **free AI resources**. Panggilan ini membongkar model dari memori GPU, mencegah kebocoran pada layanan yang berjalan lama.

```python
# Step 9: Release AI resources when done
ai_processor.free_resources()
```

> **Mengapa penting:** Lupa membebaskan sumber daya dapat menyebabkan crash out‑of‑memory, terutama di lingkungan serverless di mana setiap pemanggilan harus membersihkan dirinya sendiri.

---

## How to Load Image OCR Efficiently

Jika Anda perlu memproses puluhan file, bungkus proses pemuatan dan pengenalan dalam loop:

```python
def ocr_one(path):
    ocr_engine.load_image(path)
    return ocr_engine.recognize()
```

Ingat untuk menggunakan kembali instance `ocr_engine` yang sama; membuat yang baru per gambar menambah overhead yang tidak perlu dan mengalahkan tujuan optimasi **load image OCR**.

---

## Techniques to Improve OCR Accuracy

1. **Pre‑process the image** – Konversi ke skala abu‑abu, tingkatkan kontras, dan luruskan sebelum memberi ke mesin.  
2. **Enable GPU** – Seperti yang ditunjukkan pada Langkah 2, jalur GPU sering menghasilkan skor kepercayaan lebih tinggi.  
3. **Post‑process with AI** – Langkah **correct OCR errors** adalah tuas paling kuat; dapat menangani keanehan bahasa spesifik yang tidak terdeteksi oleh pemeriksa ejaan berbasis aturan.  

Menggabungkan tiga taktik ini biasanya menurunkan word‑error‑rate sebesar 30‑40 % pada pemindaian dunia nyata.

---

## Correct OCR Errors Using an AI Post‑Processor

Fungsi `fix` yang kami definisikan sebelumnya sengaja minimal. Anda dapat memperkaya dengan instruksi tambahan, misalnya:

```python
def fix_with_formatting(text, _):
    prompt = (
        "You are a proofreading assistant. Return ONLY the corrected text, "
        "preserving line breaks and punctuation. Do not add explanations.\n\n"
        f"{text}"
    )
    return ai_processor.run_inference(prompt, temperature=0.0, max_new_tokens=1024)
```

Swapping `ai_processor.set_post_processor(fix_with_formatting, None)` yields cleaner, format‑preserving results—another way to **improve

## What Should You Learn Next?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Konversi Gambar ke Teks – Lakukan OCR pada Gambar dari URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}