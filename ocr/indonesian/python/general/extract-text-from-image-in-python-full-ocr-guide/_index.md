---
category: general
date: 2026-06-25
description: Ekstrak teks dari gambar menggunakan OCR Python. Pelajari cara memuat
  gambar untuk OCR, melakukan OCR di Python, dan mengonversi struk menjadi JSON dalam
  beberapa langkah sederhana.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: id
og_description: Ekstrak teks dari gambar menggunakan OCR Python. Tutorial ini memandu
  Anda melalui memuat gambar untuk OCR, melakukan OCR di Python, dan mengonversi struk
  menjadi JSON.
og_title: Ekstrak Teks dari Gambar dengan Python – Panduan OCR Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Ekstrak Teks dari Gambar dengan Python – Panduan OCR Lengkap
url: /id/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Image in Python – Full OCR Guide

Pernah perlu **mengekstrak teks dari gambar** tapi tidak yakin harus mulai dari mana? Pada tutorial ini kami akan memandu Anda melalui cara **memuat gambar untuk OCR**, **melakukan OCR di Python**, dan **mengonversi receipt ke JSON**—semua dengan hanya beberapa baris kode.

Jika Anda pernah membuat aplikasi pemindaian receipt, pelacak pengeluaran, atau sekadar ingin mengotomatisasi entri data, Anda akan melihat mengapa menguasai alur ini sangat penting. Pada akhir tutorial Anda akan memiliki skrip yang membaca foto receipt dan menghasilkan payload JSON bersih yang siap dipakai oleh layanan downstream.

## What You’ll Learn

Kami akan membahas setiap langkah mulai dari menginstal pustaka `aocr` hingga menangani hasil mentah. Secara khusus Anda akan belajar cara:

1. **Create an OCR engine instance** – titik masuk untuk semua pekerjaan pengenalan.  
2. **Load an image for OCR** – memberi tahu engine file mana yang akan dibaca.  
3. **Choose the export format** – JSON atau XML, kami pilih JSON karena lebih mudah dikonsumsi.  
4. **Run the recognition** – benar‑benarnya melakukan OCR di Python.  
5. **Print or store the result** – mengonversi receipt ke JSON dan melihat outputnya.

Tidak diperlukan pengalaman sebelumnya dengan OCR; hanya setup Python dasar dan sebuah file gambar (receipt, flyer, apa saja yang Anda butuhkan).  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="extract text from image using Python OCR"}

## Extract Text from Image – Step‑by‑Step Python OCR

Berikut adalah skrip lengkap yang siap dijalankan. Silakan salin‑tempel ke file bernama `receipt_ocr.py` dan jalankan `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Why This Works

- **Engine instance** – `aocr.OcrEngine()` mengenkapsulasi semua pekerjaan berat (pemuatan model, pra‑pemrosesan, dll.).  
- **Loading the image** – `engine.load_image()` memberi tahu pustaka tepat bitmap mana yang akan dianalisis; Anda dapat memberi JPEG, PNG, atau bahkan PDF multi‑halaman.  
- **Export format** – Menetapkan `engine.export_format` ke `aocr.ExportFormat.JSON` membuat hasil menjadi string terstruktur, sempurna untuk API yang mengharapkan JSON.  
- **Recognition call** – `engine.recognize()` menjalankan inferensi jaringan saraf di belakang layar; ia mengembalikan string JSON yang berisi blok teks yang terdeteksi, skor kepercayaan, dan informasi tata letak.  

---

## Load Image for OCR with aocr

Jika Anda bertanya‑tanya apakah gambar memerlukan pra‑pemrosesan khusus, jawab singkatnya **tidak**—`aocr` menangani sebagian besar kasus umum (penyesuaian kontras, deskewing) secara otomatis. Namun, Anda dapat meningkatkan akurasi dengan:

- Memastikan gambar setidaknya 300 dpi.  
- Memotong tepi yang tidak relevan.  
- Mengonversi ke grayscale sebelum memberi ke library (opsional, `engine.load_image()` akan melakukannya untuk Anda).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro tip:* Jika receipt mengandung banyak noise, langkah tambahan di atas dapat meningkatkan **perform OCR in Python** secara signifikan.

---

## Choose Export Format and Convert Receipt to JSON

Anda mungkin bertanya, “Mengapa tidak langsung mendapatkan teks biasa?” Karena JSON mempertahankan struktur hierarki (baris, kata, bounding box). Ini membuat pemetaan bidang seperti *total amount* atau *date* menjadi jauh lebih mudah nantinya.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Saat Anda menjalankan skrip, `json_result` akan terlihat seperti ini (dipangkas untuk singkat):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Sekarang Anda memiliki payload **convert receipt to JSON** yang dapat langsung dimasukkan ke basis data, endpoint REST, atau model machine‑learning.

---

## Run Recognition and Retrieve Results

Langkah terakhir—memang benar‑benarnya melakukan OCR—semudah memanggil `recognize()`. Di balik layar pustaka:

1. Mengirim gambar melalui jaringan konvolusional yang telah dilatih.  
2. Mendekode output jaringan menjadi karakter yang dapat dibaca.  
3. Mengemas semuanya ke dalam format yang dipilih (JSON dalam kasus kami).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Jika Anda perlu menyimpan output alih‑alih mencetaknya, cukup tulis ke file:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Edge case:* Beberapa receipt mengandung karakter non‑ASCII (misalnya “€”). Pastikan Anda membuka file dengan encoding UTF‑8, seperti yang ditunjukkan di atas, untuk menghindari teks yang rusak.

---

## Full Working Example (All Steps in One Script)

Menggabungkan semuanya, berikut skrip akhir yang dapat Anda jalankan dari awal hingga akhir:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Jalankan dengan:

```bash
python receipt_ocr.py
```

Anda akan melihat baris konfirmasi dan, di folder yang sama, file `receipt_output.json` yang berisi data terstruktur.

---

## Conclusion

Anda kini tahu **cara mengekstrak teks dari gambar** menggunakan Python, **cara memuat gambar untuk OCR**, **cara melakukan OCR di Python**, dan **cara mengonversi receipt ke JSON** untuk konsumsi downstream. Alur end‑to‑end ini ringan, hanya memerlukan paket `aocr`, dan dapat dimasukkan ke dalam pipeline otomatisasi apa pun.

Apa selanjutnya? Coba ubah format ekspor ke XML, bereksperimen dengan teknik pra‑pemrosesan gambar yang berbeda, atau bangun API Flask kecil yang menerima receipt yang di‑upload dan langsung mengembalikan payload JSON. Langit adalah batasnya setelah Anda menguasai dasar‑dasarnya.

Ada pertanyaan atau mengalami kendala? Tinggalkan komentar di bawah, dan selamat coding!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}