---
category: general
date: 2026-06-25
description: Pelajari cara mengenali tulisan tangan dengan Python OCR. Contoh Python
  OCR ini memandu Anda melalui proses mengekstrak teks tulisan tangan dan memuat gambar
  untuk OCR.
draft: false
keywords:
- how to recognize handwriting
- extract handwritten text
- convert handwritten image
- python ocr example
- load image for ocr
language: id
og_description: Cara mengenali tulisan tangan di Python menggunakan perpustakaan OCR
  sederhana. Ikuti panduan langkah demi langkah ini untuk mengekstrak teks tulisan
  tangan dari gambar apa pun.
og_title: Cara Mengenali Tulisan Tangan di Python – Tutorial OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to recognize handwriting with Python OCR. This python ocr
    example walks you through extracting handwritten text and loading image for OCR.
  headline: How to Recognize Handwriting in Python – Complete OCR Guide
  type: TechArticle
- questions:
  - answer: Convert the first page to PNG using `pdf2image` before feeding it to `aocr`.
    question: What if my image is a PDF?
  - answer: Try increasing the DPI when you scan (300 dpi or higher) and ensure good
      lighting—shadows trick the model.
    question: Can I improve accuracy on cursive notes?
  - answer: Wrap the script in a loop that iterates over a directory, reusing the
      same `engine` instance for speed.
    question: Is there a way to batch‑process many files?
  - answer: As of v23.12 `aocr` supports English only; for other languages you’ll
      need a different library (e.g., Tesseract with language packs).
    question: What about non‑English handwriting?
  type: FAQPage
tags:
- OCR
- Python
- Handwriting Recognition
title: Cara Mengenali Tulisan Tangan di Python – Panduan OCR Lengkap
url: /id/python/general/how-to-recognize-handwriting-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengenali Tulisan Tangan di Python – Panduan OCR Lengkap

Pernah bertanya-tanya **bagaimana cara mengenali tulisan tangan** dalam foto yang Anda ambil dengan ponsel? Anda tidak sendirian. Banyak pengembang mengalami kesulitan yang sama ketika mereka perlu mengambil catatan tulisan tangan, tanda tangan, atau coretan untuk entri data. Kabar baiknya? Dengan beberapa baris Python Anda dapat mengubah pemindaian berantakan menjadi teks bersih yang dapat dicari.

Dalam tutorial ini kami akan membahas **python ocr example** yang menunjukkan secara tepat cara **extract handwritten text**, **convert handwritten image** data menjadi string, dan **load image for OCR** menggunakan pustaka `aocr`. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang dapat Anda masukkan ke proyek mana pun—tanpa sulap, hanya kode yang jelas dan penjelasan mengapa ia bekerja.

## Prasyarat & Penyiapan

Sebelum kita menyelam, pastikan Anda memiliki:

- Python 3.8+ terinstal (pustaka ini bekerja pada semua versi terbaru).
- Terminal atau command prompt yang Anda kuasai.
- File gambar yang berisi teks tulisan tangan campuran (kami akan menyebutnya `handwritten_mixed.png`).

Jika ada yang belum Anda kenal, berhentilah sejenak dan selesaikan dulu—jika tidak, langkah‑langkah berikut akan terasa seperti mencoba membuat kue tanpa tepung.

### Instal pustaka OCR

Paket `aocr` bukan bagian dari pustaka standar, jadi dapatkan dari PyPI:

```bash
pip install aocr
```

> **Pro tip:** Gunakan lingkungan virtual (`python -m venv venv`) untuk menjaga ketergantungan tetap rapi.

## Langkah 1: Impor pustaka OCR dan buat instance engine

Membuat engine adalah hal pertama yang Anda lakukan ketika ingin **recognize handwriting**. Anggap engine sebagai otak yang akan melihat gambar Anda dan mulai menebak huruf.

```python
# Step 1: Import the OCR library and instantiate the engine
import aocr

# The OcrEngine object holds all configuration and state
engine = aocr.OcrEngine()
```

Mengapa kita membutuhkan objek? `OcrEngine` memungkinkan Anda menyesuaikan pengaturan—seperti beralih antara mode teks cetak dan mode tulisan tangan—tanpa harus membuat ulang seluruh pipeline setiap kali.

## Langkah 2: Muat gambar untuk OCR

Sekarang kita benar‑benarnya **load image for OCR**. Jalur dapat berupa absolut atau relatif; pastikan file tersebut ada.

```python
# Step 2: Load the image containing mixed handwritten text
image_path = "YOUR_DIRECTORY/handwritten_mixed.png"
engine.load_image(image_path)
```

Jika gambar berukuran besar, `aocr` secara otomatis akan menurunkan skala ke ukuran yang wajar, tetapi Anda juga dapat memberikan argumen tambahan untuk mengontrol DPI atau mode warna. Fleksibilitas ini membantu ketika Anda perlu **convert handwritten image** data yang berasal dari berbagai sumber (scanner, ponsel, PDF).

## Langkah 3: Aktifkan mode pengenalan tulisan tangan

Pengenalan tulisan tangan tidak selalu aktif secara default. Mulai versi 23.12 pustaka ini memperkenalkan mode khusus, yang secara dramatis meningkatkan akurasi pada skrip kursif atau miring.

```python
# Step 3: Turn on handwritten mode (available from v23.12)
engine.recognition_mode = aocr.RecognitionMode.HANDWRITTEN
```

Di balik layar, engine mengganti model internalnya dengan model yang dilatih pada jutaan goresan pena. Jika Anda melewatkan langkah ini, Anda akan mendapatkan hasil teks cetak yang tampak seperti omong kosong.

## Langkah 4: Lakukan OCR dan dapatkan hasilnya

Setelah semuanya siap, minta engine melakukan tugasnya. Pemanggilan `recognize()` bersifat sinkron—ia menunggu hingga teks siap.

```python
# Step 4: Run OCR on the loaded image
result = engine.recognize()
```

Variabel `result` adalah string Python biasa, sehingga Anda dapat memperlakukannya seperti teks lainnya—menyimpannya, mencarinya, atau mengirimkannya ke sistem lain.

## Langkah 5: Tampilkan teks tulisan tangan yang diekstrak

Akhirnya, cetak output sehingga Anda dapat memverifikasi bahwa langkah **extract handwritten text** berhasil.

```python
# Step 5: Show the recognized handwriting
print("Handwritten mixed text:")
print(result)
```

### Output yang diharapkan

Jika `handwritten_mixed.png` berisi sesuatu seperti:

```
Dear Alice,
Meet me at 5pm.
- Bob
```

Anda akan melihat:

```
Handwritten mixed text:
Dear Alice,
Meet me at 5pm.
- Bob
```

Perhatikan bagaimana baris baru dipertahankan—`aocr` menghormati tata letak asli, yang berguna ketika Anda nanti perlu memformat ulang data.

## Skrip Lengkap – Jalankan Sekali Klik

Menggabungkan semuanya, berikut contoh lengkap yang dapat dijalankan. Salin‑tempel ke file bernama `handwriting_ocr.py` dan jalankan `python handwriting_ocr.py`.

```python
import aocr

def main():
    # 1️⃣ Create the OCR engine
    engine = aocr.OcrEngine()

    # 2️⃣ Load the target image
    image_path = "YOUR_DIRECTORY/handwritten_mixed.png"
    engine.load_image(image_path)

    # 3️⃣ Switch to handwritten mode (v23.12+)
    engine.recognition_mode = aocr.RecognitionMode.HANDWRITTEN

    # 4️⃣ Run the recognition process
    result = engine.recognize()

    # 5️⃣ Print the extracted text
    print("Handwritten mixed text:")
    print(result)

if __name__ == "__main__":
    main()
```

> **Catatan kasus tepi:** Jika gambar sepenuhnya kosong atau hanya berisi teks cetak, engine akan mengembalikan string kosong atau hasil dengan kepercayaan rendah. Anda dapat memeriksa `engine.last_confidence` (jika pustaka mengekspose‑nya) untuk memutuskan apakah harus mencoba lagi dengan langkah pra‑pemrosesan yang berbeda.

## Pertanyaan Umum & Tips

- **What if my image is a PDF?** Konversi halaman pertama ke PNG menggunakan `pdf2image` sebelum memasukkannya ke `aocr`.
- **Can I improve accuracy on cursive notes?** Coba tingkatkan DPI saat memindai (300 dpi atau lebih) dan pastikan pencahayaan baik—bayangan dapat menipu model.
- **Is there a way to batch‑process many files?** Bungkus skrip dalam loop yang mengiterasi direktori, menggunakan kembali instance `engine` yang sama untuk kecepatan.
- **What about non‑English handwriting?** Mulai v23.12 `aocr` hanya mendukung bahasa Inggris; untuk bahasa lain Anda memerlukan pustaka lain (misalnya, Tesseract dengan paket bahasa).

## Ringkasan Visual

![how to recognize handwriting example output](/images/handwriting_ocr_output.png)

*Alt text:* contoh cara mengenali tulisan tangan yang menampilkan teks yang diekstrak dari gambar tulisan tangan campuran.

## Kesimpulan

Anda kini tahu **how to recognize handwriting** di Python menggunakan pustaka OCR yang sederhana. Dengan mengikuti **python ocr example** ini Anda dapat **extract handwritten text**, **convert handwritten image** data menjadi string yang dapat digunakan, dan secara andal **load image for OCR** hanya dalam beberapa baris kode.

Siap untuk tantangan berikutnya? Coba masukkan output ke parser bahasa alami, simpan di basis data, atau rangkaikan dengan mesin sintesis suara untuk membaca catatan Anda dengan suara. Kemungkinannya tak terbatas seperti coretan di serbet.

---

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah dan kami akan membantu memecahkannya bersama.*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}