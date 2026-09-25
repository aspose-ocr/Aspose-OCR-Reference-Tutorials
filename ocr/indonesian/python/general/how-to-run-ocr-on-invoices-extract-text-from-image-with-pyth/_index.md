---
category: general
date: 2026-01-07
description: Cara menjalankan OCR dan mengekstrak teks dari gambar untuk pemrosesan
  faktur. Pelajari cara meningkatkan akurasi OCR, memuat gambar untuk OCR, dan memproses
  OCR faktur secara efisien.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: id
og_description: Cara menjalankan OCR pada faktur langkah demi langkah. Ekstrak teks
  dari gambar, tingkatkan akurasi OCR, dan muat gambar untuk OCR menggunakan Aspose
  AI.
og_title: Cara Menjalankan OCR pada Faktur – Panduan Python Lengkap
tags:
- OCR
- Python
- Image Processing
title: Cara Menjalankan OCR pada Faktur – Mengekstrak Teks dari Gambar dengan Python
url: /id/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR pada Faktur – Mengekstrak Teks dari Gambar dengan Python

Pernah bertanya-tanya **bagaimana menjalankan OCR** pada faktur yang dipindai dan mendapatkan teks yang bersih serta dapat dicari? Anda tidak sendirian. Banyak pengembang menemui kendala ketika output OCR mentah dipenuhi dengan kesalahan ejaan, pemisahan baris yang rusak, dan tanda baca yang hilang. Dalam tutorial ini kami akan membahas solusi full‑stack yang tidak hanya **mengekstrak teks dari gambar** tetapi juga **meningkatkan akurasi OCR** dengan post‑processing menggunakan model AI Aspose.

Anda akan melihat cara **memuat gambar untuk OCR**, menjalankan mesin bawaan, dan kemudian menerapkan pemeriksaan ejaan ringan yang membuat hasilnya siap untuk analitik downstream. Pada akhir tutorial, Anda akan memiliki skrip yang dapat digunakan kembali dan dapat dimasukkan ke dalam pipeline pemrosesan faktur apa pun.

> **Apa yang Anda perlukan**  
> * Python 3.9 atau lebih baru  
> * paket `aspose-ocr` dan `aspose-ai` (dipasang via `pip`)  
> * Gambar faktur (PNG, JPEG, atau TIFF) – kami akan menggunakan `sample_invoice.png` sebagai contoh  
> * Opsional: GPU dengan setidaknya 4 GB VRAM untuk inferensi model yang lebih cepat (skrip juga dapat berjalan di CPU)

---

## Langkah 1: Instal Paket yang Diperlukan dan Siapkan Lingkungan

Sebelum kita dapat **memuat gambar untuk OCR**, kita harus memastikan perpustakaan yang diperlukan tersedia. Mesin Aspose OCR dilengkapi dengan pembungkus Python sederhana, sementara post‑processor AI mengandalkan model kuantisasi Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Tip pro:** Jika Anda berencana menggunakan akselerasi GPU, instal `torch` dengan dukungan CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Langkah 2: Muat Gambar Faktur

Memuat gambar sangat sederhana, tetapi penting untuk menyebutkan mengapa kami secara eksplisit menetapkan path sebagai string mentah (`r"..."`). Ini mencegah kesalahan karakter escape yang tidak disengaja pada path Windows.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Mengapa ini penting:* Menggunakan `ocr.Image.load` menjamin gambar dipra‑proses (binarisasi, deskew) sesuai dengan default optimal Aspose, yang sudah **meningkatkan akurasi OCR** sebelum ada intervensi AI.

---

## Langkah 3: Jalankan Mesin OCR Bawaan

Sekarang kita benar‑benar **menjalankan OCR** dan menangkap teks mentah. Langkah ini menunjukkan output tipikal yang Anda dapatkan dari OCR standar—sering kali berantakan dengan pemisahan baris dan kesalahan ejaan sesekali.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Output mentah tipikal** (dipotong untuk singkat):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Anda mungkin memperhatikan bahwa “Invoice” muncul sebagai “Invo1ce” atau tanda baca hilang. Di sinilah post‑processor AI berperan.

---

## Langkah 4: Konfigurasikan Model AI Aspose

Model AI yang akan kami gunakan adalah **Qwen2.5‑3B‑Instruct‑GGUF**, sebuah LLM ringan yang disesuaikan dengan instruksi dan dapat berjalan dengan nyaman pada GPU kelas menengah. Konfigurasi di bawah ini memberi tahu Aspose dari mana mengambil model, berapa banyak lapisan yang disimpan di GPU, dan ukuran konteks untuk menangani paragraf panjang.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Mengapa konfigurasi ini?**  
> * `gpu_layers=30` menyeimbangkan kecepatan dan memori—kebanyakan inferensi terjadi di GPU, sementara lapisan yang tersisa tetap di CPU untuk menghindari error OOM.  
> * `context_size=4096` memastikan model dapat melihat seluruh faktur sekaligus, mencegah pemotongan bidang penting.

---

## Langkah 5: Buat Post‑Processor Pemeriksaan Ejaan Sederhana

Kami akan membungkus panggilan AI dalam fungsi kecil bernama `simple_spell_check`. Prompt dibuat sengaja singkat: “Correct spelling and punctuation:” diikuti oleh teks OCR mentah. Model mengembalikan versi yang telah dibersihkan.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Cara kerjanya:** `ai.run_prompt` mengirim prompt ke LLM yang dimuat secara lokal, yang kemudian mengembalikan satu string dengan ejaan yang diperbaiki, tanda baca yang tepat, dan tata letak pemisahan baris yang lebih alami.

---

## Langkah 6: Terapkan Post‑Processor pada Teks OCR Mentah

Sekarang keajaiban terjadi. Kami memasukkan output OCR mentah ke dalam post‑processor kami dan mencetak hasil yang ditingkatkan.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Contoh output yang ditingkatkan**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Perhatikan ejaan “Invoice” yang telah diperbaiki, penggunaan titik dua yang tepat, dan pemisahan baris yang konsisten—tepat apa yang Anda butuhkan untuk parsing downstream yang dapat diandalkan.

---

## Langkah 7: Bersihkan Sumber Daya

Baik mesin OCR maupun model AI mengalokasikan sumber daya native. Sebaiknya membebaskan sumber daya tersebut saat selesai, terutama pada layanan yang berjalan lama.

```python
ai.free_resources()
engine.dispose()
```

---

## Skrip Lengkap – Siap Disisipkan

Berikut adalah skrip lengkap yang dapat dijalankan yang menggabungkan setiap langkah. Simpan sebagai `invoice_ocr.py`, ganti `YOUR_DIRECTORY` dengan folder yang berisi gambar faktur Anda, dan jalankan dengan `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Jalankan skrip dan Anda akan melihat dump OCR mentah yang berisik serta versi yang dipoles dengan **akurasi OCR yang ditingkatkan** berdampingan.

---

## Pertanyaan yang Sering Diajukan & Kasus Tepi

### 1. Bagaimana jika gambar faktur saya berupa PDF multi‑halaman?

Aspose OCR dapat langsung memuat halaman PDF. Ganti baris pemuatan gambar dengan:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Iterasikan `page_index` untuk memproses setiap halaman secara berurutan.

### 2. GPU saya kehabisan memori—apakah saya bisa hanya menggunakan CPU?

Tentu saja. Setel `gpu_layers=0` dalam `AsposeAIModelConfig`. Model akan berjalan sepenuhnya di CPU, yang lebih lambat tetapi aman untuk perangkat keras kelas rendah.

### 3. Bagaimana saya menangani faktur non‑Inggris?

Ganti ID repositori model dengan model khusus bahasa, misalnya `"mistralai/Mistral-7B-Instruct-v0.2"` untuk dukungan multibahasa. Sisanya dari pipeline tetap tidak berubah.

### 4. Bisakah saya menautkan beberapa post‑processor (misalnya, format tanggal, ekstrak total)?

Ya. `ai.set_post_processor` menerima daftar callable. Contohnya:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

---

## Tips Kinerja & Praktik Terbaik

| Tip | Mengapa membantu |
|-----|-------------------|
| **Batch multiple invoices** – load them into a list and process in a loop. | Mengurangi overhead interpreter Python dan menjaga model AI tetap hangat di memori. |
| **Cache the model** – avoid calling `initialize` repeatedly in a web service. | Memuat model dapat memakan ~30 detik; caching memberikan respons instan. |
| **Resize large images** to 1500 px width before OCR. | Gambar yang lebih kecil mempercepat OCR dan inferensi AI tanpa mengorbankan akurasi. |
| **Set `allow_auto_download="false"` in production** – ship the model with your deployment. | Menjamin waktu startup yang deterministik dan menghindari gangguan jaringan. |

---

## Kesimpulan

Kami telah membahas **cara menjalankan OCR** pada faktur, mulai dari memuat gambar hingga memoles hasil dengan pemeriksaan ejaan berbasis AI. Dengan mengikuti langkah‑langkah ini Anda dapat secara andal **mengekstrak teks dari gambar**, **meningkatkan akurasi OCR**, dan dengan mulus **memproses OCR faktur** dalam alur kerja berbasis Python apa pun.

Cobalah dengan beberapa tata letak faktur yang berbeda—mungkin tanda terima tulisan tangan atau kontrak yang dipindai. Pipeline yang sama dapat beradaptasi dengan sedikit penyesuaian, membuktikan bahwa kombinasi OCR + AI yang terstruktur dengan baik adalah alat serbaguna untuk proyek otomasi dokumen apa pun.

Jika Anda menemukan panduan ini berguna, pertimbangkan untuk membagikannya dengan rekan tim atau memberi bintang pada repositori yang menyimpan paket Aspose

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}