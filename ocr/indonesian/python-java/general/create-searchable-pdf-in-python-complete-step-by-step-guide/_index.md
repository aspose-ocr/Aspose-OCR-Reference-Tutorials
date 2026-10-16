---
category: general
date: 2026-06-19
description: Buat PDF yang dapat dicari dari gambar menggunakan Python OCR. Pelajari
  cara mengonversi OCR ke PDF, mengekstrak teks dari gambar, dan melakukan OCR pada
  gambar dengan cepat.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: id
og_description: Buat PDF yang dapat dicari dari gambar dengan Python OCR. Panduan
  ini menunjukkan cara mengonversi OCR ke PDF, mengekstrak teks dari gambar, dan melakukan
  OCR pada gambar.
og_title: Membuat PDF yang Dapat Dicari dengan Python – Panduan Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Buat PDF yang Dapat Dicari dengan Python – Panduan Lengkap Langkah demi Langkah
url: /id/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Searchable PDF di Python – Panduan Lengkap Langkah‑per‑Langkah

Pernah perlu **membuat searchable PDF** dari kwitansi yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami kebuntuan yang sama ketika pertama kali mencoba mengubah gambar teks menjadi PDF yang sebenarnya dapat dicari.

Dalam tutorial ini kami akan membahas solusi praktis yang memungkinkan Anda **melakukan OCR pada gambar**, mengubah hasil OCR menjadi **searchable PDF**, dan bahkan mengambil teks mentah jika Anda membutuhkannya untuk pemrosesan lebih lanjut. Tanpa basa‑basi, hanya contoh yang dapat langsung Anda salin‑tempel ke proyek Anda hari ini.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan mesin OCR ringan di Python  
- Langkah‑langkah tepat untuk **convert OCR to PDF** dan menyimpannya sebagai dokumen yang dapat dicari  
- Cara **extract text from image** untuk analisis lanjutan  
- Tips menangani jebakan umum seperti orientasi gambar dan file besar  
- Skrip lengkap yang dapat dijalankan dan Anda dapat sesuaikan dengan kasus penggunaan Anda

### Prasyarat

- Python 3.8+ terpasang di mesin Anda  
- Familiaritas dasar dengan pip dan virtual environment (opsional tetapi disarankan)  
- File gambar (PNG, JPEG, dll.) yang berisi teks yang jelas dan dapat dibaca mesin  

Jika Anda sudah memiliki semuanya, mari kita mulai.

## Langkah 1: Instal Library yang Diperlukan

Potongan kode yang Anda lihat sebelumnya menggunakan paket fiktif `ocr`, tetapi ide yang sama berlaku untuk library dunia nyata seperti **EasyOCR**, **pytesseract**, atau **pdfminer.six**. Untuk panduan ini kami akan menggunakan **EasyOCR** karena berbasis Python murni, mendukung banyak bahasa, dan menyediakan metode konversi PDF yang berguna melalui helper tambahan.

```bash
pip install easyocr pillow
```

> **Pro tip:** Instal di dalam virtual environment (`python -m venv venv && source venv/bin/activate`) untuk menjaga ketergantungan Anda tetap rapi.

## Langkah 2: Inisialisasi Mesin OCR – Perform OCR on Image

Setelah library siap, kami membuat mesin OCR dan memberitahukannya untuk bekerja dengan teks bahasa Inggris. Ini adalah tempat pertama kami **perform OCR on image**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Mengapa kami memerlukan objek reader khusus? EasyOCR memuat model bahasa sebelumnya, sehingga menggunakan kembali `reader` yang sama untuk beberapa gambar jauh lebih efisien daripada menginisialisasinya kembali setiap kali.

## Langkah 3: Muat Gambar – Extract Text from Image

Mari kita bawa gambar ke memori. Langkah ini adalah tempat kami **extract text from image** nanti, tetapi untuk saat ini kami hanya memuatnya.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Jika gambar Anda terbalik atau miring, pertimbangkan menggunakan metode `rotate` atau `transpose` dari Pillow sebelum memberikannya ke mesin OCR. Pemeriksaan visual cepat dapat menghemat berjam‑jam debugging nanti.

## Langkah 4: Jalankan Mesin OCR dan Tangkap Hasil

Berikut inti proses—mengirim gambar ke mesin OCR dan menerima kembali data terstruktur.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

Flag `detail=1` memberi kami bounding box, yang akan kami perlukan saat nanti **convert OCR to PDF**. Jika Anda hanya membutuhkan string mentah, setel `detail=0`.

## Langkah 5: Konversi Hasil OCR ke Searchable PDF – Convert OCR to PDF

EasyOCR tidak menyediakan penulis PDF langsung, tetapi kami dapat merakit PDF sendiri menggunakan Pillow dan library `reportlab`. Untuk menjaga tutorial tetap ringan, kami akan menggunakan `fpdf2`, yang memungkinkan kami menyematkan gambar asli dan menimpa teks tak terlihat.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

Apa yang baru saja terjadi? Kami menempatkan gambar hasil pemindaian sebagai lapisan terlihat, kemudian menulis kata‑kata yang dikenali di atasnya menggunakan teks putih yang menyatu dengan latar belakang putih. Alat pencarian tetap dapat membaca lapisan tersembunyi, sehingga PDF menjadi **searchable** tanpa mengubah tampilan visual.

## Langkah 6: Simpan Byte PDF – Convert Image to PDF

Jika Anda lebih suka menangani PDF di memori (misalnya, mengirimnya melalui API), Anda dapat menangkap byte‑nya alih‑alih menulis langsung ke disk.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Baris itu menunjukkan alur kerja klasik **convert image to PDF**: Anda memulai dengan gambar, menjalankan OCR, menimpa teks, dan akhirnya menghasilkan aliran PDF.

## Langkah 7: Verifikasi Hasil – Pemeriksaan Cepat

Setelah Anda menjalankan skrip, buka `receipt_searchable.pdf` di penampil PDF apa pun dan coba kotak pencarian (Ctrl + F). Ketik kata yang Anda tahu ada di kwitansi—jika melompat ke posisi yang tepat, Anda telah berhasil **create searchable pdf**!

Jika pencarian gagal, periksa kembali:

1. Skor kepercayaan OCR (`conf` values). Kepercayaan rendah dapat berarti gambar blur.  
2. Koordinat bounding box—kadang EasyOCR melaporkannya dengan orientasi yang berbeda.  
3. Pastikan penampil PDF tidak disetel ke mode “hanya gambar” (jarang, tetapi beberapa penampil memiliki opsi tersebut).

## Skrip Lengkap yang Berfungsi

Menggabungkan semuanya, berikut file Python lengkap yang siap dijalankan:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Simpan ini sebagai `searchable_pdf.py`, ganti placeholder `YOUR_DIRECTORY` dengan jalur yang sebenarnya, dan jalankan:

```bash
python searchable_pdf.py
```

Anda akan melihat pesan konfirmasi dan PDF searchable baru yang berada di folder Anda.

## Pertanyaan Umum & Kasus Tepi

**Bagaimana jika gambar berwarna?**  
EasyOCR bekerja dengan gambar grayscale maupun berwarna, tetapi mengonversi ke grayscale (`pil_image.convert("L")`) kadang dapat meningkatkan akurasi pada pemindaian yang berisik.

**Bisakah saya menangani PDF multi‑halaman?**  
Ya—lakukan loop pada setiap gambar halaman, jalankan langkah OCR, dan tambahkan setiap halaman ke objek `FPDF` yang sama. Ingat untuk mereset kursor (`self.add_page()`) untuk setiap gambar baru.

**Apakah ada cara untuk mempertahankan lapisan teks asli alih‑alih teks putih tak terlihat?**  
Jika Anda membutuhkan PDF “teks‑di‑bawah‑gambar” yang sesungguhnya (misalnya, untuk aksesibilitas), pertimbangkan menggunakan `pdfminer` atau `pikepdf` untuk menyematkan lapisan teks tersembunyi dengan tag PDF yang tepat. Itu lebih lanjutan, tetapi prinsipnya tetap sama: gambar latar + teks overlay.

**Bagaimana jika kepercayaan OCR rendah?**  
Anda dapat menyaring kata‑kata dengan kepercayaan rendah:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Kesimpulan – Apa yang Kami Capai

Kami memulai dengan gambar sederhana kwitansi, **performed OCR on image**, mengekstrak string yang dikenali, dan akhirnya **create searchable pdf** yang berperilaku seperti dokumen yang dipindai secara profesional. Proses ini mencakup semua kata kunci sekunder—**convert OCR to PDF**, **extract text from image**, **convert image to PDF**, dan **perform OCR on image**—sehingga Anda kini memiliki kotak peralatan yang dapat digunakan kembali untuk proyek serupa apa pun.

### Langkah Selanjutnya

- Bereksperimen dengan bahasa lain dengan memberikan kode ISO mereka ke `easyocr.Reader(['en', 'es'])`.  
- Ganti EasyOCR dengan Tesseract jika Anda membutuhkan solusi sepenuhnya offline; sisa pipeline tetap sama.  
- Tambahkan visualisasi kepercayaan OCR (gambar bounding box pada gambar) untuk men-debug pemindaian yang bermasalah.

Ada variasi yang ingin Anda bagikan? Tinggalkan komentar, fork

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Konversi Gambar ke PDF C# – Simpan Hasil OCR Multi‑halaman](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Cara OCR Gambar – Perform OCR on Image dalam OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}