---
category: general
date: 2026-08-12
description: Jalankan OCR pada gambar menggunakan Python dan Aspose AI untuk mengekstrak
  teks dari gambar serta meningkatkan akurasi OCR dengan post‑processor pemeriksaan
  ejaan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: id
lastmod: 2026-08-12
og_description: Jalankan OCR pada gambar di Python dan segera ekstrak teks dari gambar
  sambil meningkatkan akurasi OCR menggunakan pemrosesan pasca AI Aspose.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Jalankan OCR pada gambar dengan Python – tutorial lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Jalankan OCR pada gambar dengan Python – panduan langkah demi langkah
url: /id/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada gambar dengan Python – panduan langkah demi langkah

Jika Anda perlu **menjalankan OCR pada gambar** di Python, panduan ini akan membawa Anda melalui seluruh alur kerja. Anda akan belajar cara **mengekstrak teks dari gambar**, menerapkan **koreksi teks OCR**, dan **meningkatkan akurasi OCR** hanya dengan beberapa baris kode.

Memproses dokumen yang dipindai, kwitansi, atau tangkapan layar sering menghasilkan teks yang berisik. Dengan menambahkan post‑processor pemeriksaan ejaan, Anda dapat mengubah output OCR mentah menjadi konten bersih yang dapat dicari tanpa beralih ke alat terpisah. Tutorial ini mencakup semua yang Anda perlukan—dari memuat gambar hingga menampilkan hasil yang telah dikoreksi.

## Prasyarat

* Python 3.9 atau yang lebih baru terpasang.
* Akses ke paket Aspose.OCR dan Aspose.AI untuk Python (atau pembungkus open‑source yang setara).
* Sebuah gambar contoh (misalnya `sample.png`) yang ditempatkan di direktori yang diketahui.
* Familiaritas dasar dengan fungsi Python dan kode berorientasi objek.

Anda dapat menginstal pustaka yang diperlukan dengan pip:

```bash
pip install aspose-ocr aspose-ai
```

> **Tips profesional:** Gunakan lingkungan virtual (`python -m venv .venv`) untuk menjaga dependensi terisolasi.

## Langkah 1: Jalankan OCR pada gambar – buat instance mesin

Langkah pertama adalah membuat objek `OcrEngine`. Objek ini mengenkapsulasi konfigurasi mesin OCR dan menyediakan metode untuk penanganan serta pengenalan gambar.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

Membuat mesin sekali dan menggunakannya kembali pada banyak gambar mengurangi beban awal dan memastikan pengaturan konsisten selama sesi.

## Langkah 2: Muat gambar untuk OCR

Sebelum pengenalan dapat dilakukan, mesin harus mengetahui gambar mana yang akan dianalisis. Metode `load_image` menerima jalur file atau aliran biner.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Mengapa ini penting:** Memuat gambar dengan benar adalah dasar untuk OCR yang akurat. Menyediakan gambar beresolusi tinggi (300 dpi atau lebih) biasanya **meningkatkan akurasi OCR** karena mesin dapat membedakan karakter dengan lebih jelas.

## Langkah 3: Ekstrak teks dari gambar – lakukan pengenalan dasar

Setelah gambar dimuat, Anda dapat memanggil `recognize()` untuk mendapatkan objek hasil. Hasil tersebut berisi teks mentah, skor kepercayaan, dan secara opsional kotak pembatas untuk setiap kata.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

Pada titik ini Anda telah berhasil **menjalankan OCR pada gambar** dan mengekstrak karakter mentah. Namun, teks tersebut mungkin mengandung kesalahan ejaan, terutama pada pemindaian berkualitas rendah.

## Langkah 4: Koreksi teks OCR – tambahkan pemeriksa ejaan pasca‑pemrosesan

Aspose AI menyediakan pipeline pasca‑pemrosesan yang fleksibel. Dengan menyambungkan pemeriksa ejaan khusus, Anda dapat memperbaiki kesalahan OCR umum (misalnya, “l” vs. “1”, “O” vs. “0”).

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**Cara kerja pemeriksa ejaan:** `MySpellChecker` harus mengimplementasikan metode `process(text: str) -> str`. Di dalamnya, Anda dapat menggunakan pustaka seperti `pyspellchecker` atau `symspellpy` untuk mengganti urutan kata yang tidak mungkin dengan alternatif yang divalidasi kamus.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## Langkah 5: Tampilkan teks OCR asli dan yang telah dikoreksi

Akhirnya, bandingkan output mentah dan yang telah dikoreksi. Ini membantu Anda memastikan bahwa **koreksi teks OCR** memang **meningkatkan akurasi OCR** untuk kasus penggunaan Anda.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### Output yang diharapkan

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

Baris yang telah dikoreksi menunjukkan bahwa pemeriksa ejaan menggantikan kesalahan pengenalan OCR umum (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## Langkah 6: Tingkatkan akurasi OCR – daftar periksa praktik terbaik

Bahkan dengan pasca‑pemrosesan, Anda dapat meningkatkan kualitas dasar mesin OCR:

| Item daftar periksa | Mengapa membantu |
|---------------------|------------------|
| **Gunakan gambar beresolusi tinggi (≥300 dpi)** | Lebih banyak data piksel mengurangi ambiguitas karakter. |
| **Konversi gambar berwarna ke skala abu‑abu** | Menghilangkan noise warna yang dapat membingungkan mesin. |
| **Terapkan deskewing gambar** | Meluruskan teks yang miring, mencegah kesalahan pemutusan baris. |
| **Setel bahasa/lokal secara eksplisit** | Membimbing pengenal ke set karakter yang tepat. |
| **Aktifkan model bahasa** (jika perpustakaan mendukungnya) | Menyediakan prediksi yang sadar konteks, lebih lanjut **meningkatkan akurasi OCR**. |

Anda dapat mengimplementasikan langkah‑langkah pra‑pemrosesan ini dengan Pillow atau OpenCV sebelum memberikan gambar ke `ocr_engine`.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## Skrip lengkap yang dapat dijalankan

Menggabungkan semua, skrip berikut siap untuk disalin‑tempel ke dalam file bernama `run_ocr.py` dan dijalankan.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

Menjalankan skrip mencetak teks asli dan yang telah dikoreksi, mengonfirmasi bahwa Anda telah berhasil **menjalankan OCR pada gambar**, **mengekstrak teks dari gambar**, dan **meningkatkan akurasi OCR** melalui **koreksi teks OCR**.

## Kesimpulan

Anda kini tahu cara **menjalankan OCR pada gambar** di Python, mengekstrak teks mentah, dan menerapkan pemeriksa ejaan pasca‑pemrosesan untuk mendapatkan hasil yang lebih bersih. Dengan mengikuti daftar periksa untuk **meningkatkan akurasi OCR**, Anda dapat menyesuaikan alur kerja ini untuk kwitansi, faktur, kartu identitas, atau dokumen yang dipindai apa pun.

### Selanjutnya?

* Jelajahi **kamus spesifik bahasa** untuk OCR multibahasa.
* Integrasikan pipeline dengan basis data atau indeks pencarian (misalnya Elasticsearch) agar teks yang diekstrak dapat dicari.
* Ganti pemeriksa ejaan sederhana dengan model bahasa neural (misalnya koreksi berbasis GPT) untuk akurasi yang lebih tinggi.

Silakan bereksperimen dengan teknik pra‑pemrosesan gambar yang berbeda, post‑processor yang berbeda, atau mesin OCR alternatif. Pola inti—**menjalankan OCR pada gambar → mengekstrak teks dari gambar → koreksi teks OCR → meningkatkan akurasi OCR**—tetap sama, memberikan Anda fondasi yang kuat untuk proyek digitalisasi dokumen apa pun.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}