---
category: general
date: 2026-05-31
description: Tingkatkan akurasi OCR dengan Python melalui pra‑pemrosesan gambar untuk
  OCR. Pelajari cara mengekstrak teks dari file gambar, mengenali teks dari PNG, dan
  meningkatkan hasil.
draft: false
keywords:
- improve OCR accuracy
- preprocess image for OCR
- extract text from image
- recognize text from PNG
- image preprocessing for text
language: id
og_description: Tingkatkan akurasi OCR di Python dengan menerapkan pra‑pemrosesan
  gambar untuk teks. Ikuti panduan ini untuk mengekstrak teks dari file gambar dan
  mengenali teks dari PNG dengan mudah.
og_title: Tingkatkan Akurasi OCR di Python – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  headline: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  name: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Loads the PNG into memory
    text: Loads the PNG into memory
  - name: Applies denoise and deskew based on our settings
    text: Applies denoise and deskew based on our settings
  - name: Runs the neural‑network or classic pattern matcher
    text: Runs the neural‑network or classic pattern matcher
  - name: Packages the output into `recognition_result`
    text: Packages the output into `recognition_result`
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Tingkatkan Akurasi OCR di Python – Panduan Lengkap Langkah demi Langkah
url: /id/python-java/general/improve-ocr-accuracy-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tingkatkan Akurasi OCR di Python – Panduan Lengkap Langkah‑per‑Langkah

Pernah mencoba **meningkatkan akurasi OCR** hanya untuk mendapatkan output yang berantakan? Anda tidak sendirian. Kebanyakan pengembang menemui kendala ketika gambar mentah berisik, miring, atau hanya kontras rendah. Kabar baiknya? Beberapa trik pra‑pemrosesan dapat mengubah screenshot yang buram menjadi teks bersih yang dapat dibaca mesin.

Dalam tutorial ini kita akan melewati contoh dunia nyata yang **memproses gambar untuk OCR**, menjalankan mesin pengenalan, dan akhirnya **mengekstrak teks dari file gambar**—khususnya PNG. Pada akhir tutorial Anda akan tahu persis cara **mengenali teks dari PNG** dengan tingkat keberhasilan yang lebih tinggi, dan Anda akan memiliki potongan kode yang dapat dipakai ulang dalam proyek apa pun.

## Apa yang Akan Anda Pelajari

- Mengapa pra‑pemrosesan gambar penting bagi mesin OCR  
- Mode pra‑pemrosesan (denoise, deskew) mana yang memberikan peningkatan terbesar  
- Cara mengonfigurasi instance `OcrEngine` di Python  
- Skrip lengkap yang dapat dijalankan yang **mengekstrak teks dari file gambar**  
- Tips menangani kasus tepi seperti pemindaian yang diputar atau gambar beresolusi rendah  

Tidak diperlukan pustaka eksternal selain OCR SDK, tetapi Anda memerlukan Python 3.8+ dan gambar PNG yang ingin dibaca.

---

![Diagram yang menunjukkan langkah‑langkah untuk meningkatkan akurasi OCR di Python](image.png "Alur kerja meningkatkan akurasi OCR")

*Alt text: diagram alur kerja meningkatkan akurasi OCR yang menggambarkan langkah pra‑pemrosesan dan pengenalan.*

## Prasyarat

- Python 3.8 atau lebih baru terpasang  
- Akses ke OCR SDK yang menyediakan `OcrEngine`, `OcrEngineSettings`, dan `ImagePreprocessMode` (kode di bawah menggunakan API generik; ganti dengan kelas vendor Anda jika diperlukan)  
- Gambar PNG (`input.png`) yang ditempatkan di folder yang dapat Anda referensikan  

Jika Anda menggunakan lingkungan virtual, aktifkan sekarang—tidak ada yang rumit, cukup `python -m venv venv && source venv/bin/activate`.

---

## Langkah 1: Buat Instance OCR Engine – Mulai Meningkatkan Akurasi OCR

Hal pertama yang Anda butuhkan adalah objek engine OCR. Anggaplah sebagai otak yang nanti akan membaca piksel dan menghasilkan karakter.

```python
# Step 1: Initialise the OCR engine
ocr_engine = OcrEngine()
```

Mengapa ini penting: tanpa engine Anda tidak dapat menerapkan pra‑pemrosesan apa pun, dan gambar mentah akan langsung diberikan ke recogniser—biasanya skenario terburuk untuk akurasi.

---

## Langkah 2: Muat PNG Target – Siapkan Tahapan untuk Recognize Text from PNG

Sekarang kita memberi tahu engine file mana yang akan diproses. PNG bersifat lossless, yang sudah memberi kita sedikit keunggulan dibanding JPEG.

```python
# Step 2: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

Jika gambar berada di tempat lain, cukup sesuaikan jalurnya. Engine menerima format apa pun yang didukung, tetapi PNG sering mempertahankan detail halus yang diperlukan untuk tepi karakter yang tajam.

---

## Langkah 3: Konfigurasikan Pra‑Pemrosesan – Preprocess Image for OCR

Di sinilah keajaiban terjadi. Kami membuat objek pengaturan, mengaktifkan denoising untuk menghapus bintik‑bintik, dan menyalakan deskew sehingga teks yang miring menjadi lurus secara otomatis.

```python
# Step 3: Prepare preprocessing settings to improve accuracy
preprocess_settings = OcrEngineSettings()
preprocess_settings.preprocess_mode = (
    ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
)
```

### Mengapa Denoise + Deskew?

- **Denoise**: Noise piksel acak membingungkan algoritma pencocokan pola. Menghilangkannya membuat huruf lebih tajam.  
- **Deskew**: Bahkan kemiringan 2‑derajat pun dapat menurunkan skor kepercayaan secara drastis. Deskew menyelaraskan baseline, memungkinkan recogniser mencocokkan font dengan lebih andal.

Anda dapat bereksperimen dengan flag tambahan (misalnya `ImagePreprocessMode.CONTRAST_ENHANCE`) jika gambar Anda sangat gelap. Dokumentasi SDK biasanya mencantumkan semua mode yang tersedia.

---

## Langkah 4: Terapkan Pengaturan ke Engine – Hubungkan Pra‑Pemrosesan ke OCR

Tetapkan objek pengaturan ke engine sehingga proses pengenalan berikutnya menggunakan transformasi yang baru saja kita definisikan.

```python
# Step 4: Apply the settings to the engine
ocr_engine.settings = preprocess_settings
```

Jika Anda melewatkan langkah ini, engine akan kembali ke defaultnya (sering “tanpa pra‑pemrosesan”), dan Anda akan melihat **akurasi OCR yang lebih rendah**.

---

## Langkah 5: Jalankan Proses Pengenalan – Extract Text from Image

Setelah semuanya terhubung, akhirnya kita meminta engine melakukan tugasnya. Panggilan ini sinkron, mengembalikan objek hasil yang berisi string yang dikenali.

```python
# Step 5: Run the recognition process
recognition_result = ocr_engine.recognize()
```

Di balik layar engine kini:

1. Memuat PNG ke memori  
2. Menerapkan denoise dan deskew berdasarkan pengaturan kami  
3. Menjalankan jaringan saraf atau pencocokan pola klasik  
4. Mengemas output ke dalam `recognition_result`

---

## Langkah 6: Tampilkan Teks yang Dikenali – Verifikasi Peningkatan

Mari cetak string yang diekstrak. Dalam aplikasi nyata Anda mungkin menuliskannya ke file, basis data, atau mengirimnya ke layanan lain.

```python
# Step 6: Output the recognized text
print(recognition_result.text)
```

### Output yang Diharapkan

Jika gambar berisi kalimat “Hello, OCR World!” Anda harus melihat:

```
Hello, OCR World!
```

Perhatikan bagaimana teksnya bersih—tanpa simbol aneh atau karakter yang terputus. Itu hasil dari **pra‑pemrosesan gambar untuk teks** yang tepat.

---

## Pro Tips & Kasus Tepi

| Situasi | Apa yang Harus Disesuaikan | Mengapa |
|-----------|----------------------------|---------|
| PNG beresolusi sangat rendah (≤ 72 dpi) | Tambahkan `ImagePreprocessMode.SUPER_RESOLUTION` jika tersedia | Upsampling dapat memberi recogniser lebih banyak piksel untuk diproses |
| Teks diputar > 5° | Tingkatkan toleransi deskew atau putar secara manual dengan `Pillow` sebelum memberi ke engine | Sudut ekstrem kadang melewati deskew otomatis |
| Pola latar belakang berat | Aktifkan `ImagePreprocessMode.BACKGROUND_REMOVAL` | Menghilangkan gangguan non‑teks yang sebaliknya akan terbaca salah |
| Dokumen multibahasa | Set `ocr_engine.language = "eng+spa"` (atau serupa) | Engine memilih set karakter yang tepat, meningkatkan akurasi keseluruhan |

Ingat, **meningkatkan akurasi OCR** bukan solusi satu‑ukuran‑untuk‑semua; Anda mungkin perlu iterasi pada flag pra‑pemrosesan untuk dataset spesifik Anda.

---

## Skrip Lengkap – Siap Salin & Tempel

Berikut contoh lengkap yang dapat dijalankan yang mencakup setiap langkah yang telah dibahas. Simpan sebagai `improve_ocr_accuracy.py` dan jalankan dengan `python improve_ocr_accuracy.py`.

```python
"""
Improve OCR Accuracy in Python – Full Example
Author: Your Name (2026)
Requires: OCR SDK providing OcrEngine, OcrEngineSettings, ImagePreprocessMode
"""

# Import the necessary classes from the OCR SDK
from ocr_sdk import OcrEngine, OcrEngineSettings, ImagePreprocessMode

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the PNG you want to read
    image_path = "YOUR_DIRECTORY/input.png"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure preprocessing: denoise + deskew
    preprocess_settings = OcrEngineSettings()
    preprocess_settings.preprocess_mode = (
        ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
    )

    # 4️⃣ Apply the settings
    ocr_engine.settings = preprocess_settings

    # 5️⃣ Run recognition
    recognition_result = ocr_engine.recognize()

    # 6️⃣ Print the extracted text
    print("=== Recognized Text ===")
    print(recognition_result.text)

if __name__ == "__main__":
    main()
```

Jalankan, perhatikan konsol, dan Anda akan melihat hasil **extract text from image** secara langsung. Jika output terlihat aneh, sesuaikan flag `preprocess_mode` seperti yang dijelaskan pada tabel “Pro Tips”.

---

## Kesimpulan

Kita baru saja menelusuri resep praktis untuk **meningkatkan akurasi OCR** menggunakan Python. Dengan membuat `OcrEngine`, memuat PNG, **memproses gambar untuk OCR**, dan akhirnya **mengenali teks dari PNG**, Anda dapat secara andal **mengekstrak teks dari file gambar** bahkan ketika sumbernya tidak sempurna.  

Langkah selanjutnya? Coba proses batch gambar dalam loop, simpan tiap hasil ke CSV, atau bereksperimen dengan mode pra‑pemrosesan tambahan seperti peningkatan kontras. Pola yang sama berlaku untuk PDF, kwitansi yang dipindai, atau catatan tulisan tangan—cukup ganti input dan sesuaikan pengaturannya.

Punya pertanyaan tentang tipe gambar tertentu atau ingin tahu cara mengintegrasikan ini ke layanan web? Tinggalkan komentar, dan kami akan menjelajahi skenario tersebut bersama. Selamat coding, semoga hasil OCR Anda selalu jernih!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Extract Text from Image with Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)
- [Cara Extract Text from Image dengan Menyiapkan Rectangle di OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}