---
category: general
date: 2026-01-12
description: Cara menjalankan OCR pada PDF menggunakan Aspose OCR, memuat OCR PDF,
  mengaktifkan mode OCR tulisan tangan, dan mengintegrasikan model OCR Hugging Face
  untuk pemrosesan lanjutan.
draft: false
keywords:
- how to run OCR
- load pdf OCR
- handwritten OCR mode
- hugging face OCR model
language: id
og_description: Cara menjalankan OCR pada PDF dengan Aspose OCR, mengaktifkan mode
  OCR tulisan tangan, dan meningkatkan akurasi menggunakan model OCR Hugging Face.
og_title: Cara Menjalankan OCR pada PDF – Tutorial Lengkap
tags:
- OCR
- Python
- Aspose
- Hugging Face
title: Cara Menjalankan OCR pada PDF – Panduan Langkah-demi-Langkah dengan Mode Tulis
  Tangan
url: /id/python/general/how-to-run-ocr-on-pdfs-step-by-step-guide-with-handwritten-m/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR pada PDF – Tutorial Lengkap

Pernah bertanya-tanya **bagaimana cara menjalankan OCR** pada PDF multi‑bahasa yang berisi tulisan tangan berantakan? Anda tidak sendirian. Dalam banyak proyek dunia nyata—misalnya digitalisasi faktur atau pengarsipan surat‑surat bersejarah—ekstraksi teks biasa tidak cukup. Panduan ini menunjukkan secara tepat cara menjalankan OCR pada PDF, memuat PDF OCR, beralih ke mode OCR tulisan tangan, dan kemudian memoles hasilnya dengan **model OCR Hugging Face** untuk perbaikan ejaan dan tata bahasa.

Kami akan membahas semua yang Anda perlukan: mulai dari menginstal Aspose OCR Cloud SDK, mengonfigurasi percepatan GPU, hingga menghubungkan model Qwen ringan dari Hugging Face. Pada akhir tutorial, Anda akan memiliki skrip siap‑jalankan yang dapat Anda masukkan ke dalam proyek Python apa pun.

> **Prasyarat**  
> • Python 3.9 atau lebih baru  
> • Lisensi Aspose OCR Cloud (diatur sebagai variabel lingkungan)  
> • Opsional: GPU yang kompatibel dengan CUDA untuk inferensi yang lebih cepat  

## Apa yang Dibahas dalam Tutorial Ini

- Mengaktifkan lisensi Aspose OCR dari lingkungan  
- Memuat PDF dengan `load_pdf OCR` dan mengaktifkan **mode OCR tulisan tangan**  
- Menjalankan OCR terstruktur untuk mendapatkan teks tingkat blok dan data bahasa  
- Menyiapkan **model OCR Hugging Face** (Qwen 2.5‑3B‑Instruct) untuk pemrosesan lanjutan  
- Menerapkan pemeriksaan ejaan dan koreksi tata bahasa blok per blok  
- Membersihkan sumber daya AI untuk menghindari kebocoran memori  

Jika Anda pernah mencoba mesin OCR standar dan mendapatkan teks tak terbaca pada catatan tulisan tangan, flag “handwritten OCR mode” adalah pengubah permainan yang Anda lewatkan. Dan berkat model Hugging Face, Anda juga akan mendapatkan penyempurnaan kelas profesional tanpa meninggalkan lingkungan Python Anda.

![diagram alur cara menjalankan OCR](https://example.com/ocr-workflow.png "cara menjalankan OCR")

*Image alt text: diagram alur cara menjalankan OCR*

## Langkah 1: Instal Paket yang Diperlukan

Pertama, pastikan Aspose OCR Cloud SDK dan pustaka `transformers` telah terinstal. Jalankan perintah berikut di terminal Anda:

```bash
pip install aspose-ocr-cloud transformers huggingface-hub
```

> **Pro tip:** Jika Anda berencana menggunakan percepatan GPU, juga instal `torch` dengan dukungan CUDA (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`).

## Langkah 2: Aktifkan Lisensi Aspose OCR

Mengaktifkan lisensi dari variabel lingkungan menjaga kunci Anda tetap di luar kontrol sumber. Atur `ASPOSE_OCR_LICENSE` di shell Anda, lalu panggil `activate_from_env()`:

```python
import asposeocrcloud as ocr

# Pull the license string from the ASPOSE_OCR_LICENSE environment variable
ocr.activate_from_env()
```

> Mengapa ini penting: Tanpa lisensi yang valid SDK akan beralih ke mode percobaan yang membatasi jumlah halaman dan menonaktifkan penggunaan GPU.

## Langkah 3: Inisialisasi Mesin OCR dalam Mode Tulisan Tangan

Kami membuat sebuah `OcrEngine`, mengaktifkan GPU (jika tersedia), dan secara eksplisit meminta **mode OCR tulisan tangan**. Mode ini menyesuaikan jaringan saraf yang mendasarinya agar lebih baik menangani goresan kursif.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Enable GPU acceleration – optional but speeds up large PDFs dramatically
ocr_engine.set_use_gpu(True)

# Switch to handwritten recognition mode for better accuracy on cursive text
ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)
```

> **Catatan:** Jika Anda tidak memiliki GPU, `set_use_gpu(False)` tetap berfungsi; mesin akan beralih ke CPU.

## Langkah 4: Muat PDF Anda dan Jalankan OCR Terstruktur

Sekarang kami benar‑benarnya **memuat PDF OCR**. Metode `load_image` menerima PDF, TIFF, JPG, dll. OCR terstruktur mengembalikan blok‑blok yang berisi teks mentah serta bahasa yang terdeteksi.

```python
# Replace the path with your own PDF location
pdf_path = "YOUR_DIRECTORY/multilingual_handwritten.pdf"
ocr_engine.load_image(pdf_path)

# Perform structured OCR – returns a hierarchy of blocks
structured_result = ocr_engine.recognize_structured()
```

Daftar `structured_result.blocks` mungkin terlihat seperti ini (dipotong untuk singkat):

```python
[
    Block(text="Bonjour le monde", language="fr"),
    Block(text="Hello world", language="en"),
    Block(text="こんにちは世界", language="ja")
]
```

## Langkah 5: Konfigurasikan Model OCR Hugging Face untuk Pemrosesan Lanjutan

Kami akan menggunakan model **Qwen 2.5‑3B‑Instruct** dari Hugging Face, yang di‑quantize ke `int8` untuk jejak memori yang kecil. Pembungkus `AsposeAIModelConfig` memberi tahu post‑processor AI Aspose cara mengunduh dan menjalankan model.

```python
from asposeocrcloud import AsposeAI, AsposeAIModelConfig

model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25,                # Number of transformer layers to keep on GPU
    allow_auto_download="true"   # Auto‑download the model if not cached
)

spell_corrector = AsposeAI()
spell_corrector.set_post_processor("spell_corrector", model_cfg)
```

> **Mengapa model ini?** Qwen 2.5‑3B‑Instruct menyeimbangkan kecepatan dan kualitas. Kuantisasi `int8` mengurangi penggunaan RAM menjadi ~4 GB, membuatnya dapat dijalankan pada kebanyakan laptop modern.

## Langkah 6: Terapkan Pemeriksaan Ejaan Blok per Blok

Kami mengulangi setiap blok OCR, menyerahkannya ke post‑processor AI, dan mencetak teks yang telah diperbaiki bersama bahasa yang terdeteksi. Inilah inti dari pipeline **load PDF OCR → post‑process**.

```python
for block in structured_result.blocks:
    # Run the correction; `run_postprocessor` returns an object with a .text attribute
    corrected = spell_corrector.run_postprocessor(block)
    print(f"[{block.language}] {corrected.text}")
```

### Output yang Diharapkan

```
[fr] Bonjour le monde
[en] Hello world
[ja] こんにちは世界
```

Jika OCR asli memiliki kesalahan ejaan seperti “Helllo wrold”, model akan menghasilkan versi yang telah diperbaiki.

## Langkah 7: Bersihkan Sumber Daya AI

Selalu bebaskan memori GPU setelah selesai. Pemanggilan `free_resources()` membongkar model dan membersihkan cache CUDA.

```python
spell_corrector.free_resources()
```

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Gejala | Solusi |
|-------|----------|-----|
| **GPU tidak terdeteksi** | `set_use_gpu(True)` diam-diam beralih ke CPU | Verifikasi driver CUDA (`nvidia-smi`) dan instal wheel `torch` yang tepat |
| **Pengunduhan model gagal** | `allow_auto_download` menghasilkan error jaringan | Pastikan HTTPS keluar diizinkan, atau unduh manual file GGUF dan arahkan `hugging_face_repo_id` ke path lokal |
| **Teks tulisan tangan masih berantakan** | Skor kepercayaan rendah pada `structured_result` | Tingkatkan `set_recognition_mode` menjadi `HANDWRITTEN` (sudah dilakukan) dan pertimbangkan pra‑pemrosesan PDF dengan penajaman gambar (`opencv`) sebelum OCR |
| **Kehabisan memori pada GPU** | `RuntimeError: CUDA out of memory` | Kurangi `gpu_layers` (misalnya, menjadi 10) atau beralih ke inferensi CPU (`set_use_gpu(False)`) |

## Memperluas Alur Kerja

- **Pemrosesan batch:** Bungkus seluruh skrip dalam sebuah fungsi yang menerima daftar path PDF dan menulis output yang telah diperbaiki ke file `.txt` terpisah.  
- **Kosakata khusus:** Jika domain Anda menggunakan istilah khusus (misalnya akronim medis), lakukan fine‑tuning pada model Hugging Face dengan dataset kecil.  
- **Model alternatif:** Ganti `Qwen/Qwen2.5-3B-Instruct-GGUF` dengan `mistralai/Mistral-7B-Instruct-v0.2` jika Anda memerlukan jendela konteks yang lebih besar.

## Kesimpulan

Anda kini tahu **bagaimana cara menjalankan OCR** pada PDF, memuat PDF OCR, mengaktifkan **mode OCR tulisan tangan**, dan meningkatkan akurasi dengan **model OCR Hugging Face**. Skrip lengkap—aktivasi lisensi, mesin yang diaktifkan GPU, OCR terstruktur, pemrosesan lanjutan AI, dan pembersihan—menutupi setiap langkah yang biasanya ditanyakan pengembang, mulai dari “bagaimana jika saya tidak memiliki GPU?” hingga “bagaimana cara membebaskan sumber daya?”.

Cobalah dengan dokumen Anda sendiri, eksperimen dengan model yang berbeda, atau integrasikan pipeline ke dalam layanan pemrosesan dokumen yang lebih besar. Langit adalah batasnya setelah Anda menguasai kombinasi Aspose OCR dan AI Hugging Face ini.

**Langkah Selanjutnya**

- Coba alur kerja yang sama pada gambar yang dipindai (`.png`, `.jpg`) untuk melihat bagaimana mesin beradaptasi.  
- Jelajahi fitur **analisis tata letak** Aspose OCR untuk ekstraksi tabel.  
- Selami lebih dalam teknik kuantisasi Hugging Face untuk memperkecil ukuran model lebih jauh.

Selamat bereksperimen dengan OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}