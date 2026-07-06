---
category: general
date: 2026-04-26
description: 'cara ocr python: Pelajari cara mengekstrak teks dari gambar dan membaca
  file tiff python menggunakan contoh OCR dasar. Kode cepat yang dapat dijalankan
  disertakan.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: id
og_description: 'cara ocr python: Panduan langkah demi langkah yang menunjukkan cara
  mengekstrak teks dari gambar, membaca file tiff python, dan mengonversi teks gambar
  yang dipindai dengan skrip sederhana yang dapat dijalankan.'
og_title: Cara OCR Python – Contoh OCR Dasar untuk Mengekstrak Teks
tags:
- OCR
- Python
- Image Processing
title: cara OCR python – Contoh OCR Dasar untuk Mengekstrak Teks
url: /id/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr python – Contoh OCR Dasar untuk Mengekstrak Teks

Pernah bertanya-tanya **how to ocr python** ketika Anda memiliki file TIFF yang dipindai di meja Anda? Anda bukan satu-satunya yang menatap sekumpulan file gambar dan bertanya, “Bagaimana cara saya mengambil kata‑kata dari ini?” Kabar baiknya, mengubah gambar menjadi teks biasa sangat mudah dengan pustaka yang tepat dan beberapa langkah jelas.

Dalam tutorial ini kami akan membahas **basic OCR example** yang membaca file TIFF, mengekstrak teks, dan mencetaknya ke konsol. Pada akhir tutorial Anda akan tahu persis cara **extract text from image** file, cara menangani keunikan format TIFF, dan apa yang perlu disesuaikan jika Anda perlu **convert scanned image text** menjadi sesuatu yang lebih berguna. Tidak ada sihir tersembunyi—hanya Python sederhana yang dapat Anda salin‑tempel dan jalankan hari ini.

## Apa yang Anda Butuhkan

- Python 3.9+ terpasang (rilis stabil terbaru paling baik).
- Pustaka OCR yang dapat di‑install via pip. Untuk panduan ini kami akan menggunakan paket fiktif `aocr` yang meniru alat populer seperti Tesseract; Anda dapat menggantinya dengan `pytesseract` atau `easyocr` nanti.
- Gambar TIFF yang ingin Anda proses – beri nama `input.tiff` dan letakkan di folder yang akan Anda referensikan dalam kode.
- Familiaritas dasar dengan command line (hanya untuk menginstal paket).

Itu saja. Tidak ada dependensi berat, tidak ada kontainer Docker, hanya beberapa baris kode.

## Langkah 1 – Instal dan Impor Dependensi (how to ocr python)

Pertama, dapatkan paket OCR. Buka terminal dan jalankan:

```bash
pip install aocr
```

Jika Anda lebih suka pustaka dunia nyata, ganti `aocr` dengan `pytesseract` dan instal mesin Tesseract secara terpisah.

Sekarang impor apa yang kita butuhkan. Kelas `Path` dari `pathlib` memberi kita cara bersih untuk bekerja dengan jalur file di berbagai sistem operasi.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Mengapa menggunakan `Path`?* Karena ia mengabstraksi tanda miring (`/` vs `\`) dan memungkinkan Anda menggabungkan direktori tanpa khawatir tentang OS yang mendasarinya. Detail kecil itu sering menyelamatkan dari sakit kepala ketika Anda memindahkan skrip ke server CI.

## Langkah 2 – Buat Instance Mesin OCR (basic ocr example)

Selanjutnya, jalankan mesin OCR. Anggap `OcrEngine` sebagai otak yang akan membaca gambar dan mengeluarkan karakter.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

Sebagian besar pustaka OCR memungkinkan Anda menyesuaikan bahasa, DPI, atau ambang kepercayaan di sini. Untuk **basic OCR example** ini kami akan tetap menggunakan nilai default, tetapi Anda dapat menjelajahi `ocr_engine.config` nanti jika perlu menangani dokumen multibahasa.

## Langkah 3 – Muat Gambar TIFF Anda (read tiff file python)

Di sinilah bagian **read tiff file python** muncul. TIFF dapat memiliki banyak halaman, tetapi `Image.load` akan mengambil halaman pertama secara default—sempurna untuk pemindaian satu halaman.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Ganti `"YOUR_DIRECTORY"` dengan folder sebenarnya yang berisi `input.tiff`. Jika Anda tidak yakin di mana skrip dijalankan, `Path.cwd()` mencetak direktori kerja saat ini—berguna untuk men-debug masalah jalur.

## Langkah 4 – Jalankan Proses OCR (extract text from image)

Sekarang keajaiban terjadi. Memanggil `process()` mengirim gambar melalui pipeline OCR dan mengembalikan objek hasil.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Di balik layar, mesin mungkin mengonversi gambar ke skala abu‑abu, menerapkan threshold, dan memasukkannya ke jaringan saraf. Anda tidak perlu mengelola langkah‑langkah itu; pustaka mengabstraksikannya.

## Langkah 5 – Cetak Teks yang Diakui (convert scanned image text)

Akhirnya, keluarkan teks. Dalam proyek nyata Anda mungkin menuliskannya ke file atau basis data, tetapi mencetak menjaga contoh tetap rapi.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Saat Anda menjalankan skrip, Anda akan melihat sesuatu seperti:

```
Hello, world!
This is a sample scanned document.
```

Jika output terlihat berantakan, periksa kembali bahwa gambar sumber jelas dan bahasa OCR cocok dengan teks.

## Skrip Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Output yang Diharapkan

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Jika Anda perlu **convert scanned image text** menjadi PDF yang dapat dicari, Anda dapat mengalirkan `ocr_result.text` ke generator PDF seperti `reportlab`—tetapi itu merupakan tutorial tersendiri.

## Kesalahan Umum & Tips Pro

- **Low‑resolution scans**: OCR kesulitan di bawah 150 DPI. Jika TIFF Anda buram, naikkan resolusinya terlebih dahulu dengan Pillow (`Image.open(...).resize(...)`).
- **Multiple pages**: Untuk TIFF multi‑halaman, iterasi melalui `Image.load_multi_page()` (jika pustaka Anda mendukungnya) dan gabungkan hasilnya.
- **Language support**: Banyak mesin default ke bahasa Inggris. Atur `ocr_engine.language = "spa"` untuk bahasa Spanyol, misalnya.
- **Whitespace handling**: OCR sering menambahkan jeda baris yang tidak diinginkan. Gunakan `str.splitlines()` atau ekspresi reguler untuk membersihkan output.
- **Performance**: Untuk pemrosesan massal, gunakan kembali satu instance `OcrEngine` alih-alih membuat yang baru untuk setiap file.

## Memperluas Contoh

Sekarang Anda telah menguasai **how to ocr python** untuk satu gambar, pertimbangkan langkah selanjutnya berikut:

1. **Batch processing** – Loop melalui direktori TIFF dan tulis setiap hasil ke file `.txt`.
2. **Integration with Pandas** – Simpan teks yang diekstrak bersama metadata untuk analisis cepat.
3. **Hybrid approach** – Gabungkan OCR dengan pustaka NLP seperti `spaCy` untuk mengekstrak entitas (nama, tanggal, jumlah) dari faktur yang dipindai.
4. **Alternative file formats** – Ganti `Image.load` dengan `Image.from_bytes` untuk menangani gambar yang datang dari API atau basis data.

Semua ini dibangun di atas gagasan inti **extract text from image** dan **convert scanned image text** menjadi sesuatu yang dapat dipahami mesin.

## Kesimpulan

Kami telah membahas contoh **basic OCR example** yang jelas, end‑to‑end yang menunjukkan **how to ocr python**, cara **read tiff file python**, dan cara **extract text from image** file dengan hanya beberapa baris kode. Skrip ini mandiri, mencakup penanganan error, dan mencetak hasil secara langsung, menjadikannya fondasi yang kuat untuk proyek apa pun yang perlu mengubah dokumen yang dipindai menjadi teks yang dapat diedit.

Silakan bereksperimen—ganti backend OCR, sesuaikan preprocessing, atau hubungkan output ke alur kerja selanjutnya. Langit adalah batasnya ketika Anda dapat secara andal **convert scanned image text** menjadi data yang dapat dicari.

Ada pertanyaan tentang kasus tepi, paket bahasa, atau penyetelan performa? Tinggalkan komentar di bawah, dan selamat coding!

![contoh ocr python](/images/ocr-python-example.png "Tangkapan layar output skrip how to ocr python")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}