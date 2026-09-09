---
category: general
date: 2026-01-12
description: Jalankan OCR pada file PNG dengan cepat menggunakan Python. Pelajari
  cara mengekstrak teks dari gambar dan faktur, serta memuat gambar untuk OCR menggunakan
  Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: id
og_description: Jalankan OCR pada PNG secara instan. Panduan ini menunjukkan cara
  mengekstrak teks dari gambar dan faktur, memuat gambar untuk OCR, dan menyimpan
  hasil sebagai JSON dan CSV.
og_title: Jalankan OCR pada PNG – Tutorial Python Lengkap
tags:
- OCR
- Python
- Image Processing
title: Jalankan OCR pada PNG – Panduan Python Lengkap untuk Mengekstrak Teks dari
  Gambar
url: /id/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada PNG – Panduan Python Lengkap untuk Mengekstrak Teks dari Gambar

Pernah membutuhkan untuk **run OCR on PNG** tetapi tidak yakin pustaka mana yang akan memberikan hasil bersih dan terstruktur? Anda tidak sendirian. Dalam banyak proyek dunia‑nyata—misalnya otomatisasi faktur atau pemindaian struk—langkah pertama adalah **extract text from image** dari file gambar, dan PNG adalah format umum karena mempertahankan kualitas lossless.

Dalam tutorial ini kami akan membimbing Anda melalui contoh praktis menggunakan paket Aspose.OCR Python. Pada akhir panduan Anda akan tahu cara **load image for OCR**, mengambil setiap baris teks, mengubah data tersebut menjadi objek JSON yang rapi, dan bahkan mengekspornya ke CSV untuk pemrosesan lanjutan. Tanpa basa‑basi, hanya solusi praktis yang siap dijalankan.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mengimpor pustaka Aspose.OCR.  
- Langkah‑langkah tepat untuk **run OCR on PNG** dan menangani objek hasil.  
- Cara **extract text from invoice** dan memformat output sebagai JSON atau CSV.  
- Tips menangani gambar dengan kontras rendah, dokumen multibahasa, dan skor kepercayaan.  
- Contoh kode lengkap yang dapat Anda salin‑tempel dan jalankan hari ini.

> **Prerequisite:** Python 3.8+ dan pemahaman dasar tentang pip. Jika Anda belum pernah menggunakan Aspose sebelumnya, jangan khawatir—panduan ini mencakup semua yang Anda perlukan untuk memulai.

---

## Langkah 1 – Instal Aspose.OCR dan Siapkan Lingkungan Anda

Sebelum kita dapat **run OCR on PNG**, pustaka harus sudah terpasang di sistem Anda.

```bash
pip install aspose-ocr
```

> **Pro tip:** Gunakan lingkungan virtual (`python -m venv venv`) untuk menjaga dependensi terisolasi. Ini mencegah bentrok versi jika Anda mengelola banyak proyek.

Setelah terinstal, impor modul‑modul yang diperlukan:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Di sini kami mengimpor `asposeocr` untuk melakukan pekerjaan berat dan pustaka bawaan `json` untuk serialisasi selanjutnya.

---

## Langkah 2 – Buat Mesin OCR dan Atur Bahasa

Mesin OCR adalah komponen inti yang benar‑benar membaca piksel. Untuk kebanyakan faktur berbahasa Inggris, Anda akan membutuhkan paket bahasa Inggris:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Why this matters:** Menentukan bahasa mempersempit set karakter, yang meningkatkan akurasi dan mempercepat pemrosesan. Jika Anda perlu menangani faktur multibahasa, cukup ganti `ocr.Language.ENGLISH` dengan enum yang sesuai.

---

## Langkah 3 – Muat Gambar untuk OCR

Sekarang kami akan **load image for OCR**. Metode `Image.load` menerima jalur file, dan bekerja dengan PNG, JPEG, BMP, dan lainnya.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Edge case:** Jika PNG berukuran sangat besar (lebih dari 5 MB), pertimbangkan untuk mengubah ukurannya terlebih dahulu agar penggunaan memori tetap wajar. Pillow dapat melakukannya dalam satu baris:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Langkah 4 – Jalankan OCR pada PNG dan Tangkap Hasilnya

Dengan mesin siap dan gambar sudah dimuat, saatnya **run OCR on PNG** dan mengambil hasil terstruktur.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

Objek `ocr_result` berisi koleksi item `OcrRegion`, masing‑masing dengan teks yang dikenali dan skor kepercayaan (0‑100). Di sinilah Anda mendapatkan data granular yang diperlukan untuk **extract text from invoice**.

---

## Langkah 5 – Konversi Hasil ke JSON dan Cetak dengan Indentasi

Sebagian besar sistem downstream menyukai JSON, jadi kami akan mengubah output OCR menjadi string yang diformat rapi.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Contoh Output

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Perhatikan bagaimana setiap baris menyertakan metrik kepercayaan—sempurna untuk menyaring entri dengan kepercayaan rendah jika Anda berencana **extract text from invoice** secara otomatis.

---

## Langkah 6 – Simpan Data OCR sebagai CSV (Satu Baris per Teks + Kepercayaan)

CSV ideal untuk spreadsheet atau impor data cepat. Aspose menyediakan satu baris kode untuk mengekspor semuanya ke file CSV.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

CSV yang dihasilkan akan terlihat seperti ini:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Sekarang Anda dapat membukanya di Excel, Google Sheets, atau memasukkannya ke dalam basis data.

---

## Bonus – Menangani Teks dengan Kepercayaan Rendah dan PDF Multi‑Halaman

### Penyaringan berdasarkan Kepercayaan

Jika Anda hanya menginginkan baris dengan kepastian tinggi, saring JSON sebelum menuliskannya:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Dokumen Multi‑Halaman

Aspose.OCR secara otomatis membuat entri `page` baru untuk setiap halaman dalam PNG atau PDF multi‑halaman. Loop melalui `ocr_data["pages"]` untuk memproses semuanya—tanpa kode tambahan diperlukan.

---

## Contoh Skrip Lengkap yang Berfungsi

Berikut adalah **complete script** yang dapat Anda salin, tempel, dan jalankan segera. Ganti `YOUR_DIRECTORY` dengan folder yang berisi file PNG Anda.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Jalankan skrip dengan `python run_ocr.py` dan Anda akan melihat dump JSON di konsol, file CSV di disk, serta daftar entri dengan kepercayaan tinggi yang telah disaring.

---

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan ini untuk mengekstrak teks dari struk yang dipindai alih‑alih faktur?**  
A: Tentu saja. Alur kerja yang sama berlaku—cukup arahkan `image_path` ke PNG struk Anda. Jika struk menggunakan bahasa lain, ubah `engine.language` sesuai kebutuhan.

**Q: Bagaimana jika PNG saya berisi teks yang diputar?**  
A: Aspose.OCR secara otomatis mendeteksi orientasi, tetapi untuk kasus yang sulit Anda dapat memutar gambar secara manual dengan Pillow sebelum memberikannya ke mesin.

**Q: Apakah saya memerlukan lisensi berbayar untuk Aspose.OCR?**  
A: Pustaka ini menyediakan mode evaluasi gratis dengan watermark pada output. Untuk penggunaan produksi Anda memerlukan lisensi, yang dapat diperoleh dari situs web Aspose.

---

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **run OCR on PNG** menggunakan Python: menginstal SDK, memuat gambar, mengekstrak teks terstruktur, dan menyimpan hasil sebagai JSON atau CSV. Baik Anda ingin **extract text from image** untuk skrip sederhana atau **extract text from invoice** untuk pipeline akuntansi otomatis, langkah‑langkah di atas memberikan fondasi yang kuat dan siap produksi.

Selanjutnya, Anda dapat menjelajahi:

- Mengintegrasikan output CSV dengan basis data untuk penyimpanan faktur massal.  
- Menambahkan pasca‑pemrosesan dengan ekspresi reguler untuk mengekstrak tanggal, jumlah, atau ID pajak.  
- Menggunakan fitur `ocr_engine.recognize_barcode` jika faktur Anda menyertakan kode QR.

Cobalah, sesuaikan ambang kepercayaan, dan saksikan alur kerja pemrosesan dokumen Anda menjadi lebih mudah. Ada pertanyaan lain atau kasus penggunaan menarik untuk dibagikan? Tinggalkan komentar di bawah—selamat mencoba OCR!

![contoh run OCR pada PNG](run-ocr-on-png.png "run OCR on PNG – contoh visual hasil OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}