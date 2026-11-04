---
category: general
date: 2026-03-26
description: Pelajari cara melakukan OCR di Python dan mengenali teks dari file gambar.
  Panduan ini menunjukkan cara mengekstrak teks dari PNG dan mengonversi gambar menjadi
  teks dengan cepat.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: id
og_description: Bagaimana melakukan OCR di Python? Ikuti panduan ini untuk mengenali
  teks dari gambar, mengekstrak teks dari PNG, dan mengonversi gambar menjadi teks
  dengan lisensi percobaan.
og_title: Cara Melakukan OCR dengan Python – Tutorial Lengkap
tags:
- OCR
- Python
- Image Processing
title: Cara Melakukan OCR di Python – Tutorial Lengkap Langkah demi Langkah
url: /id/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di Python – Tutorial Lengkap Langkah‑per‑Langkah  

Pernah bertanya‑tanya **cara melakukan OCR** pada foto yang baru saja Anda ambil dengan ponsel? Anda tidak sendirian—para pengembang di mana‑mana membutuhkan cara yang andal untuk mengenali teks dari file gambar tanpa harus berurusan dengan pustaka native yang rumit.  

Dalam tutorial ini kami akan menelusuri contoh praktis yang menunjukkan **cara melakukan OCR**, **mengenali teks dari gambar**, dan **mengekstrak teks dari PNG** menggunakan pembungkus Python yang ringan. Pada akhir tutorial Anda akan dapat **mengonversi gambar ke teks** hanya dengan beberapa baris kode, dan Anda tidak perlu khawatir tentang masalah lisensi karena kami akan menggunakan mode percobaan bawaan.

## Apa yang Akan Anda Pelajari  

* Cara menyiapkan lisensi percobaan untuk mesin OCR (tanpa perlu jalur file).  
* Urutan panggilan yang tepat untuk **mengenali teks dari gambar**.  
* Cara **mengekstrak teks dari PNG** dan menangani jebakan umum seperti font yang hilang.  
* Tips untuk menskalakan solusi saat Anda beralih dari lisensi percobaan ke lisensi produksi.  

**Prasyarat** – Anda memerlukan Python 3.8+ dan paket `ocr` (dapat diinstal via `pip install ocr`). Tidak ada alat eksternal lain yang diperlukan.

---  

![how to perform OCR example](https://example.com/ocr-demo.png "how to perform OCR in Python – recognized text displayed")  

*Teks alt gambar: cara melakukan OCR di Python – contoh output*  

## Langkah 1 – Aktifkan Lisensi Percobaan (Tanpa Jalur File)  

Sebelum mesin dapat membaca apa pun, ia memerlukan lisensi yang valid. Mode percobaan sangat cocok untuk eksperimen dan proyek kecil.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Mengapa ini penting:* Objek lisensi memberi tahu pustaka OCR bahwa Anda beroperasi dalam sandbox. Jika Anda melewatkan langkah ini, mesin akan mengeluarkan `LicenseError` pada saat Anda memanggil `recognize()`.  

**Tips pro:** Saat Anda beralih ke lisensi berbayar, ganti dua baris di atas dengan `ocr.License("path/to/your/license.key").apply()`.

## Langkah 2 – Buat Instance Mesin OCR  

Setelah percobaan diaktifkan, kita menginstansiasi mesin utama. Anggaplah ini sebagai “otak” yang akan melihat gambar dan memutuskan karakter apa yang berada di mana.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Mengapa ini penting:* `OcrEngine` menyimpan konfigurasi seperti paket bahasa dan pengaturan DPI. Anda dapat menyesuaikannya nanti, tetapi nilai default sudah cukup untuk kebanyakan PNG berbahasa Inggris saja.

## Langkah 3 – Muat PNG yang Ingin Diproses  

Di sinilah kita **mengenali teks dari gambar**. Metode `ocr.Imaging.Image.load()` mendukung PNG, JPEG, BMP, dan beberapa format lainnya.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Kasus tepi:* Jika PNG Anda menggunakan palet terindeks (umum pada tangkapan layar), pemuat akan secara otomatis mengonversinya menjadi buffer RGB 24‑bit. Konversi ini dapat menambah sedikit beban kinerja, tetapi menjamin hasil OCR yang akurat.

## Langkah 4 – Jalankan OCR dan Ambil Teks  

Akhirnya, kita meminta mesin melakukan tugasnya dan kemudian mengambil hasil teks biasa.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Output yang diharapkan** (contoh untuk gambar sederhana yang berisi “Hello World”):

```
Hello World
```

Jika gambar berisi beberapa baris, output akan mempertahankan jeda baris, sehingga mudah untuk diteruskan ke proses selanjutnya seperti parser CSV atau pipeline NLP.

## Opsional: Penyempurnaan untuk Akurasi Lebih Baik  

* **Paket bahasa:** `ocr_engine.set_language("eng")` (default) atau `"fra"` untuk bahasa Prancis.  
* **Skala DPI:** `ocr_engine.set_dpi(300)` dapat meningkatkan hasil pada pemindaian beresolusi rendah.  
* **Pra‑pemrosesan:** Menerapkan ambang biner (`ocr.Imaging.Image.threshold()`) sebelum `set_image` sering menghasilkan teks yang lebih bersih pada latar belakang berisik.

Penyesuaian ini berguna ketika Anda beralih dari demo cepat ke **ocr tutorial python** tingkat produksi yang memproses ratusan file per hari.

## Skrip Lengkap – Siap Salin & Tempel  

Berikut adalah skrip lengkap yang dapat dijalankan, menggabungkan semua langkah di atas. Simpan sebagai `run_ocr.py` dan ganti `YOUR_DIRECTORY/sample1.png` dengan jalur ke PNG Anda sendiri.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Jalankan dari baris perintah:

```bash
python run_ocr.py
```

Anda akan melihat teks yang diekstrak tercetak di konsol. Jika Anda mendapatkan string kosong, periksa kembali bahwa gambar memang berisi teks yang jelas dan kontras tinggi serta lisensi percobaan telah diterapkan tanpa error.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai  

* **“Apakah ini bekerja dengan JPEG?”** – Tentu saja. Metode `load()` mendeteksi format secara otomatis, jadi Anda dapat mengganti PNG dengan JPEG tanpa mengubah kode.  
* **“Bagaimana jika gambar diputar?”** – Mesin dapat mendeteksi orientasi secara otomatis, tetapi untuk hasil terbaik Anda dapat memutar terlebih dahulu dengan `input_image.rotate(90)` sebelum `set_image`.  
* **“Bisakah saya memproses banyak gambar dalam loop?”** – Ya. Pindahkan pemanggilan `load` dan `recognize()` ke dalam `for` loop; instance `ocr_engine` yang sama dapat dipakai kembali, yang menghemat sedikit overhead.  

## Langkah Selanjutnya – Dari Demo ke Produksi  

Sekarang Anda sudah tahu **cara melakukan OCR**, pertimbangkan topik lanjutan berikut:

* **Pemrosesan batch** – Gabungkan skrip ini dengan `os.listdir()` untuk **mengekstrak teks dari PNG** secara massal.  
* **Integrasi dengan PDF** – Gunakan `pdf2image` untuk mengonversi halaman PDF ke PNG, lalu alirkan ke pipeline yang sama.  
* **Pasca‑pemrosesan** – Terapkan regex atau pencocokan fuzzy untuk membersihkan kesalahan umum OCR (misalnya “0” vs “O”).  

Masing‑masing langkah ini memperluas gagasan inti **mengonversi gambar ke teks** dan meningkatkan kegunaan alur kerja OCR Anda.

---  

### TL;DR  

Kami telah membahas semua yang Anda perlukan untuk **cara melakukan OCR** di Python: mengaktifkan lisensi percobaan, membuat mesin, memuat PNG, menjalankan pengenalan, dan mencetak hasil. Dengan hanya beberapa baris kode Anda dapat **mengenali teks dari gambar**, **mengekstrak teks dari PNG**, dan **mengonversi gambar ke teks** untuk aplikasi downstream apa pun.  

Cobalah, sesuaikan DPI atau pengaturan bahasa, dan biarkan mesin melakukan pekerjaan berat. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}