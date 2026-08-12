---
category: general
date: 2026-01-12
description: Pelajari cara melakukan OCR pada PDF dengan Python dan membuat PDF dapat
  dicari dengan cepat. Konversi PDF yang dipindai, ekstrak teks PDF, dan lakukan OCR
  pada PDF yang dipindai menggunakan Python dengan Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- make pdf searchable
- convert scanned pdf
- extract text pdf
- ocr scanned pdf python
language: id
og_description: Bagaimana cara OCR PDF di Python? Tutorial langkah demi langkah ini
  menunjukkan cara mengonversi file PDF yang dipindai menjadi PDF yang dapat dicari
  dan mengekstrak teks dengan Aspose OCR.
og_title: Cara OCR PDF dan Membuatnya Dapat Dicari – Panduan Python
tags:
- OCR
- Python
- PDF processing
title: Cara OCR PDF dan Membuatnya Dapat Dicari – Panduan Python
url: /id/python-java/general/how-to-ocr-pdf-and-make-it-searchable-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR PDF dan Membuatnya Dapat Dicari – Panduan Python

Pernah bertanya-tanya **bagaimana cara OCR PDF** tanpa menghabiskan banyak uang untuk perangkat lunak komersial? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mereka perlu mengubah kontrak yang dipindai, faktur, atau PDF berbasis gambar apa pun menjadi dokumen yang dapat dicari. Kabar baik? Dengan beberapa baris Python dan Aspose OCR Anda dapat mengonversi PDF yang dipindai, mengekstrak teks PDF, dan akhirnya membuat PDF dapat dicari dalam hitungan menit.

Di tutorial ini kami akan membahas semua yang Anda perlukan: mulai dari menginstal pustaka, mengonfigurasi bahasa, memproses PDF yang dipindai, hingga menyimpan hasilnya sebagai PDF yang dapat dicari yang berisi gambar asli serta lapisan teks tersembunyi. Pada akhir tutorial Anda akan memiliki skrip yang dapat digunakan kembali dan dapat dimasukkan ke proyek apa pun—tanpa perlu menyalin‑tempel secara manual.

---

## Apa yang Anda Butuhkan

- **Python 3.8+** (kode berfungsi pada 3.9, 3.10, dan yang lebih baru)
- Lisensi **Aspose OCR for Python** yang aktif (versi percobaan gratis dapat digunakan untuk percobaan)
- File PDF yang dipindai (misalnya `scanned_contract.pdf`) yang ingin Anda buat dapat dicari
- Familiaritas dasar dengan baris perintah dan lingkungan virtual (opsional tetapi disarankan)

> **Pro tip:** Jika Anda belum memiliki lisensi, daftar untuk percobaan 30‑hari di situs web Aspose; versi percobaan berfungsi penuh untuk keperluan pengembangan.

---

## Cara OCR PDF dengan Aspose OCR (Kata Kunci Utama di H2)

Langkah pertama adalah mendapatkan paket yang tepat. Aspose OCR menyediakan API tingkat tinggi yang bersih yang menyembunyikan detail pemrosesan gambar tingkat rendah.

```bash
# Create a virtual environment (optional but tidy)
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`

# Install the Aspose OCR package
pip install aspose-ocr
```

Setelah paket terinstal, Anda dapat mulai menulis skrip.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr

# Step 2: Create an OCR engine instance and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Mengapa mengatur bahasa?**  
> Akurasi OCR sangat bergantung pada model bahasa. Dengan secara eksplisit memberi tahu mesin untuk mengharapkan teks bahasa Inggris, Anda mengurangi hasil positif palsu dan mempercepat pemrosesan.

---

## Langkah 2: Mengonversi PDF yang Dipindai menjadi PDF yang Dapat Dicari

Sekarang mesin sudah siap, arahkan ke dokumen yang dipindai. Metode `process_pdf` mengembalikan objek `PdfResult` yang berisi data gambar asli serta teks yang dikenali.

```python
# Step 3: Process the scanned PDF to extract text
input_pdf_path = "YOUR_DIRECTORY/scanned_contract.pdf"
pdf_result = ocr_engine.process_pdf(input_pdf_path)
```

Jika Anda perlu **mengonversi PDF yang dipindai** secara massal, cukup lakukan loop pada direktori dan panggil `process_pdf` untuk setiap file. Mesin menangani PDF multi‑halaman secara otomatis.

---

## Langkah 3: Menyimpan Hasil sebagai PDF yang Dapat Dicari (Membuat PDF Dapat Dicari)

Bagian akhir dari proses ini adalah menyimpan versi yang dapat dicari. Aspose OCR membuatnya menjadi satu baris kode:

```python
# Step 4: Define the output path for the searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Step 5: Save the result as a searchable PDF (image + hidden text layer)
pdf_result.save_as_searchable_pdf(searchable_pdf_path)
```

Saat Anda membuka `contract_searchable.pdf` di penampil PDF apa pun, Anda akan melihat gambar yang dipindai asli, tetapi kini Anda dapat **mencari kata apa pun** yang dikenali oleh mesin OCR. Lapisan teks tersembunyi tidak terlihat oleh mata namun dapat diindeks sepenuhnya.

---

### Skrip Lengkap – Siap Dijalan

Berikut adalah contoh lengkap yang dapat dijalankan. Salin‑tempel ke dalam file bernama `make_searchable.py` dan sesuaikan jalur agar cocok dengan lingkungan Anda.

```python
# make_searchable.py
# -------------------------------------------------
# Complete script to OCR a scanned PDF and make it searchable
# -------------------------------------------------

import os
import asposeocr as ocr

def ocr_to_searchable(input_path: str, output_path: str, language=ocr.Language.ENGLISH):
    """
    Convert a scanned PDF into a searchable PDF.
    
    Parameters
    ----------
    input_path : str
        Path to the scanned PDF file.
    output_path : str
        Destination path for the searchable PDF.
    language : ocr.Language, optional
        OCR language model (default is English).
    """
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"Input file not found: {input_path}")

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = language

    # Process the PDF (extracts images + hidden text)
    result = engine.process_pdf(input_path)

    # Save as searchable PDF
    result.save_as_searchable_pdf(output_path)
    print(f"✅ Searchable PDF saved to: {output_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    INPUT_PDF = "YOUR_DIRECTORY/scanned_contract.pdf"
    OUTPUT_PDF = "YOUR_DIRECTORY/contract_searchable.pdf"
    ocr_to_searchable(INPUT_PDF, OUTPUT_PDF)
```

**Output yang Diharapkan:**  
Menjalankan skrip mencetak baris konfirmasi dan membuat `contract_searchable.pdf`. Buka file, tekan `Ctrl + F`, dan ketik kata apa pun yang muncul di gambar yang dipindai asli—Anda akan melihat kecocokan secara instan.

---

## Pertanyaan Umum & Kasus Tepi

### 1. Bagaimana jika PDF berisi banyak bahasa?

Anda dapat mengirimkan daftar bahasa ke mesin:

```python
engine.language = [ocr.Language.ENGLISH, ocr.Language.SPANISH]
```

Aspose OCR akan mencoba mengenali teks dalam kedua bahasa pada halaman yang sama.

### 2. Bagaimana cara menangani pemindaian beresolusi rendah?

Jika gambar sumber berada di bawah 150 dpi, akurasi OCR dapat menurun. Pra‑proses PDF dengan alat seperti `pdfimages` untuk mengekstrak halaman, tingkatkan resolusinya dengan Pillow, dan masukkan kembali gambar beresolusi lebih tinggi ke `process_pdf`.

### 3. Bisakah saya mengekstrak teks polos tanpa membuat PDF yang dapat dicari?

Tentu saja. Objek `PdfResult` menyediakan properti `text`:

```python
plain_text = pdf_result.text
print(plain_text[:500])  # preview first 500 characters
```

Ini memenuhi kebutuhan **extract text pdf** ketika Anda hanya memerlukan karakter mentah.

### 4. Apakah ada cara untuk memproses batch folder PDF?

Ya—bungkus fungsi `ocr_to_searchable` dalam loop sederhana:

```python
import glob

for src in glob.glob("scans/*.pdf"):
    dst = src.replace("scans/", "searchable/").replace(".pdf", "_searchable.pdf")
    ocr_to_searchable(src, dst)
```

Sekarang Anda dapat **mengonversi pdf yang dipindai** secara massal dengan satu perintah.

---

## Tips Kinerja

- **Gunakan kembali mesin**: Membuat `OcrEngine` baru untuk setiap file menambah overhead. Instansiasi sekali dan gunakan kembali pada beberapa pemanggilan.
- **Pemrosesan paralel**: Untuk batch besar, pertimbangkan `concurrent.futures.ThreadPoolExecutor` di Python—Aspose OCR aman untuk thread pada operasi baca‑saja.
- **Manajemen memori**: Jika Anda memproses PDF sangat besar (ratusan halaman), panggil `gc.collect()` setelah setiap file untuk membebaskan memori.

---

## Kesimpulan

Kami telah membahas **bagaimana cara OCR PDF** dalam Python, mengubah pemindaian tersebut menjadi **PDF yang dapat dicari**, dan bahkan menunjukkan cara **extract text PDF** secara langsung. Dengan Aspose OCR Anda mendapatkan mesin yang handal yang menangani dokumen multi‑halaman, banyak bahasa, dan pengenalan akurasi tinggi—semua dengan hanya beberapa baris kode.

Cobalah pada kontrak, faktur, atau makalah riset arsip Anda sendiri. Setelah Anda menguasai dasar-dasarnya, bereksperimenlah dengan fitur lanjutan—seperti kamus khusus, pra‑pemrosesan gambar, atau mengintegrasikan output ke dalam indeks pencarian teks lengkap seperti Elasticsearch.

Punya pertanyaan lebih lanjut tentang **ocr scanned pdf python** atau membutuhkan bantuan memecahkan masalah pemindaian yang rumit? Tinggalkan komentar di bawah, dan selamat coding!

--- 

![how to ocr pdf example](image-placeholder.png){alt="how to ocr pdf example"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}