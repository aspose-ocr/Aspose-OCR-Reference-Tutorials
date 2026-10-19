---
category: general
date: 2026-02-27
description: Pelajari cara memperbaiki kesalahan OCR dan mengekstrak teks dari gambar
  menggunakan Aspose OCR di Python. Panduan ini menunjukkan cara memuat gambar untuk
  OCR dan membersihkan hasil.
draft: false
keywords:
- extract text from image
- load image for ocr
- how to correct ocr errors
- Aspose OCR Python
- OCR post‑processing
og_description: Pelajari cara memperbaiki kesalahan OCR dan mengekstrak teks dari
  gambar menggunakan Aspose OCR dalam Python. Ikuti tutorial langkah demi langkah
  ini.
og_title: Cara Mengoreksi Kesalahan OCR – Ekstrak Teks dari Gambar dengan Aspose OCR
tags:
- OCR
- Python
- Aspose
- Text Extraction
title: Cara Memperbaiki Kesalahan OCR – Mengekstrak Teks dari Gambar dengan Aspose
  OCR – Panduan Langkah demi Langkah
url: /id/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Memperbaiki Kesalahan OCR – Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah

Jika Anda pernah perlu **mengekstrak teks dari gambar** dalam proyek Python dan berakhir dengan output OCR yang berantakan, Anda berada di tempat yang tepat. Dalam banyak skenario otomasi—pemrosesan faktur, pemindaian struk, atau digitalisasi dokumen bersejarah—tantangan pertama adalah mengubah gambar menjadi teks bersih yang dapat dicari. Tutorial ini menunjukkan **cara memperbaiki kesalahan OCR** menggunakan AI‑powered spell‑check milik Aspose, sekaligus membahas langkah penting untuk **memuat gambar untuk OCR** dan mendapatkan hasil yang dapat diandalkan.

## Jawaban Cepat
- **Pustaka apa yang harus saya gunakan?** Aspose OCR untuk Python  
- **Apakah saya dapat memperbaiki typo secara otomatis?** Ya, dengan AI spell‑check bawaan  
- **Apakah saya memerlukan lisensi?** Versi trial dapat digunakan untuk pengujian; lisensi komersial diperlukan untuk produksi  
- **Apakah kompatibel dengan Python‑3?** Berfungsi dengan Python 3.8 ke atas  
- **Bisakah saya memproses PDF?** Konversi halaman PDF ke gambar terlebih dahulu (lihat “konversi pdf ke gambar untuk ocr”)  

## Apa itu “cara memperbaiki kesalahan OCR”?
Memperbaiki kesalahan OCR berarti mengambil string mentah yang dihasilkan oleh mesin OCR dan secara otomatis memperbaiki ejaan yang salah, karakter yang salah tempat, serta gangguan format sehingga teks dapat digunakan secara andal di tahap berikutnya (pencarian, analitik, atau entri data).

## Mengapa menggunakan Aspose OCR untuk Python?
Aspose OCR menggabungkan mesin pengenalan yang cepat dan akurat dengan AI post‑processor opsional yang menangani pengecekan ejaan dan perbaikan tata bahasa dasar. Ini merupakan **tutorial aspose ocr** lengkap dalam satu paket, memungkinkan Anda beralih dari gambar ke teks bersih tanpa alat pihak ketiga.

## Prasyarat
- Python 3.8+ terpasang  
- Lisensi Aspose OCR yang valid (atau trial gratis)  
- File gambar seperti `invoice.png` yang ingin Anda proses  
- Opsional: `pdf2image` jika Anda perlu **mengonversi pdf ke gambar untuk OCR**  

## Panduan Langkah‑per‑Langkah

### Langkah 1: Instal Aspose OCR dan AI post‑processor
```bash
pip install aspose-ocr
```

```bash
pip install aspose-ocr-ai
```

> **Tip pro:** Jaga paket tetap terbaru. Pada saat penulisan versi terbaru adalah `aspose-ocr 23.12` dan `aspose-ocr-ai 23.12`.

### Langkah 2: Impor kelas yang diperlukan
```python
# Step 1: Import the OCR and AI classes
from aspose.ocr import OcrEngine, AsposeAI
```

### Langkah 3: Buat engine dan **muat gambar untuk OCR**
```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 3: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Penjelasan:** `load_image()` menerima path, stream, atau byte array, sehingga Anda dapat memberi gambar dari disk, web, atau buffer dalam memori.

#### Kesalahan umum saat memuat gambar
| Masalah | Gejala | Perbaikan |
|-------|---------|-----|
| DPI rendah (<300) | Karakter berantakan, angka hilang | Resample ke ≥ 300 dpi sebelum memuat |
| Mode warna CMYK | Bentuk karakter salah | Konversi ke RGB dengan Pillow (`Image.convert("RGB")`) |
| PDF multi‑halaman | Hanya halaman pertama yang diproses | **Konversi PDF ke gambar untuk OCR** menggunakan `pdf2image` dan loop setiap halaman |

### Langkah 4: Jalankan OCR untuk mendapatkan string mentah
```python
# Step 4: Perform OCR to extract raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)
```

### Langkah 5: Inisialisasi prosesor AI spell‑check (inti dari **cara memperbaiki kesalahan OCR**)
```python
# Step 5: Initialise the AI post‑processor and choose a spell‑check processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")
```

Anda dapat mengganti `"spell_check"` dengan `"grammar_check"` atau `"named_entity_recognition"` untuk kasus penggunaan lain.

### Langkah 6: Bersihkan output OCR
```python
# Step 6: Clean the OCR output using the selected post‑processor
clean_text = ai_processor.run_postprocessor(raw_text)

# Step 7: Output the corrected text
print("\nCorrected OCR output:")
print(clean_text)
```

**Apa yang dilakukan spell‑check:** tokenisasi teks, pencarian setiap token dalam kamus bahasa Inggris (atau kamus khusus yang Anda sediakan), penilaian alternatif dengan model bahasa ringan, dan mengembalikan perbaikan yang paling mungkin.

#### Bahasa non‑Inggris
Berikan kode bahasa saat membuat `AsposeAI`, misalnya `AsposeAI(language="fr")` untuk bahasa Prancis.

### Langkah 7: Simpan hasil yang telah dibersihkan
```python
# Example: Save the cleaned text to a .txt file for later indexing
with open("invoice_extracted.txt", "w", encoding="utf-8") as f:
    f.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

### Contoh Skrip Lengkap
Berikut adalah skrip lengkap yang dapat Anda salin‑tempel ke `extract_invoice.py`. Skrip ini mengasumsikan dua paket Aspose telah terinstal dan gambar berada di `YOUR_DIRECTORY/invoice.png`.

```python
# extract_invoice.py
# -------------------------------------------------------------
# Complete example: extract text from image and correct OCR errors
# -------------------------------------------------------------

# 1️⃣ Import required classes
from aspose.ocr import OcrEngine, AsposeAI

# 2️⃣ Create OCR engine and load the target image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

# 3️⃣ Run OCR – get raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)

# 4️⃣ Initialise AI spell‑check post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")

# 5️⃣ Clean the OCR output
clean_text = ai_processor.run_postprocessor(raw_text)

# 6️⃣ Show the corrected result
print("\nCorrected OCR output:")
print(clean_text)

# 7️⃣ Persist the cleaned text for later use
with open("invoice_extracted.txt", "w", encoding="utf-8") as out_file:
    out_file.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

Jalankan dengan:

```bash
python extract_invoice.py
```

Anda akan melihat dump mentah, versi yang telah dirapikan, serta file bernama `invoice_extracted.txt` di folder yang sama.

## Cara memperbaiki kesalahan OCR dalam skenario lain?
- **Pemrosesan batch:** Bungkus logika inti dalam fungsi dan gunakan `concurrent.futures.ThreadPoolExecutor` untuk memparalelkan pemrosesan banyak gambar.  
- **Dokumen PDF:** Gunakan `pdf2image` untuk mengubah setiap halaman menjadi PNG, lalu beri setiap PNG ke skrip. Ini menerapkan alur kerja “konversi pdf ke gambar untuk ocr”.  
- **Kamus khusus:** Berikan daftar istilah domain‑spesifik ke `AsposeAI` melalui `set_custom_dictionary()` untuk meningkatkan akurasi spell‑check pada faktur, laporan medis, dll.

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja langsung dengan PDF?**  
J: Tidak langsung. Konversi setiap halaman PDF ke gambar terlebih dahulu (misalnya dengan `pdf2image`) lalu jalankan skrip OCR pada setiap PNG.

**T: Bahasa sumber saya bukan bahasa Inggris—apakah saya masih dapat menggunakan spell‑check?**  
J: Ya. Inisialisasi `AsposeAI(language="de")` untuk bahasa Jerman, `"es"` untuk bahasa Spanyol, dan seterusnya.

**T: Bagaimana jika mesin OCR salah mendeteksi struktur tabel?**  
J: Aktifkan analisis tata letak dengan `ocr_engine.set_layout_analysis(True)`. Ini meningkatkan deteksi tabel dengan sedikit tambahan waktu pemrosesan.

**T: Bagaimana cara menangani batch sangat besar secara efisien?**  
J: Proses gambar dalam potongan, tulis setiap hasil ke basis data atau antrian pesan, dan pertimbangkan penggunaan async I/O atau multiprocessing untuk memaksimalkan pemanfaatan CPU.

**T: Apakah ada cara menyesuaikan kamus spell‑check?**  
J: Ya. Gunakan `ai_processor.set_custom_dictionary(["Invoice", "VAT", "Subtotal"])` sebelum menjalankan post‑processor.

---

![Contoh ekstrak teks dari gambar](extract_text_image.png "Ekstrak teks dari gambar dengan Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}

---

**Terakhir Diperbarui:** 2026-02-27  
**Diuji Dengan:** Aspose OCR 23.12, Aspose OCR AI 23.12  
**Penulis:** Aspose