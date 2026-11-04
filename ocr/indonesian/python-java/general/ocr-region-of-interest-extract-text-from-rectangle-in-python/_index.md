---
category: general
date: 2026-05-31
description: Pelajari cara menggunakan wilayah minat OCR untuk memuat gambar dan mengekstrak
  teks dari persegi panjang, sempurna untuk mengenali jumlah pada faktur.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: id
og_description: Kuasai wilayah minat OCR untuk memuat gambar, mengekstrak teks dari
  persegi panjang, dan mengenali teks dari faktur dalam satu tutorial.
og_title: OCR Region of Interest – Panduan Python Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR Wilayah Minat – Ekstrak Teks dari Persegi Panjang di Python
url: /id/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – Ekstrak Teks dari Persegi Panjang di Python

Pernah bertanya-tanya bagaimana cara **ocr region of interest** pada bagian tertentu dari faktur yang dipindai tanpa harus memberi seluruh halaman ke mesin? Anda bukan orang pertama yang menatap struk buram dan berpikir, “Bagaimana cara mengekstrak jumlah yang berada di pojok kanan bawah?” Kabar baiknya, Anda dapat memberi tahu perpustakaan OCR tepat di mana harus mencari, sehingga kecepatan dan akurasi meningkat secara signifikan.

Dalam panduan ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan cara **load image for OCR**, mendefinisikan **region of interest**, dan kemudian **extract text from rectangle** untuk akhirnya **recognize text from invoice** serta menjawab pertanyaan klasik “bagaimana mengekstrak jumlah”. Tidak ada referensi samar—hanya kode konkret, penjelasan jelas, dan beberapa pro tip yang Anda harapkan sudah tahu sebelumnya.

---

## What You’ll Build

Pada akhir tutorial ini Anda akan memiliki skrip Python kecil yang:

1. Memuat gambar faktur dari disk.  
2. Menandai ROI persegi panjang tempat total jumlah berada.  
3. Menjalankan OCR hanya di dalam ROI tersebut.  
4. Mencetak string jumlah yang sudah dibersihkan.  

Semua ini bekerja dengan perpustakaan OCR apa pun yang mendukung ROI—di sini kami menggunakan paket fiktif namun representatif `SimpleOCR` yang meniru alat populer seperti Tesseract atau EasyOCR. Silakan ganti dengan yang lain; konsepnya tetap sama.

---

## Prerequisites

- Python 3.8+ terpasang (`python --version` harus menampilkan ≥3.8).  
- Paket OCR yang dapat di‑install via pip (misalnya `pip install simpleocr`).  
- Gambar faktur (PNG atau JPEG) yang ditempatkan di folder yang dapat Anda referensikan.  
- Familiaritas dasar dengan fungsi dan kelas Python (tidak ada yang rumit).

Jika semua sudah ada, bagus—mari kita mulai. Jika belum, ambil dulu gambarnya; langkah‑langkah selanjutnya tidak bergantung pada isi file sebenarnya.

---

## Step 1: Load Image for OCR

Hal pertama yang dibutuhkan dalam alur kerja OCR apa pun adalah bitmap untuk dibaca. Kebanyakan perpustakaan menyediakan metode sederhana `load_image` yang menerima jalur file. Berikut cara melakukannya dengan mesin `SimpleOCR` kami:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Gunakan jalur absolut atau `os.path.join` untuk menghindari kejutan “file not found” ketika menjalankan skrip dari direktori kerja yang berbeda.

---

## Step 2: Define OCR Region of Interest

Alih‑alih membiarkan mesin memindai seluruh halaman, kita memberi tahu *tepat* di mana jumlah berada. Ini adalah langkah **ocr region of interest**, dan merupakan kunci ekstraksi yang dapat diandalkan, terutama ketika dokumen mengandung header atau footer yang berisik.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Mengapa angka‑angka itu? `x` dan `y` adalah offset piksel dari sudut kiri‑atas, sementara `width` dan `height` menggambarkan ukuran kotak. Jika Anda tidak yakin, buka gambar di editor apa pun, aktifkan penggaris, dan catat koordinatnya. Banyak IDE bahkan memungkinkan Anda melihat posisi kursor saat mengarahkan mouse.

---

## Step 3: Extract Text from Rectangle

Setelah ROI ditetapkan, kita meminta mesin untuk **recognize text from invoice** namun terbatas pada persegi panjang yang baru saja ditambahkan. Pemanggilan ini mengembalikan objek hasil yang biasanya berisi string mentah, skor kepercayaan, dan kadang‑kadang kotak pembatas.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Di balik layar, `recognize()` mengiterasi setiap ROI, memotong potongan tersebut, menjalankan model OCR, dan menyatukan hasilnya. Inilah mengapa mendefinisikan wilayah **extract text from rectangle** yang ketat dapat menghemat detik pada proses batch.

---

## Step 4: How to Extract Amount – Clean the Output

OCR tidak sempurna; Anda sering mendapatkan spasi berlebih, baris baru, atau bahkan karakter yang salah dibaca (misalnya “S” vs “5”). `strip()` cepat dan regex kecil biasanya cukup untuk nilai moneter.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** Jika Anda berencana memasukkan jumlah ke basis data atau gateway pembayaran, Anda memerlukan format yang dapat diprediksi. Menghapus spasi putih dan menyaring karakter non‑numerik mencegah kesalahan di tahap selanjutnya.

---

## Step 5: Recognize Text from Invoice – Full Script

Menggabungkan semuanya, berikut skrip lengkap yang siap dijalankan. Simpan sebagai `extract_amount.py` dan jalankan `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Expected Output

```
Amount: 1,245.67
```

Jika ROI tidak sejajar, Anda mungkin melihat sesuatu seperti `Amount: 1245.6S`—perhatikan “S” yang mengambang. Sesuaikan koordinat persegi panjang dan jalankan kembali hingga output terlihat bersih.

---

## Common Pitfalls & Edge Cases

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ROI terlalu kecil** | Teks jumlah terpotong, menghasilkan pengenalan parsial. | Perbesar `width`/`height` sekitar 10‑20 % dan uji kembali. |
| **DPI tidak tepat** | Scan beresolusi rendah (≤150 dpi) menurunkan akurasi OCR. | Resample gambar ke 300 dpi sebelum memuat, atau minta scanner dengan DPI lebih tinggi. |
| **Beberapa mata uang** | Regex mengambil grup numerik pertama, yang mungkin adalah nomor faktur. | Perbaiki regex untuk mencari simbol mata uang (`$`, `€`, `£`) sebelum digit. |
| **Faktur terrotasi** | Mesin OCR mengasumsikan teks tegak; halaman yang diputar mengganggu pengenalan. | Terapkan koreksi rotasi (`ocr_engine.rotate(90)`) sebelum menambahkan ROI. |
| **Noise di latar belakang** | Bayangan atau stempel membingungkan model. | Pra‑proses dengan threshold sederhana (`cv2.threshold`) atau gunakan filter denoising. |

Menangani kasus tepi ini lebih awal menghemat berjam‑jam debugging di kemudian hari.

---

## Pro Tips for Real‑World Projects

- **Batch Processing:** Loop melalui folder faktur, hitung ROI secara dinamis (misalnya berdasarkan deteksi template), dan simpan hasil ke CSV.  
- **Template Matching:** Jika Anda menangani beberapa tata letak faktur, pertahankan peta JSON `template_id → ROI coordinates`. Ganti ROI berdasarkan classifier tata letak cepat.  
- **Parallel Execution:** Gunakan `concurrent.futures.ThreadPoolExecutor` untuk menjalankan beberapa instance OCR secara bersamaan—ideal untuk pipeline back‑office volume tinggi.  
- **Confidence Filtering:** Kebanyakan hasil OCR menyertakan skor kepercayaan. Buang hasil di bawah ambang tertentu (misalnya 85 %) dan tandai untuk peninjauan manual.

---

## Conclusion

Kami telah membahas semua yang Anda perlukan untuk **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, dan akhirnya **recognize text from invoice** guna menjawab pertanyaan klasik **how to extract amount**. Skripnya ringkas, namun cukup fleksibel untuk disesuaikan dengan format dokumen, bahasa, dan backend OCR yang berbeda.

Setelah menguasai dasar‑dasarnya, pertimbangkan memperluas alur kerja: tambahkan pemindaian barcode, integrasikan dengan parser PDF, atau kirim jumlah yang diekstrak ke API akuntansi. Langit adalah batasnya, dan dengan ROI yang terdefinisi dengan baik Anda akan selalu mendapatkan hasil yang lebih cepat dan bersih.

Jika Anda mengalami kendala, tinggalkan komentar di bawah—selamat OCRing!

![ocr region of interest example](https://example.com/ocr_roi_example.png "contoh ocr region of interest")


## What Should You Learn Next?

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}