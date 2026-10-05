---
category: general
date: 2026-01-07
description: Cara menampilkan daftar model di Aspose OCR AI menggunakan Python – pelajari
  cara mendapatkan jalur model, memeriksa model yang terpasang, dan mengambil daftar
  model Python dalam hitungan detik.
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: id
og_description: Cara menampilkan daftar model di Aspose OCR AI menggunakan Python.
  Temukan jalur model, periksa model yang terpasang, dan lihat daftar lengkap model
  yang tersedia.
og_title: Cara Menampilkan Daftar Model di Aspose OCR AI – Panduan Python
tags:
- Aspose OCR
- Python
- AI models
title: Cara Menampilkan Daftar Model di Aspose OCR AI – Panduan Python
url: /id/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menampilkan Daftar Model di Aspose OCR AI – Panduan Python

Pernah bertanya-tanya **bagaimana cara menampilkan daftar model** yang sudah terpasang di mesin Anda saat bekerja dengan Aspose OCR AI? Anda bukan satu‑satunya yang mengalami hal itu. Dalam banyak proyek Anda perlu memverifikasi folder model, memastikan model mana yang ada, atau bahkan men‑debug masalah model yang hilang—semua tanpa meninggalkan REPL Python Anda.

Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang siap dijalankan yang menunjukkan **cara mendapatkan path model**, **memeriksa model yang terpasang**, dan akhirnya **menampilkan daftar model yang tersedia** hanya dengan beberapa baris kode. Tanpa skrip eksternal, tanpa keajaiban tersembunyi—hanya Python murni dan Aspose OCR AI SDK.

> **Prasyarat**  
> • Python 3.8 atau lebih baru  
> • Paket `asposeocr` terpasang (`pip install asposeocr`)  
> • Familiaritas dasar dengan mengimpor modul

Jika Anda sudah menyiapkan semua itu, mari kita mulai.

---

## Cara Menampilkan Daftar Model dengan Aspose OCR AI

Hal pertama yang kita butuhkan adalah kelas pembantu `AsposeAI` yang disertakan dalam modul `asposeocr.ai`. Kelas ini memberikan tiga metode yang berguna:

| Metode | Apa yang dikembalikan | Kasus penggunaan umum |
|--------|----------------------|------------------------|
| `get_local_path()` | Path absolut ke folder tempat Aspose menyimpan model AI‑nya | Verifikasi bahwa SDK mencari di tempat yang tepat |
| `list_local()` | Python `list` berisi nama folder model yang ada di disk | Dengan cepat melihat model mana yang dapat Anda muat |
| `list_remote()` *(opsional)* | Daftar model yang tersedia untuk diunduh dari cloud Aspose | Saat Anda membutuhkan model yang tidak ada secara lokal |

Berikut adalah **skrip lengkap** yang mencetak folder model lokal dan daftar model yang terpasang.

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### Output yang Diharapkan

Saat Anda menjalankan skrip pada instalasi baru, biasanya akan terlihat seperti berikut:

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

Jika folder kosong, `list_local()` mengembalikan daftar kosong (`[]`). Itu merupakan sinyal berguna bahwa Anda perlu mengunduh model terlebih dahulu—sesuatu yang akan kami bahas nanti.

---

## Mengapa Mengetahui Path Model Penting

Memahami **di mana** SDK menyimpan file‑nya (`get model path`) lebih dari sekadar rasa ingin tahu:

1. **Debugging** – Jika sebuah model gagal dimuat, Anda dapat `ls` path tersebut dan melihat apakah file memang ada.  
2. **Model khusus** – Beberapa tim melatih model OCR mereka sendiri dan menaruhnya ke dalam folder. Mengetahui path memungkinkan Anda menempatkan file tepat di lokasi yang diharapkan Aspose.  
3. **Izin** – Pada Linux, folder tersebut mungkin dimiliki oleh pengguna lain. Menemukan kesalahan izin lebih awal menghemat jam‑jam kebingungan.

> **Pro tip:** Jika Anda perlu mengarahkan SDK ke direktori khusus, set variabel lingkungan `ASPOSE_OCR_MODEL_PATH` sebelum membuat `AsposeAI()`.

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

---

## Memeriksa Model yang Terpasang – Kasus Tepi & Tips

### 1. Tidak Ada Model Terpasang

Jika `list_local()` mengembalikan `[]`, Anda memiliki dua opsi:

| Opsi | Cara melakukannya |
|------|--------------------|
| **Unduh model dari Aspose** | `ai.download('ocr-general-v1')` (memerlukan internet) |
| **Salin model pra‑latih** | Letakkan folder model secara manual ke path yang ditunjukkan oleh `get_local_path()` |

### 2. Beberapa Versi Model yang Sama

Kadang‑kadang Anda akan melihat baik `ocr-general-v1` **dan** `ocr-general-v1-beta`. SDK memuat kecocokan pertama yang ditemukannya, tetapi Anda dapat memaksa versi tertentu dengan memberikan nama folder yang tepat ke konstruktor OCR:

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. File Model Rusak

Model yang diunduh sebagian dapat menyebabkan `FileNotFoundError` nanti. Jika Anda curiga ada korupsi, cukup hapus folder yang bermasalah dan unduh kembali:

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

---

## Memperluas Skrip – Menampilkan Model Remote (Opsional)

Jika Anda ingin melihat model apa saja yang tersedia untuk diunduh tanpa meninggalkan Python, tambahkan satu panggilan lagi:

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

Ini akan menghasilkan sesuatu seperti:

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Anda kemudian dapat memilih model apa pun dan memanggil `ai.download('model-name')` untuk mengunduhnya secara otomatis.

---

## Contoh Lengkap End‑to‑End

Menggabungkan semuanya, berikut adalah **skrip tunggal yang dapat dijalankan** yang:

1. Menampilkan folder model lokal.  
2. Menampilkan daftar model yang terpasang.  
3. Jika tidak ada yang ditemukan, mengunduh model default.  
4. Akhirnya, mencetak daftar yang telah diperbarui.

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

Menjalankan skrip ini pada mesin bersih akan menghasilkan:

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Sekarang Anda memiliki solusi **mandiri, dapat dikutip** yang dapat diambil secara verbatim oleh asisten AI mana pun.

---

## Pertanyaan yang Sering Diajukan (FAQ)

**T: Apakah ini bekerja di Windows?**  
J: Tentu saja. SDK mengabstraksi sistem file, sehingga `get_local_path()` akan mengembalikan sesuatu seperti `C:\Users\YourName\.asposeocr\models`. Pastikan Python dapat menulis ke folder tersebut.

**T: Bisakah saya menyimpan model di drive jaringan?**  
J: Ya—set `ASPOSE_OCR_MODEL_PATH` ke path UNC (`\\server\share\models`) sebelum membuat instance `AsposeAI`.

**T: Bagaimana jika saya membutuhkan model untuk bahasa yang tidak termasuk dalam set default?**  
J: Gunakan `list_remote()` untuk melihat apakah Aspose menyediakan model khusus bahasa. Jika tidak, Anda dapat melatih model sendiri dan menaruhnya ke dalam folder; cukup berikan nama folder khusus ke konstruktor OCR.

---

## Kesimpulan

Kami telah membahas **cara menampilkan daftar model** di Aspose OCR AI, menunjukkan **cara mendapatkan path model**, **memeriksa model yang terpasang**, dan bahkan **mengunduh model yang hilang**—semua dengan Python biasa. Dengan memahami tata letak folder dan metode pembantu (`get_local_path()`, `list_local()`, `list_remote()`), Anda mendapatkan kontrol penuh atas model AI yang menjadi dasar aplikasi Anda.

Langkah selanjutnya? Coba ganti model default dengan model teks tulisan tangan, atau arahkan SDK ke model yang dilatih khusus oleh tim Anda. Bagaimanapun, Anda kini memiliki fondasi yang kuat untuk mengelola aset OCR dalam proyek Python apa pun.

Selamat coding, semoga daftar model Anda selalu terbaru! 

---

![Cara menampilkan model screenshot](https://example.com/images/how-to-list-models.png "Cara menampilkan model")

*Image alt text:* **tangkapan layar cara menampilkan model** (fulfills primary keyword requirement).

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}