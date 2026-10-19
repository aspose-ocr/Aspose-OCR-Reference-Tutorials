---
category: general
date: 2026-06-06
description: Cara melakukan OCR pada PDF dan membuat file PDF yang dapat dicari dari
  gambar menggunakan Python. Pelajari cara menambahkan teks yang dapat dicari dan
  mengonversi gambar ke PDF/A dalam hitungan menit.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: id
og_description: Cara OCR PDF langkah demi langkah. Pelajari cara menambahkan teks
  yang dapat dicari dan mengonversi gambar ke PDF/A menggunakan skrip Python sederhana.
og_title: Cara OCR PDF – Panduan Cepat Membuat PDF yang Dapat Dicari
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Cara OCR PDF di Python – Membuat PDF yang Dapat Dicari dari Gambar
url: /id/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR PDF – Mengubah Gambar Pindai menjadi PDF yang Dapat Dicari

Pernah bertanya-tanya **cara OCR PDF** ketika yang Anda miliki hanya gambar pindai dari faktur atau kwitansi? Anda tidak sendirian. Di banyak kantor, dokumen masuk datang sebagai PNG atau JPEG datar, dan langkah selanjutnya—membuat konten tersebut dapat dicari—terasa seperti kotak hitam.  

Kabar baik? Dengan hanya beberapa baris Python Anda dapat **membuat PDF yang dapat dicari**, **menambahkan teks yang dapat dicari**, dan bahkan **mengonversi gambar ke PDF/A** untuk pengarsipan jangka panjang. Dalam tutorial ini kami akan membahas setiap langkah, menjelaskan mengapa langkah tersebut penting, dan memberi Anda skrip siap‑jalankan yang dapat Anda masukkan ke proyek apa pun.

> **Pro tip:** Pendekatan yang sama bekerja untuk pemindaian multi‑halaman; cukup lakukan loop pada file‑file dan mesin akan menangani proses beratnya.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut di mesin Anda:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.9 atau lebih baru | Sintaks modern dan dukungan pustaka yang lebih baik |
| Mesin OCR berbasis `pdfium` (misalnya `pdfocr` atau SDK komersial) | Menangani baik pengenalan gambar maupun pembuatan PDF/A |
| File gambar (PNG, JPEG, TIFF) yang ingin Anda ubah menjadi PDF yang dapat dicari | Sumber teks |
| Izin menulis ke folder output | Agar skrip dapat menyimpan PDF baru |

Jika Anda belum menginstal SDK OCR, jalankan:

```bash
pip install pdfocr   # replace with your vendor's package name
```

Itu saja—tidak ada ketergantungan sistem yang rumit, hanya instalasi pip.

---

## Cara OCR PDF – Ikhtisar

Secara umum prosesnya terdiri dari tiga tindakan sederhana:

1. **Mengenali** teks di dalam gambar sambil mempertahankan grafik asli.  
2. **Mengekspor** hasil OCR bersama gambar asli sebagai **PDF/A yang dapat dicari** (varian PDF yang ramah arsip).  
3. **Memvalidasi** bahwa file yang dihasilkan berisi teks yang dapat dipilih dan dicari di atas gambar asli.

Di bawah ini Anda akan melihat setiap langkah dalam kode, dengan penjelasan *mengapa* di balik perintah‑perintah tersebut.

---

## Langkah 1: Mengenali Teks dari Gambar

Pertama kami meminta mesin OCR membaca piksel dan mengembalikan objek hasil yang memuat baik gambar mentah maupun teks yang diekstrak. Anggap saja mesin “membaca” faktur untuk Anda.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Mengapa ini penting

- **Mempertahankan grafis** berarti tata letak visual (tabel, logo, stempel) tetap persis seperti yang dipindai.  
- Objek `result` biasanya berisi lapisan teks tersembunyi yang nanti akan kami sematkan ke PDF.  
- Menggunakan `recognize_image` alih‑alih `recognize_pdf` menghindari langkah konversi tambahan, yang mempercepat pemrosesan untuk gambar satu halaman.

#### Variasi umum

- Jika Anda memiliki **TIFF multi‑halaman**, berikan jalur file secara langsung; kebanyakan mesin akan memperlakukan setiap halaman sebagai gambar terpisah.  
- Untuk PDF yang sudah berisi gambar, Anda dapat memanggil `engine.recognize_pdf("file.pdf")` dan melewati langkah ini sepenuhnya.

---

## Langkah 2: Mengekspor Hasil OCR sebagai PDF/A yang Dapat Dicari

Sekarang kami mengambil `result` dari langkah 1 dan memberi tahu mesin untuk menulis file baru. Flag kunci di sini adalah *PDF/A*—versi standar ISO dari PDF yang dirancang untuk preservasi jangka panjang.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Mengapa ini penting

- **PDF yang dapat dicari**: File output berisi lapisan teks tersembunyi yang dapat dipilih. Anda kini dapat menggunakan Ctrl + F pada dokumen.  
- **Kepatuhan PDF/A**: Beberapa organisasi (hukum, keuangan) memerlukan PDF/A untuk jejak audit; langkah ini memenuhi aturan tersebut secara otomatis.  
- Metode ini juga **menambahkan teks yang dapat dicari** tanpa meratakan gambar, sehingga kesetiaan visual tetap sempurna.

#### Kasus khusus: Membutuhkan PDF biasa saja?

Jika Anda tidak memerlukan PDF/A, ganti `save_as_pdfa` dengan `save_as_pdf`. Sisa alur kerja tetap sama.

---

## Langkah 3: Memverifikasi PDF yang Dapat Dicari

Pemeriksaan cepat menyelamatkan Anda dari bug misterius di kemudian hari. Buka file yang dihasilkan di penampil PDF apa pun, coba pilih sebuah kata, dan gunakan fungsi pencarian.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Output yang Diharapkan

Saat Anda menjalankan skrip, konsol akan mencetak:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

Membuka file, Anda akan melihat gambar faktur asli dengan lapisan teks yang samar dan tak terlihat. Sorot kata apa pun dan Anda akan melihat bahwa teks tersebut dapat dipilih—**itulah teks yang dapat dicari** yang baru saja Anda tambahkan.

---

## Menambahkan Teks yang Dapat Dicari ke PDF yang Ada (Bonus)

Kadang‑kadang Anda sudah memiliki PDF tetapi perlu **menambahkan teks yang dapat dicari** ke dalamnya. Mesin yang sama dapat menimpa hasil OCR pada PDF yang sudah ada:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Di sini `apply_to` menggabungkan lapisan tersembunyi dengan halaman‑halaman asli, memungkinkan Anda **membuat PDF yang dapat dicari** tanpa harus memindai ulang.

---

## Kesalahan Umum dan Tips

| Masalah | Cara menghindarinya |
|---------|---------------------|
| **Gambar sumber beresolusi rendah** (< 150 dpi) | Perbesar atau minta pemindaian beresolusi lebih tinggi; akurasi OCR turun drastis di bawah 150 dpi. |
| **Data bahasa hilang** | Instal paket bahasa yang sesuai untuk mesin OCR Anda (`pip install pdfocr[eng,spa]`). |
| **Folder output tidak dapat ditulis** | Jalankan skrip dengan izin yang cukup atau pilih direktori lain. |
| **Validasi PDF/A gagal** | Pastikan Anda tidak menyematkan font yang tidak didukung atau JavaScript; kebanyakan SDK menangani ini secara otomatis ketika Anda menggunakan `save_as_pdfa`. |

---

## Skrip Lengkap – Solusi Satu‑File

Berikut adalah skrip mandiri yang mengikat semua langkah bersama. Salin‑tempel, ganti jalur placeholder, dan Anda siap **mengonversi gambar ke PDF/A** dalam hitungan detik.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**Apa yang dilakukan skrip ini:**  
1. Memuat mesin OCR.  
2. Membaca gambar yang dipilih dan mengekstrak teks.  
3. Menulis **PDF/A yang dapat dicari** yang dapat langsung Anda distribusikan atau arsipkan.  

Silakan bungkus logika `main` dalam fungsi yang memproses seluruh folder—cukup iterasi melalui `os.listdir()` dan ulangi tiga langkah untuk setiap file.

---

## Langkah Selanjutnya & Topik Terkait

Sekarang Anda telah menguasai **cara OCR PDF**, pertimbangkan menjelajahi ide‑ide lanjutan berikut:

- **Pemrosesan batch:** Gunakan `concurrent.futures` untuk OCR puluhan faktur secara paralel.  
- **Penyuntikan metadata:** Tambahkan tanggal pembuatan atau nomor faktur ke metadata PDF untuk indeksasi yang lebih mudah.  
- **PDF hibrida:** Gabungkan teks yang dapat dicari dengan gambar asli yang disematkan untuk “kembar digital” dokumen kertas.  
- **Output alternatif:** Ekspor ke **DOCX** atau **HTML** jika sistem hilir memerlukan format yang dapat diedit.

Masing‑masing hal ini dibangun di atas konsep inti yang baru saja Anda pelajari—mengenali, mengekspor, memverifikasi.

---

## Wrap‑Up

Singkatnya, Anda kini tahu **cara OCR PDF** dengan mengubah gambar sederhana menjadi **PDF/A yang dapat dicari** hanya dengan tiga baris Python. Skrip menangani pekerjaan berat, mempertahankan grafis asli, dan memberi Anda dokumen yang sesuai standar yang dapat Anda cari, arsipkan, atau bagikan.  

Cobalah dengan faktur, kwitansi, atau kontrak pindai Anda sendiri. Jika Anda menemui kendala, tinggalkan komentar di bawah atau periksa dokumentasi resmi SDK—biasanya penuh dengan contoh tambahan. Selamat coding, dan nikmati kemampuan baru untuk membuat gambar apa pun langsung dapat dicari! 

![Contoh Cara OCR PDF yang menampilkan gambar asli dan lapisan PDF yang dapat dicari](placeholder.png "Contoh Cara OCR PDF")

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik‑topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Mengenali Teks PDF – Operasi OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/)
- [Mengonversi Gambar ke PDF C# – Simpan Hasil OCR Multi‑halaman](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}