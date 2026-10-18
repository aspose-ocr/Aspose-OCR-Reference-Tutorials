---
category: general
date: 2026-06-25
description: Pra‑proses gambar untuk OCR dan mengenali teks dari dokumen yang dipindai
  menggunakan Python. Tutorial langkah demi langkah dengan kode lengkap.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: id
og_description: Pra-proses gambar untuk OCR dan kenali teks dari dokumen yang dipindai
  dengan Python. Ikuti tutorial terperinci yang dapat dijalankan ini.
og_title: Pra-pemrosesan Gambar untuk OCR di Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Pra-pemrosesan Gambar untuk OCR di Python – Panduan Lengkap
url: /id/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pratinjau Gambar untuk OCR di Python – Panduan Lengkap

Pernah bertanya-tanya bagaimana **mempratinjau gambar untuk OCR** agar teks yang dihasilkan bersih dan dapat diandalkan? Anda tidak sendirian—banyak pengembang mengalami masalah yang sama ketika halaman yang dipindai miring atau kontrasnya tidak merata. Kabar baiknya, beberapa baris Python dapat meluruskan kekacauan itu, membinarisasi gambar, dan mengembalikan teks yang tajam serta dapat dicari.

Dalam tutorial ini kita akan melangkah melalui langkah‑langkah tepat untuk **mempratinjau gambar untuk OCR** *dan* **mengenali teks dari file dokumen yang dipindai**, menggunakan perpustakaan OCR populer. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan, memahami mengapa setiap pengaturan penting, serta tahu cara menyesuaikannya untuk kasus‑kasus tepi yang sulit.

## Apa yang Anda Butuhkan

- Python 3.8 atau lebih baru (kode juga berfungsi pada 3.10+)
- Paket OCR yang menyediakan kelas `OcrEngine`, `ImagePreProcessingOptions`, dan `Image` (misalnya modul fiktif `ocr` yang digunakan dalam contoh)
- Dokumen yang dipindai atau difoto yang sedikit miring atau berkontras rendah
- IDE favorit Anda atau terminal sederhana—tidak memerlukan GUI berat

Itu saja. Tidak ada biner tambahan, tidak ada Docker yang rumit. Mari kita mulai.

## Pratinjau Gambar untuk OCR – Langkah‑per‑Langkah

Berikut adalah alur kerja inti yang dibagi menjadi lima tahap jelas. Setiap tahap mencakup **mengapa** kita melakukannya, **kode** yang tepat, dan penjelasan singkat tentang apa yang terjadi di balik layar.

### Langkah 1: Buat Instance OCR Engine

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Mengapa ini penting:*  
Objek `OcrEngine` adalah otak dari operasi ini. Ia menyimpan konfigurasi seperti paket bahasa, ambang kepercayaan, dan—yang paling penting bagi kita—bendera pratinjau gambar. Membuatnya terlebih dahulu memberi kita kanvas bersih untuk mengaktifkan trik‑trik berikutnya.

### Langkah 2: Aktifkan Deskewing dan Binarisasi Otomatis

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Mengapa ini penting:*  
- **Deskewing** memutar gambar sehingga baris teks menjadi horizontal. Mesin OCR kesulitan ketika baseline miring lebih dari beberapa derajat.  
- **Binarisasi** mengubah gambar menjadi hitam‑putih murni, menghilangkan noise latar belakang yang dapat membingungkan pengklasifikasi karakter.  
Kedua opsi ini *otomatis* di banyak perpustakaan modern, tetapi Anda tetap harus mengaktifkannya—oleh karena itu penetapan eksplisit diperlukan.

> **Tip pro:** Jika gambar sumber Anda sudah sejajar sempurna, Anda dapat mengatur `auto_deskew=False` untuk menghemat satu milidetik waktu pemrosesan.

### Langkah 3: Muat Gambar Miring yang Ingin Diproses

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Mengapa ini penting:*  
Metode `Image.load` membaca file ke memori dan membungkusnya dalam objek yang dipahami mesin OCR. Ia juga mengekstrak metadata seperti DPI, yang dapat memengaruhi faktor skala default untuk deskewing.

> **Kasus tepi:** Jika gambar berupa TIFF multi‑halaman, Anda harus mengiterasi setiap halaman atau menggunakan pembantu seperti `ocr.MultiPageImage.load`. Pengaturan pratinjau yang sama berlaku untuk setiap halaman.

### Langkah 4: Lakukan OCR pada Gambar yang Telah Dipratinjau

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Mengapa ini penting:*  
Pada titik ini mesin menerapkan langkah deskew dan binarisasi yang telah diaktifkan sebelumnya, lalu menjalankan jaringan sarafnya (atau pipeline gaya Tesseract klasik) pada bitmap yang sudah dibersihkan. Objek `result` yang dikembalikan biasanya berisi teks polos, skor kepercayaan, dan kadang‑kadang data posisi untuk setiap kata.

> **Bagaimana jika teks masih berantakan?**  
Periksa resolusi gambar: OCR bekerja paling baik pada 300 dpi atau lebih. Jika sumber Anda lebih rendah, pertimbangkan untuk memperbesar gambar sebelum memuatnya, atau minta scan asli dari sumber dokumen.

### Langkah 5: Keluarkan Teks yang Dikenali

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Mengapa ini penting:*  
`result.text` adalah representasi string polos dari semua yang dapat dibaca mesin. Mencetaknya berguna untuk debugging cepat; dalam aplikasi nyata Anda mungkin akan menuliskannya ke file `.txt`, basis data, atau mengirimnya ke pipeline NLP selanjutnya.

---

## Mengenali Teks dari Dokumen yang Dipindai – Lebih Dari Dasar

Setelah pipeline dasar berfungsi, mari jelajahi beberapa variasi umum yang mungkin Anda temui saat **mengenali teks dari dokumen yang dipindai** dalam situasi nyata.

### 1. Menangani Banyak Bahasa

Jika dokumen Anda berisi bahasa Inggris dan Prancis, konfigurasikan mesin sebelum langkah 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

Sebagian besar mesin OCR menerima kode ISO‑639‑2; memuat paket bahasa tambahan menambah sedikit beban tetapi secara dramatis meningkatkan akurasi pada halaman multibahasa.

### 2. Menyetel Ambang Binarisasi Secara Halus

Binarisasi otomatis bekerja untuk kebanyakan kasus, tetapi beberapa fotokopi lama memerlukan ambang khusus:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Bereksperimenlah dengan nilai antara 120 dan 220 hingga latar belakang menghilang tanpa menghapus karakter yang pudar.

### 3. Mengekstrak Informasi Tata Letak

Kadang‑kadang Anda membutuhkan lebih dari teks mentah—Anda ingin tahu di mana setiap paragraf berada pada halaman. Banyak mesin menyediakan koleksi `result.blocks`:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

Ini sangat berharga untuk merekonstruksi tabel atau mempertahankan urutan kolom.

### 4. Memproses Sekelompok File

Jika Anda memiliki folder berisi PDF yang dipindai dan dikonversi ke JPEG, bungkus seluruh alur dalam sebuah loop:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

Loop ini menggunakan kembali instance `engine` yang sama, yang lebih efisien daripada membuatnya kembali untuk setiap file.

### 5. Menghadapi Scan Resolusi Rendah

Gambar beresolusi rendah (< 150 dpi) sering menghasilkan karakter yang kabur. Solusi cepat adalah memperbesar gambar menggunakan algoritma berkualitas tinggi sebelum memberi ke mesin OCR:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

Memperbesar tidak akan secara ajaib menciptakan detail, tetapi langkah binarisasi dapat bekerja dengan tepi yang lebih tajam, memberikan peningkatan modest.

---

## Output yang Diharapkan

Menjalankan skrip lima‑langkah asli pada scan yang agak miring dengan 300 dpi seharusnya mencetak sesuatu seperti:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Jika Anda melihat karakter yang berantakan, periksa kembali flag pratinjau, resolusi gambar, dan konfigurasi bahasa.

---

## Kesimpulan

Kami telah membahas segala yang Anda perlukan untuk **mempratinjau gambar untuk OCR** dan **mengenali teks dari dokumen yang dipindai** menggunakan Python. Mulai dari instance engine baru, kami mengaktifkan deskewing dan binarisasi otomatis, memuat gambar miring, menjalankan pengenalan, dan mencetak teks bersih. Sepanjang jalan kami mengeksplor dukungan multibahasa, penyesuaian ambang binarisasi, ekstraksi tata letak, pemrosesan batch, serta solusi untuk resolusi rendah.

Cobalah skrip ini pada scan Anda sendiri—mungkin tumpukan struk, formulir tulisan tangan, atau potongan koran lama. Setelah Anda merasa nyaman, coba tambahkan pembuatan PDF atau alirkan output ke indeks pencarian. Langit adalah batasnya.

**Siap untuk tantangan berikutnya?** Lihat tutorial kami tentang *“Extract Tables from Scanned PDFs with Python”* dan *“Train Custom OCR Models with TensorFlow”* untuk terus memperluas kotak peralatan otomatisasi dokumen Anda.

Selamat coding, semoga OCR Anda selalu tajam!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplor pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}