---
category: general
date: 2026-07-05
description: Cara menampilkan daftar model dengan Aspose AI, mengaktifkan unduhan
  otomatis, dan mengunduh model Hugging Face di Python. Ikuti tutorial langkah demi
  langkah ini untuk menyiapkan cache dan mulai menggunakan Aspose AI hari ini.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: id
og_description: Cara menampilkan daftar model dengan Aspose AI, mengaktifkan unduhan
  otomatis, dan mengunduh model Hugging Face. Pelajari cara mengatur cache dan menggunakan
  Aspose AI dalam hitungan menit.
og_title: Cara menampilkan daftar model dengan Aspose AI – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Cara menampilkan daftar model dengan Aspose AI – Panduan Lengkap
url: /id/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menampilkan Daftar Model dengan Aspose AI – Panduan Lengkap

Cara menampilkan daftar model dengan Aspose AI adalah pertanyaan yang muncul begitu Anda mulai bereksperimen dengan model bahasa besar di Python. Dalam tutorial ini kita akan membahas cara mengaktifkan **auto download**, mengonfigurasi cache lokal, dan mengambil model langsung dari Hugging Face—sehingga Anda dapat langsung bekerja tanpa harus mencari file secara manual.

Jika Anda pernah bertanya *“bagaimana cara menggunakan Aspose untuk AI berbasis OCR?”* atau *“apa cara termudah mengatur cache untuk file model?”* Anda berada di tempat yang tepat. Pada akhir tutorial Anda akan memiliki skrip yang berfungsi penuh untuk menampilkan semua model yang disimpan secara lokal, secara otomatis mengunduh yang belum ada, dan menunjukkan tepatnya di mana file tersebut berada di disk.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

- Python 3.9 atau lebih baru (perpustakaan menggunakan type hints yang memerlukan interpreter terbaru)
- Akses `pip` untuk menginstal paket **Aspose OCR** (`aocr`).  
  ```bash
  pip install aocr
  ```
- Koneksi internet untuk unduhan pertama dari Hugging Face.
- Sebuah folder tempat Anda ingin menyimpan cache model (misalnya, `./model_cache`).

Itu saja—tidak perlu kontainer Docker tambahan, tidak ada lingkungan virtual berat selain instalasi Python yang bersih.

---

## ## Cara Menampilkan Daftar Model dengan Aspose AI

Inti panduan ini adalah kemampuan untuk **menampilkan daftar model** yang telah di‑cache secara lokal oleh Aspose AI. Setelah cache disiapkan, perpustakaan dapat menenumerasi semua yang diketahui, memudahkan debugging dan kontrol versi.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Mengapa ini berhasil:**  
- `AsposeAI()` membuat titik masuk tingkat tinggi yang berkomunikasi dengan mesin inferensi di bawahnya.  
- `AsposeAIModelConfig()` menyimpan semua pengaturan yang dapat Anda ubah; mengatur `allow_auto_download` ke `"true"` memberi tahu perpustakaan untuk secara otomatis mengambil file yang belum ada dari repositori yang Anda tentukan.  
- `directory_model_path` adalah *direktori cache*—tempat semua biner yang diunduh disimpan.  
- `initialize()` menerapkan konfigurasi, melakukan unduhan pertama jika cache kosong.  
- Akhirnya, `list_local()` memindai folder cache dan mengembalikan daftar Python berisi identifier model, yang kami cetak.

### Output yang Diharapkan (run pertama)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Jika Anda menjalankan skrip lagi, perpustakaan akan melewatkan unduhan dan hanya menampilkan model yang sudah ada, membuktikan bahwa **cara mengatur cache** memang memberi manfaat pada eksekusi selanjutnya.

---

## ## Aktifkan auto download untuk model yang belum ada

Seringkali Anda akan bekerja dengan beberapa model di berbagai proyek. Mengunduh masing‑masing secara manual dari Hugging Face bisa melelahkan. Dengan mengaktifkan auto download, Aspose AI menangani proses berat tersebut.

```python
cfg.allow_auto_download = "true"
```

> **Pro tip:** Simpan `allow_auto_download` diset ke `"true"` **hanya** di lingkungan pengembangan atau CI. Di produksi Anda mungkin ingin mengunci cache untuk menghindari lalu lintas jaringan yang tidak terduga.

Jika nanti Anda memutuskan untuk mematikannya, cukup ubah flag menjadi `"false"` sebelum memanggil `initialize()` lagi.

---

## ## Unduh Model Hugging Face Secara Dinamis

Baris

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

memberitahu Aspose AI repositori remote mana yang harus diambil. Perpustakaan mendukung semua model publik di Hugging Face yang menyediakan file GGUF. Ingin model lain? Ganti ID repositori:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Saat Anda menjalankan skrip, Aspose AI memeriksa cache:

- **Jika model sudah ada**, ia memuatnya secara instan.  
- **Jika tidak**, flag auto‑download memicu unduhan, menyimpan file di bawah `directory_model_path`, dan kemudian mendaftarkannya untuk penggunaan langsung.

Pendekatan ini menghilangkan proses dua langkah “unduh‑lalu‑jalankan” yang sering dipaksa oleh tutorial lain.

---

## ## Cara Menggunakan Aspose AI Setelah Model Ditampilkan

Menampilkan daftar model hanyalah setengah cerita. Setelah Anda tahu sebuah model tersedia, Anda dapat memulai inferensi:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Mengapa ini penting:**  
- `run_inference()` menyederhanakan tokenisasi, batching, dan penanganan GPU.  
- Dengan memberikan *nama model* yang Anda peroleh dari `list_local()`, Anda memastikan bahwa panggilan inferensi cocok dengan file tepat di disk.

---

## ## Cara Mengatur Lokasi Cache untuk Beberapa Proyek

Jika Anda menangani beberapa proyek, mungkin Anda ingin masing‑masing memiliki folder cache sendiri. Field `directory_model_path` hanyalah string biasa, sehingga Anda dapat membangunnya secara dinamis:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Sekarang setiap proyek mendapatkan sub‑folder terisolasi (`./model_cache/sentiment_analysis`), mencegah bentrok versi dan memudahkan pembersihan.

---

## ## Kesalahan Umum dan Cara Menghindarinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| **`PermissionError` saat mengakses cache** | Folder cache dimiliki oleh pengguna lain (umum pada server bersama) | Buat folder secara manual dengan izin yang tepat: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Model tidak pernah muncul di `list_local()`** | `allow_auto_download` diset ke `"false"` dan model belum di‑cache | Aktifkan flag sementara, jalankan sekali, lalu matikan kembali jika diinginkan |
| **Versi model tidak terduga** | Dua repositori berbeda memiliki nama yang sama tetapi file berbeda | Pin ID repositori yang tepat (termasuk tag/commit) atau kunci cache dengan menonaktifkan auto‑download setelah unduhan pertama berhasil |
| **Error out‑of‑memory** | File GGUF besar pada mesin tanpa RAM/VRAM cukup | Gunakan model yang lebih kecil (mis., `Qwen2.5-1.5B`) atau set `cfg.device = "cpu"` untuk memaksa inferensi CPU |

---

## ## Skrip Lengkap yang Dapat Anda Salin‑Tempel

Berikut contoh lengkap yang siap dijalankan, menggabungkan semua konsep di atas. Simpan sebagai `list_models_demo.py` dan jalankan dengan `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Menjalankannya** akan menghasilkan output serupa dengan contoh sebelumnya, diikuti oleh jawaban singkat dari model. Jangan ragu mengganti prompt dengan apa saja yang Anda inginkan—ini cara tercepat untuk menguji bahwa model benar‑benar dapat dipakai setelah Anda **menampilkan daftar model**.

---

## ## Ringkasan

Kami telah membahas semua yang Anda perlukan untuk **menampilkan daftar model** menggunakan Aspose AI, mulai dari mengaktifkan **auto download** hingga mengonfigurasi **cache** yang persisten dan mengambil **model Hugging Face** secara on‑demand. Poin pentingnya:

1. Buat objek `AsposeAI` dan `AsposeAIModelConfig`.  
2. Set `allow_auto_download = "true"` dan arahkan `directory_model_path` ke folder yang Anda kontrol.  
3. Inisialisasi AI, lalu panggil `list_local()` untuk melihat apa saja yang telah di‑cache.  
4. Gunakan nama model yang terdaftar untuk inferensi, dan Anda siap membangun aplikasi dunia nyata.

---

## Apa Selanjutnya?

- **Bereksperimen dengan model lain** – ganti `cfg.hugging_face_repo_id` dengan repositori lain dan lihat bagaimana daftar berubah.  
- **Fine‑tune cache**

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Memproses Batch Gambar OCR dengan List di Aspose.OCR untuk .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Cara Mengatur Lisensi Aspose OCR dan Memverifikasinya di Java](/ocr/english/java/ocr-basics/set-license/)
- [Cara Mengekstrak Teks dari Gambar Menggunakan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}