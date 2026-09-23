---
category: general
date: 2026-02-09
description: cara menjalankan OCR menggunakan Aspose AI dan model Hugging Face – pelajari
  cara mengunduh model Hugging Face, memperbaiki kesalahan OCR, dan membebaskan memori
  GPU.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: id
og_description: Cara menjalankan OCR dengan Aspose AI dijelaskan di paragraf pertama
  – temukan cara mengunduh model Hugging Face, memperbaiki kesalahan OCR, dan membebaskan
  memori GPU.
og_title: Cara menjalankan OCR dengan Aspose AI – Panduan Lengkap
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Cara Menjalankan OCR dengan Aspose AI – Panduan Langkah demi Langkah
url: /id/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara menjalankan OCR dengan Aspose AI – Panduan Lengkap

Pernah bertanya-tanya **bagaimana menjalankan OCR** pada faktur yang dipindai dan mendapatkan angka yang bersih sempurna tanpa menghabiskan berjam‑jam memperbaiki typo? Anda tidak sendirian. Dalam banyak proyek dunia nyata, teks mentah yang dihasilkan oleh mesin OCR klasik masih mengandung karakter asing, simbol mata uang yang rusak, atau digit yang kacau—terutama ketika gambar sumber berisik.  

Kabar baiknya, Anda dapat menghubungkan LLM ke Aspose OCR, mengunduh model Hugging Face secara langsung, dan membiarkan AI memoles output untuk Anda. Dalam tutorial ini kami akan menjelaskan seluruh alur kerja, mulai dari mengambil model (ya, kami akan menunjukkan cara **download hugging face model** secara otomatis) hingga membebaskan sumber daya GPU ketika selesai. Pada akhir tutorial Anda akan memiliki skrip yang dapat direproduksi yang **corrects OCR errors**, berjalan cepat pada GPU yang sederhana, dan membersihkan dirinya sendiri sehingga Anda tidak membuang memori.

## Apa yang Akan Anda Pelajari

- Konfigurasikan Aspose AI untuk mengambil model **Qwen2.5‑3B‑Instruct‑GGUF** dari Hugging Face.
- Jalankan mesin Aspose OCR standar pada file gambar.
- Gunakan prompt LLM khusus yang menjaga angka dan simbol mata uang tetap utuh.
- Bebaskan memori GPU dengan rutin bawaan **free gpu memory**.
- Sesuaikan alur kerja untuk kasus tepi seperti PDF multi‑halaman atau GPU kelas rendah.

> **Prerequisites** – Python 3.9+, paket `aspose-ocr`, akses internet untuk unduhan model pertama, dan GPU dengan setidaknya 4 GB VRAM (opsional tetapi disarankan). Jika Anda tidak memiliki GPU, skrip akan otomatis beralih ke CPU untuk lapisan yang tersisa.

---

## Cara Menjalankan OCR dan Meningkatkan Hasil

Berikut adalah skrip Python lengkap yang siap dijalankan. Simpan sebagai `ocr_with_ai.py` dan ganti jalur placeholder dengan file Anda sendiri.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** Parameter `gpu_layers` memungkinkan Anda menentukan berapa banyak lapisan transformer yang tetap di GPU. Jika Anda mengalami error out‑of‑memory, turunkan angka ini dan sisanya akan berjalan di CPU – Anda tetap dapat **free gpu memory** nanti dengan `ai.free_resources()`.

### Output yang Diharapkan

Menjalankan skrip pada contoh faktur menghasilkan sesuatu seperti:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Perhatikan bagaimana AI memperbaiki “O” dalam `$1O0.00` menjadi nol yang tepat sambil mempertahankan tanda dolar. Itulah inti dari **correct OCR errors** untuk dokumen keuangan.

---

## Unduh Model Hugging Face – Apa yang Terjadi di Balik Layar?

Ketika Anda mengatur `allow_auto_download="true"` wrapper Aspose AI memeriksa `directory_model_path`. Jika file model tidak ada di sana, ia akan menghubungi Hugging Face Hub, mengambil versi **int8‑quantized** dari `Qwen2.5‑3B‑Instruct‑GGUF`, dan menyimpannya secara lokal. Unduhan satu kali ini biasanya berukuran kurang dari 2 GB, sehingga memungkinkan bahkan pada SSD yang sederhana.

> **Why int8?** Mengkuantisasi ke 8‑bit mengurangi penggunaan memori secara dramatis—penting ketika Anda juga ingin **free gpu memory** setelah pemrosesan. Trade‑off-nya adalah sedikit penurunan akurasi, tetapi untuk post‑processing teks OCR dampaknya dapat diabaikan.

Jika Anda lebih suka menampung model sendiri, cukup letakkan file `.gguf` ke dalam `YOUR_DIRECTORY/Models` dan Aspose akan mengambilnya tanpa harus mengakses internet lagi.

## Cara Membebaskan GPU – Praktik Terbaik

Sumber daya GPU adalah komoditas yang dibagi pada banyak workstation. Membiarkan tensor tetap hidup setelah skrip selesai dapat menyebabkan error “CUDA out of memory” untuk pekerjaan berikutnya. Pemanggilan `ai.free_resources()` melakukan tiga hal:

1. **Disposes the underlying transformer** – semua bobot yang berada di GPU dilepaskan.
2. **Clears the PyTorch cache** – `torch.cuda.empty_cache()` dipanggil secara internal.
3. **Deletes temporary files** – semua cache di disk yang dibuat selama unduhan dihapus.

Anda juga dapat memanggil secara manual `torch.cuda.empty_cache()` jika Anda mencampur Aspose AI dengan beban kerja PyTorch lainnya, tetapi metode bawaan biasanya sudah cukup.

## Panduan Langkah‑per‑Langkah (H2 dengan Kata Kunci Sekunder)

### Unduh Model Hugging Face Secara Otomatis

Konstruktor `AsposeAIModelConfig` menyembunyikan kompleksitas berurusan dengan API Hugging Face. Pastikan Anda memiliki akses internet saat pertama kali menjalankan skrip. Setelah itu, model berada di `YOUR_DIRECTORY/Models`, dan eksekusi berikutnya dimulai secara instan.

### Bebaskan Memori GPU Setelah Inferensi

Jika Anda menjalankan ini di dalam layanan yang berjalan lama (mis., API Flask), panggil `ai.free_resources()` setelah setiap permintaan. Ini mencegah kebocoran memori dan memastikan permintaan berikutnya dapat menggunakan kembali GPU yang sama tanpa gangguan.

### Perbaiki Kesalahan OCR dengan Prompt Kustom

Fungsi `financial_prompt` kami mengembalikan sebuah dictionary dengan satu kunci `prompt`. Anda dapat menyesuaikannya untuk domain apa pun:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Ganti nama fungsi di `ai.set_post_processor(...)` dan Anda akan memiliki pipeline **correct OCR errors** untuk catatan medis.

### Cara Menjalankan OCR pada PDF Multi‑Halaman

Aspose OCR dapat menangani PDF secara langsung:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

Setelah Anda mendapatkan string mentah, post‑processor LLM yang sama akan membersihkan teks setiap halaman. Tidak diperlukan kode tambahan.

### Saat Anda Tidak Memiliki GPU – Cara Membebaskan GPU (Bahkan Tanpa GPU)

Bahkan pada mesin hanya CPU, memanggil `ai.free_resources()` tidak berbahaya. Itu hanya membersihkan cache internal, yang masih dapat membebaskan RAM. Jadi saran **how to free gpu** berlaku secara universal: selalu bersihkan setelah selesai.

## Kesalahan Umum & Cara Kami Menyelesaikannya

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑Memory on GPU** | `gpu_layers` set terlalu tinggi untuk kartu Anda | Kurangi `gpu_layers` menjadi 10 atau 5, biarkan sisanya berjalan di CPU |
| **Model never downloads** | Firewall perusahaan memblokir HTTPS ke huggingface.co | Unduh model secara manual pada jaringan lain, lalu arahkan `directory_model_path` ke folder lokal |
| **Numbers get corrupted** | Prompt tidak cukup eksplisit tentang menjaga digit | Tambahkan “preserve all numeric values and currency symbols exactly as they appear” ke dalam prompt |
| **`free_resources` raises an exception** | Menggunakan versi Aspose OCR yang lebih lama | Upgrade ke paket `aspose-ocr` terbaru (pip install --upgrade aspose-ocr) |

## Ringkasan Contoh Lengkap

Berikut skripnya lagi, kali ini dengan komentar inline yang menjelaskan setiap baris untuk referensi di masa mendatang:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

## Kesimpulan

Kami telah membahas **how to run OCR** dengan Aspose, mengunduh model Hugging Face sesuai permintaan, membuat prompt yang **corrects OCR errors**, dan akhirnya **free gpu memory** sehingga workstation Anda tetap responsif. Seluruh alur kerja masuk dalam satu file Python yang berdiri sendiri—tanpa skrip eksternal, tanpa penanganan model manual, dan tanpa alokasi GPU yang tertinggal.

Langkah selanjutnya? Coba ganti `financial_prompt` dengan sebuah

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}