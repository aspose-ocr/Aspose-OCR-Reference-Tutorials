---
category: general
date: 2026-03-18
description: Pelajari cara mengekstrak teks dari gambar dan mengubah teks gambar yang
  dipindai menjadi string yang dapat diedit menggunakan Aspose OCR di Python. Kode
  langkah demi langkah disertakan.
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: id
og_description: Ekstrak teks dari gambar menggunakan Aspose OCR di Python. Tutorial
  ini menunjukkan cara mengonversi teks gambar yang dipindai hanya dengan beberapa
  baris kode.
og_title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Python
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Python
url: /id/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Python

Pernah membutuhkan untuk **mengekstrak teks dari gambar** tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—para pengembang terus-menerus menghadapi kesulitan mengubah PDF yang dipindai, tangkapan layar yang berisik, atau kwitansi yang difoto menjadi string yang dapat dicari dan diedit.  

Kabar baiknya? Dengan Aspose OCR untuk Python Anda dapat **mengonversi teks gambar yang dipindai** secara massal, tanpa meninggalkan IDE Anda. Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang siap dijalankan, menunjukkan secara tepat cara melakukannya, mengapa setiap langkah penting, dan hal‑hal yang perlu diwaspadai.

## Apa yang Akan Anda Pelajari

- Menyiapkan pustaka Aspose OCR di lingkungan Python.  
- Menyiapkan daftar file gambar (PNG, JPG, TIFF, dll.).  
- Menjalankan OCR batch dengan satu pemanggilan metode.  
- Mengakses dan menampilkan teks yang diekstrak untuk setiap file.  
- Menangani jebakan umum seperti format yang tidak didukung dan penggunaan memori untuk file besar.  

Pada akhir tutorial, Anda akan memiliki skrip yang dapat **mengekstrak teks dari gambar** sesuai permintaan—sempurna untuk mengotomatisasi entri data, mengindeks dokumen, atau memberi masukan ke pipeline NLP selanjutnya.

---

![Contoh ekstrak teks dari gambar](/images/ocr-extract-text.png "ekstrak teks dari gambar")

*Image alt text: “ekstrak teks dari gambar menggunakan Aspose OCR di Python”*

## Prasyarat

- Python 3.8 atau lebih baru (kode menggunakan f‑strings).  
- Lisensi Aspose OCR untuk Python yang valid atau kunci percobaan gratis.  
- Gambar yang ingin Anda proses disimpan secara lokal (campuran PNG, JPG, atau TIFF).  

Jika Anda sudah memiliki lingkungan virtual, bagus—jika belum, buat satu dengan:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

Sekarang Anda siap menginstal SDK.

## Langkah 1: Instal SDK Aspose OCR

Aspose mendistribusikan mesin OCR-nya melalui PyPI, jadi satu perintah `pip` sudah cukup:

```bash
pip install aspose-ocr
```

> **Pro tip:** Tentukan versi (misalnya `aspose-ocr==22.12`) untuk menghindari perubahan yang dapat merusak fungsi di kemudian hari.

## Langkah 2: Impor Kelas OCR Engine

Kelas inti yang akan Anda gunakan adalah `OcrEngine`. Impor di bagian atas skrip Anda:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *Mengapa ini penting:* Mengimpor hanya apa yang Anda butuhkan menjaga waktu start‑up tetap rendah, terutama ketika Anda nanti menyematkan skrip ini ke dalam aplikasi yang lebih besar.

## Langkah 3: Definisikan File Gambar yang Akan Diproses

Buat daftar Python yang berisi jalur lengkap ke setiap gambar yang ingin Anda pindai. Ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya.

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **Kasus tepi:** Jika Anda memiliki ratusan file, pertimbangkan menghasilkan daftar ini secara programatis dengan `glob.glob('*.png')` untuk menghindari pengeditan manual.

## Langkah 4: Jalankan OCR pada Semua Gambar Sekaligus

Aspose OCR menyediakan metode `processMultiple` yang nyaman dan mengembalikan daftar objek `OcrResult`—satu untuk setiap file input.

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *Mengapa pemrosesan batch?* Mengirim setiap gambar secara terpisah menimbulkan overhead tambahan (inisialisasi engine, memuat pustaka native). Pemanggilan batch mengurangi beban CPU dan mempercepat pekerjaan secara keseluruhan.

### Menangani Kesalahan dengan Elegan

Jika sebuah gambar tidak dapat dibaca (file rusak, format tidak didukung), `processMultiple` akan melemparkan pengecualian. Bungkus pemanggilan dalam blok `try/except` agar skrip tetap berjalan:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## Langkah 5: Keluarkan Teks yang Diekstrak untuk Setiap File

Iterasikan hasil, mengaitkan setiap `OcrResult` dengan nama file aslinya. Metode `getText()` mengembalikan string yang dikenali.

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### Output yang Diharapkan

Menjalankan skrip lengkap pada tiga tangkapan layar sederhana dapat menghasilkan sesuatu seperti:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

Jika sebuah gambar tidak mengandung karakter yang dapat dikenali, Anda akan melihat string kosong—tidak ada yang rusak, dan Anda dapat memutuskan apakah akan menandai file tersebut untuk peninjauan manual.

## Bonus: Menyetel Akurasi OCR

Aspose OCR menawarkan beberapa pengaturan opsional yang mungkin ingin Anda coba:

| Pengaturan | Fungsinya | Kapan Digunakan |
|------------|-----------|-----------------|
| `ocr_engine.setLanguage('eng')` | Memaksa model bahasa Inggris (mengurangi false positive). | Dokumen mayoritas berbahasa Inggris. |
| `ocr_engine.setResolution(300)` | Meningkatkan akurasi pada pemindaian ber‑dpi rendah. | Pemindaian di bawah 200 dpi. |
| `ocr_engine.setPageSegMode('single_block')` | Menganggap seluruh gambar sebagai satu blok teks. | Kwitansi sederhana atau kartu identitas. |

Anda dapat menambahkan baris‑baris ini tepat setelah membuat `ocr_engine`:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## Jebakan Umum & Cara Menghindarinya

1. **Stack TIFF besar** – TIFF multi‑halaman dapat mengonsumsi gigabyte RAM ketika dimuat sekaligus. Bagi file menjadi gambar satu halaman sebelum memberi ke `processMultiple`.  
2. **Skrip non‑Latin** – Jika Anda perlu **mengekstrak teks dari gambar** yang berisi karakter Cyrillic, Arab, atau Cina, ubah kode bahasa sesuai (`'rus'`, `'ara'`, `'chi_sim'`).  
3. **Spasi di jalur file** – Jalur Windows dengan spasi dapat menyebabkan `FileNotFoundError`. Bungkus setiap jalur dalam string mentah (`r"C:\My Folder\image.png"`) atau gunakan `os.path.abspath`.  

Menangani isu‑isu ini sejak awal menyelamatkan Anda dari error runtime yang membingungkan di kemudian hari.

---

## Contoh Skrip Lengkap

Berikut adalah skrip lengkap yang dapat Anda salin‑tempel ke file bernama `batch_ocr.py`. Skrip ini mencakup semua penyesuaian praktik terbaik yang dibahas di atas.

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

Simpan, aktifkan lingkungan virtual Anda, dan jalankan:

```bash
python batch_ocr.py
```

Anda akan melihat string yang diekstrak tercetak di konsol, siap untuk diproses lebih lanjut (misalnya, menyimpan ke basis data atau memberi masukan ke model bahasa alami).

---

## Kesimpulan

Dalam panduan ini kami menunjukkan cara **mengekstrak teks dari gambar** menggunakan Aspose OCR untuk Python, mencakup semua hal mulai dari instalasi hingga pemrosesan batch dan penanganan kesalahan. Skrip ini ringkas, berfungsi penuh, dan mudah diperluas—apapun kebutuhan Anda, baik mengonversi teks gambar yang dipindai ke file CSV, memberi masukan ke indeks pencarian, atau sekadar mengotomatisasi entri data.

Siap untuk langkah selanjutnya? Pertimbangkan menggabungkan pipeline OCR ini dengan penggabung PDF untuk membuat PDF yang dapat dicari, atau hubungkan dengan pemicu penyimpanan cloud sehingga setiap scan yang diunggah langsung diproses. Langit adalah batasnya, dan Anda kini memiliki fondasi yang kuat untuk membangunnya.

Punya pertanyaan atau ide untuk perbaikan? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}