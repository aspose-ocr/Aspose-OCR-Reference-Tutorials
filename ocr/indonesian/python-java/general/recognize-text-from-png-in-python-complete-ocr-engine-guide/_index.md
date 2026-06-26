---
category: general
date: 2026-06-25
description: 'mengenali teks dari png dengan Python: panduan langkah demi langkah
  untuk membuat mesin OCR Python, menjalankan OCR pada dokumen teknis, dan mengekstrak
  teks dari gambar dokumen teknis.'
draft: false
keywords:
- recognize text from png
- ocr image to text python
- create OCR engine python
- extract text from technical document image
- run OCR on technical document
language: id
og_description: Mengenali teks dari PNG menggunakan Python. Pelajari cara membuat
  mesin OCR Python, menjalankan OCR pada dokumen teknis, dan mengekstrak teks dari
  gambar dokumen teknis.
og_title: Mengenali Teks dari PNG dengan Python – Tutorial Lengkap Mesin OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: 'recognize text from png with Python: step‑by‑step guide to create
    OCR engine python, run OCR on technical document and extract text from technical
    document image.'
  headline: Recognize Text from PNG in Python – Complete OCR Engine Guide
  type: TechArticle
- description: 'recognize text from png with Python: step‑by‑step guide to create
    OCR engine python, run OCR on technical document and extract text from technical
    document image.'
  name: Recognize Text from PNG in Python – Complete OCR Engine Guide
  steps:
  - name: Low‑Resolution Images
    text: 'If the PNG originates from a scanned fax, you might be dealing with 72
      dpi. OCR accuracy drops dramatically below 150 dpi. A quick fix is to upscale
      the image using a bicubic algorithm before recognition:'
  - name: Rotated Pages
    text: 'Technical manuals sometimes come scanned at an angle. The engine can auto‑deskew,
      but you can also pre‑rotate:'
  - name: Multi‑Page Documents
    text: 'When you need to **run OCR on technical document** PDFs that have been
      exported to PNG per page, wrap the logic in a loop:'
  - name: Language Selection
    text: 'Aspose OCR defaults to English, but you can switch to other languages (e.g.,
      German) by loading the appropriate language pack:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Mengenali Teks dari PNG di Python – Panduan Lengkap Mesin OCR
url: /id/python-java/general/recognize-text-from-png-in-python-complete-ocr-engine-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali Teks dari PNG di Python – Panduan Lengkap Mesin OCR

Pernahkah Anda perlu **mengenali teks dari PNG** tetapi tidak yakin pustaka Python mana yang harus dipilih? Anda tidak sendirian. Baik Anda mendigitalkan manual yang dipindai, mengambil nomor seri dari label produk, atau mengekstrak data dari gambar dokumen teknis, sebuah pipeline OCR yang handal dapat menghemat Anda berjam‑jam penyalinan manual.

Dalam tutorial ini kami akan menunjukkan contoh langsung yang memperlihatkan cara **membuat OCR engine python**, memberi masukan PNG, dan **mengekstrak teks dari gambar dokumen teknis** dengan hanya beberapa baris kode. Pada akhir tutorial Anda juga akan tahu cara **menjalankan OCR pada dokumen teknis** dengan kualitas beragam, dan Anda akan memiliki skrip yang dapat digunakan kembali untuk proyek berikutnya.

## Apa yang Akan Anda Pelajari

- Menginstal dan menyiapkan pustaka OCR Python (Aspose OCR digunakan, tetapi langkah‑langkahnya berlaku untuk kebanyakan paket OCR modern).  
- **Membuat OCR engine python** instance dan mengonfigurasi kamus khusus untuk terminologi domain‑spesifik.  
- Memuat gambar PNG, menjalankan OCR, dan **mengenali teks dari png** secara efisien.  
- Menangani jebakan umum seperti resolusi rendah, halaman miring, dan latar belakang berisik.  
- Memperluas skrip untuk memproses batch beberapa dokumen teknis.

> **Prasyarat** – Anda harus memiliki Python 3.8+ terinstal, pemahaman dasar tentang pip, dan gambar PNG yang berisi teks yang dapat dibaca mesin. Tidak diperlukan pengalaman OCR sebelumnya.

---

## Langkah 1: Instal Pustaka OCR (Create OCR Engine Python)

Hal pertama yang harus dilakukan: kita membutuhkan pustaka yang benar‑benar melakukan pekerjaan berat. Aspose OCR untuk Python via .NET adalah opsi komersial yang menawarkan akurasi tinggi langsung dari kotak, tetapi pola yang sama bekerja dengan alternatif sumber terbuka seperti `pytesseract`. Untuk menjaga contoh tetap mandiri, kami akan menggunakan Aspose OCR.

```bash
pip install aspose-ocr
```

> **Pro tip:** Jika Anda mengalami kesalahan izin di Windows, jalankan perintah dari PowerShell yang dijalankan sebagai administrator atau tambahkan `--user` di akhir.

Setelah terinstal, Anda dapat mengimpor modul dan memulai mesin:

```python
import aspose.ocr as ocr
```

Baris impor tunggal itu memberi Anda akses ke kelas `OcrEngine`, yang merupakan fondasi **membuat OCR engine python**.

## Langkah 2: Inisialisasi Mesin OCR dan Sesuaikan (Run OCR on Technical Document)

Sekarang kami akan membuat instance mesin dan secara opsional memberi masukan kamus khusus. Kamus khusus adalah daftar kata yang harus diperlakukan OCR sebagai valid—sempurna untuk jargon teknis, kode produk, atau akronim internal.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: define a custom dictionary for domain‑specific terms
engine.custom_dictionary = [
    "AsposeOCR", "OCRSDK", "Invoice#2026", "SKU-12345"
]
```

Mengapa repot menambahkan kamus? Bayangkan memindai manual perawatan yang berulang kali menyebut “SKU‑12345”. Tanpa kamus OCR mungkin membaca sebagai “SKU‑12345” atau bahkan “S K U‑12345”. Dengan menambahkan istilah ke `custom_dictionary`, Anda secara dramatis meningkatkan akurasi **ocr image to text python** untuk dokumen spesifik tersebut.

## Langkah 3: Muat Gambar PNG (Extract Text from Technical Document Image)

Selanjutnya, kami memuat PNG yang berisi teks yang ingin Anda **mengenali teks dari png**. Aspose OCR mendukung berbagai format gambar, tetapi PNG adalah pilihan yang solid karena mempertahankan kualitas lossless.

```python
# Step 3: Load the image file
image_path = "YOUR_DIRECTORY/technical_doc.png"
image = ocr.Image.load(image_path)
```

Jika PNG Anda sangat besar (misalnya, cetak biru yang dipindai), Anda mungkin ingin menurunkannya sebelum OCR agar penggunaan memori tetap wajar:

```python
# Optional downscale for huge images
max_dim = 2000  # pixels
if max(image.width, image.height) > max_dim:
    scale = max_dim / max(image.width, image.height)
    image = image.resize(int(image.width * scale), int(image.height * scale))
```

## Langkah 4: Lakukan OCR (OCR Image to Text Python)

Dengan mesin siap dan gambar dimuat, pengenalan sebenarnya cukup dengan satu pemanggilan metode:

```python
# Step 4: Run OCR on the loaded image
result = engine.recognize(image)
```

Di balik layar, `engine.recognize` menjalankan serangkaian langkah pra‑pemrosesan—binarisasi, deskew, analisis tata letak—sebelum mengirim bitmap yang telah dibersihkan ke jaringan saraf. Itulah mengapa satu baris kode dapat **menjalankan OCR pada dokumen teknis** yang sebaliknya akan membuat skrip sederhana gagal.

## Langkah 5: Keluarkan Teks yang Dikenali (Recognize Text from PNG)

Akhirnya, kami mencetak teks yang diekstrak. Anda juga dapat menuliskannya ke file, memasukkannya ke basis data, atau meneruskannya ke pipeline NLP selanjutnya.

```python
# Step 5: Output the recognized text
print("=== OCR Result ===")
print(result.text)
```

Jika Anda menjalankan skrip dengan PNG yang valid, Anda akan melihat sesuatu seperti:

```
=== OCR Result ===
Invoice #2026
Product: AsposeOCR SDK
SKU-12345
Total: $1,299.00
```

> **Contoh Gambar**  
> ![hasil mengenali teks dari png](images/ocr_result.png)  
> *Alt text:* *hasil mengenali teks dari png – contoh hasil OCR yang ditampilkan di konsol.*

Tangkapan layar tersebut memperlihatkan ekstraksi bersih di mana kamus khusus kami memastikan kode produk tetap utuh.

---

## Penjelasan Lebih Dalam: Menangani Kasus Tepi Umum

### Gambar Resolusi Rendah

Jika PNG berasal dari faks yang dipindai, Anda mungkin berhadapan dengan 72 dpi. Akurasi OCR turun drastis di bawah 150 dpi. Solusi cepat adalah memperbesar gambar menggunakan algoritma bikubik sebelum pengenalan:

```python
if image.dpi < 150:
    image = image.resize(image.width * 2, image.height * 2, interpolation=ocr.InterpolationMode.BICUBIC)
```

### Halaman yang Diputar

Manual teknis kadang dipindai dengan sudut. Mesin dapat melakukan auto‑deskew, tetapi Anda juga dapat memutar terlebih dahulu:

```python
# Detect and correct rotation
angle = engine.auto_rotate(image)
if angle != 0:
    image = image.rotate(-angle)
```

### Dokumen Multi‑Halaman

Ketika Anda perlu **menjalankan OCR pada dokumen teknis** PDF yang telah diekspor ke PNG per halaman, bungkus logika dalam loop:

```python
import glob

for png_path in sorted(glob.glob("pages/*.png")):
    img = ocr.Image.load(png_path)
    txt = engine.recognize(img).text
    with open("output.txt", "a", encoding="utf-8") as f:
        f.write(f"--- Page {png_path} ---\n{txt}\n\n")
```

### Pemilihan Bahasa

Aspose OCR secara default menggunakan bahasa Inggris, tetapi Anda dapat beralih ke bahasa lain (misalnya, Jerman) dengan memuat paket bahasa yang sesuai:

```python
engine.language = ocr.Language.German
```

Ini berguna ketika **ekstrak teks dari gambar dokumen teknis** Anda mencakup tabel atau spesifikasi multibahasa.

---

## Skrip Lengkap yang Siap Dijalan

Berikut adalah skrip lengkap, siap dijalankan, yang menggabungkan semua langkah. Simpan sebagai `ocr_technical_doc.py` dan ganti `YOUR_DIRECTORY/technical_doc.png` dengan jalur ke PNG Anda.



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}