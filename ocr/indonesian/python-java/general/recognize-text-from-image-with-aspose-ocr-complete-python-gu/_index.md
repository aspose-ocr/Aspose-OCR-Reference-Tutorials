---
category: general
date: 2026-06-28
description: Pelajari cara mengenali teks dari gambar dan melakukan OCR pada gambar
  menggunakan Aspose OCR untuk Python. Termasuk langkah-langkah untuk mengatur bahasa
  OCR dan mengekstrak skor kepercayaan.
draft: false
keywords:
- recognize text from image
- perform ocr on image
- how to set OCR language
language: id
og_description: Mengenali teks dari gambar menggunakan Aspose OCR di Python. Panduan
  ini menunjukkan cara mengatur bahasa OCR, melakukan OCR pada gambar, dan membaca
  tingkat kepercayaan.
og_title: Mengenali teks dari gambar – Tutorial OCR Python Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  headline: recognize text from image with Aspose OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  name: recognize text from image with Aspose OCR – Complete Python Guide
  steps:
  - name: What if my image contains multiple languages?
    text: 'Aspose OCR supports multi‑language detection, but you need to pass a **combined
      language flag**. For example, to handle both Latin and Cyrillic:'
  - name: How do I improve accuracy on low‑resolution images?
    text: '- **Pre‑process** the image: increase contrast, apply binarization, or
      upscale using a library like Pillow. - **Set the correct DPI** if you know it;
      Aspose respects the image metadata. - **Choose the right language**—the more
      specific you are, the better the model performs.'
  - name: Can I extract only certain regions of the image?
    text: Yes. Use the `recognizeRegion` method (not shown in the basic example) and
      pass a rectangle object defining the area of interest. This is handy when you
      only need a table or a specific block of text.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Mengenali teks dari gambar dengan Aspose OCR – Panduan Python Lengkap
url: /id/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-python-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar dengan Aspose OCR – Panduan Python Lengkap

Pernah perlu **mengenali teks dari gambar** tetapi tidak yakin pustaka mana yang memberikan kecepatan dan akurasi? Anda tidak sendirian. Dalam dunia otomatisasi dokumen, kemampuan **melakukan OCR pada gambar** adalah kebutuhan harian—baik Anda mendigitalkan struk, memindai paspor, atau mengekstrak data dari tanda multilingual.

Dalam tutorial ini kita akan menjalankan contoh praktis yang menunjukkan secara tepat cara **mengenali teks dari gambar** menggunakan Aspose OCR untuk Python, dan juga membahas **cara mengatur bahasa OCR** sehingga mesin tahu apakah yang dihadapi adalah Latin, Cyrillic, atau skrip lainnya. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang mencetak teks lengkap, kepercayaan baris‑per‑baris, dan bahkan kotak pembatas untuk setiap kata.

## Apa yang Anda Butuhkan

- **Python 3.8+** (kode berfungsi pada versi terbaru apa pun)
- Paket **Aspose.OCR for Python via Java** – instal dengan `pip install aspose-ocr`
- Sebuah file gambar (misalnya `mixed_script.png`) yang berisi teks yang ingin Anda ekstrak
- IDE atau editor dasar—VS Code, PyCharm, atau bahkan editor teks sederhana sudah cukup

Tanpa ketergantungan berat, tanpa binary native yang harus dikompilasi. Cukup instal via pip dan Anda siap.

## Langkah 1: Instal dan Impor Mesin OCR

Langkah pertama, mari pasang pustaka ke mesin Anda dan impor kelas‑kelas yang diperlukan.

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

# Import the OCR engine and the language enumeration
from asposeocrjava import OcrEngine, Language
```

> **Tip pro:** Jika Anda berada di belakang proxy korporat, tambahkan flag `--proxy` pada perintah pip. Ini akan menghemat banyak waktu berpikir belakangan.

## Langkah 2: Buat Mesin dan **cara mengatur bahasa OCR**

Membuat instance `OcrEngine` semudah memanggil konstruktornya, tetapi kekuatan sesungguhnya muncul ketika Anda memberi tahu mesin bahasa apa yang diharapkan. Inilah bagian yang menjawab pertanyaan “**cara mengatur bahasa OCR**”.

```python
# Instantiate the OCR engine
ocr_engine = OcrEngine()

# Tell the engine we’re dealing with Latin script (you can pick others like Language.Cyrillic)
ocr_engine.setLanguage(Language.Latin)
```

Mengapa ini penting? Algoritma OCR menggunakan model karakter spesifik bahasa; mengatur bahasa yang tepat secara dramatis meningkatkan akurasi, terutama untuk skrip dengan glyph yang mirip (misalnya “0” vs “O” dalam Latin versus “О” dalam Cyrillic).

## Langkah 3: **melakukan OCR pada gambar** – Mengenali Teks

Sekarang kita memberikan jalur gambar ke mesin dan membiarkannya bekerja. Metode ini mengembalikan objek `RecognitionResult` yang berisi semua yang Anda perlukan.

```python
# Path to the image you want to process
image_path = "YOUR_DIRECTORY/mixed_script.png"

# Run the OCR operation
recognition_result = ocr_engine.recognizeImage(image_path)
```

Jika file tidak ditemukan, Aspose akan melempar `FileNotFoundError`. Bungkus pemanggilan dalam blok `try/except` untuk kode produksi—tidak ada yang lebih buruk daripada pengecualian tak tertangani yang menghentikan layanan Anda.

## Langkah 4: Keluarkan Teks yang Telah Diakui Secara Lengkap

Permintaan paling umum hanyalah “berikan saya teksnya”. Metode `getText()` menggabungkan semua baris yang terdeteksi menjadi satu string.

```python
# Print the complete text extracted from the image
print("Full text:", recognition_result.getText())
```

Anda akan melihat sesuatu seperti:

```
Full text: Hello World!
This is a sample mixed‑script image.
```

Itulah inti dari **mengenali teks dari gambar**—satu baris kode yang mengembalikan semua yang dapat diuraikan mesin.

## Langkah 5: (Opsional) Tampilkan Kepercayaan untuk Setiap Baris yang Terdeteksi

Skor kepercayaan membantu Anda menilai keandalan. Baris dengan skor di bawah, misalnya, 0.70 mungkin memerlukan tinjauan manusia.

```python
print("\n--- Line‑by‑Line Confidence ---")
for line in recognition_result.getLines():
    # Each line object provides its text and a confidence value between 0 and 1
    print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")
```

Output tipikal:

```
Line: 'Hello World!'  Confidence: 0.98
Line: 'This is a sample mixed‑script image.'  Confidence: 0.85
```

## Langkah 6: (Opsional) Dapatkan Kotak Pembatas untuk Setiap Kata – Berguna untuk Penyorotan UI

Jika Anda membangun penampil yang memungkinkan pengguna mengklik kata untuk melihat data OCR, koordinat kotak pembatas sangat berharga.

```python
print("\n--- Word Bounding Boxes ---")
for word in recognition_result.getWords():
    bbox = word.getBoundingBox()   # Returns (x, y, width, height)
    print(f"Word '{word.getText()}' at {bbox}")
```

Contoh output:

```
Word 'Hello' at (12, 34, 58, 20)
Word 'World' at (78, 34, 60, 20)
```

Koordinat ini dalam piksel relatif terhadap gambar asli, sehingga Anda dapat menimpanya langsung pada kanvas.

## Skrip Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip siap‑jalankan yang dapat Anda masukkan ke proyek apa pun. Cukup ganti `YOUR_DIRECTORY/mixed_script.png` dengan jalur sebenarnya ke gambar Anda.

```python
# ocr_demo.py
from asposeocrjava import OcrEngine, Language

def main(image_path: str, language: Language = Language.Latin):
    """
    Recognize text from an image using Aspose OCR.
    Parameters:
        image_path (str): Full path to the image file.
        language (Language): OCR language to use (default: Latin).
    """
    # Create the OCR engine and set the desired language
    ocr_engine = OcrEngine()
    ocr_engine.setLanguage(language)

    try:
        # Perform OCR
        result = ocr_engine.recognizeImage(image_path)

        # Full text output
        print("Full text:", result.getText())

        # Optional: line confidence
        print("\n--- Line‑by‑Line Confidence ---")
        for line in result.getLines():
            print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")

        # Optional: word bounding boxes
        print("\n--- Word Bounding Boxes ---")
        for word in result.getWords():
            bbox = word.getBoundingBox()
            print(f"Word '{word.getText()}' at {bbox}")

    except FileNotFoundError:
        print(f"Error: Image file not found at {image_path}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    # Change the path below to point at your own test image
    IMAGE_PATH = "YOUR_DIRECTORY/mixed_script.png"
    main(IMAGE_PATH, Language.Latin)
```

Jalankan dengan:

```bash
python ocr_demo.py
```

Anda akan melihat teks yang diekstrak lengkap, skor kepercayaan, dan kotak pembatas tercetak di konsol.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika gambar saya berisi banyak bahasa?

Aspose OCR mendukung deteksi multi‑bahasa, tetapi Anda harus memberikan **bendera bahasa gabungan**. Misalnya, untuk menangani Latin dan Cyrillic sekaligus:

```python
ocr_engine.setLanguage(Language.Latin | Language.Cyrillic)
```

Operator pipe (`|`) menggabungkan enum. Ini menjawab kebutuhan “**melakukan OCR pada gambar**” untuk skenario multilingual.

### Bagaimana cara meningkatkan akurasi pada gambar beresolusi rendah?

- **Pra‑proses** gambar: tingkatkan kontras, terapkan binarisasi, atau upscale menggunakan pustaka seperti Pillow.
- **Set DPI yang tepat** jika Anda mengetahuinya; Aspose menghormati metadata gambar.
- **Pilih bahasa yang tepat**—semakin spesifik, semakin baik model bekerja.

### Bisakah saya mengekstrak hanya wilayah tertentu dari gambar?

Ya. Gunakan metode `recognizeRegion` (tidak ditampilkan dalam contoh dasar) dan berikan objek persegi panjang yang mendefinisikan area minat. Ini berguna ketika Anda hanya membutuhkan tabel atau blok teks tertentu.

## Kesimpulan

Kita baru saja menelusuri contoh lengkap end‑to‑end tentang cara **mengenali teks dari gambar** menggunakan Aspose OCR untuk Python. Anda kini tahu cara **melakukan OCR pada gambar**, mengatur **bahasa OCR** dengan benar, serta mengambil skor kepercayaan dan kotak pembatas tingkat kata untuk keperluan UI selanjutnya.

Dari sini Anda dapat:

- Bereksperimen dengan bahasa lain (`Language.Arabic`, `Language.Japanese`, dll.)
- Mengintegrasikan skrip ke layanan web (Flask/Django) untuk menyediakan OCR sebagai API
- Menggabungkan data kotak‑pembatas dengan kanvas frontend agar pengguna dapat menyorot teks

Kemungkinannya seluas dokumen yang perlu Anda digitalisasi. Memiliki gambar sulit yang menolak bekerja? Tinggalkan komentar, dan kami akan membantu memecahkan masalah bersama. Selamat coding! 

![recognize text from image example](/images/ocr_example.png "recognize text from image – Aspose OCR output")


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}