---
category: general
date: 2025-12-27
description: Ekstrak teks dari gambar menggunakan Aspose OCR dan perbaiki kesalahan
  OCR. Pelajari cara memuat gambar untuk OCR dan memperbaiki kesalahan dengan cepat.
draft: false
keywords:
- extract text from image
- load image for ocr
- how to correct ocr errors
- Aspose OCR Python
- OCR post‑processing
language: id
og_description: Ekstrak teks dari gambar dengan Aspose OCR dan segera perbaiki kesalahan
  OCR. Ikuti tutorial ini untuk memuat gambar untuk OCR dan membersihkan hasil.
og_title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Lengkap
tags:
- OCR
- Python
- Aspose
- Text Extraction
title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah-demi-Langkah
url: /id/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑demi‑Langkah

Pernah perlu **mengekstrak teks dari gambar** tetapi terjebak dengan output OCR yang berantakan? Anda tidak sendirian. Dalam banyak proyek otomatisasi—seperti pemrosesan faktur, pemindaian kwitansi, atau mendigitalkan dokumen lama—rintangan pertama adalah mendapatkan teks yang bersih dan dapat dicari dari sebuah gambar.  

Dalam tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan cara **memuat gambar untuk OCR**, menjalankan pengenalan, dan kemudian **mengoreksi kesalahan OCR** menggunakan post‑processor pemeriksa ejaan AI‑powered milik Aspose. Pada akhir tutorial Anda akan memiliki satu skrip yang mengubah PNG faktur menjadi teks yang rapi, dapat dicari, dan siap untuk alur kerja downstream apa pun yang Anda miliki.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mengimpor pustaka Aspose OCR dan AI di Python.  
- Kode tepat yang diperlukan untuk **memuat gambar untuk OCR** (tanpa tebak‑tebakan).  
- Cara menjalankan mesin OCR dan menangkap string mentah.  
- Mengapa OCR sering menghasilkan typo dan bagaimana processor pemeriksa ejaan bawaan dapat **mengoreksi kesalahan OCR** secara otomatis.  
- Tips menangani kasus tepi seperti PDF multi‑halaman atau pemindaian beresolusi rendah.

> **Prasyarat:** Python 3.8+, lisensi Aspose OCR yang valid (atau percobaan gratis), dan file gambar (misalnya `invoice.png`) yang ingin Anda proses.

## Ekstrak Teks dari Gambar – Menyiapkan Aspose OCR

Sebelum kita dapat melakukan apa pun, kita memerlukan paket yang tepat. Aspose mendistribusikan mesin OCR‑nya sebagai modul yang dapat di‑install via pip.

```bash
pip install aspose-ocr
```

Jika Anda juga menginginkan post‑processor AI, instal paket pendampingnya:

```bash
pip install aspose-ocr-ai
```

> **Pro tip:** Jaga paket Anda tetap terbaru. Pada saat penulisan ini versi terbaru adalah `aspose-ocr 23.12` dan `aspose-ocr-ai 23.12`.

Setelah pustaka berada di sistem Anda, impor kelas‑kelas yang akan digunakan:

```python
# Step 1: Import the OCR and AI classes
from aspose.ocr import OcrEngine, AsposeAI
```

> **Mengapa ini penting:** Mengimpor kelas spesifik menjaga namespace tetap bersih dan membuat jelas komponen mana yang bertanggung jawab untuk pengenalan versus post‑processing.

## Memuat Gambar untuk OCR – Menyiapkan PNG Faktur Anda

Langkah logis berikutnya adalah menunjuk mesin ke file yang ingin Anda baca. Di sinilah kata kunci **memuat gambar untuk OCR** bersinar.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 3: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Penjelasan:** `OcrEngine()` membuat mesin baru dengan pengaturan default (bahasa Inggris, auto‑rotation, dll.). Metode `load_image()` menerima jalur file, stream, atau bahkan array byte—sehingga Anda dapat memberi gambar dari disk, web, atau buffer dalam memori.

### Kesalahan Umum Saat Memuat Gambar

| Masalah | Gejala | Solusi |
|---------|--------|--------|
| DPI rendah (<300) | Karakter terdistorsi, angka hilang | Resample gambar ke 300 dpi atau lebih tinggi sebelum memuat |
| Mode warna tidak tepat (CMYK) | Bentuk karakter salah | Konversi ke RGB menggunakan Pillow (`Image.convert("RGB")`) |
| PDF multi‑halaman | Hanya halaman pertama yang diproses | Konversi tiap halaman menjadi gambar dan iterasi satu per satu |

## Lakukan OCR dan Dapatkan Teks Mentah

Sekarang mesin tahu di mana gambar berada, kita dapat membacanya.

```python
# Step 4: Perform OCR to extract raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)
```

Pemanggilan `recognize()` mengembalikan string Python biasa. Dalam banyak skenario dunia nyata output akan berisi spasi berlebih, karakter yang salah dibaca, atau pemutusan baris yang rusak—terutama pada kwitansi yang menggunakan font padat.

> **Mengapa kami menangkap raw_text terlebih dahulu:** Ini memberi Anda baseline untuk dibandingkan dengan versi bersih nanti, yang berguna untuk debugging atau audit.

## Cara Mengoreksi Kesalahan OCR – Menggunakan Aspose AI Spell‑Check

Aspose menyediakan wrapper AI ringan yang dapat menjalankan post‑processor pemeriksa ejaan pada output mentah. Ini secara langsung menjawab pertanyaan **cara mengoreksi kesalahan OCR**.

```python
# Step 5: Initialise the AI post‑processor and choose a spell‑check processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")
```

Anda dapat mengganti `"spell_check"` dengan processor lain seperti `"grammar_check"` atau `"named_entity_recognition"` jika kasus penggunaan Anda memerlukannya.

```python
# Step 6: Clean the OCR output using the selected post‑processor
clean_text = ai_processor.run_postprocessor(raw_text)

# Step 7: Output the corrected text
print("\nCorrected OCR output:")
print(clean_text)
```

### Apa yang Dilakukan Spell‑Check di Balik Layar

1. **Tokenisasi** – Memisahkan string mentah menjadi kata dan tanda baca.  
2. **Pencarian Kamus** – Membandingkan tiap token dengan kamus bahasa Inggris (atau kamus khusus yang dapat Anda sediakan).  
3. **Skoring Kontekstual** – Menggunakan model bahasa kecil untuk memutuskan apakah koreksi cocok dengan kata‑kata di sekitarnya.  
4. **Penggantian** – Mengembalikan string baru dengan koreksi paling probabilistik yang diterapkan.

> **Kasus tepi:** Jika bahasa sumber bukan bahasa Inggris, berikan kode bahasa yang sesuai saat membuat `AsposeAI()` (mis., `AsposeAI(language="fr")`).

## Verifikasi dan Gunakan Teks yang Sudah Dibersihkan

Pada titik ini Anda memiliki dua variabel: `raw_text` (dump OCR langsung) dan `clean_text` (versi yang telah diperiksa ejaannya). Pilihan mana yang dipertahankan tergantung pada kebutuhan downstream Anda.

```python
# Example: Save the cleaned text to a .txt file for later indexing
with open("invoice_extracted.txt", "w", encoding="utf-8") as f:
    f.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

Jika Anda menyalurkan hasil ke mesin pencari, basis data, atau model machine‑learning, selalu pilih versi **dibersihkan**—jika tidak, Anda akan menyebarkan noise OCR ke seluruh pipeline.

## Contoh Skrip Lengkap yang Dapat Dijalankan

Berikut adalah skrip lengkap yang dapat Anda salin‑tempel ke file bernama `extract_invoice.py`. Skrip ini mengasumsikan Anda telah menginstal dua paket Aspose dan memiliki gambar di `YOUR_DIRECTORY/invoice.png`.

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

Anda akan melihat dump mentah diikuti oleh versi yang lebih rapi, dan sebuah file bernama `invoice_extracted.txt` akan muncul di folder yang sama.

## Pertanyaan yang Sering Diajukan (FAQ)

**T: Apakah ini bekerja dengan PDF?**  
J: Tidak secara langsung. Konversi tiap halaman PDF menjadi gambar (mis., menggunakan `pdf2image`) dan jalankan skrip pada PNG yang dihasilkan.

**T: Bahasa saya bukan Inggris—apakah saya tetap dapat menggunakan pemeriksa ejaan?**  
J: Ya. Berikan kode bahasa yang diinginkan ke `AsposeAI(language="de")` untuk Jerman, `"es"` untuk Spanyol, dll.

**T: Bagaimana jika mesin OCR salah mendeteksi tata letak tabel?**  
J: Aspose OCR menyediakan flag `set_layout_analysis(True)`. Mengaktifkannya meningkatkan deteksi tabel tetapi dapat menambah waktu pemrosesan.

**T: Bagaimana cara menangani batch yang sangat besar?**  
J: Bungkus logika inti dalam fungsi dan gunakan thread pool atau async IO untuk memparalelkan proses di beberapa core atau mesin.

## Kesimpulan

Kami telah menunjukkan cara **mengekstrak teks dari gambar** menggunakan Aspose OCR, cara **memuat gambar untuk OCR**, dan cara paling sederhana untuk **mengoreksi kesalahan OCR** dengan pemeriksa ejaan AI bawaan. Skrip lengkap yang dapat dijalankan memperlihatkan alur end‑to‑end—from memuat PNG faktur hingga menyimpan file `.txt` yang bersih dan dapat dicari.

Silakan bereksperimen: ganti pemeriksa ejaan dengan koreksi tata bahasa, alirkan output ke classifier NLP, atau integrasikan proses ke sistem manajemen dokumen yang lebih besar. Langit adalah batasnya begitu Anda memiliki teks yang dapat diandalkan dan telah dikoreksi.

Ada pertanyaan lebih lanjut tentang OCR, Aspose, atau otomatisasi Python? Tinggalkan komentar di bawah, dan selamat coding! 

![Contoh ekstrak teks dari gambar](extract_text_image.png "Ekstrak teks dari gambar dengan Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}