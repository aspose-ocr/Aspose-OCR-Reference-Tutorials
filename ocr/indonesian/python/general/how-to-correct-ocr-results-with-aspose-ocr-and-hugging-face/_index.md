---
category: general
date: 2026-01-07
description: Cara memperbaiki output OCR dan menjalankan OCR pada gambar menggunakan
  Aspose OCR, kemudian menggunakan model Hugging Face untuk memperbaiki kesalahan.
  Pelajari cara mengenali teks dan memuat gambar untuk OCR.
draft: false
keywords:
- how to correct ocr
- how to recognize text
- use hugging face model
- run ocr on image
- load image for ocr
language: id
og_description: Cara memperbaiki output OCR di Python menggunakan Aspose OCR dan model
  Hugging Face. Panduan langkah demi langkah yang mencakup cara mengenali teks, menjalankan
  OCR pada gambar, dan memuat gambar untuk OCR.
og_title: Cara Memperbaiki Hasil OCR – Tutorial Lengkap Aspose & Hugging Face
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Cara Mengoreksi Hasil OCR dengan Aspose OCR dan Hugging Face – Panduan Langkah
  demi Langkah
url: /id/python/general/how-to-correct-ocr-results-with-aspose-ocr-and-hugging-face/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengoreksi Hasil OCR dengan Aspose OCR dan Hugging Face – Panduan Langkah‑per‑Langkah

Pernah bertanya‑tanya **bagaimana cara mengoreksi OCR** yang hasilnya masih terlihat seperti coretan setelah proses pertama? Anda bukan satu‑satunya. Catatan tulisan tangan, pemindaian dengan kontras rendah, atau foto ponsel murah sering membuat mesin OCR menebak‑tebak, dan hasil mentahnya bisa penuh dengan kesalahan ejaan. Dalam tutorial ini kami akan membahas solusi lengkap yang **menjalankan OCR pada gambar**, menggunakan Aspose OCR untuk mengekstrak teks mentah, dan kemudian memanfaatkan **model Hugging Face** untuk membersihkan ejaan dan tata bahasa – secara efektif menjawab pertanyaan “bagaimana cara mengoreksi OCR”.

Kami juga akan membahas **bagaimana cara mengenali teks** dari sumber tulisan tangan, mendemonstrasikan langkah **memuat gambar untuk OCR**, serta menambahkan beberapa tips praktis yang menyelamatkan Anda dari jebakan umum. Pada akhir tutorial Anda akan memiliki satu skrip yang dapat Anda masukkan ke proyek Python mana pun dan mulai mengoreksi hasil OCR secara instan.

> **Pro tip:** Jika Anda sudah menginstal `asposeocr` dan memiliki GPU, atur `gpu_layers` > 0 untuk percepatan. Contoh di bawah ini juga bekerja dengan sempurna pada mesin yang hanya menggunakan CPU.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

- Python 3.9 atau yang lebih baru.
- Paket `asposeocr` (`pip install asposeocr`).
- Akses internet untuk run pertama – model Hugging Face akan diunduh secara otomatis.
- Gambar tulisan tangan (misalnya `handwritten_note.jpg`) yang ditempatkan di folder yang dapat Anda referensikan.

Tidak ada pustaka tambahan yang diperlukan; pembungkus Aspose AI menangani pengunduhan Hugging Face untuk Anda.

---

## Langkah 1: Memuat Gambar untuk OCR dan Menginisialisasi Mesin

Hal pertama yang harus Anda lakukan adalah **memuat gambar untuk OCR**. Aspose OCR menyediakan metode `Image.load` yang nyaman dan menerima jalur file atau aliran.

```python
import asposeocr as ocr

# Initialize the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the handwritten image – replace with your own path
ocr_engine.image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
```

> **Mengapa ini penting:** Memuat gambar lebih awal memungkinkan mesin memeriksa resolusi, DPI, dan kedalaman warna, yang sangat penting untuk ekstraksi teks yang akurat. Melewatkan langkah ini atau memberi gambar yang rusak adalah penyebab umum hasil **bagaimana cara mengenali teks** yang buruk.

---

## Langkah 2: Mengatur Mode Pengakuan ke Handwritten dan Menjalankan OCR

Aspose mendukung beberapa mode pengenalan. Karena kita berurusan dengan catatan yang ditulis dengan pena, kita mengaktifkan mode tulisan tangan.

```python
# Enable handwritten recognition mode
ocr_engine.recognition_mode = ocr.RecognitionMode.HANDWRITTEN

# Run the OCR process
ocr_engine.recognize()
raw_handwritten_text = ocr_engine.recognized_text

print("Handwritten raw output:")
print(raw_handwritten_text)
```

Pemanggilan `recognize()` **menjalankan OCR pada gambar** dan mengisi `recognized_text`. Pada titik ini Anda kemungkinan akan melihat string yang penuh dengan huruf yang hilang, spasi berlebih, atau kata‑kata yang kacau – tepatnya jenis output yang ingin kita koreksi.

---

## Langkah 3: Mengonfigurasi Model Hugging Face untuk Post‑Processing

Sekarang bagian yang menyenangkan: menggunakan **model hugging face** untuk membersihkan teks. Aspose AI menyediakan pembungkus tipis di sekitar model apa pun yang kompatibel dengan GGUF yang dihosting di Hugging Face. Dalam contoh kami kami memilih model ringan `Qwen/Qwen2.5-3B-Instruct-GGUF` – sempurna untuk mesin CPU.

```python
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# Model configuration – auto‑download on first run
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    gpu_layers=0,                # Set >0 if you have a supported GPU
)

# Initialize the AI engine with the config
ai_engine = AsposeAI()
ai_engine.initialize(ai_config)
```

> **Mengapa model ini?** Model ini menyeimbangkan ukuran dan kemampuan mengikuti instruksi, menjadikannya ideal untuk koreksi secara langsung tanpa memerlukan GPU besar.

---

## Langkah 4: Menulis Prompt Koreksi Sederhana

AI memerlukan instruksi yang jelas. Kami membungkus output OCR mentah dalam prompt yang meminta model untuk “Memperbaiki semua kesalahan ejaan/tata bahasa”. Di sinilah **bagaimana cara mengoreksi OCR** bertemu dengan pemrosesan bahasa alami.

```python
def correct_handwritten(text):
    prompt = f"Fix any spelling/grammar errors in this handwritten OCR result:\n{text}"
    return ai_engine.run_prompt(prompt)

# Register the post‑processor with the AI engine
ai_engine.set_post_processor(correct_handwritten, None)
```

Pemanggilan `set_post_processor` memberi tahu Aspose AI untuk memanggil `correct_handwritten` setiap kali kami kemudian memanggil `run_postprocessor`.

---

## Langkah 5: Menerapkan Post‑Processor dan Melihat Hasil yang Dibersihkan

Akhirnya kami memasukkan string OCR mentah ke dalam post‑processor. Model mengembalikan versi yang dipoles sehingga terasa seperti diketik oleh manusia.

```python
# Apply correction
corrected_text = ai_engine.run_postprocessor(raw_handwritten_text)

print("\nCorrected handwritten output:")
print(corrected_text)
```

**Output yang diharapkan** (contoh):

```
Handwritten raw output:
Ths is a smple note wth some erors.

Corrected handwritten output:
This is a simple note with some errors.
```

Perhatikan bagaimana AI memperbaiki huruf “i” yang hilang, menambahkan “l” yang terlewat, dan mengoreksi “wth” menjadi “with”. Itulah inti **bagaimana cara mengoreksi OCR** – model bahasa ringan yang berfungsi sebagai pemeriksa ejaan dan tata bahasa.

---

## Langkah 6: Membersihkan Sumber Daya (Praktik Baik)

Objek Aspose menyimpan sumber daya native, jadi sebaiknya Anda melepaskannya ketika selesai.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose the OCR engine
ocr_engine.dispose()
```

Mengabaikan pembersihan dapat menyebabkan kebocoran memori, terutama jika Anda menjalankan skrip dalam layanan yang hidup lama.

---

## Kasus Khusus & Tips yang Mungkin Belum Anda Pikirkan

| Situasi | Apa yang Harus Dilakukan |
|-----------|------------|
| **Gambar resolusi sangat rendah** (mis., 72 dpi) | Upscale dengan `Pillow` sebelum memuat, atau minta mesin OCR menerapkan filter binarisasi (`ocr_engine.image.apply_binarization()`). |
| **Teks campuran cetak dan tulisan tangan** | Jalankan dua kali: pertama dengan `RecognitionMode.PRINTED`, kemudian dengan `HANDWRITTEN`, dan gabungkan hasilnya sebelum post‑processing. |
| **Model gagal diunduh** | Atur `allow_auto_download="false"` dan unduh file GGUF secara manual dari Hugging Face, lalu arahkan `hugging_face_repo_id` ke jalur lokal. |
| **GPU tersedia tetapi `gpu_layers` diatur ke 0** | Tingkatkan `gpu_layers` ke jumlah lapisan yang ingin Anda alihkan – nilai tipikal 10‑20 untuk model 3 B. |
| **Kosakata domain khusus** (mis., istilah medis) | Tambahkan “petunjuk kosakata” singkat di akhir prompt: “Gunakan istilah berikut: …”. Model menghormati daftar sederhana. |

Nuansa‑nuansa ini membuat pipeline **bagaimana cara mengenali teks** Anda menjadi tangguh di berbagai data dunia nyata.

---

## Skrip Lengkap yang Siap Pakai (Copy‑Paste)

Berikut adalah seluruh skrip, siap dijalankan setelah Anda mengganti jalur gambar.

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# 1️⃣ Load image for OCR
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")

# -------------------------------------------------
# 2️⃣ Run OCR in handwritten mode
# -------------------------------------------------
ocr_engine.recognition_mode = ocr.RecognitionMode.HANDWRITTEN
ocr_engine.recognize()
raw_handwritten_text = ocr_engine.recognized_text
print("Handwritten raw output:")
print(raw_handwritten_text)

# -------------------------------------------------
# 3️⃣ Configure Hugging Face model
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    gpu_layers=0,                # Change >0 for GPU acceleration
)
ai_engine = AsposeAI()
ai_engine.initialize(ai_config)

# -------------------------------------------------
# 4️⃣ Define correction prompt
# -------------------------------------------------
def correct_handwritten(text):
    prompt = f"Fix any spelling/grammar errors in this handwritten OCR result:\n{text}"
    return ai_engine.run_prompt(prompt)

ai_engine.set_post_processor(correct_handwritten, None)

# -------------------------------------------------
# 5️⃣ Apply post‑processor
# -------------------------------------------------
corrected_text = ai_engine.run_postprocessor(raw_handwritten_text)
print("\nCorrected handwritten output:")
print(corrected_text)

# -------------------------------------------------
# 6️⃣ Clean up
# -------------------------------------------------
ai_engine.free_resources()
ocr_engine.dispose()
```

Simpan sebagai `correct_ocr.py` dan jalankan dengan `python correct_ocr.py`. Jika semuanya sudah disiapkan dengan benar, Anda akan melihat teks mentah dan teks yang telah dikoreksi tercetak di konsol.

---

## Kesimpulan

Dalam panduan ini kami menunjukkan **bagaimana cara mengoreksi OCR** dengan menggabungkan Aspose OCR dan **model hugging face** untuk post‑processing cerdas. Mulai dari memuat gambar, **menjalankan OCR pada gambar**, dan **bagaimana cara mengenali teks**, kami menelusuri setiap langkah, menjelaskan mengapa penting, dan memberikan skrip siap pakai.  

Sekarang Anda dapat dengan percaya diri membersihkan catatan tulisan tangan, kwitansi, atau pemindaian berkualitas rendah tanpa harus mengedit setiap baris secara manual. Ingin melangkah lebih jauh? Coba ganti model Qwen dengan varian LLaMA yang lebih besar, atau integrasikan skrip ke dalam API Flask sehingga aplikasi web Anda dapat mengoreksi OCR secara real‑time.  

Punya pertanyaan tentang memuat gambar untuk OCR, menyesuaikan prompt, atau menskalakan solusi? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}