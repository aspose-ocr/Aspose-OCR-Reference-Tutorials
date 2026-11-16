---
category: general
date: 2026-02-22
description: Pelajari cara menampilkan daftar model yang di‑cache dan dengan cepat
  menampilkan direktori cache di mesin Anda. Termasuk langkah‑langkah untuk melihat
  folder cache dan mengelola penyimpanan model AI lokal.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: id
og_description: Temukan cara untuk menampilkan daftar model yang di‑cache, memperlihatkan
  direktori cache, dan melihat folder cache dalam beberapa langkah mudah. Contoh Python
  lengkap disertakan.
og_title: Daftar model yang di-cache – panduan cepat untuk melihat direktori cache
tags:
- AI
- caching
- Python
- development
title: Daftar model yang di‑cache – cara melihat folder cache dan menampilkan direktori
  cache
url: /id/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# list cached models – panduan cepat untuk melihat direktori cache

Pernah bertanya-tanya bagaimana cara **list cached models** di workstation Anda tanpa harus menggali folder yang tidak jelas? Anda bukan satu-satunya. Banyak pengembang mengalami kebuntuan ketika mereka perlu memverifikasi model AI mana yang sudah disimpan secara lokal, terutama ketika ruang disk terbatas. Kabar baik? Dalam beberapa baris saja Anda dapat **list cached models** dan **show cache directory**, memberi Anda visibilitas penuh ke folder cache Anda.

Dalam tutorial ini kami akan membahas skrip Python yang berdiri sendiri yang melakukan hal tersebut. Pada akhir tutorial Anda akan tahu cara melihat folder cache, memahami di mana cache berada pada berbagai OS, dan bahkan melihat daftar tercetak yang rapi dari setiap model yang telah diunduh. Tanpa dokumentasi eksternal, tanpa tebakan—hanya kode yang jelas dan penjelasan yang dapat Anda salin‑tempel sekarang.

## Apa yang Akan Anda Pelajari

- Cara menginisialisasi klien AI (atau stub) yang menyediakan utilitas caching.  
- Perintah tepat untuk **list cached models** dan **show cache directory**.  
- Di mana cache berada pada Windows, macOS, dan Linux, sehingga Anda dapat menavigasinya secara manual jika diinginkan.  
- Tips untuk menangani kasus tepi seperti cache kosong atau jalur cache khusus.  

**Prerequisites** – Anda memerlukan Python 3.8+ dan klien AI yang dapat di‑install via pip yang mengimplementasikan `list_local()`, `get_local_path()`, dan opsional `clear_local()`. Jika Anda belum memilikinya, contoh ini menggunakan kelas mock `YourAIClient` yang dapat Anda ganti dengan SDK sebenarnya (misalnya, `openai`, `huggingface_hub`, dll.).  

Siap? Mari kita mulai.

## Langkah 1: Siapkan Klien AI (atau Mock)

Jika Anda sudah memiliki objek klien, lewati blok ini. Jika tidak, buatlah stand‑in kecil yang meniru antarmuka caching. Ini membuat skrip dapat dijalankan bahkan tanpa SDK nyata.

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Pro tip:** Jika Anda sudah memiliki klien nyata (misalnya, `from huggingface_hub import HfApi`), cukup ganti pemanggilan `YourAIClient()` dengan `HfApi()` dan pastikan metode `list_local` dan `get_local_path` ada atau dibungkus sesuai.

## Langkah 2: **list cached models** – ambil dan tampilkan

Sekarang klien sudah siap, kita dapat memintanya untuk menenumerasi semua yang diketahui secara lokal. Ini adalah inti dari operasi **list cached models** kami.

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Expected output** (dengan data dummy dari langkah 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

Jika cache kosong Anda hanya akan melihat:

```
Cached models:
```

Baris kosong kecil itu memberi tahu Anda bahwa belum ada yang disimpan—berguna saat Anda menulis skrip pembersihan.

## Langkah 3: **show cache directory** – di mana cache berada?

Mengetahui jalur seringkali setengah dari pertempuran. Sistem operasi yang berbeda menempatkan cache di lokasi default yang berbeda, dan beberapa SDK memungkinkan Anda menggantinya melalui variabel lingkungan. Potongan kode berikut mencetak jalur absolut sehingga Anda dapat `cd` ke dalamnya atau membukanya di penjelajah file.

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Typical output** pada sistem mirip Unix:

```
Cache directory: /home/youruser/.ai_cache
```

Di Windows Anda mungkin melihat sesuatu seperti:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

Sekarang Anda tahu persis **how to view cache folder** pada platform apa pun.

## Langkah 4: Gabungkan Semua – skrip tunggal yang dapat dijalankan

Berikut adalah program lengkap yang siap dijalankan yang menggabungkan tiga langkah. Simpan sebagai `view_ai_cache.py` dan jalankan `python view_ai_cache.py`.

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

Jalankan dan Anda akan langsung melihat daftar model yang di‑cache **dan** lokasi direktori cache.

## Kasus Tepi & Variasi

| Situation | What to Do |
|-----------|------------|
| **Empty cache** | Skrip akan mencetak “Cached models:” tanpa entri. Anda dapat menambahkan peringatan kondisional: `if not models: print("⚠️ No models cached yet.")` |
| **Custom cache path** | Berikan jalur saat membuat klien: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. Pemanggilan `get_local_path()` akan mencerminkan lokasi khusus tersebut. |
| **Permission errors** | Pada mesin dengan batasan, klien mungkin mengeluarkan `PermissionError`. Bungkus inisialisasi dalam blok `try/except` dan gunakan direktori yang dapat ditulis pengguna sebagai fallback. |
| **Real SDK usage** | Ganti `YourAIClient` dengan kelas klien yang sebenarnya dan pastikan nama metode cocok. Banyak SDK menyediakan atribut `cache_dir` yang dapat Anda baca langsung. |

## Pro Tips untuk Mengelola Cache Anda

- **Periodic cleanup:** Jika Anda sering mengunduh model besar, jadwalkan cron job yang memanggil `shutil.rmtree(ai.get_local_path())` setelah memastikan Anda tidak lagi membutuhkannya.  
- **Disk usage monitoring:** Gunakan `du -sh $(ai.get_local_path())` di Linux/macOS atau `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` di PowerShell untuk memantau ukuran.  
- **Versioned folders:** Beberapa klien membuat subfolder per versi model. Saat Anda **list cached models**, Anda akan melihat setiap versi sebagai entri terpisah—gunakan itu untuk memangkas revisi lama.  

## Gambaran Visual

![list cached models screenshot](https://example.com/images/list-cached-models.png "list cached models – console output showing models and cache path")

*Alt text:* *list cached models – output konsol yang menampilkan nama model yang di‑cache dan jalur direktori cache.*

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **list cached models**, **show cache directory**, dan secara umum **how to view cache folder** pada sistem apa pun. Skrip singkat ini menunjukkan solusi lengkap yang dapat dijalankan, menjelaskan **mengapa** setiap langkah penting, dan menawarkan tips praktis untuk penggunaan dunia nyata.  

Selanjutnya, Anda mungkin ingin menjelajahi **how to clear the cache** secara programatik, atau mengintegrasikan panggilan ini ke dalam pipeline deployment yang lebih besar yang memvalidasi ketersediaan model sebelum meluncurkan pekerjaan inferensi. Bagaimanapun, Anda kini memiliki dasar untuk mengelola penyimpanan model AI lokal dengan percaya diri.  

Ada pertanyaan tentang SDK AI tertentu? Tinggalkan komentar di bawah, dan selamat mengelola cache!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}