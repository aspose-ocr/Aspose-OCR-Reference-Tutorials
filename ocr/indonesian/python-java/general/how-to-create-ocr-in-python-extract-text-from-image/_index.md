---
category: general
date: 2026-04-26
description: Cara membuat OCR dengan cepat dan andal. Pelajari cara mengekstrak teks
  dari gambar, memuat gambar untuk OCR, dan menjalankan OCR pada PNG dengan kamus
  khusus.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: id
og_description: Cara membuat OCR di Python dan mengekstrak teks dari gambar. Panduan
  ini menunjukkan cara memuat gambar untuk OCR, menjalankan OCR pada PNG, dan menggunakan
  kamus khusus.
og_title: Cara Membuat OCR di Python – Ekstraksi Teks Cepat
tags:
- OCR
- Python
- Image Processing
title: Cara Membuat OCR di Python – Ekstrak Teks dari Gambar
url: /id/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat OCR di Python – Panduan Langkah‑per‑Langkah

Pernah bertanya-tanya **bagaimana cara membuat OCR** yang dapat membaca PDF yang dipindai, tangkapan layar, atau catatan tulisan tangan Anda? Anda tidak sendirian. Dalam banyak proyek dunia nyata kami perlu *mengekstrak teks dari file gambar*, tetapi mesin bawaan sering kesulitan dengan kata‑kata khusus domain.  

Dalam tutorial ini Anda akan melihat contoh lengkap yang dapat dijalankan yang memuat gambar untuk OCR, menerapkan kamus khusus, dan akhirnya **menjalankan OCR pada file PNG**. Pada akhir tutorial Anda akan dapat mengekstrak teks dari gambar apa pun dan menyesuaikan mesin dengan terminologi Anda sendiri.

## Apa yang Dibahas dalam Tutorial Ini

Kami akan membahas setiap langkah yang Anda perlukan:

* Menginstal paket `aocr` yang kecil namun kuat (atau perpustakaan kompatibel lainnya).  
* Mengonfigurasi **kamus khusus** sehingga istilah seperti `aspocorp` atau `licensekey` dikenali.  
* **Memuat gambar untuk OCR**, baik itu PNG, JPEG, atau halaman PDF yang dipindai.  
* Menjalankan proses OCR dan mencetak hasilnya.  

Tidak ada tautan dokumentasi eksternal, hanya solusi mandiri yang dapat Anda salin‑tempel dan jalankan hari ini.

### Prasyarat

* Python 3.8 atau lebih baru (kode menggunakan f‑strings).  
* Familiaritas dasar dengan command line – Anda akan mengetik beberapa perintah `pip install`.  
* File gambar (`technical_doc.png` dalam contoh) ditempatkan di suatu lokasi yang dapat Anda referensikan.  

Jika Anda memenuhi ketiga hal tersebut, Anda siap melanjutkan.  

---

## Langkah 1: Instal Library OCR

Pertama, kita memerlukan mesin OCR yang mendukung objek konfigurasi yang dapat diprogram. Paket `aocr` adalah pembungkus ringan di atas mesin OCR native dan bekerja dengan baik untuk demo.

```bash
# Install the library (run once)
pip install aocr
```

> **Tip Pro:** Jika Anda menggunakan Windows dan mengalami error kompilasi, coba `pip install aocr‑binary` yang menyediakan wheel pra‑dibangun.

### Mengapa Menginstal Library Ini?

`aocr` memberi kita akses langsung ke objek `config` dimana kita dapat menyuntikkan **kamus khusus**. Itulah rahasia meningkatkan akurasi pada kosakata khusus.

---

## Langkah 2: Buat Instance Mesin OCR & Tambahkan Kamus Khusus

Sekarang kita memutar mesin dan memberi tahu kata‑kata apa yang harus dianggap dikenal.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Mengapa Kamus Khusus Penting

Model OCR standar dilatih pada korpus umum. Ketika model melihat “aspocorp”, ia mungkin memisahkannya menjadi “aspo corp” atau menghilangkan huruf sama sekali. Dengan memberikan daftar khusus, kami memihak pengenalan ke ejaan tepat yang kami butuhkan, secara dramatis mengurangi upaya pasca‑pemrosesan.

---

## Langkah 3: Muat Gambar yang Ingin Diproses

Di sinilah kita **memuat gambar untuk OCR**. Metode `Image.load` menerima string path dan secara otomatis menentukan tipe file.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Kasus khusus:** Jika sumber Anda adalah PDF multi‑halaman, konversi setiap halaman ke PNG terlebih dahulu (mis., dengan `pdf2image`) dan berikan satu per satu ke mesin.

### Tips untuk Kualitas Gambar yang Lebih Baik

* Pertahankan resolusi minimal 300 dpi.  
* Pastikan gambar dalam posisi tegak; putar dengan `Pillow` jika diperlukan.  
* Konversi pemindaian berwarna ke grayscale untuk mengurangi noise.

---

## Langkah 4: Jalankan Proses OCR pada File PNG

Dengan mesin yang dikonfigurasi dan gambar yang dimuat, kita akhirnya **menjalankan OCR pada PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

Pemanggilan `process()` mengembalikan objek yang berisi teks yang dikenali, skor kepercayaan, dan bounding box untuk setiap kata.

---

## Langkah 5: Keluarkan Teks yang Dikenali

Cara paling sederhana untuk melihat apa yang ditemukan mesin adalah mencetak atribut `text`.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Output yang Diharapkan

Jika `technical_doc.png` berisi kalimat *“The Aspocorp licensekey expires on 2025‑12‑31.”*, konsol akan menampilkan:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Perhatikan bagaimana kamus khusus mempertahankan nama merek tetap utuh—sesuatu yang mungkin diacak oleh OCR standar.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut seluruh skrip, siap disimpan sebagai `run_ocr.py`. Cukup ganti path placeholder dengan lokasi gambar Anda.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Jalankan dari terminal:

```bash
python run_ocr.py
```

Anda akan melihat teks yang diekstrak dicetak ke konsol, persis seperti yang ditunjukkan pada contoh sebelumnya.

---

## Pertanyaan yang Sering Diajukan (FAQ)

| Question | Answer |
|----------|--------|
| **Apakah Saya dapat mengekstrak teks dari PDF yang dipindai?** | Ya. Konversi setiap halaman ke PNG (atau TIFF) terlebih dahulu, kemudian berikan gambar-gambar tersebut ke skrip yang sama. |
| **Bagaimana jika gambar saya berupa JPEG bukan PNG?** | `Image.load` mendukung JPEG, BMP, TIFF, dan PNG secara bawaan. Cukup ubah ekstensi file. |
| **Bagaimana cara meningkatkan akurasi pada pemindaian dengan kontras rendah?** | Pra‑proses dengan `Pillow` – tingkatkan kontras, terapkan binarisasi, atau gunakan `opencv` untuk mengoreksi kemiringan. |
| **Apakah ada cara untuk mendapatkan skor kepercayaan untuk setiap kata?** | `ocr_result` mencakup `words` – setiap kata memiliki atribut `confidence` yang dapat Anda iterasi. |
| **Apakah saya dapat menjalankan ini di server tanpa tampilan (headless)?** | Tentu saja. `aocr` tidak memiliki ketergantungan GUI, menjadikannya sempurna untuk pipeline CI. |

---

## Langkah Selanjutnya & Topik Terkait

Sekarang Anda tahu **cara membuat OCR** dan **mengekstrak teks dari file gambar**, pertimbangkan untuk menjelajahi:

* **Teknik pra‑pemrosesan** – `load image for OCR` hanyalah langkah pertama; gunakan `opencv` untuk mengurangi noise atau menajamkan.  
* **Pemrosesan batch** – iterasi melalui direktori PNG untuk menghasilkan arsip yang dapat dicari.  
* **Dukungan multi‑bahasa** – tambahkan paket bahasa ke mesin jika Anda perlu membaca dokumen dalam bahasa Prancis atau Jerman.  
* **Integrasi dengan Elasticsearch** – indeks teks yang diekstrak untuk pencarian full‑text di seluruh aset yang dipindai.  

Setiap ekstensi ini dibangun di atas pola inti yang baru saja kami bahas, jadi Anda akan menemukan transisinya tanpa kesulitan.

---

## Kesimpulan

Dalam beberapa menit kami telah menjawab **cara membuat OCR** yang secara andal **mengekstrak teks dari file gambar**, terutama PNG, dan kami telah menunjukkan cara **memuat gambar untuk OCR**, menerapkan **kamus khusus**, dan **menjalankan OCR pada PNG** tanpa layanan eksternal apa pun.  

Jalankan skrip tersebut, sesuaikan kamus agar cocok dengan jargon Anda, dan Anda akan memiliki fondasi yang kuat untuk proyek digitalisasi dokumen apa pun.  

Jika Anda mengalami kendala, tinggalkan komentar di bawah—kami senang membantu. Dan jangan lupa membagikan kisah sukses Anda; komunitas belajar paling baik dari contoh dunia nyata.  

**Siap mengotomatisasi pekerjaan kertas Anda?** Ambil kode, sesuaikan, dan mulailah mengubah piksel menjadi teks yang dapat dicari hari ini!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}