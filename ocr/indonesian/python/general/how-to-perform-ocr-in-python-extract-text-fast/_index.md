---
category: general
date: 2026-03-26
description: Pelajari cara melakukan OCR di Python dan dengan mudah mengekstrak teks
  dari gambar, membaca teks dari pemindaian, atau mengekstrak teks dari faktur menggunakan
  OcrEngine sederhana.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: id
og_description: Bagaimana melakukan OCR di Python? Panduan ini menunjukkan cara mengekstrak
  teks dari gambar, membaca teks dari pemindaian, dan mengekstrak teks dari faktur
  dalam hitungan menit.
og_title: Cara Melakukan OCR di Python – Ekstrak Teks dengan Cepat
tags:
- OCR
- Python
- Image Processing
title: Cara Melakukan OCR di Python – Ekstrak Teks dengan Cepat
url: /id/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di Python – Ekstrak Teks dengan Cepat

Pernah bertanya-tanya **bagaimana cara melakukan OCR** pada kwitansi yang dipindai atau PDF yang buram? Anda tidak sendirian. Dalam banyak proyek kebutuhan untuk **mengekstrak teks dari gambar** muncul lebih cepat daripada yang diperkirakan, dan pendekatan “mengetik semuanya secara manual” tidak dapat diskalakan.  

Dalam tutorial ini Anda akan melihat contoh lengkap yang siap dijalankan yang menunjukkan **cara menggunakan OCR** untuk membaca teks dari pemindaian, mengambil data dari faktur, dan bahkan menangani koreksi kemiringan otomatis—semua dengan hanya beberapa baris Python.

## Apa yang Akan Anda Pelajari

* Dependensi dan impor yang tepat diperlukan.
* Cara membuat dan mengonfigurasi instance `OcrEngine`.
* Cara **mengekstrak teks dari gambar**, **membaca teks dari pemindaian**, dan **mengekstrak teks dari faktur** menggunakan mesin yang sama.
* Kesalahan umum (bahasa salah, file hilang, gambar besar) dan cara menghindarinya.
* Output yang diharapkan sehingga Anda dapat memverifikasi bahwa OCR berhasil.

Tidak diperlukan tautan dokumentasi eksternal—semua bersifat mandiri, sehingga Anda dapat menyalin‑tempel kode dan melihat hasilnya segera.

## Prasyarat

Sebelum kita menyelam lebih dalam, pastikan Anda memiliki:

* Python 3.8+ terinstal (paket `ocr` bekerja dengan versi terbaru apa pun).
* Perpustakaan `ocr` tersedia (`pip install ocr‑engine` – ganti dengan nama paket yang sebenarnya jika berbeda).
* File gambar yang ingin Anda proses – untuk demo kita akan menggunakan `invoice.png` yang berada di folder bernama `YOUR_DIRECTORY`.

Itu saja. Jika Anda sudah memiliki semua ini, Anda siap melanjutkan.

## Langkah 1: Instal dan Impor Modul OCR

Pertama-tama: kita membutuhkan perpustakaan OCR. Jika Anda belum menginstalnya, jalankan perintah berikut di terminal Anda:

```bash
pip install ocr-engine
```

Sekarang kita mengimpor modul dalam skrip kita.

```python
# Step 1: Import the OCR module
import ocr
```

> **Tip profesional:** Jaga lingkungan virtual Anda tetap rapi; ini mencegah bentrok versi ketika Anda kemudian menambahkan paket pemrosesan gambar lainnya.

## Langkah 2: Buat dan Konfigurasikan Mesin OCR

Membuat mesin ini semudah memanggil konstruktornya, tetapi kekuatan sebenarnya terletak pada mengkonfigurasikannya dengan tepat. Kami akan mengatur bahasa ke English dan mengaktifkan koreksi kemiringan otomatis, yang penting saat menangani faktur yang dipindai yang tidak sejajar sempurna.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Mengapa mengaktifkan `auto_skew`? Banyak pemindai menghasilkan gambar yang sedikit miring beberapa derajat. Tanpa koreksi, mesin dapat melewatkan karakter, mengubah faktur yang dapat dibaca dengan sempurna menjadi tidak dapat dipahami.

## Langkah 3: Lakukan OCR pada Gambar Target Anda

Sekarang kami memasukkan file gambar ke dalam mesin. Metode `recognize_image` mengembalikan objek yang berisi teks mentah serta skor kepercayaan (jika perpustakaan menyediakannya).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Jika Anda bekerja dengan skenario **membaca teks dari pemindaian**, cukup ganti path dengan PDF yang dipindai yang telah dikonversi ke PNG atau JPEG. Pemanggilan yang sama bekerja untuk format gambar apa pun yang didukung perpustakaan di bawahnya.

## Langkah 4: Periksa dan Gunakan Teks yang Diekstrak

Mari cetak output OCR mentah. Dalam alur pemrosesan faktur dunia nyata, Anda mungkin akan mengurai string ini, mengekstrak item baris, total, dan tanggal, tetapi untuk saat ini sekilas cepat akan mengonfirmasi bahwa OCR berhasil.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Output yang diharapkan (dipotong untuk singkat):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Jika output terlihat berantakan, periksa kembali bahwa gambar jelas dan bahwa `engine.language` cocok dengan bahasa dokumen.

## Langkah 5: Menangani Kasus Pinggir Umum

### Gambar Besar

Memproses pemindaian 5000 × 5000 piksel dapat memakan banyak memori. Cara cepat untuk mengurangi hal ini adalah memperkecil ukuran gambar sebelum mengirimkannya ke mesin:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Banyak Bahasa

Jika Anda perlu **mengekstrak teks dari gambar** yang berisi bahasa Inggris dan Spanyol, Anda dapat mengatur daftar bahasa:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

Mesin akan berusaha mengenali karakter dari kedua set.

### Penanganan Kesalahan

Jangan pernah mengasumsikan file ada. Bungkus pemanggilan dalam blok try‑except untuk memberikan pesan yang ramah:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Referensi Visual

Di bawah ini adalah tangkapan layar contoh faktur yang kami gunakan dalam demo. Perhatikan kemiringan ringan—tepat apa yang diperbaiki oleh `auto_skew`.

![cara melakukan OCR pada gambar faktur](/images/ocr-example.png)

*Alt text:* cara melakukan OCR pada gambar faktur yang menunjukkan koreksi kemiringan otomatis.

## Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semuanya, berikut satu skrip yang dapat Anda jalankan dari baris perintah. Skrip ini mencakup instalasi, konfigurasi, penanganan kesalahan, dan langkah pasca‑pemrosesan sederhana yang menulis teks yang diekstrak ke file bernama `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Menjalankan `python full_ocr_demo.py` akan mencetak teks yang diekstrak ke konsol dan menyimpannya di `output.txt`. Dari sana Anda dapat menerapkan ekspresi reguler, penulis CSV, atau logika lain yang Anda perlukan untuk otomatisasi **mengekstrak teks dari faktur**.

## Kesimpulan

Anda sekarang memiliki jawaban yang solid, menyeluruh untuk **cara melakukan OCR** di Python. Dengan membuat `OcrEngine`, mengkonfigurasi bahasa dan koreksi kemiringan, serta menangani beberapa kasus pinggir praktis, Anda dapat dengan andal **mengekstrak teks dari gambar**, **membaca teks dari pemindaian**, dan **mengekstrak teks dari faktur** tanpa harus mencari dokumentasi yang tersebar.

Apa selanjutnya? Cobalah memproses sekumpulan file dalam loop, bereksperimen dengan bahasa yang berbeda, atau menghubungkan output ke perpustakaan pembuatan PDF untuk membuat PDF yang dapat dicari. Tidak ada batasan, dan kode yang baru saja Anda lihat adalah landasan yang kuat.

Ada pertanyaan tentang format file tertentu atau membutuhkan bantuan menyesuaikan ambang kepercayaan? Tinggalkan komentar di bawah—senang membantu Anda menyempurnakan pipeline OCR Anda!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}