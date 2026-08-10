---
category: general
date: 2026-04-26
description: Cara memproses hasil OCR dan mengekstrak teks dengan koordinat. Pelajari
  solusi langkah demi langkah menggunakan output terstruktur dan koreksi AI.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: id
og_description: Cara memproses hasil OCR dan mengekstrak teks dengan koordinat. Ikuti
  tutorial komprehensif ini untuk alur kerja yang andal.
og_title: Cara Memproses Ulang OCR – Panduan Lengkap
tags:
- OCR
- Python
- AI
- Text Extraction
title: Cara Memproses Pasca OCR – Mengekstrak Teks dengan Koordinat di Python
url: /id/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Memproses Ulang OCR – Mengekstrak Teks dengan Koordinat di Python

Pernahkah Anda perlu **cara memproses ulang OCR** karena output mentahnya berisik atau tidak sejajar? Anda bukan satu-satunya. Dalam banyak proyek dunia nyata—pemindaian faktur, digitalisasi kwitansi, atau bahkan menambah pengalaman AR—mesin OCR memberi Anda kata‑kata mentah, tetapi Anda tetap harus membersihkannya dan melacak di mana setiap kata berada di halaman. Di sinilah mode output terstruktur yang dikombinasikan dengan post‑processor berbasis AI bersinar.

> **Pro tip:** Jika Anda menggunakan perpustakaan OCR yang berbeda, cari mode “structured” atau “layout”; konsepnya tetap sama.

---

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.9+ | Sintaks modern dan petunjuk tipe |
| `ocr` library that supports `OutputMode.STRUCTURED` (e.g., a fictional `myocr`) | Perpustakaan `ocr` yang mendukung `OutputMode.STRUCTURED` (misalnya, `myocr` fiktif) |
| Needed for bounding‑box data | Diperlukan untuk data kotak‑pembatas |
| An AI post‑processing module (could be OpenAI, HuggingFace, or a custom model) | Modul post‑processing AI (bisa OpenAI, HuggingFace, atau model kustom) |
| Improves accuracy after OCR | Meningkatkan akurasi setelah OCR |
| An image file (`input.png`) in your working directory | File gambar (`input.png`) di direktori kerja Anda |
| The source we’ll read | Sumber yang akan kami baca |

Jika ada yang terdengar tidak familiar, cukup instal paket placeholder dengan `pip install myocr ai‑postproc`. Kode di bawah juga menyertakan stub fallback sehingga Anda dapat menguji alur tanpa perpustakaan sebenarnya.

---

## Langkah 1: Aktifkan Mode Output Terstruktur untuk Mesin OCR  

Hal pertama yang kami lakukan adalah memberi tahu mesin OCR untuk memberikan lebih dari sekadar teks biasa. Output terstruktur mengembalikan setiap kata beserta kotak‑pembatas dan skor kepercayaan, yang penting untuk **mengekstrak teks dengan koordinat** nanti.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Mengapa ini penting:* Tanpa mode terstruktur Anda hanya akan mendapatkan string panjang, dan Anda akan kehilangan informasi spasial yang dibutuhkan untuk menumpangkan teks pada gambar atau memberi analisis tata letak selanjutnya.

---

## Langkah 2: Kenali Gambar dan Tangkap Kata, Kotak, serta Kepercayaan  

Sekarang kami memasukkan gambar ke dalam mesin. Hasilnya adalah sebuah objek yang berisi daftar objek kata, masing‑masing memiliki `text`, `x`, `y`, `width`, `height`, dan `confidence`.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Kasus tepi:* Jika gambar kosong atau tidak dapat dibaca, `structured_result.words` akan menjadi daftar kosong. Sebaiknya periksa hal ini dan tangani dengan baik.

---

## Langkah 3: Jalankan Post‑Processing Berbasis AI Sambil Mempertahankan Posisi  

Bahkan mesin OCR terbaik membuat kesalahan—misalnya “O” vs. “0” atau diakritik yang hilang. Model AI yang dilatih pada teks spesifik domain dapat memperbaiki kesalahan tersebut. Yang penting, kami mempertahankan koordinat asli sehingga tata letak spasial tetap utuh.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Mengapa kami mempertahankan koordinat:* Banyak tugas selanjutnya (misalnya, pembuatan PDF, pelabelan AR) bergantung pada penempatan yang tepat. AI hanya mengubah bidang `text`, meninggalkan `x`, `y`, `width`, `height` tidak tersentuh.

---

## Langkah 4: Iterasi Kata yang Diperbaiki dan Tampilkan Teksnya dengan Koordinat  

Akhirnya, kami mengulangi kata‑kata yang telah diperbaiki dan mencetak setiap kata bersama sudut kiri‑atasnya `(x, y)`. Ini memenuhi tujuan **mengekstrak teks dengan koordinat**.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**Output yang diharapkan (contoh):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

Setiap baris menampilkan kata yang telah diperbaiki dan lokasinya yang tepat pada gambar asli.

---

## Contoh Kerja Lengkap  

Berikut adalah satu skrip yang menggabungkan semuanya. Anda dapat menyalin‑tempelnya, menyesuaikan pernyataan impor agar cocok dengan perpustakaan Anda yang sebenarnya, dan menjalankannya langsung.

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**Menjalankan skrip**

```bash
python ocr_postprocess_demo.py
```

Jika Anda memiliki perpustakaan nyata yang terinstal, skrip akan memproses `input.png` Anda. Jika tidak, implementasi stub memungkinkan Anda melihat alur dan output yang diharapkan tanpa ketergantungan eksternal.

---

## Pertanyaan yang Sering Diajukan (FAQ)

| Pertanyaan | Jawaban |
|------------|---------|
| *Apakah ini bekerja dengan Tesseract?* | Tesseract sendiri tidak menyediakan mode terstruktur secara bawaan, tetapi pembungkus seperti `pytesseract.image_to_data` mengembalikan kotak‑pembatas yang dapat Anda masukkan ke dalam post‑processor AI yang sama. |
| *Bagaimana jika saya membutuhkan sudut kanan‑bawah alih‑alih sudut kiri‑atas?* | Setiap objek kata juga menyediakan `width` dan `height`. Hitung `x2 = x + width` dan `y2 = y + height` untuk mendapatkan sudut yang berlawanan. |
| *Bisakah saya memproses banyak gambar secara batch?* | Tentu saja. Bungkus langkah‑langkah dalam loop `for image_path in Path("folder").glob("*.png"):` dan kumpulkan hasil per file. |
| *Bagaimana saya memilih model AI untuk koreksi?* | Untuk teks umum, GPT‑2 kecil yang di‑fine‑tune pada kesalahan OCR bekerja. Untuk data spesifik domain (misalnya resep medis), latih model sequence‑to‑sequence pada data berpasangan noisy‑clean. |
| *Apakah skor kepercayaan berguna setelah koreksi AI?* | Anda masih dapat menyimpan kepercayaan asli untuk debugging, tetapi AI mungkin mengeluarkan kepercayaan sendiri jika model mendukungnya. |

---

## Kasus Tepi & Praktik Terbaik  

1. **Gambar kosong atau rusak** – selalu verifikasi bahwa `structured_result.words` tidak kosong sebelum melanjutkan.  
2. **Skrip non‑Latin** – pastikan mesin OCR Anda dikonfigurasi untuk bahasa target; post‑processor AI harus dilatih pada skrip yang sama.  
3. **Kinerja** – koreksi AI dapat memakan biaya tinggi. Cache hasil jika Anda akan menggunakan kembali gambar yang sama, atau jalankan langkah AI secara asynchronous.  
4. **Sistem koordinat** – perpustakaan OCR mungkin menggunakan asal yang berbeda (kiri‑atas vs. kiri‑bawah). Sesuaikan sesuai kebutuhan saat menumpangkan pada PDF atau kanvas.  

---

## Kesimpulan  

Anda kini memiliki resep menyeluruh yang solid untuk **cara memproses ulang OCR** dan secara andal **mengekstrak teks dengan koordinat**. Dengan mengaktifkan output terstruktur, mengalirkan hasil melalui lapisan koreksi AI, dan mempertahankan kotak‑pembatas asli, Anda dapat mengubah pemindaian OCR yang berisik menjadi teks bersih yang sadar spasial, siap untuk tugas selanjutnya seperti pembuatan PDF, otomatisasi entri data, atau overlay realitas tertambah.

Siap untuk langkah selanjutnya? Coba ganti AI stub dengan panggilan OpenAI `gpt‑4o‑mini`, atau integrasikan pipeline ke dalam FastAPI

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}