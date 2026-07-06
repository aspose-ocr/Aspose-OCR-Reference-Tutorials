---
category: general
date: 2026-06-22
description: Dapatkan koordinat bounding box dari gambar menggunakan Python. Pelajari
  cara mengekstrak teks dari gambar dengan Python menggunakan Aspose OCR dan parsing
  JSON dalam hitungan menit.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: id
og_description: Dapatkan koordinat kotak pembatas dari gambar menggunakan Python.
  Panduan ini menunjukkan cara mengekstrak teks dari gambar dengan Python menggunakan
  Aspose OCR dan mengurai data tata letak.
og_title: Dapatkan Koordinat Bounding Box dari OCR di Python – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Dapatkan Koordinat Bounding Box dari OCR di Python – Panduan Lengkap
url: /id/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Koordinat Bounding Box dari OCR di Python – Panduan Lengkap

Pernah perlu **mendapatkan koordinat bounding box** untuk setiap kata dalam faktur yang dipindai, tapi tidak tahu harus mulai dari mana? Anda tidak sendirian. Dalam banyak proyek otomasi, Anda harus menemukan teks pada gambar untuk menyorot, menyensor, atau memasukkannya ke dalam analitik lanjutan. Kabar baik? Dengan beberapa baris Python dan Aspose.OCR Anda dapat mengambil **teks dan posisi tepatnya** dalam satu proses.

Dalam tutorial ini kami akan menunjukkan contoh praktis yang memperlihatkan cara **mengekstrak teks dari gambar gaya python**, lalu menyelami data tata letak JSON untuk mengambil bounding box tersebut. Tanpa basa‑basi, hanya skrip yang berfungsi, penjelasan mengapa setiap langkah penting, dan tips menghindari jebakan umum.

---

## Apa yang Akan Anda Bangun

Pada akhir panduan ini Anda akan memiliki skrip Python siap‑jalankan yang:

1. Memuat gambar (misalnya, faktur PNG) ke dalam Aspose OCR.  
2. Mengonfigurasi mesin untuk menghasilkan informasi tata letak dalam format JSON.  
3. Mengurai JSON menjadi kamus Python.  
4. Mengiterasi setiap kata yang dikenali, mencetak teks **dan** koordinat bounding box‑nya.

Anda juga akan melihat cara menyesuaikan kode untuk PDF multi‑halaman, format gambar berbeda, dan sistem koordinat khusus.

### Prasyarat

- Python 3.8+ terpasang di mesin Anda.  
- Lisensi aktif Aspose.OCR untuk Python atau percobaan gratis (perpustakaan tetap berfungsi tanpa lisensi tetapi menambahkan watermark).  
- `pip install aspose-ocr` (nama paket di PyPI).  
- Gambar contoh bernama `invoice.png` ditempatkan di folder yang dapat Anda referensikan.

Itu saja—tanpa kerangka kerja berat, tanpa layanan eksternal. Mari kita mulai.

---

## Langkah 1: Instal dan Impor Pustaka yang Diperlukan

Pertama, pastikan paket Aspose OCR dan modul bawaan `json` tersedia. Modul `json` sudah termasuk dalam Python, jadi kita hanya perlu menginstal Aspose.

```bash
pip install aspose-ocr
```

Sekarang impor keduanya dalam skrip Anda:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Mengapa ini penting:** Mengimpor `aspose.ocr` memberi Anda akses ke mesin OCR berperforma tinggi, sementara `json` memungkinkan Anda mengubah string tata letak mentah menjadi kamus Python native untuk penelusuran yang mudah.

---

## Langkah 2: Buat Engine OCR dan Muat Gambar Anda

Engine adalah inti dari proses. Anda menginstansiasinya, lalu menunjuk ke gambar yang ingin dipindai.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Tips pro:** Ganti `"YOUR_DIRECTORY/invoice.png"` dengan jalur absolut atau relatif yang mengarah ke file Anda yang sebenarnya. Jika file tidak ditemukan, Aspose akan mengeluarkan `FileNotFoundError`, jadi periksa kembali ejaannya.

---

## Langkah 3: Konfigurasikan Engine agar Mengeluarkan Data Tata Letak JSON

Aspose OCR dapat mengembalikan teks biasa, JSON hanya OCR, atau JSON tata letak lengkap yang mencakup koordinat untuk kata, baris, bahkan karakter individual. Untuk **mendapatkan koordinat bounding box**, kita memerlukan JSON tata letak.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Mengapa JSON?** JSON bersifat bahasa‑agnostik, dapat dibaca manusia, dan memetakan dengan bersih ke kamus Python. JSON tata letak berisi array `"words"` di mana setiap entri menyimpan teks dan array `boundingBox` berisi delapan angka (empat titik sudut).

---

## Langkah 4: Jalankan Pengenalan dan Ambil String JSON Mentah

Sekarang kita menjalankan OCR. Metode `recognize()` mengembalikan objek `OcrResult`, dari mana kita dapat mengekstrak string JSON.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Jika Anda mencetak `layout_json`, Anda akan melihat sesuatu seperti:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Kasus tepi:** Beberapa gambar dapat menghasilkan array `"words"` kosong jika mesin OCR tidak dapat mendeteksi teks apa pun. Dalam hal ini, periksa kualitas gambar (kontras, resolusi) sebelum melanjutkan.

---

## Langkah 5: Parse JSON menjadi Kamus Python

Bekerja dengan struktur native Python jauh lebih mudah daripada memanipulasi string. Gunakan fungsi `json.loads()` untuk mengonversi string.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Sekarang `layout_data["words"]` adalah daftar kamus, masing‑masing mewakili sebuah kata dan bounding box‑nya.

---

## Langkah 6: Iterasi Kata‑Kata dan **Dapatkan Koordinat Bounding Box**

Berikut inti tutorial kami: mengulang setiap kata, mengekstrak teks, dan mencetak koordinat. Inilah tempat tepat di mana kita **mendapatkan koordinat bounding box**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Contoh output** (angka Anda akan berbeda tergantung gambar):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Mengapa format delapan titik?** Empat sudut (atas‑kiri, atas‑kanan, bawah‑kanan, bawah‑kiri) memungkinkan Anda menggambar poligon di sekitar kata, bahkan jika teks miring. Jika Anda hanya membutuhkan persegi panjang sederhana, Anda dapat menghitung `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, dan `height = max(y…) - y_min`.

---

## Peningkatan Opsional

### 1. Konversi Bounding Box ke Persegi Panjang Sederhana

Jika alat downstream Anda mengharapkan `(x, y, width, height)` alih‑alih delapan titik, tambahkan pembantu berikut:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Tangani PDF Multi‑Halaman

Aspose OCR dapat menerima aliran PDF. Ganti baris pemuatan gambar dengan:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Iterasikan `set_page_number` untuk setiap halaman, kumpulkan koordinat per halaman.

### 3. Visualisasikan Bounding Box

Jika Anda ingin melihat kotak‑kotak digambar pada gambar asli, gunakan Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Sekarang Anda akan melihat outline merah di sekitar setiap kata yang dikenali—sempurna untuk debugging atau overlay UI.

---

## Pertanyaan Umum & Gotchas

- **Bagaimana jika JSON sangat besar?** Untuk dokumen besar, pertimbangkan streaming JSON atau memproses per halaman untuk menjaga penggunaan memori tetap rendah.  
- **Mengapa beberapa kata tidak muncul?** Kontras rendah atau teks tulisan tangan sering membuat mesin OCR gagal. Praproses gambar (tingkatkan kontras, binarisasi) sebelum memberi ke Aspose.  
- **Bisakah saya mendapatkan koordinat tingkat karakter?** Ya—atur `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` untuk menerima array `"characters"` dengan `boundingBox` masing‑masing.  
- **Apakah sistem koordinat berbasis nol?** Ya. (0, 0) berada di sudut kiri‑atas gambar.

---

## Skrip Lengkap – Siap Salin & Jalankan

Berikut contoh lengkap yang dapat dijalankan, menggabungkan semua langkah. Simpan sebagai `extract_bboxes.py` dan jalankan `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}