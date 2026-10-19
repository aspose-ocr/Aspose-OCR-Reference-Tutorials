---
category: general
date: 2026-03-18
description: Lakukan OCR pada gambar dan ekstrak teks tulisan tangan dari foto. Pelajari
  cara mengonversi gambar tulisan tangan, mengekstrak teks dari JPG, dan mengenali
  teks dari foto.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: id
og_description: Lakukan OCR pada gambar untuk mengekstrak teks tulisan tangan dari
  foto. Tutorial ini menunjukkan cara mengonversi gambar tulisan tangan dan mengenali
  teks dari file JPG.
og_title: Lakukan OCR pada Gambar – Panduan Lengkap Teks Tangan
tags:
- OCR
- Python
- Handwriting Recognition
title: Lakukan OCR pada Gambar – Konversi Gambar Tertulis Tangan menjadi Teks
url: /id/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar – Ekstraksi Teks Tangan Full‑Stack

Pernahkah Anda **melakukan OCR pada gambar** tetapi tidak yakin apakah mesin dapat membaca tulisan tangan yang berantakan? Anda tidak sendirian. Dalam banyak aplikasi dunia nyata—misalnya pemindai kwitansi pengeluaran atau utilitas pencatatan—Anda akan menemui foto coretan yang perlu diubah menjadi teks biasa.  

Dalam panduan ini kami akan menunjukkan cara **mengonversi gambar tulisan tangan**, **mengekstrak teks dari jpg**, dan bahkan **mengenali teks dari aliran foto** menggunakan sebuah pustaka bergaya Python kecil bernama `ocr`. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang mengambil setiap kata dari catatan tulisan tangan, tidak peduli seberapa goyah pena itu.

## Apa yang Anda Butuhkan

- Python 3.8+ (kode berfungsi pada interpreter terbaru apa pun)
- Paket hipotetik `ocr` – pasang dengan `pip install ocr-lib` (ganti dengan nama paket nyata yang Anda gunakan)
- Foto yang jelas dari catatan tulisan tangan yang disimpan sebagai `note.jpg` (atau format gambar lainnya)
- Sedikit rasa ingin tahu—tidak diperlukan latar belakang ML lanjutan

Itu saja. Tanpa layanan eksternal, tanpa kunci API, hanya mesin lokal yang dapat **melakukan OCR pada gambar**.

![perform OCR on image screenshot](example.png)

*Alt text: tangkapan layar melakukan OCR pada gambar yang menampilkan editor kode dengan skrip OCR.*

## Implementasi Langkah‑per‑Langkah

Di bawah ini kami memecah proses menjadi potongan‑potongan kecil. Setiap judul mencakup kata kunci sehingga Anda dapat menelusurnya dengan cepat, dan setiap blok menjelaskan **mengapa** kami melakukan apa yang kami lakukan—bukan hanya **apa**.

### Langkah 1: Pasang dan Verifikasi Pustaka OCR

Sebelum Anda dapat **melakukan OCR pada gambar**, pustaka harus ada di lingkungan Anda. Buka terminal dan jalankan:

```bash
pip install ocr-lib
```

> **Pro tip:** Jika Anda bekerja dalam lingkungan virtual (sangat disarankan), aktifkan terlebih dahulu. Itu menjaga ketergantungan tetap rapi dan menghindari benturan versi.

Setelah pemasangan, mari pastikan Python dapat mengimpor paket tersebut:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

Jika Anda melihat pesan sukses, Anda siap **mengonversi gambar tulisan tangan**.

### Langkah 2: Buat Instance Engine dan Pilih Mode Tulisan Tangan

Sebagian besar mesin OCR secara default mengenali teks cetak. Karena kami ingin **mengekstrak teks tulisan tangan**, kami harus mengubah mode secara eksplisit. Langkah ini penting karena tulisan tangan sering memerlukan pra‑pemrosesan berbeda (seperti menghaluskan goresan).

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Mengapa ini penting:* Karakter tulisan tangan dapat sangat bervariasi dalam ukuran dan kemiringan. Dengan menetapkan `RecognitionMode.HANDWRITTEN`, mesin menerapkan model yang dilatih pada contoh kursif, meningkatkan akurasi secara dramatis.

### Langkah 3: Muat Foto yang Ingin Anda Analisis

Sekarang kami benar‑benar **melakukan OCR pada gambar**. Metode `load_image` menerima jalur atau objek mirip‑file. Untuk demonstrasi, kami akan memuat JPEG, tetapi pemanggilan yang sama bekerja untuk PNG, BMP, atau bahkan halaman PDF.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

Jika gambar Anda berada di bucket cloud, cukup unduh terlebih dahulu atau berikan aliran `BytesIO`—`ocr` cukup fleksibel untuk menangani keduanya.

### Langkah 4: Jalankan Proses Pengenalan

Dengan engine yang sudah siap dan gambar berada di memori, kami akhirnya **melakukan OCR pada gambar** dan mengambil teks mentah.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

Pemanggilan `recognize()` mengembalikan string Unicode biasa. Untuk kebanyakan kasus penggunaan Anda dapat menuliskannya langsung ke file `.txt`, mengirimkannya ke pipeline bahasa alami, atau menampilkannya di GUI.

### Langkah 5: Opsional – Bersihkan atau Proses Lanjutan Output

OCR tulisan tangan tidak sempurna; Anda sering akan melihat pemisah baris yang tidak diinginkan atau karakter yang salah dibaca. Langkah pembersihan cepat dapat meningkatkan hasil selanjutnya.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

Silakan sambungkan pemeriksa ejaan, model bahasa, atau regex khusus tergantung pada domain Anda.

### Skrip Lengkap – Siap Salin & Tempel

Menggabungkan semuanya, berikut program lengkap yang dapat dijalankan yang **mengekstrak teks tulisan tangan** dari JPEG dan mencetak hasil yang rapi.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Output yang diharapkan** (teks Anda tentu akan berbeda):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

Jika Anda melihat teks tak terbaca, periksa kembali kualitas gambar (pencahayaan baik, blur minimal) dan pastikan Anda berada dalam mode `HANDWRITTEN`. Kedua faktor tersebut menyumbang sebagian besar kesalahan pengenalan.

## Pertanyaan yang Sering Diajukan (FAQ)

| Pertanyaan | Jawaban |
|------------|---------|
| **Apakah saya bisa menggunakan ini untuk mengekstrak teks dari PNG?** | Tentu saja. `engine.load_image("scan.png")` berfungsi dengan cara yang sama. |
| **Bagaimana jika gambar saya berupa halaman PDF?** | Konversi halaman tersebut ke gambar terlebih dahulu (misalnya dengan `pdf2image`) lalu berikan ke engine. |
| **Apakah pustaka ini thread‑safe?** | Ya, Anda dapat menginstansiasi objek `OcrEngine` terpisah per thread. |
| **Bagaimana perbedaannya dengan `pytesseract`?** | `ocr` menyembunyikan binary Tesseract dan menyertakan model tulisan tangan bawaan, sehingga Anda tidak perlu menginstal eksekutabel eksternal. |
| **Bagaimana jika saya perlu **mengekstrak teks dari JPG** secara massal?** | Bungkus skrip dalam loop, atau gunakan `engine.load_image` pada setiap file dan kumpulkan hasilnya dalam daftar atau CSV. |

## Kasus Khusus & Praktik Terbaik

1. **Foto dengan kontras rendah** – Tingkatkan kontras secara programatis sebelum memuat, atau gunakan `engine.apply_preprocessing('contrast', level=2)`.
2. **Campuran teks cetak & tulisan tangan** – Lakukan dua kali proses: pertama dengan `HANDWRITTEN`, kemudian dengan `PRINTED`, dan gabungkan outputnya.
3. **Gambar berukuran besar** – Turunkan skala menjadi lebar ~1500 px; mesin OCR biasanya lebih cepat dengan buffer yang lebih kecil tanpa mengorbankan akurasi.
4. **Karakter Unicode** – Pustaka mengembalikan string UTF‑8, sehingga Anda dapat menangani emoji, huruf beraksen, atau simbol matematika secara langsung.

## Penutup

Kami baru saja menelusuri contoh konkret tentang cara **melakukan OCR pada gambar**, khususnya untuk catatan tulisan tangan. Dengan memasang paket `ocr`, mengonfigurasi engine ke mode `HANDWRITTEN`, memuat foto, dan memanggil `recognize()`, Anda dapat **mengonversi gambar tulisan tangan** menjadi teks bersih yang dapat dicari.  

Dari sini Anda dapat **mengekstrak teks dari jpg** secara massal, mengalirkan output ke aplikasi pencatatan, atau menggabungkannya dengan sintesis suara untuk aksesibilitas. Langit adalah batasnya, dan kode di atas memberi Anda fondasi yang kuat untuk bereksperimen.

Punya trik lain yang ingin dibagikan—mungkin format file berbeda atau pra‑pemrosesan unik? Tinggalkan komentar, dan mari teruskan diskusi. Selamat coding, dan nikmati mengubah coretan menjadi emas digital!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}