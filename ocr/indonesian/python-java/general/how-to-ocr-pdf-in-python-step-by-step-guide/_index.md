---
category: general
date: 2026-03-28
description: Pelajari cara melakukan OCR PDF dengan Python secara cepat. Panduan ini
  menunjukkan cara mengekstrak teks dari PDF, mengenali teks dari PDF, dan mengonversi
  PDF yang dipindai menjadi teks menggunakan Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: id
og_description: Kuasi cara OCR PDF dengan Python. Ekstrak teks dari PDF, kenali teks
  dari PDF, dan ubah PDF yang dipindai menjadi teks dalam hitungan menit.
og_title: Cara OCR PDF di Python – Panduan Lengkap
tags:
- PDF
- OCR
- Python
- Aspose
title: Cara OCR PDF di Python – Panduan Langkah demi Langkah
url: /id/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR PDF di Python – Panduan Langkah‑ demi‑Langkah

Pernah bertanya‑tanya **cara OCR PDF** ketika file tersebut hanya berupa gambar halaman? Anda tidak sendirian. Pada tutorial ini kami akan membahas langkah‑langkah tepat untuk OCR PDF, mengekstrak teks dari PDF, dan mengubah PDF yang dipindai menjadi teks yang dapat dicari—semua dengan kode Python biasa.

Kami akan membahas semuanya mulai dari menginstal library Aspose OCR hingga mengambil teks yang dikenali dari setiap halaman. Pada akhir tutorial Anda akan dapat **OCR PDF dengan Python**, **mengekstrak teks dari PDF**, dan **mengonversi PDF yang dipindai menjadi teks** tanpa harus mencari‑cari dokumentasi yang tersebar. Tanpa basa‑basi, hanya contoh praktis yang dapat dijalankan dan Anda dapat menyalin‑tempel.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

* Python 3.8+ (rilisan stabil terbaru paling cocok)  
* Lisensi Aspose OCR untuk Python atau kunci percobaan gratis – Anda dapat mengambilnya dari situs web Aspose.  
* PDF yang dipindai yang ingin Anda proses (kami akan menyebutnya `input.pdf`).  

Jika semua sudah ada, bagus—mari kita mulai. Jika belum, menginstal paketnya sangat mudah dan kami akan tunjukkan caranya.

## Cara OCR PDF – Menyiapkan Lingkungan

Hal pertama yang harus Anda lakukan adalah mendapatkan modul Aspose OCR ke mesin Anda. Paketnya bernama `aspose-ocr`, dan Anda dapat menginstalnya via pip:

```bash
pip install aspose-ocr
```

> **Pro tip:** Gunakan lingkungan virtual (`python -m venv venv`) agar dependensi Anda tetap rapi.

Setelah paket terinstal, Anda siap mengimpornya dan memulai mesin OCR. Ini adalah fondasi untuk setiap alur kerja **ocr pdf with python** yang akan Anda bangun nanti.

## OCR PDF dengan Python – Mengimpor Aspose OCR

Sekarang pustaka sudah tersedia, mari kita bawa ke dalam skrip kita. Kita juga akan mengatur mesin untuk bekerja dalam *direct PDF mode*, yang memberi tahu Aspose untuk membaca byte PDF langsung dari file alih‑alih mengonversi setiap halaman menjadi gambar terlebih dahulu.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Mengapa menggunakan `PdfMode.DIRECT`? Karena ini melewatkan langkah rasterisasi tambahan, membuat proses lebih cepat dan mempertahankan tata letak asli—sangat berguna ketika Anda perlu **recognize text from PDF** secara akurat.

## Mengenali Teks dari PDF – Menjalankan Mesin

Dengan mesin siap, arahkan ke file yang dipindai. Metode `recognize_from_pdf` melakukan semua pekerjaan berat: ia mem-parsing setiap halaman, menjalankan algoritma OCR, dan mengembalikan objek `OcrResult` yang berisi koleksi objek `Page`.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Jika Anda bertanya‑tanya apakah ini bekerja dengan PDF yang dienkripsi—ya, selama Anda menyediakan kata sandi melalui `ocr_engine.password = "secret"` sebelum memanggil `recognize_from_pdf`. Itu adalah kasus pinggir yang banyak tutorial abaikan, namun sangat berguna dalam pipeline dunia nyata.

## Mengekstrak Teks dari PDF – Mengakses Hasil Halaman

Daftar `ocr_result.pages` berisi satu entri per halaman. Setiap objek `Page` memiliki atribut `.text` yang berisi representasi teks polos dari halaman yang dipindai. Mari kita loop dan cetak hasilnya sehingga Anda dapat melihat tepat apa yang diekstrak.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Menjalankan skrip akan menghasilkan sesuatu seperti:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Output tersebut membuktikan bahwa Anda telah berhasil **extract text from PDF** dan **recognize text from PDF** menggunakan Aspose OCR. Sekarang Anda dapat menyalurkan string tersebut ke basis data, indeks pencarian, atau pipeline NLP apa pun.

![how to ocr pdf example](placeholder-image.png "how to ocr pdf example")

*Teks alt gambar:* **how to ocr pdf example** – menampilkan output konsol teks yang dikenali per halaman.

## Mengonversi PDF yang Dipindai menjadi Teks – Menyimpan Output

Sebagian besar pengembang tidak hanya ingin melihat teks di konsol; mereka membutuhkan file yang persisten. Di bawah ini ada helper kecil yang menulis teks setiap halaman ke file `.txt` terpisah, secara efektif **convert scanned PDF to text** ke dalam folder bernama `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Setelah skrip selesai, Anda akan memiliki direktori yang rapi:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Sekarang Anda telah sepenuhnya **convert scanned PDF to text** dan dapat memasukkan file‑file tersebut ke proses selanjutnya—pencarian, analitik, atau bahkan sekadar `grep`.

## Pertanyaan Umum & Kasus Pinggir

**Bagaimana jika PDF saya berisi gambar yang dicampur dengan teks asli?**  
Aspose OCR akan mencoba mengenali semuanya, tetapi Anda dapat mempercepat proses dengan menonaktifkan OCR untuk halaman yang sudah berisi teks yang dapat dipilih. Atur `ocr_engine.auto_detect_page_orientation = True` dan kemudian panggil `ocr_engine.recognize_from_pdf(..., detect_text=False)` untuk halaman yang sudah baik.

**Apakah saya dapat mengontrol model bahasa?**  
Tentu saja. Atur `ocr_engine.language = aocr.Language.English` (atau bahasa lain yang didukung) sebelum memanggil `recognize_from_pdf`. Ini meningkatkan akurasi untuk dokumen non‑English.

**Bagaimana cara menangani PDF yang sangat besar (100+ halaman)?**  
Proses dalam potongan. Metode `recognize_from_pdf` menerima argumen `page_range`, misalnya `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Loop melalui rentang untuk menjaga penggunaan memori tetap rendah.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip tunggal yang dapat Anda simpan sebagai `ocr_pdf.py` dan jalankan:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Jalankan dengan:

```bash
python ocr_pdf.py
```

Anda akan melihat output konsol yang mengonfirmasi teks setiap halaman dan lokasi file `.txt` yang disimpan.

## Kesimpulan

Kami telah membahas **cara OCR PDF** menggunakan Python, menunjukkan cara **ocr pdf with python** yang bersih, memperlihatkan cara **extract text from PDF**, menjelaskan mekanisme di balik **recognize text from PDF**, dan akhirnya memberikan potongan kode siap pakai yang **convert scanned PDF to text**. Seluruh proses telah dibungkus

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}