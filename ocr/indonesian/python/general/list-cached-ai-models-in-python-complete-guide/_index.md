---
category: general
date: 2026-06-22
description: Pelajari cara menampilkan daftar model AI yang di‑cache menggunakan AI
  SDK di Python. Termasuk langkah‑langkah untuk mengambil direktori cache model dan
  mengelola model AI lokal secara efisien.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: id
og_description: Daftar model AI yang di-cache dengan Python menggunakan AI SDK. Ikuti
  tutorial langkah demi langkah ini untuk mengambil direktori cache model dan menangani
  model AI lokal.
og_title: Daftar Model AI yang Di-cache di Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Daftar Model AI yang Di‑cache di Python – Panduan Lengkap
url: /id/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Daftar Model AI yang Di‑cache di Python – Panduan Lengkap

Pernah bertanya‑tanya bagaimana cara **list cached AI models** di workstation Anda tanpa harus menggali folder‑folder yang tidak jelas? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika harus memverifikasi model‑model mana yang sudah disimpan secara lokal, terutama saat bekerja dengan bandwidth terbatas atau deployment offline. Dalam tutorial ini Anda akan melihat cara cepat, tanpa basa‑basi, untuk menanyakan AI SDK, mencetak isi cache, dan menemukan tepatnya di mana file‑file tersebut berada.

Kami juga akan menyentuh topik terkait seperti **retrieving the model cache directory**, menangani cache kosong, dan praktik terbaik untuk **managing AI model cache** dalam skrip produksi. Pada akhir tutorial Anda akan memiliki potongan kode mandiri yang dapat ditempelkan ke proyek Python mana pun.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- Python 3.8 atau yang lebih baru terpasang.
- AI SDK (paket `ai`) terpasang via `pip install ai-sdk` atau repositori internal organisasi Anda.
- Familiaritas dasar dengan menjalankan skrip dari command line.

Tidak ada pustaka tambahan yang diperlukan, sehingga contoh tetap ringan dan dapat dipindahkan.

---

## Daftar Model AI yang Di‑cache – Ikhtisar Cepat

Hal pertama yang perlu Anda lakukan adalah mengimpor SDK dan memanggil fungsi bantuannya. SDK menyediakan dua metode berguna:

1. `ai.list_local()` – mengembalikan daftar Python berisi identifier model yang sudah di‑cache.
2. `ai.get_local_path()` – mengembalikan direktori absolut tempat file‑file model tersebut berada.

Kedua pemanggilan bersifat sinkron dan akan mengeluarkan `AIError` yang jelas jika ada yang salah, sehingga penanganan error menjadi sederhana.

> **Mengapa menggunakan fungsi‑fungsi ini?**  
> Mengetahui kumpulan model yang di‑cache secara tepat memungkinkan Anda menghindari unduhan yang tidak perlu, men-debug ketidaksesuaian versi, dan membersihkan artefak lama secara otomatis. Ini merupakan bagian kecil dari alur kerja **AI SDK Python** yang lebih besar, namun dapat menghemat jam‑jam pencarian manual di sistem berkas.

### Langkah 1: Impor AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Mengapa ini penting:* Mengimpor paket mendaftarkan ekstensi C‑underlying dan memuat berkas konfigurasi (seperti jalur cache) dari lingkungan Anda. Melewatkan langkah ini akan memunculkan `ModuleNotFoundError` pada saat Anda memanggil fungsi SDK apa pun.

### Langkah 2: Daftar Semua Model yang Di‑cache

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**Apa yang akan Anda lihat:** Jika Anda memiliki tiga model yang disimpan, outputnya mungkin terlihat seperti:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

Jika cache kosong, Anda akan mendapatkan daftar kosong:

```
Cached models: []
```

> **Tip pro:** Bungkus pemanggilan dalam blok try/except jika Anda curiga SDK belum diinisialisasi dengan benar.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Langkah 3: Dapatkan Direktori Cache Model

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Output tipikal pada sistem mirip Unix:

```
Model cache directory: /home/you/.cache/ai/models
```

Di Windows Anda mungkin melihat sesuatu seperti `C:\Users\you\AppData\Local\ai\models`. Mengetahui jalur ini penting ketika Anda perlu **manage AI model cache** secara manual—misalnya untuk membersihkan versi lama atau menyalin berkas ke drive bersama.

---

## Ringkasan Visual

![Diagram showing how to list cached AI models, retrieve their names, and locate the cache directory](https://example.com/images/list-cached-ai-models.png)

*Alt text:* Diagram yang menggambarkan proses **list cached AI models** menggunakan AI SDK di Python.

---

## Menangani Kasus Tepi dan Kesalahan Umum

### Cache Kosong

Jika `ai.list_local()` mengembalikan daftar kosong, Anda mungkin bertanya-tanya apakah SDK salah konfigurasi. Periksa kembali variabel lingkungan `AI_CACHE_DIR` (atau berkas konfigurasi SDK) untuk memastikan ia menunjuk ke lokasi yang dapat ditulisi.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Masalah Izin

Saat mengakses `ai.get_local_path()`, `PermissionError` dapat muncul pada sistem yang restriktif. Solusinya biasanya menjalankan skrip dengan hak pengguna yang tepat atau menyesuaikan ACL direktori tersebut.

### Ketidaksesuaian Versi

Kadang‑kadang cache berisi versi model yang lebih lama sementara kode Anda meminta versi yang lebih baru. SDK akan otomatis mengunduh versi terbaru, namun Anda dapat mencegahnya dengan memeriksa tag versi dalam daftar:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Membersihkan Model Lama

Jika Anda perlu mengosongkan ruang, Anda dapat menghapus folder model tertentu secara langsung:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

Menjalankan `purge_model('bert-base-uncased')` akan menghapus model tersebut dan membebaskan ruang disk.

---

## Skrip Lengkap yang Dapat Anda Salin‑Tempel

Berikut adalah skrip siap‑jalankan yang menggabungkan semua langkah, menambahkan penanganan error dasar, dan mencetak ringkasan yang ramah.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Output yang diharapkan (ketika cache terisi):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Jalankan skrip dengan `python list_models.py` dan Anda akan langsung mengetahui apa yang ada di disk.

---

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja di semua sistem operasi?**  
J: Ya. SDK mengabstraksi jalur spesifik OS, sehingga `ai.get_local_path()` mengembalikan string yang valid di Linux, macOS, dan Windows.

**T: Bisakah saya daftar model dari cache remote?**  
J: `list_local()` bawaan hanya melaporkan artefak yang disimpan secara lokal. Untuk registri remote Anda dapat menggunakan `ai.list_remote()` (jika versi SDK Anda menyediakannya).

**T: Bagaimana jika nama SDK bukan `ai`?**  
J: Ganti baris impor dengan nama paket yang sebenarnya, misalnya `import myai as ai`. Semua panggilan selanjutnya tetap sama karena kontrak API konsisten di seluruh implementasi.

---

## Kesimpulan

Anda kini memiliki metode yang solid dan siap produksi untuk **list cached AI models** menggunakan pustaka **AI SDK Python**, mendapatkan **model cache directory**, dan bahkan membersihkan berkas lama. Pengetahuan ini membantu Anda menjaga lingkungan tetap rapi, menghindari unduhan berulang, serta men-debug masalah versi dengan mudah.

Siap untuk langkah selanjutnya? Cobalah memperluas skrip untuk secara otomatis mengunduh model yang belum ada, atau integrasikan ke dalam pipeline CI yang memvalidasi kesehatan cache sebelum setiap build. Menjelajahi strategi **manage AI model cache** akan membuat aplikasi berbasis AI Anda lebih cepat dan lebih andal.

Selamat coding, semoga cache Anda tetap ramping!

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}