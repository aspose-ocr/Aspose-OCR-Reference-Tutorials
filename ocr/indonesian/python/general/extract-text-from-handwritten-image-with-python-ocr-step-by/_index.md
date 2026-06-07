---
category: general
date: 2026-06-06
description: Ekstrak teks dari gambar tulisan tangan menggunakan Python OCR. Pelajari
  cara mengubah foto tulisan tangan menjadi teks dengan cepat dan andal.
draft: false
keywords:
- extract text from handwritten image
- convert handwritten photo to text
- how to recognize handwritten text
- python ocr handwritten recognition
language: id
og_description: Ekstrak teks dari gambar tulisan tangan dengan Python. Panduan ini
  menunjukkan cara mengubah foto tulisan tangan menjadi teks dan menjawab cara mengenali
  teks tulisan tangan.
og_title: Ekstrak Teks dari Gambar Tulisan Tangan – Tutorial OCR Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from handwritten image using Python OCR. Learn how to
    convert handwritten photo to text quickly and reliably.
  headline: Extract Text from Handwritten Image with Python OCR – Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Handwriting
title: Ekstrak Teks dari Gambar Tulisan Tangan dengan Python OCR – Panduan Langkah
  demi Langkah
url: /id/python/general/extract-text-from-handwritten-image-with-python-ocr-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar Tulisan Tangan dengan Python OCR – Panduan Langkah‑per‑Langkah

Pernah bertanya-tanya **bagaimana cara mengenali teks tulisan tangan** dalam foto yang Anda ambil dengan ponsel? Anda tidak sendirian. Dalam banyak proyek—baik itu mendigitalkan catatan kuliah atau mengambil data dari formulir yang ditandatangani—Anda perlu **mengekstrak teks dari gambar tulisan tangan** dengan cepat dan tanpa masalah.  

Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang siap dijalankan yang menunjukkan secara tepat cara **mengubah foto tulisan tangan menjadi teks** menggunakan pustaka Python OCR yang populer. Tanpa referensi yang samar, hanya kode konkret, penjelasan, dan tip yang dapat Anda salin‑tempel hari ini.

![ekstrak teks dari gambar tulisan tangan](https://example.com/placeholder-handwritten.jpg "ekstrak teks dari gambar tulisan tangan")

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.9 atau lebih baru | Sintaks modern & dukungan pustaka |
| `pip` (manajer paket Python) | Untuk menginstal paket OCR |
| Gambar yang jelas dari catatan tulisan tangan (JPEG/PNG) | Akurasi OCR menurun pada gambar yang buram |
| Pemahaman dasar tentang fungsi Python | Membantu Anda menyesuaikan contoh nanti |

Jika Anda belum memiliki salah satu dari ini, unduh Python terbaru dari <https://python.org> dan instal—tanpa ribet.

## Instal Pustaka Python OCR

Potongan kode yang akan kami gunakan bergantung pada paket `ocr` (pembungkus tipis di atas Tesseract yang menambahkan pengaturan berguna). Instal dengan satu perintah:

```bash
pip install ocr
```

> **Tip pro:** Setelah instalasi, jalankan `tesseract --version` di terminal Anda untuk memastikan mesin dasar tersedia. Jika Anda belum memiliki Tesseract, ikuti panduan resmi untuk OS Anda—kebanyakan manajer paket sudah menyediakannya (`apt-get install tesseract-ocr` di Ubuntu, `brew install tesseract` di macOS).

## Langkah 1: Buat Instance Mesin OCR

Membuat mesin adalah batu pertama dalam dinding **python ocr handwritten recognition**. Anggap mesin sebagai otak yang nanti akan membaca coretan.

```python
# Step 1: Import the library and instantiate the OCR engine
import ocr

# The OcrEngine class gives us access to all the low‑level settings.
engine = ocr.OcrEngine()
```

Mengapa ini penting: tanpa mesin Anda tidak dapat menyesuaikan alur pengenalan. Pengaturan default dioptimalkan untuk teks cetak, jadi kita perlu menyesuaikannya pada langkah berikutnya.

## Langkah 2: Aktifkan Pengenalan Tulisan Tangan

Secara default mesin mengasumsikan karakter cetak. Mengaktifkan mode tulisan tangan mengubah saklar yang memberi tahu Tesseract untuk menggunakan model LSTM yang dilatih pada goresan kursif.

```python
# Step 2: Turn on handwritten mode
engine.ocr_settings.enable_handwritten_recognition = True
```

> **Bagaimana jika Anda melewatkannya?** OCR akan memperlakukan goresan sebagai noise, menghasilkan output yang kacau. Mengaktifkan flag tersebut adalah inti dari **bagaimana cara mengenali teks tulisan tangan**.

## Langkah 3: Muat Foto Tulisan Tangan Anda

Sekarang kami mengarahkan mesin ke file gambar. Path dapat berupa absolut atau relatif; pastikan file tersebut ada.

```python
# Step 3: Load the image containing the handwritten notes
image_path = "YOUR_DIRECTORY/handwritten_note.jpg"
engine.load_image(image_path)
```

Pemeriksaan cepat: buka gambar di penampil OS Anda. Jika teksnya buram, pertimbangkan pra‑pemrosesan (peningkatan kontras, rotasi) sebelum memberikannya ke mesin—penyesuaian tersebut sering meningkatkan tingkat keberhasilan **ekstrak teks dari gambar tulisan tangan**.

## Langkah 4: Jalankan Proses Pengenalan

Setelah semuanya siap, kami akhirnya meminta mesin untuk melakukan tugasnya. Metode `recognize()` mengembalikan objek hasil yang berisi string yang diekstrak dan skor kepercayaan.

```python
# Step 4: Execute the OCR process
handwritten_result = engine.recognize()
```

Di balik layar, mesin mengubah bitmap menjadi serangkaian vektor fitur, memprosesnya melalui jaringan LSTM, dan menyatukan karakter‑karakter. Itulah keajaiban **python ocr handwritten recognition**.

## Langkah 5: Tampilkan Teks yang Diekstrak

Objek hasil menyediakan atribut `.text` yang berisi string Unicode biasa. Cetak, tulis ke file, atau masukkan ke pipeline lain—pilihan Anda.

```python
# Step 5: Print the extracted text to the console
print("=== Extracted Text ===")
print(handwritten_result.text)
```

### Output yang Diharapkan

Jika gambar sumber berisi catatan “Buy milk, eggs, and bread”, Anda akan melihat sesuatu seperti:

```
=== Extracted Text ===
Buy milk, eggs, and bread
```

Perhatikan bagaimana output mempertahankan tanda baca dan pemisah baris (jika ada). Jika Anda mendapatkan teks tak terbaca, periksa kembali kualitas gambar dan flag `enable_handwritten_recognition`.

## Menangani Kendala Umum

| Masalah | Gejala | Solusi |
|---------|--------|--------|
| Skor kepercayaan rendah | Banyak “?” atau karakter tak masuk akal | Tingkatkan DPI gambar menjadi ≥300, terapkan binarisasi (`opencv`), atau potong ke wilayah yang diinginkan. |
| Bahasa campuran | Output mencampur bahasa Inggris dengan skrip lain | Set `engine.ocr_settings.language = "eng"` (atau kode ISO lain) sebelum `recognize()`. |
| File besar | Waktu pemrosesan lama atau error memori | Ubah ukuran gambar ke dimensi yang wajar (mis., lebar maksimum 1200 px) sebelum memuat. |
| Tesseract tidak ada | `ImportError` atau `FileNotFoundError` | Instal Tesseract secara terpisah dan pastikan berada di PATH sistem Anda. |

Penyesuaian ini membuat alur kerja **convert handwritten photo to text** Anda tetap kuat di berbagai dataset.

## Skrip Lengkap yang Dapat Anda Jalankan Hari Ini

Berikut adalah program lengkap yang berdiri sendiri yang menyatukan semua bagian. Salin ke file bernama `handwritten_ocr.py` dan jalankan `python handwritten_ocr.py`.

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py

A minimal example that demonstrates how to extract text from handwritten image
using Python OCR (handwritten recognition mode). Adjust `image_path` to point
to your own file before running.
"""

import ocr  # pip install ocr

def main():
    # 1️⃣ Create the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Enable the handwritten recognition flag
    engine.ocr_settings.enable_handwritten_recognition = True

    # 3️⃣ Load the target image
    image_path = "YOUR_DIRECTORY/handwritten_note.jpg"
    engine.load_image(image_path)

    # 4️⃣ Run the OCR process
    result = engine.recognize()

    # 5️⃣ Output the extracted text
    print("=== Extracted Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

Jalankan, dan Anda akan melihat teks tercetak di konsol—tepat hasil yang Anda butuhkan ketika ingin **convert handwritten photo to text**.

## Melangkah Lebih Jauh

Sekarang Anda telah menguasai dasar **ekstrak teks dari gambar tulisan tangan**, pertimbangkan langkah selanjutnya berikut:

- **Pemrosesan batch:** Loop melalui folder gambar dan simpan setiap hasil ke file CSV.
- **Pasca‑pemrosesan:** Gunakan regular expression untuk membersihkan kesalahan OCR umum (mis., “1” vs “l”).
- **Integrasi:** Masukkan string yang diekstrak ke pipeline Natural Language Processing untuk analisis sentimen atau ekstraksi kata kunci.
- **Pustaka alternatif:** Jika Anda membutuhkan akurasi lebih tinggi, jelajahi `easyocr` atau `pytesseract` dengan model LSTM khusus—keduanya juga mendukung **python ocr handwritten recognition**.

Ingat, kualitas gambar sumber sering menentukan keberhasilan, jadi luangkan beberapa menit untuk pra‑pemrosesan. Sedikit usaha ekstra sekarang menghemat banyak debugging nanti.

## Kesimpulan

Kami telah membahas contoh lengkap end‑to‑end yang menunjukkan **bagaimana cara mengenali teks tulisan tangan** dan, yang lebih penting, bagaimana **mengekstrak teks dari gambar tulisan tangan** menggunakan Python. Dengan menginstal paket `ocr`, mengaktifkan flag tulisan tangan, memuat gambar Anda, dan memanggil `recognize()`, Anda dapat **convert handwritten photo to text** dalam beberapa baris kode.

Cobalah dengan catatan Anda sendiri, sesuaikan langkah pra‑pemrosesan, dan biarkan OCR melakukan pekerjaan berat. Jika Anda menemui kendala, tinjau kembali tabel “Menangani Kendala Umum” atau coba alternatif back‑end OCR. Selamat coding, semoga data tulisan tangan Anda menjadi dapat dicari secara instan!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara Mengenali Persegi Panjang Halaman untuk Pengenalan Teks OCR di Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [Cara Menggunakan OCR - Mengenali Gambar tanpa Deteksi Area Teks](/ocr/english/net/image-and-drawing-recognition/recognize-image-without-text-area-detection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}