---
category: general
date: 2026-03-18
description: Buat PDF yang dapat dicari dari file hasil pemindaian Anda menggunakan
  Aspose OCR. Pelajari cara mengonversi PDF hasil pemindaian, mengekstrak teks dari
  PDF, dan mengenali teks PDF dengan cepat.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: id
og_description: Buat PDF yang dapat dicari secara instan. Ikuti panduan ini untuk
  mengonversi PDF yang dipindai, mengekstrak teks dari PDF, dan mengenali teks PDF
  menggunakan Aspose OCR.
og_title: Buat PDF yang Dapat Dicari – Langkah demi Langkah dengan Aspose OCR
tags:
- OCR
- PDF
- Aspose
- Python
title: Buat PDF yang Dapat Dicari – Konversi PDF yang Dipindai dengan Aspose OCR
url: /id/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari – Panduan Langkah‑per‑Langkah  

Pernah perlu **membuat PDF yang dapat dicari** dari sekumpulan halaman yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami kebuntuan ketika pemindaian pertama tiba di server mereka.  

Kabar baiknya, dengan Aspose OCR Anda dapat **convert scanned pdf** dalam hanya beberapa baris kode, **extract text from pdf** untuk validasi, dan bahkan **recognize text pdf** secara langsung. Dalam tutorial ini kami akan membahas seluruh proses, mulai dari menginstal pustaka hingga menyimpan dokumen yang sepenuhnya dapat dicari, serta memberikan beberapa tips untuk menangani kasus tepi **convert image pdf**.

## Apa yang Akan Anda Capai  

* Memuat PDF yang dipindai (atau PDF yang hanya berisi gambar) ke dalam Aspose OCR.  
* Memberitahu mesin halaman mana yang akan diproses – berguna ketika Anda hanya membutuhkan sebagian.  
* Menyematkan hasil OCR kembali ke file asli sehingga output menjadi **searchable PDF** yang sesungguhnya.  
* Memverifikasi operasi dengan mencetak jumlah halaman dan, jika diinginkan, menampilkan teks yang diekstrak.  

Tidak ada layanan eksternal, tidak ada sihir tersembunyi—hanya Python murni dan API milik Aspose.

## Prasyarat  

* Python 3.8 atau lebih baru.  
* Paket `aspose-ocr` – instal dengan `pip install aspose-ocr`.  
* File PDF yang dipindai (atau PDF yang hanya berisi gambar).  
* Familiaritas dasar dengan scripting Python.  

Jika Anda sudah memiliki semuanya, bagus—mari kita mulai.

<img src="searchable-pdf-workflow.png" alt="Alur kerja membuat PDF yang dapat dicari">  

*(Ilustrasi alur kerja OCR – tidak diperlukan untuk kode tetapi membantu pembelajar visual.)*

## Langkah 1 – Inisialisasi Mesin OCR  

Hal pertama yang perlu dilakukan: Anda membutuhkan sebuah instance `OcrEngine`. Anggaplah itu sebagai otak yang akan membaca setiap piksel dan mengubahnya menjadi karakter Unicode.

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**Mengapa ini penting:** Tanpa mesin Anda tidak dapat mengatur opsi atau menjalankan pengenalan. Menginisialisasinya lebih awal juga memberi Anda tempat untuk melampirkan kamus khusus nanti.

## Langkah 2 – Muat PDF Sumber Anda  

Aspose OCR dapat membaca PDF secara langsung, yang berarti Anda tidak perlu meraster setiap halaman secara manual. Cukup arahkan mesin ke file.

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*Tip pro:* Jika PDF berukuran besar, pertimbangkan memuatnya dari stream untuk menghindari penguncian file di disk.

## Langkah 3 – Konfigurasikan Opsi Pengenalan PDF  

Di sinilah kata kunci sekunder mulai bersinar. Anda dapat memberi tahu mesin untuk **convert scanned pdf** hanya pada halaman tertentu, menyematkan teks yang dikenali, atau bahkan membiarkan gambar asli tidak tersentuh.

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**Mengapa ini penting:**  
* `setEmbedRecognisedText(True)` adalah kunci untuk mengubah PDF raster menjadi **searchable PDF**.  
* `setPageRange` membantu Anda **convert image pdf** secara selektif—berguna untuk dokumen besar di mana Anda hanya membutuhkan beberapa halaman yang di‑OCR.  
* Mengaktifkan ekstraksi teks memungkinkan Anda nanti **extract text from pdf** tanpa membuka penampil.

## Langkah 4 – Lampirkan Opsi ke Mesin  

Sekarang hubungkan opsi ke mesin. Langkah ini mudah terlewat, tetapi melewatkannya berarti mesin berjalan dengan pengaturan default (tanpa teks yang dapat dicari).

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## Langkah 5 – Jalankan OCR pada Halaman yang Dipilih  

Dengan semua terhubung, pengenalan sebenarnya cukup dengan satu pemanggilan metode.

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

Jika Anda memproses dokumen berukuran multi‑megabyte, Anda mungkin ingin membungkus ini dalam blok try/except untuk menangkap `OcrException` dan mencatat halaman yang bermasalah.

## Langkah 6 – Verifikasi Hasil  

Pemeriksaan cepat adalah mencetak berapa banyak halaman yang dianggap mesin telah diproses. Anda juga dapat mengambil teks mentah jika perlu **extract text from pdf** untuk analisis lebih lanjut.

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**Mengapa ini penting:** Melihat jumlah halaman mengonfirmasi bahwa `setPageRange` berfungsi, dan potongan teks yang diekstrak membuktikan OCR memang mengenali karakter.

## Langkah 7 – Simpan PDF yang Dapat Dicari  

Akhirnya, tulis output kembali ke disk. Konstanta `ImageFormats.PDF` memberi tahu Aspose untuk menyimpan file sebagai PDF, kini diperkaya dengan teks yang dapat dicari.

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

Buka file hasilnya di pembaca PDF apa pun dan coba pencarian teks—voilà, Anda telah **created searchable pdf**!

## Menangani Kasus Tepi Umum  

### Ketika sumber adalah PDF *hanya‑gambar*  

Jika PDF input Anda hanya berisi gambar (tanpa lapisan teks), kode yang sama tetap berfungsi—pastikan `setEmbedRecognisedText(True)` tetap diaktifkan. Anda juga mungkin ingin meningkatkan DPI untuk akurasi yang lebih baik:

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### Menangani Banyak Bahasa  

Aspose OCR mendukung paket bahasa. Muat bahasa sebelum memanggil `recognize()`:

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### Dokumen Besar  

Memproses PDF yang dipindai 500‑halaman dapat memakan banyak memori. Bagi pekerjaan:

1. Loop over rentang halaman (`setPageRange(start, end)`).  
2. Simpan setiap bagian sebagai PDF yang dapat dicari sementara.  
3. Gabungkan bagian-bagian dengan `PdfMerger` (komponen Aspose lainnya).

## Contoh Kerja Lengkap (Semua Langkah Bersama)

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

Menjalankan skrip ini akan memberi Anda **searchable PDF** yang dapat Anda buka di Adobe Reader, Chrome, atau pembaca PDF apa pun dan langsung mencari kata.

## Kesimpulan  

Anda kini memiliki solusi lengkap, end‑to‑end untuk **create searchable PDF** menggunakan Aspose OCR. Dari memuat sumber, mengonfigurasi opsi yang **convert scanned pdf**, mengekstrak dan memverifikasi teks, hingga akhirnya menyimpan hasil yang dapat dicari, setiap langkah telah tercakup.  

Selanjutnya, Anda mungkin ingin menjelajahi skenario **convert image pdf** di mana sumbernya adalah serangkaian JPEG yang dikemas ke dalam PDF, atau menyelami OCR spesifik bahasa untuk meningkatkan akurasi dokumen multibahasa. Bagaimanapun, pola tetap sama: atur opsi, jalankan `recognize()`, dan simpan.  

Silakan bereksperimen—ubah rentang halaman, sesuaikan DPI, atau pasang kamus khusus. Jika Anda menemui kendala, tinggalkan komentar di bawah atau periksa dokumentasi resmi Aspose untuk nuansa API terbaru. Selamat OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}