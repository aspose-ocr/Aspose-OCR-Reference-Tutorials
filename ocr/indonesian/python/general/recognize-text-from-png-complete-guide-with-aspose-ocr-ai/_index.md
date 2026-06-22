---
category: general
date: 2026-06-22
description: Mengenali teks dari file PNG menggunakan Aspose OCR di Python. Pelajari
  OCR batch gambar dan atur lapisan GPU untuk pemrosesan cepat.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: id
og_description: Mengenali teks dari file PNG dengan Aspose OCR di Python. Panduan
  ini menunjukkan cara melakukan OCR batch pada gambar dan mengatur lapisan GPU untuk
  meningkatkan kecepatan.
og_title: Mengenali teks dari PNG – Tutorial OCR Aspose Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: Mengenali Teks dari PNG – Panduan Lengkap dengan Aspose OCR & AI
url: /id/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari png – Tutorial Aspose OCR & AI Fitur Lengkap

Pernah perlu **mengenali teks dari png** tetapi terjebak dalam detail pengaturan? Anda tidak sendirian. Baik Anda mendigitalkan kwitansi, memindai formulir, atau mengubah tangkapan layar menjadi teks yang dapat dicari, menguasai batch OCR images di Python dapat menghemat waktu berjam‑jam.  

Dalam panduan ini kami akan menelusuri contoh siap‑jalankan yang tidak hanya **mengenali teks dari png** tetapi juga menunjukkan cara **set GPU layers** untuk peningkatan kecepatan yang signifikan. Pada akhir tutorial Anda akan memiliki skrip mandiri, penjelasan jelas setiap langkah, dan beberapa tip praktis yang dapat Anda salin‑tempel ke proyek Anda sendiri.

## Apa yang Dibahas dalam Tutorial Ini

- Menginstal paket Python Aspose OCR dan Aspose AI  
- Mengonfigurasi model AI dengan unduhan otomatis dari Hugging Face  
- Membuat post‑processor kecil yang memperbaiki typo OCR paling umum  
- Menjalankan loop **batch OCR images** pada seluruh folder PNG  
- Menggunakan opsi **set GPU layers** untuk memanfaatkan kartu grafis Anda  
- Membersihkan sumber daya dengan aman setelah pemrosesan  

Tanpa layanan eksternal, tanpa keajaiban tersembunyi—hanya kode Python murni yang dapat Anda letakkan ke file `.py` dan jalankan.

![Diagram of recognize text from png workflow](workflow.png){alt="diagram alur kerja mengenali teks dari png"}

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.8+ | Aspose AI’s wheels target recent interpreters |
| GPU yang kompatibel dengan CUDA (opsional) | Diperlukan jika Anda ingin **set GPU layers** untuk percepatan |
| Akses internet pada run pertama | Model akan diunduh otomatis dari Hugging Face |
| `pip` terpasang | Untuk mengambil paket Aspose |

Jika Anda sudah memiliki semua ini, bagus—Anda siap memulai. Jika belum, langkah instalasi di bawah ini akan memandu Anda melengkapi yang belum ada.

---

## Langkah 1: Instal Paket Aspose OCR dan Aspose AI

Pertama, dapatkan pustaka dari PyPI. Perintah di bawah ini menarik kedua mesin OCR dan bantuan AI sekaligus.

```bash
pip install aspose-ocr aspose-ai
```

*Tip profesional:* Gunakan lingkungan virtual (`python -m venv .venv`) agar paket tetap terisolasi dari instalasi Python global Anda.

---

## Langkah 2: Buat dan Konfigurasikan Instansi Aspose AI

Komponen AI memberi daya pada mode “cerdas” mesin OCR. Kami akan menunjuk ke model `Qwen/Qwen2.5-3B-Instruct-GGUF`, meminta unduhan otomatis bila belum ada, dan **set GPU layers** ke 30 (Anda dapat menyesuaikannya nanti).

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**Mengapa ini penting:**  
- `allow_auto_download` menghilangkan langkah manual mengunduh model ~2 GB.  
- `gpu_layers=30` memberi tahu transformer di bawah untuk menjalankan 30 lapisan pertama di GPU, memotong waktu inferensi secara dramatis bila GPU kompatibel tersedia.  
- Kuantisasi `int8` menjaga penggunaan memori tetap rendah tanpa mengorbankan akurasi secara signifikan.

---

## Langkah 3: Definisikan Post‑Processor Sederhana untuk Membersihkan Kesalahan OCR

OCR tidak sempurna—terutama pada PNG beresolusi rendah. Solusi cepat adalah mengganti karakter yang sering salah dibaca. Fungsi berikut menukar “0” dengan “o” dan “1” dengan “l”, pola yang sering muncul pada faktur yang dipindai.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

Kami akan menautkan ini ke instansi AI pada langkah berikutnya sehingga setiap hasil pengenalan otomatis melewati proses pembersihan.

---

## Langkah 4: Sambungkan Post‑Processor dan Mesin OCR

Sekarang kami menghubungkan semuanya: mesin OCR, model AI, dan post‑processor.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**Apa yang terjadi di balik layar?**  
`OcrEngine` menyerahkan pekerjaan berat ke model AI yang Anda konfigurasikan. Setelah model mengembalikan teks mentah, Aspose memanggil `fix_common_errors` untuk merapikan output sebelum Anda melihatnya.

---

## Langkah 5: Batch OCR Images – Proses Setiap PNG dalam Folder

Berikut inti tutorial: loop yang menelusuri direktori, memuat setiap `.png`, menjalankan OCR, dan mencetak hasil yang sudah dibersihkan. Pola ini adalah cara kanonik untuk **batch OCR images** secara efisien.

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**Output yang diharapkan** (contoh kwitansi):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

Jika Anda memiliki puluhan atau ratusan file, loop ini akan memprosesnya secara berurutan, menggunakan kembali instansi AI yang sama untuk menghindari beban memuat model berulang kali.

---

## Langkah 6: Bersihkan – Bebaskan Sumber Daya dan Hapus Mesin

Setelah selesai, sebaiknya lepaskan memori GPU dan sumber daya native lainnya. Aspose menyediakan metode eksplisit untuk itu.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

Melewatkan langkah ini dapat meninggalkan memori GPU yang masih teralokasi, yang dapat menyebabkan error out‑of‑memory pada run berikutnya.

---

## Bonus: Menyesuaikan GPU Layers untuk Berbagai Perangkat Keras

Nilai `gpu_layers` yang Anda set sebelumnya merupakan titik optimal untuk banyak GPU modern, tetapi Anda mungkin perlu menyesuaikannya:

| Memori GPU (GB) | `gpu_layers` yang Disarankan |
|-----------------|------------------------------|
| 4 GB atau kurang | 10‑15 |
| 6‑8 GB | 20‑30 |
| 12 GB+ | 35‑45 (atau lebih tinggi) |

Jika Anda melebihi memori GPU, mesin secara otomatis akan beralih ke CPU untuk lapisan yang tersisa, sehingga tidak akan crash—hanya lebih lambat. Silakan bereksperimen dan pantau penggunaan dengan `nvidia‑smi`.

---

## Kesalahan Umum & Cara Menghindarinya

1. **Unduhan model gagal** – Pastikan lingkungan Anda dapat mengakses `https://huggingface.co`. Proxy perusahaan mungkin memerlukan konfigurasi (`https_proxy` env var).  
2. **GPU tidak terdeteksi** – Verifikasi bahwa pustaka `torch` (dipasang sebagai dependensi) melihat GPU: `import torch; print(torch.cuda.is_available())`. Jika mengembalikan `False`, instal wheel PyTorch yang kompatibel dengan CUDA.  
3. **Path gambar salah** – `Path.glob("*.png")` bersifat case‑sensitive di Linux. Gunakan `*.PNG` atau `*.png` sesuai, atau tambahkan `pathlib.Path(...).rglob("*.[pP][nN][gG]")` untuk keamanan.  
4. **Post‑processor terlalu agresif** – Penggantian sederhana dapat mengubah karakter “0” yang sah menjadi “o”. Uji pada sampel representatif dan sesuaikan logika bila diperlukan.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

Jalankan dengan:

```bash
python recognize_text_from_png_batch.py
```

Anda akan melihat setiap nama file PNG diikuti oleh teks yang diekstrak, persis seperti yang ditunjukkan sebelumnya.

---

## Kesimpulan

Kami baru saja menelusuri alur kerja lengkap dan siap produksi untuk **mengenali teks dari png** menggunakan Aspose OCR dan Aspose AI di Python. Dengan menggabungkan langkah‑langkah ke dalam skrip bersih, Anda dapat dengan mudah **batch OCR images**, dan berkat `set gpu layers`

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Batch OCR Gambar dengan List di Aspose.OCR untuk .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Ekstrak Teks dari Gambar Menggunakan Operasi OCR pada Folder](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}