---
category: general
date: 2026-06-22
description: Jalankan model di CPU dan pelajari cara mengurangi penggunaan memori
  GPU dengan mengonfigurasi lapisan GPU di Aspose AI. Panduan langkah demi langkah
  dengan potongan kode.
draft: false
keywords:
- run model on cpu
- reduce gpu memory usage
- limit gpu layers
- configure gpu layers
language: id
og_description: Jalankan model di CPU dan kurangi konsumsi memori GPU dengan mengonfigurasi
  lapisan GPU. Tutorial lengkap untuk penyiapan model Aspose AI.
og_title: Jalankan Model di CPU – Kurangi Penggunaan Memori GPU
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  headline: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  type: TechArticle
- description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  name: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  steps:
  - name: Attach any required post‑processors.
    text: Attach any required post‑processors.
  - name: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
    text: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
  - name: Initialize the model with that configuration.
    text: Initialize the model with that configuration.
  - name: Verify placement and run a test inference.
    text: Verify placement and run a test inference.
  type: HowTo
tags:
- AsposeAI
- CPU inference
- GPU optimization
title: Jalankan Model di CPU – Kurangi Penggunaan Memori GPU dengan Aspose AI
url: /id/python/general/run-model-on-cpu-reduce-gpu-memory-usage-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan Model di CPU – Kurangi Penggunaan Memori GPU dengan Aspose AI

Pernah bertanya-tanya bagaimana cara **run model on CPU** ketika server Anda tidak memiliki GPU? Atau mungkin Anda sedang berjuang melawan error out‑of‑memory pada GPU yang sederhana dan perlu **reduce GPU memory usage** tanpa mengorbankan terlalu banyak kecepatan. Dalam panduan ini kami akan membahas secara detail: melampirkan post‑processor, menginisialisasi Aspose AI pada CPU, dan menyesuaikan jumlah lapisan GPU agar jejak memori tetap kecil.

Kami akan mencakup semuanya mulai dari baris kode pertama hingga memvalidasi bahwa model benar‑benar menggunakan konfigurasi yang Anda minta. Pada akhir tutorial Anda akan dapat **run model on CPU**, **limit GPU layers**, dan **configure GPU layers** untuk beban kerja apa pun—tanpa sulap, hanya Python standar.

## Prasyarat

- Python 3.8+ terinstal (kode menggunakan type hints tetapi juga bekerja pada versi lebih lama)
- Paket `asposeai` (pasang via `pip install asposeai`)
- Pemahaman dasar tentang konsep inferensi jaringan saraf (Anda tidak perlu PhD, cukup rasa ingin tahu)
- Opsional: mesin yang mendukung GPU untuk menguji perbedaan antara jalur CPU dan GPU

Jika Anda belum memiliki salah satu dari hal tersebut, silakan instal SDK terlebih dahulu; sisa tutorial mengasumsikan impor berhasil.

![Diagram illustrating how to run model on cpu instead of gpu](run-model-on-cpu-diagram.png)

## Langkah 1: Lampirkan Post‑Processor Pemeriksa Ejaan (Tidak Perlu Pengaturan Khusus)

Sebelum kita berpikir tentang CPU atau GPU, mari hubungkan post‑processor pemeriksa ejaan yang disertakan oleh Aspose AI. Ini adalah kebiasaan yang baik untuk melampirkan post‑processor lebih awal sehingga mereka menjadi bagian dari setiap panggilan inferensi.

```python
from asposeai import AI, spell_check_processor

# Create the AI client
ai = AI()

# Attach the built‑in spell‑check processor; no custom settings required
ai.set_post_processor(spell_check_processor, custom_settings={})
```

*Mengapa ini penting:* Post‑processor dijalankan **setelah** model menghasilkan token mentah. Dengan menyiapkannya sekarang, Anda menjamin bahwa teks apa pun yang Anda hasilkan—baik di CPU maupun GPU—akan otomatis dibersihkan. Ini langkah kecil yang mencegah bug di tahap selanjutnya.

## Langkah 2: Jalankan Model di CPU – Inisialisasi Aspose AI Tanpa GPU

Berikutnya adalah inti tutorial: memberi tahu Aspose AI untuk **run model on CPU**. SDK menyediakan `AsposeAIModelConfig`, di mana parameter `gpu_layers` mengontrol berapa banyak lapisan yang tetap berada di GPU. Menetapkannya ke `0` memaksa seluruh jaringan berjalan di CPU.

```python
from asposeai import AsposeAIModelConfig

# Initialize the model configuration to use zero GPU layers (i.e., CPU only)
cpu_config = AsposeAIModelConfig(gpu_layers=0)

# Apply the configuration; this will load the model onto the CPU
ai.initialize(cpu_config)

print("✅ Model initialized on CPU – ready for inference.")
```

*Apa yang terjadi di balik layar?* Ketika `gpu_layers=0`, runtime mengalokasikan semua tensor di memori host. Ini menghilangkan kebutuhan driver CUDA, sehingga skrip dapat dijalankan di hampir semua server. Trade‑off‑nya adalah throughput yang lebih lambat, tetapi untuk pekerjaan batch atau prototipe latensi rendah, kesederhanaan sering kali lebih berharga daripada kecepatan mentah.

## Langkah 3: Batasi Lapisan GPU untuk Mengurangi Penggunaan Memori GPU

Jika Anda memang memiliki GPU tetapi memori terbatas, Anda dapat **limit GPU layers** alih‑alih memindahkan semuanya ke CPU. Dengan menyimpan hanya beberapa lapisan awal di GPU, Anda tetap mendapatkan akselerasi perangkat keras sambil secara drastis mengurangi konsumsi memori.

```python
# Example: keep only the first 10 layers on the GPU; the rest run on CPU
limited_gpu_config = AsposeAIModelConfig(gpu_layers=10)

ai.initialize(limited_gpu_config)

print("✅ Model initialized with 10 GPU layers – memory usage trimmed.")
```

*Mengapa membatasi lapisan GPU membantu:* Model transformer modern mengalokasikan sebagian besar memori per lapisan. Mengurangi beberapa lapisan dari GPU dapat membebaskan ratusan megabyte. Pendekatan ini sempurna untuk “pekerjaan dengan keterbatasan memori” di mana Anda masih menginginkan percepatan untuk komputasi paling berat.

## Langkah 4: Konfigurasikan Lapisan GPU untuk Manajemen Memori Fleksibel

Kadang‑kadang Anda memerlukan pendekatan yang lebih granular—misalnya ingin **configure GPU layers** berdasarkan ukuran pekerjaan tertentu. SDK memungkinkan Anda membaca total jumlah lapisan model dan menghitung jumlah lapisan GPU yang aman pada runtime.

```python
# Determine total number of layers (this is model‑specific; assume 36 for illustration)
total_layers = ai.model_info.total_layers  

# Choose a safe percentage, e.g., 25% of layers on GPU
gpu_layer_fraction = 0.25
desired_gpu_layers = int(total_layers * gpu_layer_fraction)

# Build the config dynamically
dynamic_config = AsposeAIModelConfig(gpu_layers=desired_gpu_layers)

ai.initialize(dynamic_config)

print(f"✅ Configured {desired_gpu_layers}/{total_layers} layers on GPU.")
```

*Pro tip:* Saat menjalankan di server bersama, query memori GPU yang tersedia terlebih dahulu (`torch.cuda.get_device_properties(0).total_memory`) dan sesuaikan `desired_gpu_layers` sesuai. Langkah tambahan ini memastikan Anda tidak pernah oversubscribe GPU, yang dapat menyebabkan crash OOM.

## Langkah 5: Verifikasi Konfigurasi dan Uji Inferensi

Setelah mengatur konfigurasi, sebaiknya periksa kembali di mana setiap lapisan berada. Aspose AI menyediakan metode diagnostik yang mengembalikan pemetaan lapisan ke perangkat.

```python
# Retrieve the device placement map
placement = ai.get_layer_placement()

cpu_layers = [l for l, dev in placement.items() if dev == "cpu"]
gpu_layers = [l for l, dev in placement.items() if dev == "gpu"]

print(f"Layers on CPU: {len(cpu_layers)}")
print(f"Layers on GPU: {len(gpu_layers)}")
```

Setelah Anda puas, jalankan inferensi cepat untuk melihat semuanya beraksi:

```python
input_text = "The quick brown fox jumps over the lazy dog."
output = ai.process(input_text)

print("Model output:", output)
```

Jika skrip mencetak teks yang diharapkan dan laporan penempatan cocok dengan konfigurasi Anda, Anda telah berhasil **run model on CPU**, **reduce GPU memory usage**, dan **configure GPU layers** untuk skenario Anda.

## Masalah Umum & Cara Menghindarinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| `CUDA out of memory` error | Terlalu banyak lapisan GPU | Kurangi `gpu_layers` atau ubah menjadi `gpu_layers=0` |
| No output from `ai.process` | Model tidak diinisialisasi | Pastikan `ai.initialize` dipanggil **setelah** melampirkan post‑processor |
| Inferensi lambat pada GPU | Semua lapisan masih di CPU | Verifikasi `gpu_layers` > 0 dan peta perangkat menunjukkan penggunaan GPU |
| Kesalahan ejaan yang tidak terduga | Post‑processor tidak terlampir | Panggil `set_post_processor` sebelum `initialize` |

## Bonus: Beralih Antara CPU dan GPU Secara Dinamis

Karena SDK menginisialisasi ulang model setiap kali Anda memanggil `initialize`, Anda dapat beralih antara CPU dan GPU tanpa harus memulai ulang skrip.

```python
def switch_to_cpu():
    ai.initialize(AsposeAIModelConfig(gpu_layers=0))
    print("🔄 Switched to CPU mode.")

def switch_to_gpu(layers=12):
    ai.initialize(AsposeAIModelConfig(gpu_layers=layers))
    print(f"🔄 Switched to GPU mode with {layers} layers.")
```

Cukup panggil `switch_to_cpu()` ketika Anda memerlukan jalur memori rendah, dan `switch_to_gpu(12)` ketika Anda siap untuk percepatan kecepatan.

## Kesimpulan

Kami telah membahas contoh lengkap, hands‑on tentang cara **run model on CPU**, **reduce GPU memory usage**, **limit GPU layers**, dan **configure GPU layers** dengan Aspose AI. Langkah‑langkahnya sederhana:

1. Lampirkan post‑processor yang diperlukan.  
2. Pilih konfigurasi (`gpu_layers=0` untuk CPU murni, atau angka modest untuk mode campuran).  
3. Inisialisasi model dengan konfigurasi tersebut.  
4. Verifikasi penempatan dan jalankan inferensi percobaan.  

Dengan teknik ini Anda dapat menjaga pipeline inferensi tetap ringan, menghindari crash OOM yang mahal, dan tetap mengekstrak performa dari GPU sederhana bila tersedia. Selanjutnya, Anda dapat mengeksplorasi strategi batching, kuantisasi, atau bahkan memindahkan bagian model ke CPU sambil mempertahankan attention heads di GPU—semua topik tersebut dibangun langsung di atas fondasi **configure GPU layers** yang baru saja Anda kuasai.

Ada pertanyaan tentang arsitektur model tertentu atau butuh bantuan menyesuaikan jumlah lapisan untuk sebuah

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Tutorial Aspose OCR – Pengenalan Karakter Optik](/ocr/english/)
- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}