---
category: general
date: 2026-03-18
description: Tutorial OCR dasar Python menunjukkan cara mengonversi TIFF menjadi teks,
  memuat OCR gambar, mengatur lapisan GPU, dan memperbaiki angka nol di depan dengan
  Aspose AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: id
og_description: Tutorial OCR Python dasar memandu Anda melalui konversi file TIFF
  menjadi teks bersih, memuat gambar, mengatur lapisan GPU, dan memperbaiki nol di
  depan.
og_title: OCR dasar Python – mengonversi TIFF ke teks
tags:
- OCR
- Python
- AI
- Aspose
title: OCR dasar Python – mengonversi TIFF ke teks
url: /id/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Mengonversi TIFF ke Teks dengan AI Post‑Processing

Mencari cara untuk melakukan **basic ocr python** pada dokumen hasil pemindaian Anda? Pada panduan ini kami akan menjelaskan cara mengonversi file TIFF menjadi teks bersih yang dapat dicari menggunakan Aspose OCR dan post‑processor AI.  

Jika Anda pernah mengalami kesulitan **mengonversi TIFF ke teks** karena output mentah penuh dengan typo atau simbol aneh, Anda tidak sendirian. Kami juga akan menunjukkan cara **memuat image OCR**, menyesuaikan mesin untuk **set GPU layers**, dan bahkan **memperbaiki leading zeroes** yang sering muncul pada nomor faktur.

## Apa yang Akan Anda Pelajari

- Cara menginisialisasi mesin Aspose OCR untuk dokumen tercetak.  
- Langkah‑langkah tepat untuk **memuat image OCR** dari file TIFF dan mendapatkan teks mentah.  
- Mengonfigurasi model AI, mengunduhnya secara otomatis, dan **menyetel GPU layers** untuk inferensi yang lebih cepat.  
- Menambahkan pemeriksaan ejaan bawaan serta fungsi khusus yang **memperbaiki leading zeroes**.  
- Membersihkan hasil OCR dan melepaskan sumber daya dengan benar.  

Pada akhir tutorial ini Anda akan memiliki satu skrip Python yang dapat digunakan kembali untuk mengubah TIFF apa pun menjadi teks yang rapi dan dapat dicari—tanpa perlu menyalin‑tempel secara manual.  

### Prasyarat

- Python 3.8+ terpasang di mesin Anda.  
- Paket `aspose-ocr` (`pip install aspose-ocr`).  
- Opsional: GPU dengan setidaknya 4 GB VRAM jika Anda ingin **set GPU layers**; jika tidak, kode akan otomatis beralih ke CPU.  

---

## basic ocr python – memuat gambar dan mengenali teks

Hal pertama yang perlu kita lakukan adalah **memuat image OCR** sehingga mesin dapat membaca pikselnya. `OcrEngine` milik Aspose menangani banyak format, tetapi di sini kita fokus pada TIFF karena paling umum untuk faktur yang dipindai.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** Jika Anda menangani TIFF multi‑halaman, Aspose secara otomatis memproses setiap halaman secara berurutan, jadi Anda tidak memerlukan loop tambahan.

Setelah gambar dimuat, mari jalankan proses pengenalan dasar.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Anda akan melihat sesuatu seperti:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Perhatikan *zeroes* sebelum huruf? Itu adalah artefak OCR klasik yang akan kami bersihkan nanti.

![alur kerja basic ocr python](/images/ocr-workflow.png "diagram alur kerja basic ocr python")

---

## Langkah 2: Mengonversi TIFF ke teks – menyiapkan AI post‑processor

OCR mentah berguna, tetapi kebanyakan pipeline produksi memerlukan versi yang dipoles. Aspose menyediakan wrapper `AsposeAI` yang dapat mengunduh model dari Hugging Face, menjalankannya di GPU, dan menerapkan pemeriksaan ejaan secara otomatis.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Mengapa `set GPU layers` penting

Parameter `gpu_layers` memberi tahu model GGUF di bawahnya berapa banyak lapisan transformer yang harus dipertahankan di GPU. Lebih banyak lapisan = inferensi lebih cepat tetapi penggunaan VRAM lebih tinggi. Jika Anda menggunakan laptop dengan spesifikasi sedang, turunkan nilainya menjadi `10` atau hapus sama sekali untuk tetap menggunakan CPU.

---

## Langkah 3: Terapkan spellcheck dan **perbaiki leading zeroes**

Aspose AI dilengkapi dengan pemeriksa ejaan bawaan, yang menangkap sebagian besar kesalahan ejaan bahasa Inggris. Namun, perbaikan khusus domain—seperti mengubah `0` di depan menjadi `O` untuk kode faktur—memerlukan post‑processor khusus.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Mengapa ini berhasil:** Ekspresi reguler mencari batas kata (`\b`), sebuah nol, lalu tepat tiga huruf kapital. Kemudian mengganti nol tersebut dengan huruf “O”. Anda dapat memperluas pola untuk keanehan lain (misalnya, `0[0-9]{2}` untuk angka yang terbaca salah).

---

## Langkah 4: Bersihkan hasil OCR dengan AI post‑processor

Sekarang kita gabungkan semuanya: string mentah dari **basic ocr python**, pemeriksaan ejaan, dan perbaikan nol. Metode `run_postprocessor` mengembalikan versi yang telah dibersihkan dan siap untuk sistem hilir.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Output tipikal setelah post‑processor:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Anda dapat melihat bahwa leading zero telah berubah menjadi `O`, dan kesalahan ejaan umum telah diperbaiki. Teks kini cocok untuk diindeks dalam mesin pencari atau dimasukkan ke pipeline ekstraksi data.

---

## Langkah 5: Lepaskan sumber daya AI – jaga GPU Anda tetap bahagia

Jika Anda menjalankan banyak pekerjaan OCR dalam layanan yang berjalan lama, sebaiknya bebaskan memori GPU model saat selesai.

```python
ocr_ai.free_resources()
```

Melewatkan langkah ini dapat menyebabkan error “out‑of‑memory” pada pemanggilan berikutnya, terutama ketika **set GPU layers** diatur ke nilai tinggi.

---

## Variasi Opsional & Kasus Tepi

| Situasi | Apa yang perlu diubah |
|-----------|----------------|
| **Dokumen tulisan tangan** | Gunakan `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` alih‑alih `PRINTED`. |
| **Tidak ada GPU** | Set `gpu_layers=0` atau hapus argumen; model akan berjalan di CPU (lebih lambat tetapi aman). |
| **Bahasa berbeda** | Ganti ID repo Hugging Face ke model spesifik bahasa, misalnya `microsoft/Florence-2-base`. |
| **Pemrosesan batch** | Bungkus langkah‑langkah dalam loop `for file in glob("*.tif"):` dan akumulasi hasil dalam list atau CSV. |
| **Pola nol yang lebih kompleks** | Perluas `invoice_fix` dengan regex tambahan, seperti `r"\b0+([A-Z]{2,})\b"` untuk beberapa nol di depan. |

---

## Kesimpulan

Kami baru saja menyelesaikan pipeline **basic ocr python** yang memuat TIFF, mengekstrak teks mentah, lalu membersihkannya menggunakan model AI sambil **set GPU layers** untuk kinerja. Post‑processor khusus menunjukkan cara **memperbaiki leading zeroes**, detail kecil yang sering terlewat namun dapat merusak analitik hilir.

Silakan bereksperimen: coba kuantisasi berbeda (`float16` untuk akurasi lebih tinggi), ganti pemeriksaan ejaan dengan kamus khusus domain, atau rangkaian beberapa perbaikan khusus sekaligus. Polanya tetap sama—load, recognize, configure AI, post‑process, dan clean up.

**Langkah selanjutnya** yang dapat Anda jelajahi meliputi:

- Mengintegrasikan output yang telah dibersihkan dengan basis data atau indeks Elasticsearch.  
- Menggunakan pendekatan yang sama untuk **mengonversi TIFF ke teks** pada PDF multi‑bahasa.  
- Menambahkan UI dengan Flask atau FastAPI sehingga pengguna non‑teknis dapat mengunggah file dan menerima teks bersih secara instan.  

Selamat coding, semoga hasil OCR Anda selalu tajam dan bebas nol!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}