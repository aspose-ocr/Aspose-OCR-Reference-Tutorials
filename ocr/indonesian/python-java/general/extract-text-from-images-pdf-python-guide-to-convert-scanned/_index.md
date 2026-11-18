---
category: general
date: 2026-06-06
description: Ekstrak teks dari gambar PDF menggunakan OCR Python. Pelajari cara mengonversi
  dokumen yang dipindai menjadi teks dengan cepat menggunakan pengenalan batch asynchronous.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: id
og_description: Ekstrak teks dari gambar PDF dengan Python. Panduan langkah demi langkah
  ini menunjukkan cara mengonversi dokumen yang dipindai menjadi teks menggunakan
  OCR asinkron.
og_title: Ekstrak Teks dari PDF Gambar – Tutorial OCR Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Ekstrak Teks dari PDF Gambar – Panduan Python untuk Mengonversi Dokumen Pindai
  menjadi Teks
url: /id/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari PDF Gambar – Panduan Python untuk Mengonversi Dokumen Pindai menjadi Teks

Pernah membutuhkan untuk **extract text from images pdf** tanpa menghabiskan berjam‑jam mengetik ulang? Dalam panduan ini kami akan menunjukkan cara **convert scanned documents to text** menggunakan alur kerja OCR asynchronous yang sederhana di Python.  

Jika Anda pernah menatap tumpukan PDF yang dipindai dan berpikir, “Harusnya ada cara yang lebih cepat,” Anda berada di tempat yang tepat. Kami akan menelusuri setiap baris kode, menjelaskan mengapa setiap bagian penting, dan bahkan membahas beberapa kasus tepi yang mungkin Anda temui.

## Apa yang Akan Anda Pelajari

- Cara memulai mesin OCR dan mengatur bahasa pengenalan.  
- Mekanisme memberi daftar campuran PNG dan PDF ke pengenalan batch.  
- Menjalankan pekerjaan OCR secara asynchronous sehingga aplikasi Anda tetap responsif.  
- Mengambil kembali hasilnya, memadukannya dengan file sumber, dan mencetak output yang bersih.  

**Prerequisites**: Python 3.8+, pemahaman dasar tentang `asyncio` atau `concurrent.futures`, dan perpustakaan OCR yang menyediakan kelas `OcrEngine` serupa dengan contoh (misalnya, Aspose.OCR, wrapper Tesseract, atau wrapper khusus). Tidak memerlukan pengaturan berat—cukup instal perpustakaan dan Anda siap.

![extract text from images pdf](https://example.com/placeholder.png "Screenshot of OCR output – extract text from images pdf")

## Ekstrak Teks dari PDF Gambar – Menyiapkan Mesin OCR

Hal pertama yang Anda butuhkan adalah sebuah instance mesin OCR yang dikonfigurasi untuk bahasa dokumen Anda. Dalam kasus kami, kami akan menggunakan bahasa Prancis, tetapi Anda dapat menggantinya dengan bahasa apa pun yang didukung.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Why this matters**: Menetapkan bahasa di awal secara dramatis meningkatkan akurasi. Mesin menggunakan kamus dan model karakter khusus bahasa; memberi bahasa yang salah merupakan sumber umum output yang kacau.

## Siapkan Daftar File – Gambar dan PDF Bersama-sama

Pengrecognizer batch kami dapat menangani baik gambar raster (`.png`, `.jpg`) maupun kontainer PDF. Cukup berikan daftar Python biasa berisi jalur file.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Tip**: Jaga daftar tetap datar; mesin akan secara internal mengekstrak setiap halaman PDF menjadi gambar sebelum pengenalan. Jika Anda memiliki ribuan file, pertimbangkan memecah daftar menjadi batch lebih kecil untuk menghindari lonjakan memori.

## Memulai Pengakuan Batch Asynchronous

Alih-alih memblokir thread utama, kami meluncurkan pekerjaan OCR di latar belakang. Metode ini mengembalikan sebuah `Future` yang pada akhirnya akan berisi daftar objek `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**How it works**: Di balik layar, mesin membuat thread pool (atau tugas async, tergantung implementasinya). Ini memungkinkan Anda terus melakukan pekerjaan lain—seperti memperbarui UI, mengambil lebih banyak file, atau mencatat kemajuan—sementara proses berat terjadi di tempat lain.

## Lakukan Sesuatu yang Berguna Saat OCR Berjalan

Kesalahan umum adalah duduk diam dan mem-poll future dalam loop ketat. Sebagai gantinya, Anda dapat melakukan pekerjaan tidak terkait apa pun. Untuk demonstrasi, kami hanya akan mencetak baris status.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Kumpulkan Hasil Setelah Future Selesai

Saat Anda siap mengumpulkan output OCR, gunakan `as_completed` dari `concurrent.futures`. Pola ini bekerja baik Anda memiliki satu future atau banyak.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**What you’ll see**: Setiap jalur file diikuti oleh representasi teks polos yang diekstrak. Untuk PDF, `result.text` berisi teks yang digabungkan dari setiap halaman.

### Output yang Diharapkan (contoh)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Jika Anda melihat karakter yang hilang, periksa kembali bahwa bahasa yang Anda atur cocok dengan bahasa dokumen, dan pertimbangkan pra‑pemrosesan gambar (meluruskan, meningkatkan kontras) sebelum memberikannya ke mesin.

## Menangani Kasus Tepi dan Jebakan Umum

| Situasi | Apa yang Harus Dilakukan |
|-----------|------------|
| **Mixed languages** | Jalankan proses deteksi bahasa terlebih dahulu, kemudian buat instance mesin terpisah per bahasa. |
| **Huge PDFs (> 100 MB)** | Bagi PDF menjadi halaman individual di disk (mis., menggunakan `PyPDF2`) dan berikan sebagai entri terpisah. |
| **Non‑Latin scripts** | Pastikan perpustakaan OCR menyertakan paket bahasa yang diperlukan; beberapa perpustakaan mengharuskan Anda mengunduh file data tambahan. |
| **Performance bottleneck** | Tingkatkan ukuran thread pool (`engine.set_thread_pool_size(8)`) atau beralih ke backend yang dipercepat GPU jika tersedia. |
| **Missing text in low‑resolution images** | Pra‑proses dengan OpenCV: `cv2.resize`, `cv2.threshold`, dan `cv2.medianBlur` untuk meningkatkan keterbacaan. |

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Simpan ini sebagai `extract_text_async.py`, ganti `YOUR_DIRECTORY` dengan jalur ke file Anda, instal paket OCR (`pip install your-ocr-lib`), dan jalankan `python extract_text_async.py`. Anda akan melihat output konsol seperti yang ditunjukkan sebelumnya.

## Langkah Selanjutnya – Melampaui Ekstraksi Dasar

- **Post‑processing**: Hapus spasi ekstra, normalisasi Unicode (`unicodedata.normalize`), atau jalankan pemeriksa ejaan untuk membersihkan noise OCR.  
- **Structured output**: Ekspor hasil ke CSV, JSON, atau langsung ke basis data untuk pencarian downstream.  
- **Parallel batches**: Jika Anda memiliki ratusan file, buat beberapa future dan gunakan antrian untuk menjaga CPU sibuk tanpa membebani memori.  
- **Integrate with web frameworks**: Sambungkan skrip ini ke endpoint Flask atau FastAPI untuk menyediakan OCR on‑demand sebagai layanan.

---

### TL;DR

Anda sekarang tahu cara **extract text from images pdf** dengan skrip Python minimal yang menjalankan OCR secara asynchronous, memungkinkan Anda **convert scanned documents to text** sementara program Anda tetap responsif. Bereksperimenlah dengan pengaturan bahasa, ukuran batch, dan trik pra‑pemrosesan untuk memperoleh akurasi karakter hingga yang terakhir.

Ada variasi yang ingin Anda bagikan—mungkin OCR pada catatan tulisan tangan atau layanan berbasis cloud? Tinggalkan komentar, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Ekstrak Teks dari Gambar Menggunakan Operasi OCR pada Folder](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Ekstrak Teks dari Gambar Menggunakan Aspose.OCR – Karakter yang Diizinkan](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}