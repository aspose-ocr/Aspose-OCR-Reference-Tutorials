---
category: general
date: 2026-03-26
description: Cara menjalankan OCR pada file PNG dan mengekstrak teks dari gambar dengan
  kamus khusus untuk meningkatkan akurasi OCR. Pelajari cara memuat gambar untuk OCR
  dengan cepat.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: id
og_description: Cara menjalankan OCR pada file PNG dan mengekstrak teks dari gambar
  dengan kamus khusus untuk meningkatkan akurasi OCR. Panduan langkah demi langkah.
og_title: Cara Menjalankan OCR – Mengekstrak Teks dari Gambar dengan Python
tags:
- OCR
- Python
- Image Processing
title: Cara Menjalankan OCR – Mengekstrak Teks dari Gambar dengan Python
url: /id/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR – Ekstrak Teks dari Gambar dengan Python

Pernah bertanya‑tanya **cara menjalankan OCR** pada faktur yang dipindai atau tangkapan layar dan mendapatkan teks bersih yang dapat dicari? Anda tidak sendirian. Dalam banyak proyek, kendala utama hanyalah memuat gambar untuk OCR dan kemudian memaksa mesin memahami kata‑kata khusus domain.  

Di tutorial ini kita akan membahas contoh lengkap yang siap dijalankan yang **mengekstrak teks dari file gambar**, menunjukkan cara **mengenali teks dari PNG**, dan bahkan memperlihatkan trik untuk **meningkatkan akurasi OCR** dengan kamus khusus dan karakter khusus. Pada akhir tutorial Anda akan memiliki skrip mandiri yang dapat dimasukkan ke dalam basis kode Python mana pun.

## Apa yang Anda Butuhkan

- Python 3.8+ (kode menggunakan type hints tetapi dapat berjalan pada versi 3.x sebelumnya)
- Library `ocr` yang disertakan dengan mesin OCR yang Anda targetkan (pasang via `pip install ocr‑engine` – ganti dengan nama paket yang sebenarnya)
- File gambar (`input.png`) yang ingin Anda proses
- Opsional: file teks biasa (`invoice_terms.txt`) yang berisi kata‑kata khusus domain, satu per baris

Tidak ada ketergantungan eksternal yang berat, tidak ada kunci API cloud, hanya mesin OCR lokal.

---

## Langkah 1: Pasang dan Impor Library OCR

Pertama, pastikan paket OCR sudah terpasang. Jika Anda menggunakan paket hipotetik `ocr-engine`, jalankan:

```bash
pip install ocr-engine
```

Sekarang impor kelas‑kelas yang Anda perlukan:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Pro tip:** Jika Anda berada di lingkungan virtual, aktifkan dulu sebelum memasang agar Python global tetap bersih.

## Langkah 2: Buat Instance Mesin OCR

Membuat objek mesin adalah titik masuk untuk setiap tugas OCR. Anggap saja ini seperti menyalakan perangkat pemindai secara virtual.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Mengapa ini penting: mesin menyimpan konfigurasi seperti paket bahasa, mode pengenalan, dan sumber daya khusus yang akan Anda lampirkan nanti. Tanpa mesin, Anda tidak dapat **memuat gambar untuk OCR** atau menjalankan pipeline pengenalan.

## Langkah 3: Muat Gambar yang Ingin Diakui

Di sini kita benar‑benar **memuat gambar untuk OCR**. Metode `Imaging.Image.load()` membaca file dan mengubahnya menjadi format bitmap internal yang diharapkan mesin.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Jika Anda memiliki JPEG atau TIFF, metode yang sama tetap berlaku—cukup ubah ekstensi. Mesin secara otomatis mendeteksi formatnya.

> **Kasus tepi:** Gambar yang sangat besar (lebih dari 5 MP) dapat menyebabkan lonjakan memori. Pertimbangkan untuk menurunkan skala dengan Pillow sebelum memuat jika Anda mengalami masalah performa.

## Langkah 4: Sediakan Kamus Khusus untuk Meningkatkan Akurasi

Sebagian besar mesin OCR dilengkapi dengan model bahasa generik. Untuk faktur, kwitansi, atau dokumen hukum Anda sering menemukan kata yang terlewat. Menyediakan daftar kata khusus memberi tahu mesin “istilah ini sah, perlakukan sebagai benar”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Entri tipikal mungkin berupa:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Menambahkan entri ini meningkatkan metrik **meningkatkan akurasi OCR** secara dramatis—terutama untuk simbol non‑ASCII.

## Langkah 5: Tambahkan Karakter Khusus yang Tidak Ada di Set Default

Jika domain Anda menggunakan simbol seperti tanda Euro (€) atau Ø Skandinavia, Anda dapat menambahkannya secara eksplisit:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

Mesin kini akan memperlakukan glyph tersebut sebagai valid selama fase pengenalan, mengurangi kemungkinan output “sampah”.

## Langkah 6: Jalankan Proses OCR dan Dapatkan Teks

Akhirnya, panggil recognizer dan ambil hasil teks mentah. Pemanggilan `recognize()` mengembalikan objek kaya; kita hanya membutuhkan string mentah untuk kebanyakan kasus penggunaan.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Jika output terlihat berantakan, periksa kembali apakah kamus khusus dan karakter khusus sudah dimuat dengan benar.

---

## Gambaran Visual

![how to run OCR diagram](ocr-workflow.png){alt="how to run OCR diagram"}

Diagram di atas menggambarkan alur dari memuat gambar hingga mendapatkan teks bersih, menyoroti titik di mana Anda dapat menyuntikkan kamus khusus dan set karakter.

---

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

### Apakah ini bekerja dengan PDF multi‑halaman?

Ya—cukup konversi setiap halaman menjadi PNG (menggunakan `pdf2image` atau serupa) dan berikan secara berurutan ke instance `ocr_engine` yang sama. Mesin memproses tiap gambar secara independen, sehingga Anda akan mendapatkan daftar string yang dapat digabungkan.

### Bagaimana jika gambar diputar?

Sebagian besar mesin OCR modern mendeteksi orientasi secara otomatis, tetapi Anda dapat memaksa rotasi dengan:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Bagaimana menangani bahasa selain Inggris?

Ganti model bahasa sebelum memuat gambar:

```python
ocr_engine.set_language("de")  # German
```

Pastikan paket bahasa yang bersangkutan sudah terpasang.

---

## Skrip Lengkap – Siap Salin & Tempel

Berikut seluruh program, siap dijalankan setelah Anda mengganti jalur placeholder.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Jalankan dengan:

```bash
python run_ocr.py
```

Anda akan melihat teks yang diekstrak tercetak di konsol. Dari sana Anda dapat menulisnya ke file, memasukkannya ke basis data, atau mengirimnya ke pipeline NLP selanjutnya.

---

## Ringkasan & Langkah Selanjutnya

Kami telah membahas **cara menjalankan OCR** pada PNG, cara **mengekstrak teks dari gambar**, dan menunjukkan cara praktis **mengenali teks dari PNG** sambil **meningkatkan akurasi OCR** dengan kamus dan karakter khusus.  

Selanjutnya, pertimbangkan:

- **Pemrosesan batch:** Loop melalui direktori gambar.
- **Pasca‑pemrosesan:** Gunakan regex untuk mengekstrak nomor faktur atau tanggal.
- **Integrasi:** Sambungkan skrip ke API Flask untuk layanan OCR on‑demand.

Jika Anda tertarik pada topik yang lebih maju, lihat tutorial tentang **memuat gambar untuk OCR** dengan pra‑pemrosesan OpenCV, atau selami model OCR berbasis deep‑learning seperti Tesseract 4+ dengan lapisan LSTM.

---

### Terus Bereksperimen!

Coba ganti `invoice_terms.txt` dengan daftar istilah medis, tambahkan karakter Yunani, atau beri mesin foto beresolusi rendah untuk melihat seberapa jauh akurasi dapat ditingkatkan. Semakin banyak Anda bereksperimen, semakin baik Anda memahami trade‑off antara pra‑pemrosesan, kosakata khusus, dan pengaturan mesin.

Selamat coding, semoga hasil OCR Anda selalu tajam!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}