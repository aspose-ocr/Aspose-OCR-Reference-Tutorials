---
category: general
date: 2026-04-26
description: Cara menjalankan OCR pada formulir yang dipindai, pelajari cara memproses
  gambar terlebih dahulu untuk mengurangi noise, dan mengekstrak teks dari gambar
  dengan cepat.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: id
og_description: Cara menjalankan OCR pada dokumen yang dipindai, memproses gambar,
  mengurangi noise, dan mengekstrak teks secara efisien.
og_title: Cara Menjalankan OCR dan Memproses Gambar – Panduan Cepat
tags:
- OCR
- image processing
- Python
title: Cara Menjalankan OCR dan Memproses Gambar – Ekstrak Teks dari Formulir yang
  Dipindai
url: /id/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR – Panduan Lengkap untuk Mengekstrak Teks dari Gambar

Pernah bertanya-tanya **cara menjalankan OCR** pada formulir hasil scan yang berantakan dan mendapatkan teks bersih yang dapat dicari? Anda tidak sendirian. Dalam banyak proyek dunia nyata, gambar mentah penuh dengan bintik‑bintik, pencahayaan tidak merata, dan keanehan lain yang membuat OCR standar kesulitan.  

Berita baiknya? Dengan hanya beberapa baris Python dan pipeline pra‑pemrosesan yang cerdas, Anda dapat secara dramatis meningkatkan akurasi pengenalan, **mengurangi noise**, dan mengambil kata‑kata tepat yang Anda butuhkan. Dalam tutorial ini kami akan membahas setiap langkah—dari memuat gambar hingga mencetak string akhir—sehingga Anda akan memiliki cuplikan kode siap pakai yang dapat Anda sesuaikan untuk faktur, kwitansi, atau dokumen hasil scan apa pun.

## Apa yang Akan Anda Bangun

- Sebuah instance `OcrEngine` yang berkomunikasi dengan perpustakaan OCR di bawahnya.  
- Rangkaian pra‑pemrosesan yang **binarizes** gambar dan menerapkan **median blur** untuk menghaluskan bintik‑bintik.  
- Panggilan sederhana ke `process()` yang mengembalikan objek yang menampilkan `text`, string yang diekstrak.  

Pada akhir tutorial, Anda akan memiliki skrip mandiri yang dapat dijalankan pada file gambar apa pun dan langsung melihat teks yang diekstrak di konsol.

## Prasyarat

- Python 3.9+ (sintaks yang digunakan di sini cocok dengan rilis stabil terbaru).  
- Paket fiktif `aocr` – anggap sebagai pembungkus tipis di atas Tesseract atau mesin OCR modern apa pun. Instal dengan `pip install aocr`.  
- Gambar hasil scan (`scanned_form.jpg`) yang ditempatkan di folder yang dapat Anda referensikan.  

Jika Anda menggunakan perpustakaan OCR nyata seperti `pytesseract`, Anda dapat mengganti `OcrEngine` dengan kelas yang sesuai—semua hal lain tetap sama.

![](how-to-run-ocr-example.png "contoh cara menjalankan OCR yang menampilkan formulir hasil scan dan teks yang diekstrak")

*Teks alternatif: cara menjalankan OCR pada dokumen hasil scan dan melihat teks yang diekstrak.*

---

## Langkah 1: Cara Menjalankan OCR – Inisialisasi Engine

Sebelum engine dapat membaca apa pun, kita perlu membuat sebuah instance. Anggap `OcrEngine` sebagai otak yang nantinya akan menafsirkan data visual.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Mengapa ini penting:** Menginstansiasi engine menyiapkan model internal, memuat paket bahasa, dan menyiapkan lingkungan runtime. Melewatkan langkah ini biasanya menghasilkan error `NoneType` ketika Anda kemudian memanggil `process()`.

---

## Langkah 2: Cara Memproses Gambar – Memuat Form Hasil Scan Anda

Sekarang otak sudah siap, kita memberinya gambar. Gambar dapat berupa format apa pun yang didukung oleh `aocr.Image`.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Tips pro:** Gunakan path absolut selama pengembangan untuk menghindari kejutan “file tidak ditemukan” ketika skrip dijalankan dari direktori kerja yang berbeda.

---

## Langkah 3: Cara Mengurangi Noise – Terapkan Binarisasi & Median Blur

Scan mentah sering mengandung titik‑titik terpisah, latar belakang tidak merata, atau bayangan samar. Dua trik klasik—**binarization** dan **median blur**—membersihkan gambar tanpa mengorbankan tepi yang mendefinisikan karakter.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Menyelam Lebih Dalam

- **Binarization**: Nilai `threshold=180` memberi tahu algoritma: “Apa pun yang lebih terang dari 180 menjadi putih; sisanya menjadi hitam.” Sesuaikan angka ini jika scan Anda terlalu gelap atau terlalu terang.  
- **Median Blur**: Radius `2` berarti filter melihat jendela piksel 5×5 dan mengganti piksel tengah dengan nilai median. Ini menghaluskan bintik‑bintik terisolasi sambil mempertahankan goresan huruf tetap utuh.

> **Kasus khusus:** Jika dokumen Anda memiliki sorotan berwarna, ambang batas biner sederhana dapat menghapusnya. Dalam skenario tersebut, pertimbangkan menggunakan `aocr.ImageFilters.adaptive_threshold()` sebagai gantinya—ini menyesuaikan ambang secara lokal di seluruh gambar.

---

## Langkah 4: Cara Mengekstrak Teks – Jalankan Proses OCR

Dengan gambar bersih di tangan, akhirnya kita biarkan engine melakukan keajaibannya.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Apa yang terjadi di balik layar?** Engine menjalankan jaringan saraf (atau pencocokan pola lama) pada matriks piksel, menerjemahkan setiap glyph yang dikenali menjadi karakter Unicode, dan menyusunnya menjadi baris serta paragraf.

---

## Langkah 5: Cara Mengekstrak Teks – Cetak Hasil

Objek `ocr_result` menyediakan atribut `text` yang nyaman. Mari lihat apa yang kita dapatkan.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Output yang Diharapkan

Jika formulir hasil scan berisi:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Anda seharusnya melihat sesuatu seperti:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Perhatikan bagaimana langkah pra‑pemrosesan menghilangkan titik‑titik terpisah yang sebelumnya mengubah “Amount” menjadi “Am0unt”. Itulah kekuatan **cara mengurangi noise** sebelum OCR.

---

## Kesalahan Umum & Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Solusi Cepat |
|--------|----------------------|--------------|
| Karakter kacau (mis., “@#%”) | Gambar terlalu gelap atau terlalu terang | Sesuaikan `threshold` di `binarize()`; coba `adaptive_threshold`. |
| Kata hilang | Noise masih ada | Tingkatkan `radius` untuk `median_blur` atau tambahkan filter `gaussian_blur`. |
| Bahasa salah (mis., huruf Inggris menjadi Cina) | Paket bahasa yang salah dimuat | Berikan `language="eng"` saat membuat `OcrEngine()` jika perpustakaan mendukungnya. |
| Pemrosesan lambat pada file besar | Resolusi tinggi | Ukur ulang gambar terlebih dahulu: `aocr.ImageFilters.resize(width=1200)` sebelum binarisasi. |

---

## Melangkah Lebih Jauh – Langkah Selanjutnya dan Topik Terkait

- **Pemrosesan batch**: Bungkus logika di atas dalam loop untuk menangani puluhan file secara otomatis.  
- **Output terstruktur**: Gunakan ekspresi reguler pada `ocr_result.text` untuk mengekstrak bidang seperti tanggal atau jumlah.  
- **Perpustakaan alternatif**: Ganti `aocr` dengan `pytesseract`—kode hanya berubah pada langkah inisialisasi engine.  
- **Cara memproses gambar untuk PDF**: Konversi setiap halaman PDF menjadi gambar, lalu terapkan pipeline yang sama.  

Ekstensi ini memungkinkan Anda memperluas solusi dari satu formulir menjadi pipeline ingest dokumen tingkat perusahaan.

---

## Kesimpulan

Kami telah membahas **cara menjalankan OCR** dari awal hingga akhir, menunjukkan **cara memproses gambar** untuk **mengurangi noise**, dan mendemonstrasikan **cara mengekstrak teks dari gambar** dengan skrip yang bersih dan dapat direproduksi. Inti utama? Beberapa filter sederhana—binarization dan median blur—dapat mengubah scan yang berisik menjadi sumber data yang dapat diandalkan, menghemat Anda berjam‑jam pembersihan manual.

Jalankan skrip ini dengan dokumen Anda sendiri, sesuaikan ambang batas, dan saksikan akurasi meningkat. Saat Anda siap, jelajahi pemrosesan batch atau integrasikan output ke dalam basis data untuk arsip yang dapat dicari. Selamat coding, semoga OCR Anda selalu tepat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}