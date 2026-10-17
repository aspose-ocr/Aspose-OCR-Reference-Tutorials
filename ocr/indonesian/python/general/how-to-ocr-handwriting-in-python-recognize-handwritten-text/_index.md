---
category: general
date: 2026-06-28
description: Cara melakukan OCR tulisan tangan di Python dengan cepat. Pelajari cara
  mengenali teks tulisan tangan, mengonversi gambar catatan tulisan tangan, dan mengekstrak
  teks dari tulisan tangan menggunakan Aspose OCR.
draft: false
keywords:
- how to ocr handwriting
- recognize handwritten text
- convert handwritten note
- handwritten text extraction
- extract text from handwriting
language: id
og_description: Cara melakukan OCR tulisan tangan di Python. Panduan ini menunjukkan
  cara mengenali teks tulisan tangan, mengonversi gambar catatan tulisan tangan, dan
  mengekstrak teks dari tulisan tangan dengan Aspose OCR.
og_title: Cara OCR Tulisan Tangan di Python – Mengenali Teks Tulisan Tangan
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to OCR handwriting in Python quickly. Learn to recognize handwritten
    text, convert handwritten note images and extract text from handwriting using
    Aspose OCR.
  headline: How to OCR Handwriting in Python – Recognize Handwritten Text
  type: TechArticle
tags:
- OCR
- Python
- HandwritingRecognition
title: Cara OCR Tulisan Tangan di Python – Mengenali Teks Tulisan Tangan
url: /id/python/general/how-to-ocr-handwriting-in-python-recognize-handwritten-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR Tulisan Tangan di Python – Mengenali Teks Tulisan Tangan

Pernah bertanya-tanya **cara OCR tulisan tangan** langsung dari foto buku catatan Anda? Anda tidak sendirian. Dalam banyak proyek—baik Anda mendigitalkan notulen rapat atau membangun aplikasi pencatatan—**mengenali teks tulisan tangan** adalah potongan yang hilang yang mengubah gambar berantakan menjadi data yang dapat dicari.

Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang **mengonversi gambar catatan tulisan tangan** menjadi string biasa. Pada akhir tutorial Anda akan dapat **mengekstrak teks dari tulisan tangan** dengan hanya beberapa baris kode Python, tanpa perpustakaan misterius yang tersembunyi.

## Prasyarat – Apa yang Anda Butuhkan Sebelum Memulai

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Sintaks modern dan petunjuk tipe |
| `aspose-ocr` package | Menyediakan kelas `OcrEngine` dan `Image` yang digunakan di bawah |
| File gambar yang berisi teks tulisan tangan (misalnya `handwritten_note.jpg`) | Ini adalah sumber untuk **ekstraksi teks tulisan tangan** |
| Pemahaman dasar tentang lingkungan virtual (opsional tetapi disarankan) | Menjaga ketergantungan tetap rapi |

Anda dapat menginstal pustaka Aspose OCR dengan pip:

```bash
pip install aspose-ocr
```

> **Tip pro:** Jika Anda bekerja di dalam lingkungan virtual, aktifkan terlebih dahulu (`python -m venv venv && source venv/bin/activate`) untuk menghindari pencemaran paket situs global Anda.

## Langkah 1 – Membuat Instance Mesin OCR (Cara OCR Tulisan Tangan)

Hal pertama yang Anda lakukan ketika ingin **cara OCR tulisan tangan** adalah membuat objek mesin. Anggaplah itu sebagai otak yang akan menafsirkan goresan pada halaman Anda.

```python
from aspose.ocr import OcrEngine, OcrRecognitionMode, Image

# Step 1: Initialize the OCR engine
engine = OcrEngine()
```

> `Kelas `OcrEngine` ringan; Anda dapat membuat banyak instance jika membutuhkan pemrosesan paralel. Di sini kami menyederhanakannya dengan satu mesin.`

## Langkah 2 – Memuat Gambar Tulisan Tangan Anda (Mengonversi Catatan Tulisan Tangan)

Selanjutnya, kami memberi mesin gambar catatan tulisan tangan yang ingin Anda digitalisasi. Pembantu `Image.from_file` membaca format umum seperti JPEG, PNG, atau BMP.

```python
# Step 2: Load the image that contains the handwritten note
engine.set_image(Image.from_file("YOUR_DIRECTORY/handwritten_note.jpg"))
```

> Pastikan jalur mengarah ke lokasi tepat file Anda. Jika gambar buram, akurasi OCR akan menurun—pertimbangkan pra‑pemrosesan (peningkatan kontras, pengurangan noise) sebelum langkah ini.

## Langkah 3 – Beralih ke Mode Pengakuan Tulisan Tangan (Mengenali Teks Tulisan Tangan)

Secara default, Aspose OCR mengasumsikan teks cetak. Untuk **mengenali teks tulisan tangan**, Anda harus secara eksplisit mengaktifkan mode tulisan tangan *sebelum* memanggil `recognize()`.

```python
# Step 3: Enable handwritten recognition mode
engine.recognition_mode = OcrRecognitionMode.HANDWRITTEN
```

> Mengapa mengatur flag ini lebih awal? Mesin memuat model bahasa yang berbeda berdasarkan mode, dan mengubahnya setelah memuat gambar dapat menyebabkan fallback diam-diam ke pengenalan teks cetak, menghasilkan teks yang tidak dapat dibaca.

## Langkah 4 – Melakukan OCR (Ekstraksi Teks Tulisan Tangan)

Sekarang keajaiban terjadi. Pemanggilan `recognize()` memindai gambar, menerapkan model tulisan tangan, dan mengembalikan string teks biasa.

```python
# Step 4: Run OCR to extract the text
handwritten_text = engine.recognize()
```

> Di balik layar, Aspose menggunakan kombinasi jaringan saraf dan pencocokan pola. Hasilnya berupa Unicode, jadi Anda akan mendapatkan aksen dan karakter khusus yang tepat jika tulisan tangan Anda menyertakannya.

## Langkah 5 – Menampilkan Output yang Diakui (Mengekstrak Teks dari Tulisan Tangan)

Akhirnya, kami cukup mencetak hasilnya. Dalam aplikasi dunia nyata Anda mungkin menyimpannya di basis data atau mengirimkannya ke indeks pencarian.

```python
# Step 5: Show the extracted text
print(handwritten_text)
```

Menjalankan skrip seharusnya menghasilkan sesuatu seperti:

```
Meeting notes:
- Discuss project timeline
- Assign tasks to Alice and Bob
- Review budget next week
```

![contoh output ocr tulisan tangan yang menunjukkan teks yang dikenali dari catatan tulisan tangan](handwriting_ocr_result.png)

*Image alt text: contoh output ocr tulisan tangan yang menunjukkan teks yang dikenali dari catatan tulisan tangan.*

### Skrip Lengkap – Solusi Satu‑Pintu

Menggabungkan semuanya, berikut program lengkap yang dapat dijalankan:

```python
# -*- coding: utf-8 -*-
"""
How to OCR Handwriting in Python – a complete example.
This script loads a handwritten image, enables handwritten mode,
and prints the extracted text.
"""

from aspose.ocr import OcrEngine, OcrRecognitionMode, Image

def ocr_handwritten_image(image_path: str) -> str:
    """Convert a handwritten note image to plain text."""
    engine = OcrEngine()
    engine.set_image(Image.from_file(image_path))
    engine.recognition_mode = OcrRecognitionMode.HANDWRITTEN
    return engine.recognize()

if __name__ == "__main__":
    # Replace with the path to your own image
    result = ocr_handwritten_image("YOUR_DIRECTORY/handwritten_note.jpg")
    print("=== Recognized Handwritten Text ===")
    print(result)
```

Simpan ini sebagai `handwriting_ocr.py` dan jalankan `python handwriting_ocr.py`. Jika semuanya telah diatur dengan benar, Anda akan melihat output **mengonversi catatan tulisan tangan** tercetak di konsol.

## Kesulitan Umum & Kasus Tepi (Ekstraksi Teks Tulisan Tangan)

Bahkan dengan skrip yang solid, Anda mungkin mengalami kendala. Di bawah ini adalah masalah paling umum dan cara menanganinya.

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Gambar buram atau kontras rendah** | Model OCR membutuhkan goresan yang jelas. | Pra‑proses dengan OpenCV: tingkatkan kontras, terapkan binarisasi (`cv2.threshold`). |
| **Konten campuran cetak & tulisan tangan** | Mesin mungkin memilih model yang salah. | Jalankan dua kali: pertama dengan `HANDWRITTEN`, kemudian dengan `PRINTED`, dan gabungkan hasilnya. |
| **Karakter non‑Latin** | Bahasa default adalah Inggris. | Setel `engine.language = "es"` (atau kode ISO lain) sebelum `recognize()`. |
| **Gambar besar menyebabkan kesalahan memori** | Mesin memuat seluruh gambar ke RAM. | Ubah ukuran gambar ke dimensi yang wajar (mis., lebar maks 1024 px) sebelum memuat. |
| **Beberapa halaman dalam satu file** | OCR gambar tunggal hanya mengembalikan halaman pertama. | Loop melalui setiap halaman jika Anda menggunakan PDF atau TIFF multi‑halaman. |

### Menangani Kualitas Gambar Buruk (Tambahan Cepat)

Jika Anda curiga gambar tidak cukup tajam, Anda dapat menambahkan beberapa baris OpenCV sebelum memberikannya ke mesin:

```python
import cv2
import numpy as np

def preprocess_image(path: str) -> Image:
    raw = cv2.imread(path, cv2.IMREAD_GRAYSCALE)
    # Apply Gaussian blur to reduce noise
    blurred = cv2.GaussianBlur(raw, (5, 5), 0)
    # Adaptive threshold to sharpen ink
    thresh = cv2.adaptiveThreshold(
        blurred, 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C,
        cv2.THRESH_BINARY_INV, 11, 2
    )
    # Convert back to Aspose Image
    _, encoded = cv2.imencode('.png', thresh)
    return Image.from_stream(encoded.tobytes())
```

Ganti baris `engine.set_image(...)` dengan `engine.set_image(preprocess_image(image_path))`. Penambahan kecil ini dapat meningkatkan akurasi **ekstraksi teks tulisan tangan** secara dramatis.

## Menguji Implementasi Anda (Verifikasi Ekstraksi)

Cara andal untuk memastikan Anda benar‑benar menguasai **cara OCR tulisan tangan** adalah menulis unit test sederhana. Menggunakan kerangka kerja `unittest` bawaan Python:

```python
import unittest

class TestHandwritingOCR(unittest.TestCase):
    def test_simple_note(self):
        sample_path = "test_samples/simple_note.jpg"
        text = ocr_handwritten_image(sample_path)
        self.assertIn("Meeting", text)   # Expect the word "Meeting" in the result

if __name__ == "__main__":
    unittest.main()
```

Menjalankan `python -m unittest` akan memberi tahu Anda secara langsung apakah mesin mengambil kata‑kata yang diharapkan dari gambar contoh Anda.

## Langkah Selanjutnya – Melampaui Ekstraksi Dasar

Sekarang Anda telah mempelajari **cara OCR tulisan tangan**, pertimbangkan ekstensi berikut:

* **Pemrosesan batch** – Loop over a

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Gambar Teks – Dasar OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-basics/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Cara Mengekstrak Teks dari Gambar dengan Menyiapkan Persegi Panjang dalam OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}