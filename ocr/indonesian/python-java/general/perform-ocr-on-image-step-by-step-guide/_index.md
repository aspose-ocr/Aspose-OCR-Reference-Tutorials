---
category: general
date: 2026-03-18
description: Lakukan OCR pada gambar untuk mengekstrak teks dari gambar dengan cepat.
  Pelajari cara memuat gambar untuk OCR, membuat mesin OCR, dan meningkatkan akurasi
  OCR dengan opsi bahasa.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: id
og_description: Lakukan OCR pada gambar dengan panduan detail ini. Pelajari cara memuat
  gambar untuk OCR, membuat mesin OCR, dan meningkatkan akurasi OCR untuk ekstraksi
  teks yang andal.
og_title: Lakukan OCR pada Gambar – Tutorial Pemrograman Lengkap
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Lakukan OCR pada Gambar – Panduan Langkah demi Langkah
url: /id/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar – Tutorial Pemrograman Lengkap

Pernah **perform OCR on image** tetapi tidak yakin pustaka mana yang harus dipilih atau bagaimana mendapatkan hasil yang dapat diandalkan? Anda tidak sendirian. Dalam panduan ini kami akan membahas semua yang Anda perlukan untuk **extract text from image**, mulai dari memuat gambar hingga menyesuaikan opsi bahasa sehingga Anda dapat **improve OCR accuracy** pada setiap langkah.

Kami akan membahas cara **load image for OCR**, cara **create OCR engine**, dan mengapa setiap pengaturan penting. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang mencetak teks yang dikenali, dan Anda akan memahami “mengapa” di balik setiap baris—tanpa jalan pintas “lihat dokumentasinya”. Mari kita mulai.

## Apa yang Anda Butuhkan

- Python 3.8+ (kode menggunakan f‑strings dan type hints)
- Paket hipotetik `ocr_lib` – instal dengan `pip install ocr_lib`
- File gambar yang berisi teks cetak yang jelas (misalnya `lab_report.png`)
- Editor teks atau IDE dasar (VS Code, PyCharm, apa saja yang Anda suka)

Jika Anda sudah memiliki semua itu, bagus—Anda siap. Jika belum, unduh Python dari python.org dan jalankan perintah pip; hanya memerlukan satu menit.

![perform OCR on image example](/images/ocr-example.png)

*Alt text: perform OCR on image – contoh output yang menampilkan teks yang diekstrak.*

## Langkah 1: Buat OCR Engine – Cara **create OCR engine** di Python

Sebelum pengenalan apa pun dapat terjadi, pustaka memerlukan objek engine yang menyimpan konfigurasi dan status runtime. Anggap engine sebagai otak di balik operasi ini.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Mengapa ini penting:** Menginstansiasi engine di awal memungkinkan Anda menambahkan opsi bahasa nanti, dan juga menyimpan model internal dalam cache untuk panggilan selanjutnya yang lebih cepat.

## Langkah 2: Muat Gambar untuk OCR – Cara yang tepat untuk **load image for OCR**

Setelah kita memiliki engine, kita harus memberikannya sesuatu untuk dibaca. Metode `setImageFromFile` menerima jalur sistem file; jalur dapat berupa absolut atau relatif terhadap direktori kerja skrip.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Tips pro:** Gunakan jalur absolut atau `os.path.join` untuk menghindari kejutan “file tidak ditemukan” ketika skrip dijalankan dari folder yang berbeda.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Langkah 3: Tingkatkan Akurasi OCR – Menyetel **language options** untuk **improve OCR accuracy**

OCR bawaan berfungsi, tetapi kosakata khusus domain (seperti istilah laboratorium) sering membuatnya gagal. Dengan memberikan kamus khusus dan daftar hitam, Anda mengurangi kesalahan pengenalan seperti mengira “0” dengan “O”.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Mengapa ini membantu:** Kamus memberi tahu model OCR bahwa “HPLC” adalah token yang valid, mencegahnya memecah kata menjadi tidak masuk akal. Daftar hitam memberi tahu model untuk memperlakukan simbol ambigu sebagai noise, yang secara langsung **improves OCR accuracy**.

## Langkah 4: Lakukan OCR pada Gambar – Panggilan inti **perform OCR on image**

Dengan engine yang sudah dipersiapkan dan gambar yang terpasang, saatnya benar‑benar mengenali teks. Langkah ini mengembalikan objek `OcrResult` yang dapat Anda query untuk teks mentah, skor kepercayaan, atau bounding box.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Jika gambar buram, Anda akan melihat angka kepercayaan yang lebih rendah dalam hasil. Itu menjadi sinyal untuk pra‑proses gambar (misalnya, tingkatkan kontras) sebelum memberikannya ke engine.

## Langkah 5: Ekstrak Teks dari Gambar – Mengambil string akhir

Akhirnya, kita meminta `OcrResult` untuk representasi tekstualnya. Metode `getText()` mengembalikan string teks biasa yang siap untuk diproses lebih lanjut (menyimpan ke file, memasukkan ke basis data, dll.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Output yang diharapkan:** Dengan asumsi `lab_report.png` berisi tabel sederhana, Anda mungkin melihat sesuatu seperti:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Itulah bagian **extract text from image** selesai.

## Contoh Lengkap yang Berfungsi – Gabungkan Semua

Berikut adalah satu skrip yang menyatukan potongan‑potongan dari bagian‑bagian sebelumnya. Anda dapat menyalin‑tempelnya ke dalam `run_ocr.py` dan menjalankan `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Daftar Periksa Verifikasi Cepat

| ✅ | Item |
|---|------|
| ✔️ | Engine dibuat (`create OCR engine`) |
| ✔️ | Gambar dimuat (`load image for OCR`) |
| ✔️ | Opsi bahasa diatur (`improve OCR accuracy`) |
| ✔️ | OCR dijalankan (`perform OCR on image`) |
| ✔️ | Teks diekstrak (`extract text from image`) |

Jalankan skrip dan perhatikan konsol. Jika Anda melihat blok “OCR Output” dengan isi laporan Anda, maka Anda telah berhasil **perform OCR on image**.

## Masalah Umum & Cara Menghindarinya

| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| **Input buram** | Model OCR tidak dapat membedakan karakter | Pra‑proses dengan OpenCV: `cv2.GaussianBlur` atau tingkatkan DPI |
| **Bahasa salah** | Bahasa default mungkin diatur ke selain bahasa Inggris | Panggil `engine.setLanguage("eng")` sebelum `recognize()` |
| **Istilah kamus yang hilang** | Kata khusus domain menjadi berantakan | Tambahkan melalui `setDictionary` seperti pada Langkah 3 |
| **Karakter dalam daftar hitam menyebabkan |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}