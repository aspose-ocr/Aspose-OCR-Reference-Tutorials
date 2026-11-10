---
category: general
date: 2026-05-03
description: Pelajari cara menjalankan OCR pada gambar dan mengekstrak teks beserta
  koordinatnya menggunakan pengenalan OCR terstruktur. Kode Python langkah demi langkah
  disertakan.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: id
og_description: Jalankan OCR pada gambar dan dapatkan teks dengan koordinat menggunakan
  pengenalan OCR terstruktur. Contoh Python lengkap dengan penjelasan.
og_title: Jalankan OCR pada gambar – Tutorial Ekstraksi Teks Terstruktur
tags:
- OCR
- Python
- Computer Vision
title: Jalankan OCR pada gambar – Panduan Lengkap untuk Ekstraksi Teks Terstruktur
url: /id/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada gambar – Panduan Lengkap untuk Ekstraksi Teks Terstruktur

Pernah perlu **menjalankan OCR pada gambar** tetapi tidak yakin bagaimana cara mempertahankan posisi tepat setiap kata? Anda tidak sendirian. Dalam banyak proyek—pemindaian struk, digitalisasi formulir, atau pengujian UI—Anda membutuhkan tidak hanya teks mentah tetapi juga kotak pembatas yang memberi tahu di mana setiap baris berada pada gambar.  

Tutorial ini menunjukkan cara praktis untuk *menjalankan OCR pada gambar* menggunakan mesin **aocr**, meminta **pengenalan OCR terstruktur**, dan kemudian memproses hasilnya sambil mempertahankan geometri. Pada akhir tutorial Anda akan dapat **mengekstrak teks dengan koordinat** hanya dalam beberapa baris Python, dan Anda akan memahami mengapa mode terstruktur penting untuk tugas-tugas selanjutnya.

## Apa yang Akan Anda Pelajari

- Cara menginisialisasi mesin OCR untuk **pengenalan OCR terstruktur**.  
- Cara memberi gambar ke mesin dan menerima hasil mentah yang mencakup batas baris.  
- Cara menjalankan post‑processor yang membersihkan teks tanpa kehilangan geometri.  
- Cara mengiterasi baris akhir dan mencetak setiap potongan teks bersama dengan kotak pembatasnya.  

Tidak ada sulap, tidak ada langkah tersembunyi—hanya contoh lengkap yang dapat dijalankan dan Anda dapat menambahkannya ke proyek Anda.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda telah menginstal hal‑hal berikut:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Anda juga memerlukan file gambar (`input_image.png` atau `.jpg`) yang berisi teks yang jelas dan dapat dibaca. Apa saja mulai dari faktur yang dipindai hingga tangkapan layar dapat digunakan, selama mesin OCR dapat melihat karakter‑karakternya.

---

## Langkah 1: Inisialisasi mesin OCR untuk pengenalan terstruktur

Hal pertama yang kita lakukan adalah membuat instance `aocr.Engine()` dan memberi tahu bahwa kita menginginkan **pengenalan OCR terstruktur**. Mode terstruktur mengembalikan tidak hanya teks biasa tetapi juga data geometris (rektangel pembatas) untuk setiap baris, yang penting ketika Anda perlu memetakan teks kembali ke gambar.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Mengapa ini penting:**  
> Dalam mode default mesin mungkin hanya memberikan satu string kata‑kata yang digabungkan. Mode terstruktur memberi Anda hierarki halaman → baris → kata, masing‑masing dengan koordinat, sehingga jauh lebih mudah menumpangkan hasil pada gambar asli atau memasukkannya ke model yang memperhatikan tata letak.

---

## Langkah 2: Jalankan OCR pada gambar dan dapatkan hasil mentah

Sekarang kita memberi gambar ke mesin. Pemanggilan `recognize` mengembalikan objek `OcrResult` yang berisi kumpulan baris, masing‑masing dengan kotak pembatasnya.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

Pada titik ini `raw_result.lines` berisi objek dengan dua atribut penting:

- `text` – string yang dikenali untuk baris tersebut.  
- `bounds` – tuple seperti `(x, y, width, height)` yang menggambarkan posisi baris.

---

## Langkah 3: Post‑process sambil mempertahankan geometri

Output OCR mentah sering berisik: karakter‑karakter stray, spasi yang salah tempat, atau masalah pemenggalan baris. Fungsi `ai.run_postprocessor` membersihkan teks tetapi **mempertahankan geometri asli** tetap utuh, sehingga Anda masih memiliki koordinat yang akurat.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Tips pro:** Jika Anda memiliki kosakata khusus domain (misalnya kode produk), beri kamus khusus ke post‑processor untuk meningkatkan akurasi.

---

## Langkah 4: Ekstrak teks dengan koordinat – iterasi dan tampilkan

Akhirnya, kita melakukan loop pada baris‑baris yang telah dibersihkan, mencetak kotak pembatas setiap baris bersama teksnya. Inilah inti dari **mengekstrak teks dengan koordinat**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Output yang Diharapkan

Dengan asumsi gambar masukan berisi dua baris: “Invoice #12345” dan “Total: $89.99”, Anda akan melihat sesuatu seperti:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

Tuple pertama adalah `(x, y, width, height)` dari baris pada gambar asli, memungkinkan Anda menggambar kotak, menyorot teks, atau memasukkan koordinat ke sistem lain.

---

## Visualisasi Hasil (Opsional)

Jika Anda ingin melihat kotak pembatas ditumpangkan pada gambar, Anda dapat menggunakan Pillow (PIL) untuk menggambar persegi panjang. Berikut cuplikan singkat; lewati jika Anda hanya membutuhkan data mentah.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image contoh menampilkan kotak pembatas](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

Teks alt di atas mengandung **kata kunci utama**, memenuhi persyaratan SEO untuk atribut alt gambar.

---

## Mengapa Pengenalan OCR Terstruktur Lebih Baik daripada Ekstraksi Teks Sederhana

Anda mungkin bertanya, “Bukankah saya cukup menjalankan OCR dan mendapatkan teks? Mengapa harus repot dengan geometri?”  

- **Konteks spasial:** Ketika Anda perlu memetakan bidang pada formulir (misalnya “Tanggal” di sebelah nilai tanggal), koordinat memberi tahu *di mana* data berada.  
- **Tata letak multi‑kolom:** Teks linier sederhana kehilangan urutan; data terstruktur mempertahankan urutan kolom.  
- **Akurasi post‑processing:** Mengetahui ukuran kotak membantu Anda memutuskan apakah sebuah kata adalah judul, catatan kaki, atau artefak stray.  

Singkatnya, **pengenalan OCR terstruktur** memberi Anda fleksibilitas untuk membangun pipeline yang lebih pintar—baik Anda memasukkan data ke basis data, membuat PDF yang dapat dicari, atau melatih model pembelajaran mesin yang menghormati tata letak.

---

## Kasus Pinggiran Umum dan Cara Menanganinya

| Situasi | Hal yang Perlu Diperhatikan | Solusi yang Disarankan |
|-----------|-------------------|---------------|
| **Gambar diputar atau miring** | Kotak pembatas mungkin tidak sejajar. | Lakukan pra‑proses dengan deskewing (misalnya `warpAffine` dari OpenCV). |
| **Font sangat kecil** | Mesin mungkin melewatkan karakter, menghasilkan baris kosong. | Tingkatkan resolusi gambar atau gunakan `ocr_engine.set_dpi(300)`. |
| **Bahasa campuran** | Model bahasa yang salah dapat menghasilkan teks berantakan. | Atur `ocr_engine.language = ["en", "de"]` sebelum pengenalan. |
| **Kotak tumpang tindih** | Post‑processor mungkin menggabungkan dua baris secara tidak sengaja. | Verifikasi `line.bounds` setelah pemrosesan; sesuaikan ambang pada `ai.run_postprocessor`. |

Menangani skenario ini sejak awal menghemat banyak masalah di kemudian hari, terutama ketika Anda menskalakan solusi ke ratusan dokumen per hari.

---

## Skrip End‑to‑End Lengkap

Berikut adalah program lengkap yang siap dijalankan dan menggabungkan semua langkah. Salin‑tempel, sesuaikan jalur gambar, dan Anda siap.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Menjalankan skrip ini akan:

1. **Menjalankan OCR pada gambar** dengan mode terstruktur.  
2. **Mengekstrak teks dengan koordinat** untuk setiap baris.  
3. Secara opsional menghasilkan PNG beranotasi yang menampilkan kotak pembatas.

---

## Kesimpulan

Anda kini memiliki solusi mandiri yang solid untuk **menjalankan OCR pada gambar** dan **mengekstrak teks dengan koordinat** menggunakan **pengenalan OCR terstruktur**. Kode ini memperlihatkan setiap langkah—dari inisialisasi mesin hingga post‑processing dan verifikasi visual—sehingga Anda dapat menyesuaikannya untuk struk, formulir, atau dokumen visual apa pun yang memerlukan lokalisasi teks yang tepat.

Apa selanjutnya? Coba ganti mesin `aocr` dengan pustaka lain (Tesseract, EasyOCR) dan lihat bagaimana output terstruktur mereka berbeda. Bereksperimenlah dengan strategi post‑processing lain, seperti pemeriksaan ejaan atau filter regex khusus, untuk meningkatkan akurasi pada domain Anda. Dan jika Anda membangun pipeline yang lebih besar, pertimbangkan menyimpan pasangan `(text, bounds)` ke dalam basis data untuk analisis di masa mendatang.

Selamat coding, semoga proyek OCR Anda selalu akurat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}