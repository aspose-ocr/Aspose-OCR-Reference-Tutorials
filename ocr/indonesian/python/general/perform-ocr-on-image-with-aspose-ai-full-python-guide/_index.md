---
category: general
date: 2026-06-19
description: Pelajari cara melakukan OCR pada gambar menggunakan Aspose OCR dan AI
  post‑processor di Python. Termasuk model yang diunduh otomatis, pemeriksaan ejaan,
  dan percepatan GPU.
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: id
og_description: lakukan OCR pada gambar menggunakan Aspose OCR dan AI post‑processor.
  Panduan langkah demi langkah dengan model yang diunduh otomatis, pemeriksaan ejaan,
  dan percepatan GPU.
og_title: Lakukan OCR pada gambar – Tutorial Python Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Lakukan OCR pada Gambar dengan Aspose AI – Panduan Python Lengkap
url: /id/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# melakukan OCR pada gambar – Tutorial Python Lengkap

Pernah bertanya-tanya bagaimana cara **melakukan OCR pada gambar** file tanpa berurusan dengan puluhan pustaka? Dalam pengalaman saya, titik sakit biasanya mengelola mesin OCR mentah, lalu mencoba membersihkan output yang berisik. Untungnya, Aspose OCR untuk Python yang dipasangkan dengan AI post‑processor‑nya membuat seluruh alur kerja menjadi mudah.

Dalam panduan ini kami akan menelusuri contoh praktis end‑to‑end yang menunjukkan secara tepat cara **melakukan OCR pada gambar** data, meningkatkan akurasi dengan model yang diunduh otomatis, mengaktifkan pemeriksaan ejaan, dan bahkan memanfaatkan akselerasi GPU bila tersedia. Pada akhir tutorial, Anda akan memiliki skrip yang dapat digunakan kembali dan dapat disisipkan ke dalam proyek faktur, pemindaian struk, atau digitalisasi dokumen apa pun.

## Apa yang Akan Anda Bangun

Kita akan membuat program Python kecil yang:

1. Menginisialisasi mesin Aspose OCR dan memuat gambar faktur contoh.  
2. Menjalankan proses OCR dasar dan mencetak teks mentah.  
3. Mengonfigurasi **Aspose AI** dengan **auto‑downloaded model** dari Hugging Face.  
4. Menjalankan **AI post‑processor** (termasuk **spellcheck post‑processor**) untuk membersihkan output OCR.  
5. Membebaskan semua sumber daya dengan bersih.

Tanpa layanan eksternal, tanpa kunci API—hanya beberapa baris Python dan kekuatan Aspose.

> **Pro tip:** Jika Anda menggunakan mesin dengan GPU yang memadai, mengatur `gpu_layers` dapat mengurangi beberapa detik dari langkah post‑processing.

## Prasyarat

- Python 3.8 atau lebih baru (kode menggunakan type hints tetapi bersifat opsional).  
- Paket `aspose-ocr` dan `aspose-ai` diinstal melalui `pip`.  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- Gambar contoh (PNG, JPG, atau TIFF) ditempatkan di suatu lokasi yang dapat Anda referensikan, misalnya `sample_invoice.png`.  
- (Opsional) GPU yang mendukung CUDA dan driver yang sesuai jika Anda menginginkan **GPU acceleration**.

Sekarang dasar sudah siap, mari kita selami kode.

![perform OCR on image example](image.png)

## melakukan OCR pada gambar – Langkah 1: Inisialisasi mesin OCR dan memuat gambar

Hal pertama yang kita butuhkan adalah sebuah instance mesin OCR. Aspose OCR menawarkan API yang bersih dan berorientasi objek yang menyembunyikan preprocessing gambar tingkat rendah.

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**Mengapa ini penting:**  
Menetapkan bahasa di awal memberi tahu mesin set karakter apa yang diharapkan, yang dapat meningkatkan kecepatan dan akurasi pengenalan. Jika Anda menangani dokumen multibahasa, cukup ganti `"en"` dengan `"fr"` atau `"de"` sesuai kebutuhan.

## Langkah 2: Lakukan OCR dasar dan lihat teks mentah

Sekarang kita benar-benar menjalankan proses pengenalan. Objek hasil berisi teks mentah, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti.

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

Output tipikal mungkin terlihat seperti ini (perhatikan karakter yang terkadang salah dibaca):

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

Anda dapat melihat angka nol (`0`) di tempat mesin mengira melihat “O”. Di sinilah **AI post‑processor** bersinar.

## Konfigurasi Aspose AI – model auto‑downloaded dan pemeriksaan ejaan

Sebelum kami memberikan hasil OCR mentah ke lapisan AI, kami perlu memberi tahu Aspose AI model mana yang akan digunakan. Pustaka ini dapat secara otomatis mengunduh model dari Hugging Face, sehingga Anda tidak perlu mengelola file `.bin` besar secara manual.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**Penjelasan pengaturan**

| Pengaturan | Apa fungsinya | Kapan disesuaikan |
|------------|---------------|-------------------|
| `allow_auto_download` | Lets Aspose fetch the model automatically on first run. | Keep `true` unless you pre‑download for offline use. |
| `hugging_face_repo_id` | Identifier of the model on Hugging Face. | Swap for a different model if you need a domain‑specific one. |
| `hugging_face_quantization` | Chooses the quantization level (`int8`, `float16`, etc.). | Use `int8` for low‑memory environments; `float16` for higher accuracy. |
| `gpu_layers` | Number of transformer layers executed on the GPU. | Set to `0` for CPU‑only, or a value up to the model’s total layers (20 for Qwen2.5‑3B). |

## Jalankan AI post‑processor pada hasil OCR

Dengan mesin siap, kami cukup memasukkan output OCR mentah ke dalam pipeline AI. **spellcheck post‑processor** bawaan akan memperbaiki typo yang jelas, sementara model bahasa dapat mengulang frase atau mengisi informasi yang hilang jika Anda mengaktifkan proses tambahan nanti.

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

Output yang diharapkan setelah langkah spellcheck:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Perhatikan bagaimana angka nol telah diperbaiki menjadi huruf yang tepat, dan kata yang salah eja “Am0unt” berubah menjadi “Amount”. **AI post‑processor** bekerja dengan mengirimkan teks mentah melalui model yang dipilih, yang kemudian mengembalikan versi yang disempurnakan berdasarkan pelatihannya.

### Kasus Pinggir & Tips

- **Low‑resolution images**: Jika mesin OCR kesulitan, pertimbangkan memperbesar gambar terlebih dahulu (`Pillow` dapat membantu) atau meningkatkan `ocr_engine.ImagePreprocessingOptions`.  
- **Non‑Latin scripts**: Ubah `ocr_engine.Language` ke kode ISO yang sesuai (`"zh"` untuk bahasa Cina, `"ar"` untuk bahasa Arab).  
- **GPU not detected**: Pengaturan `gpu_layers` secara diam-diam beralih ke CPU jika tidak ada GPU yang kompatibel, jadi Anda tidak memerlukan penanganan error tambahan.  
- **Model size limits**: Model Qwen2.5‑3B berukuran ~4 GB terkompresi; pastikan disk Anda memiliki ruang yang cukup untuk auto‑download.

## Lepaskan sumber daya – penutupan bersih

Objek Aspose menyimpan handle native, jadi sebaiknya membebaskannya saat selesai. Ini mencegah kebocoran memori, terutama pada layanan yang berjalan lama.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

Anda dapat membungkus seluruh skrip dalam blok `try…finally` jika lebih suka pembersihan eksplisit.

## Skrip Lengkap – siap salin‑tempel

Berikut adalah seluruh program, siap dijalankan setelah Anda mengganti `YOUR_DIRECTORY` dengan path ke gambar Anda.

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

Jalankan dengan:

```bash
python perform_ocr_on_image.py
```

Anda akan melihat output mentah dan bersih dicetak ke konsol.

## Kesimpulan


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Konversi Gambar ke Teks – Lakukan OCR pada Gambar dari URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}