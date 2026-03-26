---
category: general
date: 2026-03-26
description: Pelajari cara meluruskan gambar, mengenali teks dari gambar, dan membangun
  pipeline pra‑pemrosesan gambar untuk menghilangkan noise pada pemindaian serta mengonversi
  gambar yang dipindai menjadi teks.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: id
og_description: Cara memperbaiki kemiringan gambar dan mengubah pemindaian yang miring
  menjadi teks yang dapat dicari. Ikuti panduan ini untuk mengenali teks dari gambar,
  menghilangkan noise pada pemindaian, dan mengonversi gambar yang dipindai menjadi
  teks.
og_title: Cara Mengoreksi Kemiringan Gambar – Panduan OCR Langkah demi Langkah
tags:
- OCR
- image-processing
- Python
title: Cara Mengoreksi Kemiringan Gambar – Panduan Lengkap dengan OCR
url: /id/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengoreksi Kemiringan Gambar – Panduan Lengkap dengan OCR

Pernah bertanya-tanya **bagaimana cara mengoreksi kemiringan gambar** yang dihasilkan oleh pemindai murah? Anda tidak sendirian. Halaman yang miring terlihat tidak profesional, dan yang lebih penting, kemiringan tersebut dapat mengacaukan mesin OCR mana pun yang mencoba **mengenali teks dari gambar**.  

Dalam tutorial ini kami akan menelusuri **pipeline pra‑pemrosesan gambar** lengkap yang mengoreksi kemiringan, melakukan binarisasi, dan menghilangkan noise pada hasil pindai, kemudian menyerahkannya ke mesin OCR sehingga Anda dapat **mengonversi gambar yang dipindai menjadi teks** dengan sedikit usaha. Tidak ada sulap, hanya Python standar dan pustaka kecil yang melakukan pekerjaan berat.

## Apa yang Anda Butuhkan

- Python 3.9+ (kode berfungsi pada 3.10 dan lebih baru)
- Paket `ocr` (pasang via `pip install ocr‑toolkit` – ganti dengan nama pustaka Anda yang sebenarnya)
- File JPEG atau PNG yang dipindai dan jelas miring (misalnya, `skewed_scan.jpg`)
- Sedikit rasa ingin tahu tentang mengapa setiap langkah pra‑pemrosesan penting

Itu saja. Tidak ada ketergantungan berat seperti OpenCV kecuali Anda ingin menggali lebih dalam nanti.

## Langkah 1: Muat Gambar yang Dipindai

Hal pertama adalah mengambil file ke memori. Langkah ini sederhana namun krusial—jika jalurnya salah, semua hal lain akan gagal.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Mengapa?**  
> Memuat gambar memberi kita objek yang dapat dimanipulasi sehingga `ocr.ImagePreprocessor` dapat bekerja dengannya. Melewatkan langkah ini akan membuat pipeline tidak memiliki data piksel yang sebenarnya.

## Cara Mengoreksi Kemiringan Gambar dan Menyiapkannya untuk OCR

Sekarang kita memiliki gambar, mari luruskan. Metode `deskew()` memperkirakan sudut kemiringan dan memutar gambar kembali ke posisi horizontal.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Tip pro:** Jika pemindaian Anda hanya sedikit melenceng (≤ 3°), algoritma default biasanya sudah tepat. Untuk sudut yang ekstrem Anda mungkin perlu menyesuaikan parameter internal—cek dokumentasi pustaka untuk `max_angle`.

## Binarisasi Gambar – Jadikan Hitam‑Putih

Mesin OCR menyukai input dengan kontras tinggi. Mengonversi gambar ke representasi biner (hitam‑putih) menghilangkan nuansa halus yang dapat membingungkan pengenalan karakter.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **Apa yang terjadi?**  
> Piksel yang lebih terang dari 128 menjadi putih; sisanya menjadi hitam. Sesuaikan ambang batas jika pemindaian Anda sangat gelap atau sangat terang.

## Hapus Noise dari Hasil Pindai Sebelum OCR

Bahkan gambar yang sudah lurus dapat berisi bintik‑bintik, debu, atau artefak kompresi. Blob‑blob kecil itu menjadi musuh utama mesin OCR mana pun.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Mengapa menghilangkan noise?**  
> Noise menciptakan tepi palsu yang dapat diinterpretasikan mesin OCR sebagai karakter. Radius kecil biasanya cukup untuk kebanyakan pemindaian; tingkatkan bila dokumen sangat berbutir.

## Terapkan Pipeline Pra‑Pemrosesan Gambar

Semua konfigurasi sudah siap—sekarang jalankan pipeline pada gambar asli.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Hasil:** `processed_image` adalah bitmap yang sudah dibersihkan, lurus, dan berkontras tinggi, siap untuk ekstraksi teks.

## Kenali Teks dari Gambar dengan Mesin OCR

Saatnya membaca teks sebenarnya. Kami menginisialisasi mesin OCR, memberi gambar yang sudah dipoles, dan meminta string mentah.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Output yang diharapkan** (contoh):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Jika Anda melihat karakter yang kacau, periksa kembali langkah deskew atau coba nilai `threshold` yang berbeda.

## Membuat Pipeline Pra‑Pemrosesan Gambar – Skrip Lengkap

Menggabungkan semuanya, berikut skrip tunggal yang dapat dijalankan. Simpan ke file `.py` dan eksekusi:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Tip:** Bungkus seluruh proses dalam sebuah fungsi (`def ocr_from_file(path): …`) jika Anda berencana memproses banyak file secara batch.

## Pertanyaan Umum & Kasus Tepi

- **Bagaimana jika gambar sudah lurus?**  
  Metode `deskew()` mendeteksi sudut mendekati nol dan membiarkan gambar tidak berubah, sehingga Anda dapat menjalankannya pada setiap file dengan aman.

- **Pemindaian saya berwarna—apakah harus dipertahankan?**  
  Warna tidak menambah nilai untuk kebanyakan tugas OCR. Binarisasi menghilangkannya, mempercepat pemrosesan dan mengurangi penggunaan memori.

- **Bisakah saya menambahkan beberapa langkah pra‑pemrosesan?**  
  Tentu saja. Kelas `ImagePreprocessor` dirancang untuk pipeline; Anda dapat menambahkan `sharpen()`, `contrast_enhance()`, atau filter khusus sebelum memanggil `apply()`.

- **Output OCR memiliki baris baru yang tidak diinginkan—bagaimana memperbaikinya?**  
  Lakukan pasca‑proses pada string dengan `text.replace("\n", " ").strip()` atau gunakan pustaka analisis tata letak yang lebih canggih seperti mode `--psm` pada Tesseract.

## Langkah Selanjutnya

Sekarang Anda tahu **bagaimana cara mengoreksi kemiringan gambar** dan memiliki **pipeline pra‑pemrosesan gambar** yang solid, Anda dapat menjelajahi:

- Mengintegrasikan **kenali teks dari gambar** ke dalam API Flask untuk unggahan dokumen secara real‑time.
- Menggunakan pipeline untuk **menghilangkan noise dari hasil pindai** dokumen bersejarah di mana preservasi sangat penting.
- Menskalakan proses untuk batch‑proses ribuan halaman dan menghasilkan PDF yang dapat dicari menggunakan `pdfminer` atau `PyMuPDF`.

Silakan bereksperimen dengan ambang batas, radius denoise, atau bahkan mengganti backend OCR dengan Tesseract jika Anda memerlukan dukungan multibahasa. Dasarnya tetap sama: luruskan, bersihkan, lalu baca.

---

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah—saya akan dengan senang hati membantu menyempurnakan pipeline Anda.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}