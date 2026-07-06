---
category: general
date: 2026-04-26
description: cara menggunakan OCR pada PDF yang dipindai, mengekstrak teks dari PDF,
  menjalankan OCR pada PDF, dan mengonversi PDF yang dipindai menjadi file yang dapat
  dicari dalam beberapa langkah.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: id
og_description: 'cara menggunakan OCR di Python: pelajari cara mengekstrak teks dari
  PDF, menjalankan OCR pada PDF, dan mengubah PDF yang dipindai menjadi dokumen yang
  dapat dicari.'
og_title: cara menggunakan OCR – Panduan Cepat untuk Mengekstrak Teks dari PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Cara menggunakan OCR – Ekstrak Teks dari PDF dengan Python
url: /id/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara menggunakan OCR – Ekstrak Teks dari PDF dengan Python

Pernah bertanya‑tanya **bagaimana cara menggunakan OCR** untuk mengambil teks dari kontrak, kwitansi, atau ebook yang dipindai? Anda tidak sendirian. Dalam banyak proyek dunia nyata PDF yang Anda terima hanyalah gambar, dan tanpa OCR Anda tidak dapat mencari, mengindeks, atau menganalisis isinya.  

Dalam tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan **bagaimana cara menggunakan OCR**, cara **mengekstrak teks dari PDF**, dan mengapa Anda mungkin ingin **mengonversi PDF yang dipindai** menjadi dokumen yang dapat dicari. Kami juga akan membahas seni halus **memuat PDF sebagai gambar** sehingga mesin OCR dapat melihat setiap halaman dengan jelas.

> **Pratinjau cepat:** Pada akhir tutorial Anda akan memiliki skrip yang memuat PDF multi‑halaman, menjalankan OCR pada setiap halaman, dan mencetak teks yang dikenali – tanpa layanan eksternal.

## Apa yang Anda Butuhkan

- Python 3.9+ (versi terbaru apa pun dapat digunakan)
- paket `aocr` (atau pustaka OCR kompatibel lain yang menyediakan `OcrEngine` dan `Image.load`)
- File PDF yang dipindai yang ingin Anda proses (misalnya `contract.pdf`)
- Sebagian kecil RAM (≈ 200 MB per PDF 100‑halaman biasanya cukup)

Jika Anda belum menginstal pustaka OCR, jalankan:

```bash
pip install aocr
```

> **Tips pro:** Gunakan lingkungan virtual untuk menjaga ketergantungan tetap rapi.

## Langkah 1: Muat PDF sebagai Gambar – Potongan Pertama dari Puzzle

Sebelum OCR dapat dijalankan, PDF harus direpresentasikan sebagai gambar. Di sinilah kata kunci sekunder **load pdf as image** berperan.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Mengapa ini penting:* `aocr.Image.load` secara internal meraster setiap halaman PDF menjadi bitmap yang dapat dipahami mesin OCR. Jika Anda melewatkan langkah ini dan memberi PDF mentah, mesin akan mengeluarkan error karena mengharapkan data piksel, bukan data vektor.

> **Catatan:** Jalur dapat berupa absolut atau relatif. Pastikan file dapat dibaca; jika tidak Anda akan mendapatkan `FileNotFoundError`.

## Langkah 2: Jalankan OCR pada PDF – Mengubah Piksel menjadi Karakter

Sekarang PDF sudah menjadi gambar, kita akhirnya dapat **run OCR on PDF**. Potongan kode berikut memproses semua halaman sekaligus:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Apa yang terjadi di balik layar?* `process_all_pages` mengulang halaman‑halaman yang telah diraster, menerapkan model OCR, dan mengembalikan daftar objek hasil—satu per halaman. Setiap hasil berisi teks yang dikenali, skor kepercayaan, dan kotak pembatas (jika Anda membutuhkannya nanti).

## Langkah 3: Ekstrak Teks dari PDF – Mengambil String

Dengan hasil OCR di tangan, mengekstrak teks polos menjadi sangat mudah. Kami akan mengiterasi halaman‑halaman dan mencetak output, memperlihatkan kata kunci sekunder **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Output yang diharapkan** (dipotong untuk singkat):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Jika Anda memerlukan teks dalam satu string, cukup gabungkan:

```python
full_text = "\n".join(r.text for r in page_results)
```

Sekarang Anda telah berhasil **mengekstrak teks dari PDF** menggunakan OCR.

## Langkah 4: Konversi PDF yang Dipindai – Membuatnya Dapat Dicari

Banyak alat hilir (seperti Elasticsearch atau SharePoint) mengharapkan PDF yang dapat dicari, bukan sekadar dump teks. Anda dapat menyematkan output OCR kembali ke PDF asli, secara efektif **convert scanned PDF** menjadi versi yang dapat dicari.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Mengapa repot?* PDF yang dapat dicari mempertahankan tata letak dan gambar asli sambil memungkinkan pemilihan teks dan pengindeksan—menang‑menang bagi manusia dan mesin.

## Kesulitan Umum & Kasus Tepi

### PDF Multi‑Halaman Lebih Besar Dari Memori

Jika PDF Anda memiliki ratusan halaman, memuat semuanya sekaligus dapat menghabiskan RAM. Pustaka `aocr` mendukung pemuatan malas:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Kemudian proses halaman satu per satu:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Pemindaian Berkualitas Rendah

Akurasi OCR menurun drastis pada pemindaian yang buram atau kontras rendah. Sebelum memberi gambar ke mesin, pertimbangkan pra‑pemrosesan:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Dukungan Bahasa

Secara default mesin mengasumsikan bahasa Inggris. Untuk **run OCR on PDF** dalam bahasa lain, atur kode bahasa:

```python
ocr_engine.language = "spa"  # Spanish
```

Pastikan model bahasa yang bersangkutan telah diinstal.

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut skrip mandiri yang dapat Anda simpan dalam file bernama `ocr_pdf.py` dan jalankan langsung:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Jalankan seperti ini:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Anda akan melihat teks tercetak di konsol, dan jika Anda menambahkan opsi `-o`, PDF yang dapat dicari akan muncul di samping file asli.

## Tips Pro & Praktik Terbaik

- **Pemrosesan batch:** Saat menangani puluhan PDF, bungkus logika di atas dalam loop dan catat keberhasilan/kegagalan tiap file.
- **Penyaringan kepercayaan:** Setiap `page_result` menyertakan metrik kepercayaan. Buang atau beri tanda pada halaman dengan kepercayaan rendah untuk ditinjau secara manual.
- **Paralelisme:** Jika CPU Anda memiliki banyak inti, pertimbangkan menggunakan `concurrent.futures` untuk memproses halaman secara paralel—tetapi perhatikan penggunaan memori.
- **Penguncian versi:** API `aocr` dapat berubah. Kunci versi di `requirements.txt` (misalnya `aocr==2.3.1`) untuk menghindari perubahan yang merusak.

## Kesimpulan

Kami telah menelusuri **bagaimana cara menggunakan OCR** untuk **mengekstrak teks dari PDF**, **run OCR on PDF**, **load PDF as image**, dan bahkan **convert scanned PDF** menjadi format yang dapat dicari. Kode lengkap, penjelasan mencakup baik *apa* maupun *mengapa*, dan kini Anda memiliki pola yang dapat digunakan kembali untuk proyek apa pun yang berurusan dengan PDF berbasis gambar.

Apa selanjutnya? Cobalah mengalirkan teks yang diekstrak ke pipeline bahasa alami, indeks PDF yang dapat dicari dengan Elasticsearch, atau bereksperimen dengan backend OCR lain seperti Tesseract atau Azure Computer Vision. Langit adalah batasnya, dan alat‑alatnya sudah berada di ujung jari Anda.

Selamat coding, semoga PDF Anda selalu dapat dicari! 

![contoh cara menggunakan OCR](/images/ocr_workflow.png "cara menggunakan OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}