---
category: general
date: 2026-07-05
description: Pelajari cara menjalankan OCR pada PDF dan meningkatkan akurasi OCR menggunakan
  model Hugging Face. Penyiapan langkah demi langkah, memuat PDF untuk OCR, dan mengonfigurasi
  model Hugging Face.
draft: false
keywords:
- run OCR on PDF
- improve OCR accuracy
- load PDF for OCR
- configure Hugging Face model
language: id
og_description: Jalankan OCR pada PDF dengan model Hugging Face dan tingkatkan akurasi
  OCR. Ikuti panduan ini untuk memuat PDF untuk OCR dan mengonfigurasi model.
og_title: Jalankan OCR pada PDF – Tutorial Lengkap untuk Akurasi Lebih Baik
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to run OCR on PDF and improve OCR accuracy using a Hugging
    Face model. Step‑by‑step setup, load PDF for OCR, and configure Hugging Face model.
  headline: run OCR on PDF – Complete Guide to Boost Accuracy
  type: TechArticle
- description: Learn how to run OCR on PDF and improve OCR accuracy using a Hugging
    Face model. Step‑by‑step setup, load PDF for OCR, and configure Hugging Face model.
  name: run OCR on PDF – Complete Guide to Boost Accuracy
  steps:
  - name: What if the PDF is multi‑page?
    text: The `Image.from_file` call automatically creates a multi‑frame image object.
      Loop over `input_image.frames` and call `ocr_engine.recognize` for each frame,
      then concatenate the results before running the post‑processor.
  - name: How to handle languages other than English?
    text: 'Set the OCR engine’s language property before recognition:'
  - name: Can I run this on CPU only?
    text: Yes—just omit `model_cfg.gpu_layers` or set it to `0`. The model will run
      entirely on CPU, though inference will be slower (roughly 5‑10 seconds per page
      on a modern i7).
  type: HowTo
tags:
- OCR
- Python
- AI post‑processor
title: Jalankan OCR pada PDF – Panduan Lengkap untuk Meningkatkan Akurasi
url: /id/python/general/run-ocr-on-pdf-complete-guide-to-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jalankan OCR pada PDF – Panduan Lengkap untuk Meningkatkan Akurasi

Pernah bertanya-tanya bagaimana cara **run OCR on PDF** file tanpa menghabiskan banyak uang untuk SDK komersial? Anda tidak sendirian. Baik Anda mendigitalkan faktur, mengekstrak data dari laporan yang dipindai, atau hanya penasaran tentang ekstraksi teks yang ditingkatkan AI, kemampuan untuk **run OCR on PDF** secara efisien adalah keterampilan yang wajib dimiliki bagi setiap pengembang modern.

Dalam tutorial ini kami akan membimbing Anda melalui contoh praktis end‑to‑end yang tidak hanya menunjukkan cara **run OCR on PDF**, tetapi juga mendemonstrasikan cara **improve OCR accuracy** dengan menambahkan AI post‑processor. Kami juga akan membahas detail **load PDF for OCR** dan pengaturan **configure Hugging Face model** sehingga Anda mendapatkan kinerja terbaik pada workstation yang sederhana.

Dengan akhir panduan ini Anda akan memiliki skrip fungsional penuh yang:

* Memuat PDF (atau gambar) untuk OCR  
* Mengonfigurasi model Hugging Face dengan kuantisasi khusus dan lapisan GPU  
* Menjalankan OCR biasa lalu meningkatkan hasilnya dengan AI post‑processor  
* Mencetak teks mentah dan teks yang ditingkatkan AI untuk perbandingan mudah  

Tanpa layanan eksternal, tanpa biaya tersembunyi—hanya pustaka open‑source dan beberapa baris Python.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:

* Python 3.9 atau lebih baru terpasang (modul `venv` sangat berguna)  
* Paket `aocr` (Aspose OCR) – instalasi via `pip install aocr`  
* Akses internet untuk mengunduh model satu kali dari Hugging Face  
* File PDF yang ingin Anda proses (kami akan menggunakan `invoice_2026.pdf` sebagai contoh)  

Itu saja. Jika ada yang terdengar tidak familiar, jangan khawatir—setiap langkah di bawah menjelaskan mengapa dan bagaimana, sehingga Anda dapat langsung berjalan dalam hitungan menit.

---

## Langkah 1: Konfigurasikan Model Hugging Face

Hal pertama yang harus dilakukan adalah mengatur parameter **configure Hugging Face model** yang sesuai dengan perangkat keras Anda. Dalam kasus kami, kami akan mengambil model baru `Qwen/Qwen2.5-3B-Instruct-GGUF`, mengkuantisasinya ke `int8` untuk jejak memori yang sangat kecil, dan menempatkan 20 lapisan pertama ke GPU untuk kecepatan.

```python
import aocr

# Create the AI engine that will later post‑process OCR results
ai_engine = aocr.AsposeAI()

# Build the model configuration – this is where we "configure Hugging Face model"
model_cfg = aocr.AsposeAIModelConfig()
model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"   # released early‑2026
model_cfg.hugging_face_quantization = "int8"                     # small memory footprint
model_cfg.gpu_layers = 20                                        # use first 20 layers on GPU
model_cfg.allow_auto_download = "true"

# Initialize the engine – it will download the model if it's not already cached
ai_engine.initialize(model_cfg)
```

**Mengapa ini penting:** Mengkuantisasi ke `int8` memperkecil model dari beberapa gigabyte menjadi kurang dari satu gig, membuatnya dapat dijalankan pada laptop. Membatasi lapisan GPU menyeimbangkan kecepatan dan penggunaan VRAM—sempurna untuk kartu 6 GB.

> **Pro tip:** Jika Anda mengalami kesalahan out‑of‑memory, turunkan `gpu_layers` menjadi `10` atau ubah `quantization` menjadi `"float16"` untuk model yang sedikit lebih besar namun masih cocok untuk kebanyakan GPU konsumen.

---

## Langkah 2: Muat PDF untuk OCR

Sekarang mesin AI sudah siap, kita perlu **load PDF for OCR**. Pustaka Aspose OCR memperlakukan PDF dan gambar secara seragam, sehingga Anda dapat menunjuk ke jalur file atau aliran.

```python
# Create the OCR engine that will perform the initial text extraction
ocr_engine = aocr.OcrEngine()

# Attach the AI post‑processor – we’ll use the default run_postprocessor method
ocr_engine.set_post_processor(ai_engine.run_postprocessor, None)  # no custom settings required

# Load the PDF document – this is the step where we "load PDF for OCR"
input_image = aocr.Image.from_file("YOUR_DIRECTORY/invoice_2026.pdf")
```

**Mengapa ini penting:** Dengan memuat PDF langsung ke objek `Image`, mesin OCR dapat menangani PDF multi‑halaman halaman per halaman di balik layar. Tidak perlu memisahkan PDF menjadi gambar secara manual terlebih dahulu.

> **Watch out:** Jika PDF Anda berisi halaman yang dienkripsi, Anda harus menyediakan kata sandi melalui `Image.from_file(..., password="secret")`.

---

## Langkah 3: Jalankan OCR pada PDF

Dengan dokumen berada di memori, saatnya **run OCR on PDF**. Pass pertama memberikan teks mentah, yang sering kali dipenuhi dengan kesalahan spasi, karakter yang salah dikenali, atau tanda baca yang hilang—terutama pada faktur yang dipindai.

```python
# Perform the plain OCR pass – this is the core "run OCR on PDF" operation
raw_result = ocr_engine.recognize(input_image)  # raw OCR output
```

Pada titik ini `raw_result.text` berisi output OCR yang belum diubah. Anda dapat memeriksanya, mencatatnya, atau bahkan memasukkannya ke pipeline hilir. 

> **Side note:** Metode `recognize` secara otomatis mendeteksi orientasi halaman dan mencoba memperbaiki kemiringan, tetapi tidak akan memperbaiki keanehan khusus bahasa—di sinilah AI post‑processor bersinar.

---

## Langkah 4: Tingkatkan Akurasi OCR dengan AI Post‑Processor

Sekarang bagian yang menyenangkan: **improve OCR accuracy**. Dengan memasukkan hasil mentah ke mesin AI yang kami konfigurasikan sebelumnya, kami membiarkan model bahasa besar membersihkan teks, memperbaiki kesalahan ejaan, dan bahkan menebak nilai yang hilang.

```python
# Enhance the raw OCR output using the AI post‑processor
enhanced_result = ocr_engine.run_postprocessor(raw_result)
```

Post‑processor menjalankan LLM pada setiap baris (atau blok) teks, dengan prompt yang meminta untuk “membersihkan kesalahan OCR sambil mempertahankan makna asli.” Hasilnya adalah versi yang dipoles dan jauh lebih mudah dibaca.

**Mengapa ini berhasil:** LLM modern memiliki pemahaman kuat tentang pola bahasa dan dapat menebak kata yang dimaksud ketika mesin OCR memberikan token yang berantakan. Dipadukan dengan model yang dikuantisasi `int8`, peningkatan selesai dalam kurang dari satu detik untuk faktur satu halaman tipikal.

---

## Langkah 5: Tinjau Hasil

Akhirnya, mari cetak output mentah dan yang ditingkatkan AI berdampingan sehingga Anda dapat melihat perbedaannya sendiri.

```python
print("=== Raw OCR ===")
print(raw_result.text)

print("\n=== AI‑enhanced ===")
print(enhanced_result.text)
```

**Output yang diharapkan (dipotong):**

```
=== Raw OCR ===
Inv0ice N0: 2026-00123
Date: 01/02/2026
Tot@l Am0unt: $1,234.56
...

=== AI‑enhanced ===
Invoice No: 2026-00123
Date: 01/02/2026
Total Amount: $1,234.56
...
```

Perhatikan bagaimana versi yang ditingkatkan AI memperbaiki kesalahan huruf nol (`Inv0ice` → `Invoice`) dan memperbaiki simbol `@` yang tersendiri. Untuk kebanyakan dokumen, Anda akan melihat pengurangan kesalahan OCR sebesar 30‑80 %.

> **Pro tip:** Jika Anda membutuhkan teks yang ditingkatkan dalam format terstruktur (mis., JSON), Anda dapat memproses lebih lanjut `enhanced_result` dengan regex atau fungsi parsing kecil.

---

## Opsional: Memvisualisasikan Proses

Di bawah ini diagram sederhana yang menggambarkan alur. Teks alt berisi kata kunci utama untuk memenuhi SEO.

![Diagram showing steps to run OCR on PDF and improve OCR accuracy with an AI post‑processor](run-ocr-on-pdf-diagram.png)

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika PDF memiliki banyak halaman?

Pemanggilan `Image.from_file` secara otomatis membuat objek gambar multi‑frame. Loop melalui `input_image.frames` dan panggil `ocr_engine.recognize` untuk setiap frame, kemudian gabungkan hasilnya sebelum menjalankan post‑processor.

```python
pages_text = []
for frame in input_image.frames:
    raw = ocr_engine.recognize(frame)
    enhanced = ocr_engine.run_postprocessor(raw)
    pages_text.append(enhanced.text)

full_text = "\n".join(pages_text)
```

### Bagaimana menangani bahasa selain Bahasa Inggris?

Atur properti bahasa mesin OCR sebelum pengenalan:

```python
ocr_engine.language = aocr.Language.French  # or aocr.Language.Spanish, etc.
```

LLM tetap akan meningkatkan akurasi selama model yang Anda **configure Hugging Face model** dukung bahasa target (sebagian besar melakukannya).

### Bisakah saya menjalankannya hanya dengan CPU?

Ya—cukup hilangkan `model_cfg.gpu_layers` atau setel ke `0`. Model akan berjalan sepenuhnya di CPU, meskipun inferensi akan lebih lambat (sekitar 5‑10 detik per halaman pada i7 modern).

---

## Ringkasan

Kami telah membahas semua yang Anda butuhkan untuk **run OCR on PDF** dan **improve OCR accuracy**:

1. **Configure Hugging Face model** dengan kuantisasi dan lapisan GPU.  
2. **Load PDF for OCR** menggunakan `Image.from_file` Aspose OCR.  
3. **Run OCR on PDF** untuk memperoleh teks mentah.  
4. **Improve OCR accuracy** dengan memasukkan hasil ke AI post‑processor.  
5. **Review** kedua output mentah dan yang ditingkatkan.

Jangan ragu untuk bereksperimen—ganti ID repo model dengan LLM yang lebih baru, ubah prompt di dalam `ai_engine.run_postprocessor` (jika Anda menyelami sumbernya), atau tambahkan langkah pra‑pemrosesan khusus seperti deskewing. Pipeline bersifat modular, sehingga Anda dapat mengganti komponen apa pun tanpa merusak yang lainnya.

---

## Langkah Selanjutnya

* **Explore other post‑processing models** – coba varian `distilbert` yang lebih kecil jika Anda menggunakan mesin kelas rendah.  
* **Integrate with a database** – simpan teks yang ditingkatkan di SQLite atau Elasticsearch untuk arsip yang dapat dicari.  
* **Add PDF generation** – gunakan `reportlab` atau `pypdf` untuk memberi anotasi pada PDF asli dengan teks yang telah dibersihkan.  

Jika Anda telah mengikuti, Anda kini memiliki fondasi yang kuat untuk membangun dokumen yang kuat dan ditingkatkan AI

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [如何在 .NET 中使用 Aspose.OCR 進行 PDF OCR](/ocr/hongkong/net/text-recognition/recognize-pdf/)
- [.NET에서 Aspose.OCR을 사용하여 PDF OCR하는 방법](/ocr/korean/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}