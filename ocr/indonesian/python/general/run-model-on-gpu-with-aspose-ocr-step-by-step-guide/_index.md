---
category: general
date: 2026-03-26
description: Jalankan model di GPU menggunakan Aspose OCR. Pelajari cara mengunduh
  repositori Hugging Face, mengatur lapisan GPU, mengimpor Aspose OCR, dan memuat
  model Qwen2.5 dalam hitungan menit.
draft: false
keywords:
- run model on gpu
- download hugging face repo
- import aspose ocr
- set gpu layers
- load qwen2.5 model
language: id
og_description: Jalankan model di GPU dengan Aspose OCR. Tutorial ini menunjukkan
  cara mengunduh repositori Hugging Face, mengatur lapisan GPU, mengimpor Aspose OCR,
  dan memuat model Qwen2.5.
og_title: Jalankan model di GPU dengan Aspose OCR – Panduan Lengkap
tags:
- Aspose OCR
- GPU acceleration
- Hugging Face
- Python AI
title: Jalankan model di GPU dengan Aspose OCR – Panduan Langkah demi Langkah
url: /id/python/general/run-model-on-gpu-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan model di GPU dengan Aspose OCR – Tutorial Lengkap

Pernah bertanya-tanya bagaimana **menjalankan model di GPU** tanpa harus berurusan dengan kode CUDA tingkat rendah? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika harus mempercepat model bahasa besar namun tetap menginginkan kesederhanaan pustaka tingkat tinggi. Kabar baiknya? Aspose OCR dilengkapi dengan mesin AI yang mudah digunakan yang dapat mengambil model langsung dari Hugging Face, melakukan kuantisasi, dan memindahkan beberapa lapisan pertama ke GPU Anda—semua dalam beberapa baris Python.

Dalam panduan ini kita akan melangkah melalui seluruh proses: **mengunduh repo Hugging Face**, **mengimpor Aspose OCR**, mengonfigurasi **lapisan GPU**, dan akhirnya **memuat model Qwen2.5**. Pada akhir tutorial Anda akan memiliki mesin OCR siap pakai yang sudah berjalan di kartu grafis Anda, serta memahami mengapa setiap pengaturan penting.

## Apa yang Anda Butuhkan

- Python 3.9 atau lebih baru (kode menggunakan type hints dan f‑strings)
- GPU yang kompatibel dengan CUDA (opsional tetapi disarankan untuk kecepatan)
- Akses internet untuk mengambil model dari Hugging Face
- Paket `asposeocr` (`pip install asposeocr`)  

Tidak ada dependensi eksternal lain yang diperlukan—Aspose OCR menangani semua pekerjaan berat untuk Anda.

## Langkah 1: Unduh repo Hugging Face dan impor Aspose OCR

Hal pertama yang harus Anda lakukan adalah memastikan file model tersedia secara lokal. `AsposeAIModelConfig` milik Aspose OCR dapat secara otomatis mengambil repositori dari Hugging Face, sehingga Anda tidak perlu meng‑clone apa pun secara manual.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig
```

**Mengapa ini penting:** Mengimpor paket memberi Anda akses ke kelas `AsposeAI`, yang membungkus model transformer di bawahnya. Objek `AsposeAIModelConfig` adalah tempat Anda memberi tahu mesin *di mana* mengambil model dan *bagaimana* memperlakukannya (misalnya, kuantisasi, alokasi GPU).

> **Tip pro:** Jika Anda berada di belakang proxy perusahaan, atur variabel lingkungan `HTTPS_PROXY` sebelum menjalankan skrip—Aspose OCR menghormati pengaturan proxy standar Python.

## Langkah 2: Atur lapisan GPU untuk kinerja optimal

Menjalankan model di GPU bukan sekadar saklar “on/off”. Anda dapat memutuskan berapa banyak lapisan transformer awal yang tetap berada di GPU sementara sisanya kembali ke CPU. Pendekatan hibrida ini berguna ketika memori GPU Anda terbatas.

```python
# Step 2: Define the model configuration
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # automatically pull repo if missing
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # int8 reduces memory footprint
    gpu_layers=20                                   # first 20 layers run on GPU
)
```

**Mengapa 20 lapisan?** Model Qwen2.5‑3B memiliki 32 blok transformer. Mengalokasikan 20 lapisan pertama ke GPU memberi Anda peningkatan kecepatan yang solid sambil menjaga penggunaan memori tetap terkendali pada kartu 12 GB. Silakan sesuaikan `gpu_layers` sesuai perangkat keras Anda—menetapkannya ke `0` memaksa eksekusi hanya di CPU, sementara `32` mencoba memuat semuanya ke GPU (yang mungkin menyebabkan OOM pada kartu dengan memori terbatas).

## Langkah 3: Buat mesin AI dan muat model Qwen2.5

Sekarang kita menginstansiasi mesin dan memberinya konfigurasi yang baru saja dibuat. Pemanggilan `initialize` secara eksplisit bersifat opsional—Aspose OCR akan menginisialisasi secara malas pada penggunaan pertama—but memanggilnya di awal membuat pemeriksaan kesiapan menjadi lebih jelas.

```python
# Step 3: Create and initialize the AI engine with the configuration
ocr_engine = AsposeAI()
ocr_engine.initialize(model_config)   # explicit call for clarity
```

**Apa yang terjadi di balik layar?**  
1. Aspose OCR menghubungi Hugging Face, mengunduh file GGUF (jika belum ada di cache).  
2. File tersebut dikonversi ke format yang dipahami runtime internal.  
3. `gpu_layers` blok pertama dipindahkan ke memori CUDA; sisanya tetap di CPU.  
4. Mesin menandai dirinya sebagai *initialized*, yang dapat Anda periksa dengan `is_initialized()`.

## Langkah 4: Verifikasi bahwa model siap dijalankan di GPU

Pemeriksaan cepat menyelamatkan Anda dari error runtime yang membingungkan di kemudian hari. Metode `is_initialized()` mengembalikan Boolean, memungkinkan Anda mengonfirmasi bahwa proses unduh, konversi, dan alokasi GPU berhasil.

```python
# Step 4: Confirm that the engine is ready
print("AI ready:", ocr_engine.is_initialized())
```

Jika semuanya berjalan lancar, Anda akan melihat:

```
AI ready: True
```

Jika Anda mendapatkan `False`, periksa kembali bahwa driver CUDA Anda sudah terbaru dan GPU memiliki memori bebas yang cukup untuk 20 lapisan yang Anda minta.

## Opsional: Jalankan inferensi OCR singkat untuk melihat GPU beraksi

Meskipun fokus tutorial ini adalah memuat model, kebanyakan pembaca akan segera ingin menjalankan OCR secara nyata. Berikut contoh minimal yang memproses gambar lokal (`sample.png`) dan mencetak teks yang terdeteksi.

```python
# Optional: Perform a single OCR inference
image_path = "sample.png"
result = ocr_engine.recognize_image(image_path)

print("Detected text:")
print(result.text)
```

**Mengapa menjalankannya sekarang?** Karena inferensi pertama biasanya memicu kompilasi JIT kernel CUDA. Jika Anda mengukur waktu pemanggilan dengan `time.perf_counter()`, Anda akan melihat bahwa run kedua jauh lebih cepat—tanda jelas bahwa model benar‑benar dieksekusi di GPU.

## Kesalahan Umum & Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| `RuntimeError: CUDA out of memory` | `gpu_layers` diset terlalu tinggi untuk kartu Anda | Kurangi `gpu_layers` (misalnya, menjadi 12) atau beralih ke kuantisasi `int8` (sudah diterapkan). |
| `OSError: Unable to download repository` | Tidak ada internet atau proxy memblokir | Atur variabel lingkungan `HTTPS_PROXY`/`HTTP_PROXY` atau unduh file GGUF secara manual dan arahkan `hugging_face_repo_id` ke path lokal. |
| `AttributeError: 'AsposeAI' object has no attribute 'recognize_image'` | Menggunakan versi lama `asposeocr` | Tingkatkan versi dengan `pip install --upgrade asposeocr`. |
| `False` dari `is_initialized()` | Ketidaksesuaian driver CUDA | Pastikan `nvidia-smi` menampilkan versi driver yang kompatibel dengan toolkit CUDA Anda. |

## Ringkasan Visual

![Run model on GPU diagram](run-model-on-gpu.png "Diagram showing model download, GPU layer allocation, and inference flow")

*Alt text:* *run model on GPU diagram illustrating the download of a Hugging Face repo, setting of GPU layers, and execution of the Qwen2.5 model via Aspose OCR.*

## Ringkasan – Apa yang Telah Kita Capai

- **Mengimpor Aspose OCR** dan kelas pembantu AI‑nya.  
- **Mengunduh repo Hugging Face** secara otomatis, berkat `allow_auto_download`.  
- **Menetapkan lapisan GPU** (`gpu_layers=20`) untuk memindahkan bagian paling berat ke kartu grafis.  
- **Memuat model Qwen2.5‑3B‑Instruct** dengan kuantisasi int8, secara signifikan mengurangi penggunaan memori.  
- **Memverifikasi** bahwa mesin siap (`is_initialized()` mengembalikan `True`).  

Semua itu dilakukan dalam kurang dari 30 baris Python—tanpa memerlukan kernel CUDA khusus.

## Langkah Selanjutnya & Topik Terkait

1. **Bereksperimen dengan kuantisasi berbeda** (`float16`, `bfloat16`) untuk melihat trade‑off antara kecepatan dan akurasi.  
2. **Skalakan ke model yang lebih besar** (misalnya Qwen2.5‑7B) dengan menyesuaikan `gpu_layers` dan memastikan Anda memiliki cukup VRAM.  
3. **Pemrosesan OCR batch**: berikan daftar path gambar ke `ocr_engine.recognize_images()` untuk throughput yang lebih tinggi.  
4. **Integrasikan dengan FastAPI** untuk mengekspos endpoint REST yang menjalankan OCR pada file yang masuk—sempurna untuk microservices.  

Jika Anda tertarik pada penyetelan GPU yang lebih maju, lihat panduan kinerja resmi Aspose OCR atau dokumentasi CUDA Toolkit untuk variabel lingkungan seperti `CUDA_VISIBLE_DEVICES`.

---

*Selamat coding! Jika tutorial ini membantu Anda menjalankan model di GPU, beri tahu saya di komentar atau bagikan penyesuaian Anda sendiri. Semakin banyak kita bereksperimen bersama, semakin cepat komunitas belajar.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}