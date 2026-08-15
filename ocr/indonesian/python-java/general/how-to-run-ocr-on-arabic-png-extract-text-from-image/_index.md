---
category: general
date: 2026-03-26
description: Pelajari cara menjalankan OCR pada gambar PNG berbahasa Arab dan mengekstrak
  teks Arab dengan cepat. Panduan ini menunjukkan cara mengubah gambar menjadi teks
  dengan kode Python langkah demi langkah.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: id
og_description: Bagaimana menjalankan OCR pada gambar PNG berbahasa Arab? Ikuti panduan
  lengkap ini untuk mengekstrak teks Arab, mengenali teks Arab, dan mengubah gambar
  menjadi teks menggunakan Python.
og_title: Cara Menjalankan OCR pada PNG Arab – Ekstrak Teks dari Gambar
tags:
- OCR
- Python
- Arabic
title: Cara Menjalankan OCR pada PNG Arab – Ekstrak Teks dari Gambar
url: /id/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR pada PNG Arab – Mengekstrak Teks dari Gambar

Pernah bertanya‑tanya **cara menjalankan OCR** pada gambar yang berisi tulisan Arab? Mungkin Anda memiliki kwitansi yang dipindai, naskah bersejarah, atau sekadar tangkapan layar postingan media sosial dan Anda membutuhkan teks dalam format yang dapat dicari. Anda tidak sendirian—para pengembang di seluruh dunia sering mengalami masalah ini ketika berurusan dengan bahasa yang ditulis dari kanan ke kiri.

Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang dapat dijalankan, yang menunjukkan **cara menjalankan OCR** pada file PNG, mengekstrak teks Arab, dan mencetak hasilnya ke konsol. Tanpa tautan “lihat dokumentasi” yang samar; hanya kode yang dapat Anda salin‑tempel, plus penjelasan mengapa setiap baris penting. Pada akhir tutorial Anda akan dapat **mengonversi gambar ke teks** secara andal, bahkan bila sumbernya adalah PNG Arab yang rumit.

> **Apa yang akan Anda pelajari**
> - Menyiapkan mesin OCR Python untuk bahasa Arab  
> - Memuat gambar PNG dan menangani jebakan umum  
> - Mengenali teks Arab dan memverifikasi output  
> - Tips untuk **mengekstrak teks Arab** dari berbagai kualitas gambar  

Sebelum kita mulai, pastikan Anda memiliki Python 3.8+ terpasang dan versi terbaru dari pustaka `ocr` (yang digunakan dalam cuplikan kode). Jika Anda menggunakan lingkungan virtual, aktifkan sekarang—ini akan menjaga dependensi tetap rapi.

## Prasyarat

- Python 3.8 atau lebih baru  
- Paket `ocr` (`pip install ocr‑engine` – ganti dengan nama paket yang sebenarnya)  
- Gambar PNG Arab (`arabic_doc.png`) yang ditempatkan di lokasi yang dapat Anda referensikan  
- Familiaritas dasar dengan fungsi dan kelas Python  

Itu saja. Tanpa kerangka kerja berat, tanpa kontainer Docker—hanya Python biasa.

## Langkah 1: Instal dan Impor Pustaka OCR

Langkah pertama. Kita memerlukan mesin OCR itu sendiri. Pustaka yang akan kita gunakan menyediakan kelas `OcrEngine` dengan API yang sederhana.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Mengapa mengimpor `Imaging` secara terpisah?* Submodul `Imaging` memberi kita metode `Image.load` yang nyaman dan sudah memahami PNG, JPEG, serta TIFF secara bawaan. Melewatkan langkah ini akan memaksa Anda menangani byte mentah secara manual, yang tidak diperlukan untuk kebanyakan kasus penggunaan.

## Langkah 2: Buat Instance Mesin OCR

Sekarang kita buat instance mesin. Anggap objek ini sebagai “otak” yang akan memproses gambar.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro tip:** Jika Anda berencana memproses banyak gambar secara berurutan, gunakan kembali instance `ocr_engine` yang sama. Ia menyimpan cache model bahasa, yang mempercepat pengenalan berikutnya.

## Langkah 3: Atur Bahasa ke Arab

Bahasa Arab bukan Latin; ia memiliki set karakter sendiri, arah kanan‑ke‑kiri, dan pembentukan kontekstual. Karena itu kita harus secara eksplisit memberi tahu mesin model bahasa mana yang harus dimuat.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Jika Anda lupa menambahkan baris ini, mesin akan default ke bahasa Inggris dan Anda akan mendapatkan output yang berantakan—sesuatu yang sering saya lihat terjadi.

## Langkah 4: Muat Gambar PNG Anda

Di sinilah bagian **mengonversi gambar ke teks** benar‑benar dimulai. Kita akan memuat file PNG yang berisi tulisan Arab.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Kasus Edge Umum

| Masalah | Gejala | Solusi |
|-------|---------|-----|
| Gambar terlalu gelap | Output berisi banyak ruang kosong | Pra‑proses dengan Pillow (`ImageEnhance.Brightness`) |
| PNG memiliki kanal alfa | Beberapa mesin OCR membaca piksel transparan secara salah | Konversi ke RGB (`image.convert("RGB")`) sebelum memuat |
| Teks diputar | Teks yang dikenali terbalik | Putar gambar (`image.rotate(90, expand=True)`) sebelum diberikan ke mesin |

## Langkah 5: Jalankan Proses Pengenalan

Setelah semua disiapkan, kita akhirnya meminta mesin melakukan tugasnya.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

Metode `recognize` mengembalikan objek yang berisi string Unicode mentah, skor kepercayaan, dan kotak pembatas. Bagi kebanyakan pengembang, teks polos sudah cukup.

## Langkah 6: Tampilkan Teks Arab yang Dikenali

Sekarang kita mencetak hasilnya. Pada aplikasi nyata Anda mungkin menulis ke file, basis data, atau mengirimnya ke API terjemahan.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Saat Anda menjalankan skrip, Anda seharusnya melihat karakter Arab ditampilkan di konsol (pastikan terminal Anda mendukung Unicode). Jika yang muncul tanda tanya atau string kosong, periksa kembali pengaturan bahasa dan kualitas gambar.

### Output yang Diharapkan

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Jika output terlihat mirip dengan baris di atas, selamat—Anda telah berhasil **mengekstrak teks Arab** dari sebuah PNG!

## Contoh Lengkap yang Dapat Dijalankan

Berikut seluruh skrip, siap untuk disalin‑tempel. Ganti `YOUR_DIRECTORY/arabic_doc.png` dengan jalur ke file Anda sendiri.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Jalankan dengan `python run_ocr.py` (atau nama file apa pun yang Anda pilih). Jika semua terpasang dengan benar, Anda akan melihat kalimat Arab tercetak di konsol.

## Cara Menjalankan OCR pada Berbagai Format Gambar

Kode yang sama bekerja untuk JPEG, TIFF, atau BMP—cukup ubah ekstensi file. Metode `Image.load` secara otomatis mendeteksi format, sehingga Anda dapat **mengonversi gambar ke teks** tanpa kode tambahan.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Ingat, kualitas gambar sumber sangat memengaruhi akurasi langkah **mengenali teks Arab**. Gambar beresolusi tinggi dengan kompresi rendah memberikan hasil terbaik.

## Mengekstrak Teks dari PNG: Tips untuk Akurasi Lebih Baik

1. **DPI Penting** – Targetkan setidaknya 300 dpi. DPI lebih rendah sering menyebabkan karakter terlewat.  
2. **Kontras adalah Raja** – Gunakan alat pemrosesan gambar (misalnya OpenCV) untuk meningkatkan kontras sebelum memberi gambar ke mesin OCR.  
3. **Penghilangan Noise** – Bintik‑bintik kecil dapat membingungkan model; penyaringan median membantu.  

Berikut cuplikan singkat menggunakan Pillow untuk memperbaiki PNG sebelum OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan bahasa kanan‑ke‑kiri selain Arab?**  
J: Tentu saja. Cukup ubah kode bahasa (`"ar"` → `"he"` untuk Ibrani, `"fa"` untuk Persia) dan mesin akan memuat model yang sesuai.

**T: Bagaimana jika saya perlu mengekstrak teks dari banyak PNG dalam satu folder?**  
J: Loop melalui file‑file tersebut, gunakan kembali instance `ocr_engine` yang sama, dan kumpulkan hasilnya dalam daftar atau tulis masing‑masing ke file `.txt` terpisah.

**T: Bisakah saya mendapatkan skor kepercayaan untuk setiap kata?**  
J: Ya. `ocr_result` biasanya menyediakan metode `get_confidences()`. Pasangkan setiap skor kepercayaan dengan kata yang bersangkutan untuk kontrol kualitas.

## Langkah Selanjutnya

Sekarang Anda tahu **cara menjalankan OCR** pada PNG Arab, pertimbangkan ide‑ide lanjutan berikut:

- **Pemrosesan batch:** Gabungkan skrip dengan `os.listdir` untuk **mengekstrak teks Arab** dari seluruh direktori.  
- **Pasca‑pemrosesan:** Gunakan pustaka `arabic_reshaper` dan `python-bidi` untuk menampilkan output kanan‑ke‑kiri dengan benar dalam PDF.  
- **Integrasi:** Salurkan teks yang diekstrak ke indeks pencarian (misalnya Elasticsearch) agar dokumen yang dipindai dapat dicari.  

Setiap topik ini membangun di atas dasar yang dibahas di sini, dan akan membantu Anda mengubah skrip **mengonversi gambar ke teks** sederhana menjadi pipeline siap produksi.

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}