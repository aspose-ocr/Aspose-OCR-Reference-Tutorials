---
category: general
date: 2026-06-19
description: Cara mengekstrak PDF menggunakan OCR di Python – tutorial langkah demi
  langkah yang mencakup mengekstrak teks dari PDF, mengenali teks dari gambar, dan
  contoh OCR Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: id
og_description: Cara mengekstrak PDF menggunakan OCR di Python. Pelajari cara mengekstrak
  teks dari PDF, mengenali teks dari gambar, dan lihat contoh lengkap OCR dengan Python.
og_title: Cara Mengekstrak Teks PDF dengan OCR di Python – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Cara Mengekstrak Teks PDF dengan OCR di Python – Panduan Lengkap
url: /id/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekstrak Teks PDF dengan OCR di Python – Panduan Lengkap

Pernah bertanya-tanya **cara mengekstrak PDF** ketika file hanya berupa gambar yang dipindai? Anda bukan satu-satunya. Dalam banyak proyek dunia nyata—seperti kontrak, faktur, atau arsip bersejarah—PDF yang Anda terima tidak memiliki teks yang dapat dipilih. Kabar baik? Beberapa baris Python dapat mengubah halaman yang hanya berupa gambar menjadi teks yang dapat dicari dan diedit.

Dalam tutorial ini kami akan membahas contoh **OCR Python** yang praktis, yang membaca PDF, merender halaman pertamanya sebagai gambar, dan kemudian **mengekstrak teks dari PDF** menggunakan mesin OCR. Pada akhir tutorial Anda akan tahu persis **cara membaca PDF dengan OCR**, mengapa setiap langkah penting, dan bagaimana menyesuaikan kode untuk dokumen multi‑halaman atau bahasa yang berbeda.

## Apa yang Akan Anda Pelajari

- Menginstal dan menyiapkan perpustakaan OCR yang handal untuk Python.  
- Mengonversi halaman PDF menjadi gambar yang cocok untuk OCR.  
- **Mengenali teks dari gambar** dan mengambil string Unicode yang bersih.  
- Kesulitan umum (PDF beresolusi rendah, halaman terrotasi) dan cara menghindarinya.  
- Memperluas skrip untuk menangani banyak halaman atau pemrosesan batch.

**Prasyarat**: Python 3.8+, pip, dan pemahaman dasar tentang lingkungan virtual. Tidak diperlukan pengalaman OCR sebelumnya—cukup ikuti langkahnya.

---

## ## Cara Mengekstrak Teks PDF dengan OCR di Python

Header H2 ini berisi kata kunci utama kami tepat di tempat yang disukai mesin pencari. Mari langsung menyelam ke kode.

### Langkah 1 – Instal Paket yang Diperlukan

Pertama, kami memerlukan mesin OCR. Contoh di bawah menggunakan paket **ocr** yang populer (pembungkus tipis di atas Tesseract). Jika Anda lebih suka backend yang berbeda, konsepnya tetap sama.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro tip:** Di Linux, Anda juga memerlukan binary Tesseract: `sudo apt-get install tesseract-ocr`. Pengguna macOS dapat mengunduhnya via Homebrew: `brew install tesseract`.

### Langkah 2 – Inisialisasi Mesin OCR dan Atur Bahasa

Sekarang kami memulai mesin dan memberitahunya untuk mencari karakter bahasa Inggris. Anda dapat mengganti `ocr.Language.English` dengan kode bahasa lain yang didukung.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Mengapa ini penting:** Menentukan bahasa secara signifikan meningkatkan akurasi karena mesin dapat menerapkan kamus dan model karakter khusus bahasa.

### Langkah 3 – Muat Halaman PDF sebagai Gambar

OCR bekerja pada gambar raster, bukan objek PDF. Helper `ocr.Image.from_pdf` merender halaman yang dipilih menjadi bitmap. Sesuaikan `page_number` untuk halaman lain (indeks berbasis 0).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Edge case:** Jika PDF berisi grafik vektor bukan gambar yang dipindai, Anda mungkin mendapatkan render yang tajam. Untuk pemindaian beresolusi rendah, pertimbangkan meningkatkan DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Langkah 4 – Mengenali Teks dari Gambar yang Dirender

Berikut inti dari **ocr python example**. Mesin memproses bitmap dan mengembalikan objek yang berisi string yang diekstrak.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

Atribut `ocr_result.text` menyimpan output teks biasa, mempertahankan jeda baris bila memungkinkan.

### Langkah 5 – Cetak atau Simpan Teks yang Diekstrak

Akhirnya, kami menampilkan hasilnya. Dalam aplikasi nyata Anda mungkin akan menulis ke file atau basis data.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Menjalankan skrip seharusnya menampilkan sesuatu seperti:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Itulah alur kerja **mengekstrak teks dari pdf** lengkap menggunakan OCR.

---

## ## Mengenali Teks dari Gambar – Menyetel Akurasi

Jika Anda hanya tertarik pada **mengenali teks dari gambar** (misalnya, JPEG dari kwitansi), Anda dapat melewatkan langkah konversi PDF:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Tips untuk hasil yang lebih baik:**

- **Pra‑proses** gambar: konversi ke skala abu‑abu, terapkan thresholding, atau deskew. Pillow memudahkan hal ini.  
- **Tingkatkan DPI** saat merender PDF: resolusi lebih tinggi memberi mesin OCR lebih banyak detail.  
- **Aktifkan konfigurasi mesin OCR** untuk segmentasi halaman (`ocr_engine.config = "--psm 6"` untuk blok seragam).

---

## ## Membaca PDF dengan OCR – Menangani Banyak Halaman

Sebagian besar kontrak memiliki beberapa halaman. Melakukan loop pada setiap halaman sangat mudah:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Fungsi ini **membaca PDF dengan OCR**, menggabungkan output, dan menyisipkan penanda jeda halaman yang jelas. Anda kemudian dapat memasukkan `full_text` ke indeks pencarian atau menyimpannya sebagai file `.txt`.

---

## ## Kesulitan Umum dan Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| Karakter kacau, banyak `?` | Bahasa salah atau file data bahasa tidak ada | Instal paket bahasa Tesseract yang tepat (`tesseract-ocr-<lang>`) dan atur `ocr_engine.language`. |
| Baris hilang atau kata terpotong | DPI rendah (di bawah 150) | Render PDF pada 300 DPI atau lebih tinggi (`dpi=300`). |
| Teks terrotasi atau terbalik | Halaman yang dipindai tidak tegak | Gunakan `ocr.Image.deskew(page_image)` sebelum pengenalan. |
| Pemrosesan lambat pada PDF besar | Memproses halaman secara berurutan pada satu thread | Paralelisasi dengan `concurrent.futures.ThreadPoolExecutor`. |

---

## ## Memperluas Contoh OCR Python

- **Ekspor ke PDF/A**: Setelah ekstraksi, Anda dapat menyematkan teks kembali ke PDF yang dapat dicari menggunakan `reportlab` atau `pypdf2`.  
- **Deteksi bahasa**: Gunakan `langdetect` pada output OCR untuk secara dinamis mengganti `ocr_engine.language`.  
- **Pemrosesan batch**: Jelajahi direktori dengan `os.listdir` dan terapkan `extract_all_pages` pada setiap file.

---

## ## Output yang Diharapkan dan Verifikasi

Saat Anda menjalankan skrip pada pemindaian yang jelas dan berbahasa Inggris, Anda harus melihat blok teks bersih dengan tanda baca yang tepat. Verifikasi dengan:

1. Membandingkan beberapa baris dengan gambar hasil pindai asli.  
2. Menjalankan hitung kata sederhana (`len(ocr_result.text.split())`) untuk memastikan output tidak kosong.  
3. Opsional, mengirimkan hasil ke pemeriksa ejaan seperti `pyspellchecker` untuk menemukan kesalahan OCR.

---

## Kesimpulan

Kami telah membahas **cara mengekstrak PDF** ketika parsing tradisional gagal, mendemonstrasikan contoh **ocr python** lengkap, dan menjelaskan cara **mengenali teks dari gambar** serta **membaca PDF dengan OCR** untuk skenario satu‑halaman maupun multi‑halaman. Dengan potongan kode di atas Anda kini dapat mengubah PDF yang dipindai menjadi teks yang dapat dicari dan diedit—tidak lagi harus mengetik ulang secara manual.

Langkah selanjutnya? Coba ganti bahasa ke Spanyol (`ocr.Language.Spanish`) atau bereksperimen dengan teknik pra‑proses gambar untuk meningkatkan akurasi. Jika Anda membangun sistem manajemen dokumen, pertimbangkan mengindeks teks yang diekstrak dengan Elasticsearch untuk pencarian super cepat.

Ada pertanyaan atau menemukan PDF yang aneh? Tinggalkan komentar, dan selamat coding!  

![Cara mengekstrak PDF menggunakan OCR di Python](image.png "Cara mengekstrak PDF menggunakan OCR di Python")


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah-demi-Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Mengenali Teks PDF – Operasi OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}