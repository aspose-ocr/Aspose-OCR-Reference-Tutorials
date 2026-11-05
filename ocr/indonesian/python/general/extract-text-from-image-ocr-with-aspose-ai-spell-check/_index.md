---
category: general
date: 2026-05-03
description: Ekstrak teks dari gambar menggunakan Aspose OCR dan pemeriksaan ejaan
  AI. Pelajari cara melakukan OCR pada gambar, memuat gambar untuk OCR, mengenali
  teks dari faktur, dan melepaskan sumber daya GPU.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: id
og_description: Ekstrak teks dari gambar dengan Aspose OCR dan pemeriksaan ejaan AI.
  Panduan langkah demi langkah yang mencakup cara melakukan OCR pada gambar, memuat
  gambar untuk OCR, dan melepaskan sumber daya GPU.
og_title: Ekstrak teks dari gambar – Panduan Lengkap OCR & Pemeriksaan Ejaan
tags:
- OCR
- Aspose
- AI
- Python
title: Ekstrak teks dari gambar – OCR dengan Aspose AI Spell‑Check
url: /id/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ekstrak teks dari gambar – Panduan Lengkap OCR & Pemeriksaan Ejaan

Pernah perlu **ekstrak teks dari gambar** tetapi tidak yakin perpustakaan mana yang memberikan kecepatan dan akurasi? Anda tidak sendirian. Dalam banyak proyek dunia nyata—seperti pemrosesan faktur, digitalisasi struk, atau pemindaian kontrak—mendapatkan teks bersih yang dapat dicari dari sebuah gambar adalah tantangan pertama.

Kabar baiknya, Aspose OCR yang dipasangkan dengan model Aspose AI yang ringan dapat menangani pekerjaan itu dalam beberapa baris Python. Dalam tutorial ini kami akan menjelaskan **cara OCR gambar**, memuat gambar dengan benar, menjalankan post‑processor pemeriksaan ejaan bawaan, dan akhirnya **melepaskan sumber daya GPU** agar aplikasi Anda tetap ramah memori.

Pada akhir panduan ini Anda akan dapat **mengenali teks dari gambar faktur**, memperbaiki kesalahan OCR umum secara otomatis, dan menjaga GPU Anda bersih untuk batch berikutnya.

---

## Apa yang Anda Butuhkan

- Python 3.9 atau lebih baru (kode menggunakan type hints tetapi bekerja pada versi 3.x sebelumnya)
- Paket `aspose-ocr` dan `aspose-ai` (pasang via `pip install aspose-ocr aspose-ai`)
- GPU yang mendukung CUDA bersifat opsional; skrip akan beralih ke CPU jika tidak ada.
- Contoh gambar, misalnya `sample_invoice.png`, ditempatkan di folder yang dapat Anda referensikan.

Tidak ada kerangka kerja ML berat, tidak ada unduhan model besar—hanya model kuantisasi Q4‑K‑M kecil yang muat dengan nyaman pada kebanyakan GPU.

---

## Langkah 1: Inisialisasi Mesin OCR – ekstrak teks dari gambar

Hal pertama yang Anda lakukan adalah membuat instance `OcrEngine` dan memberi tahu bahasa yang diharapkan. Di sini kami memilih Bahasa Inggris dan meminta output plain‑text, yang ideal untuk pemrosesan lanjutan.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Mengapa ini penting:** Menetapkan bahasa mempersempit set karakter, meningkatkan akurasi. Mode plain‑text menghapus informasi tata letak yang biasanya tidak Anda perlukan ketika hanya ingin mengekstrak teks dari gambar.

---

## Langkah 2: Muat gambar untuk OCR – cara OCR gambar

Sekarang kami memberi mesin gambar yang sebenarnya. Helper `Image.load` memahami format umum (PNG, JPEG, TIFF) dan mengabstraksi keanehan file‑IO.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Tip:** Jika gambar sumber Anda berukuran besar, pertimbangkan untuk mengubah ukurannya sebelum mengirim ke mesin; dimensi yang lebih kecil dapat mengurangi penggunaan memori GPU tanpa mengurangi kualitas pengenalan.

---

## Langkah 3: Konfigurasikan Model Aspose AI – mengenali teks dari faktur

Aspose AI dilengkapi dengan model GGUF kecil yang dapat diunduh otomatis. Contoh ini menggunakan repositori `Qwen2.5‑3B‑Instruct‑GGUF`, terkuantisasi menjadi `q4_k_m`. Kami juga memberi tahu runtime untuk mengalokasikan 20 lapisan pada GPU, yang menyeimbangkan kecepatan dan penggunaan VRAM.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Di balik layar:** Model terkuantisasi berukuran sekitar 1,5 GB di disk, hanya sebagian kecil dari model presisi penuh, namun tetap menangkap nuansa linguistik yang cukup untuk menandai kesalahan ejaan OCR yang umum.

---

## Langkah 4: Inisialisasi AsposeAI dan lampirkan post‑processor pemeriksaan ejaan

Aspose AI menyertakan post‑processor pemeriksaan ejaan siap pakai. Dengan melampirkannya, setiap hasil OCR akan dibersihkan secara otomatis.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Mengapa menggunakan post‑processor?** Mesin OCR sering salah membaca “Invoice” menjadi “Invo1ce” atau “Total” menjadi “T0tal”. Pemeriksaan ejaan menjalankan model bahasa ringan pada string mentah dan memperbaiki kesalahan tersebut tanpa Anda menulis kamus khusus.

---

## Langkah 5: Jalankan post‑processor pemeriksaan ejaan pada hasil OCR

Dengan semua terhubung, satu panggilan menghasilkan teks yang telah dikoreksi. Kami juga mencetak versi asli dan versi bersih sehingga Anda dapat melihat perbaikannya.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Output tipikal untuk faktur mungkin terlihat seperti ini:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Perhatikan bagaimana “Invo1ce” berubah menjadi kata yang tepat “Invoice”. Itulah kekuatan pemeriksaan ejaan AI bawaan.

---

## Langkah 6: Lepaskan sumber daya GPU – lepaskan sumber daya GPU dengan aman

Jika Anda menjalankan ini dalam layanan yang berjalan lama (mis., API web yang memproses puluhan faktur per menit), Anda harus membebaskan konteks GPU setelah setiap batch. Jika tidak, Anda akan melihat kebocoran memori dan akhirnya mendapatkan error “CUDA out of memory”.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Tips pro:** Panggil `free_resources()` di dalam blok `finally` atau context manager sehingga selalu dijalankan, bahkan jika terjadi pengecualian.

---

## Contoh Kerja Lengkap

Menggabungkan semua bagian memberikan Anda skrip mandiri yang dapat Anda masukkan ke proyek apa pun.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Simpan file, sesuaikan path ke gambar Anda, dan jalankan `python extract_text_from_image.py`. Anda akan melihat teks faktur yang telah dibersihkan tercetak di konsol.

---

## Pertanyaan yang Sering Diajukan (FAQ)

**Q: Apakah ini bekerja pada mesin hanya CPU?**  
A: Tentu saja. Jika tidak ada GPU yang terdeteksi, Aspose AI beralih ke eksekusi CPU, meskipun akan lebih lambat. Anda dapat memaksa CPU dengan mengatur `model_cfg.gpu_layers = 0`.

**Q: Bagaimana jika faktur saya dalam bahasa selain Bahasa Inggris?**  
A: Ubah `ocr_engine.language` ke nilai enum yang sesuai (mis., `aocr.Language.Spanish`). Model pemeriksaan ejaan bersifat multibahasa, tetapi Anda mungkin mendapatkan hasil yang lebih baik dengan model khusus bahasa.

**Q: Bisakah saya memproses beberapa gambar dalam loop?**  
A: Ya. Pindahkan langkah pemuatan, pengenalan, dan post‑processing ke dalam loop `for`. Ingat untuk memanggil `ocr_ai.free_resources()` setelah loop atau setelah setiap batch jika Anda menggunakan kembali instance AI yang sama.

**Q: Seberapa besar ukuran unduhan model?**  
A: Sekitar 1,5 GB untuk versi terkuantisasi `q4_k_m`. Model ini di‑cache setelah run pertama, sehingga eksekusi selanjutnya menjadi instan.

---

## Kesimpulan

Dalam tutorial ini kami menunjukkan cara **mengekstrak teks dari gambar** menggunakan Aspose OCR, mengonfigurasi model AI kecil, menerapkan post‑processor pemeriksaan ejaan, dan dengan aman **melepaskan sumber daya GPU**. Alur kerja mencakup semua hal mulai dari memuat gambar hingga membersihkan setelah selesai, memberi Anda pipeline yang handal untuk skenario **mengenali teks dari faktur**.

Langkah selanjutnya? Coba ganti pemeriksaan ejaan dengan model ekstraksi entitas khusus

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}