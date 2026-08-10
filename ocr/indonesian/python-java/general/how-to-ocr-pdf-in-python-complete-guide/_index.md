---
category: general
date: 2026-06-16
description: Cara melakukan OCR PDF menggunakan Python dalam hitungan menit – pelajari
  cara mengekstrak teks dari PDF, menjalankan OCR pada PDF, dan mengonversi teks PDF
  yang dipindai secara efisien.
draft: false
keywords:
- how to OCR PDF
- extract text from PDF
- run OCR on PDF
- convert scanned PDF text
- load PDF for OCR
language: id
og_description: 'Cara OCR PDF dengan Python: petunjuk langkah demi langkah untuk mengekstrak
  teks dari PDF, menjalankan OCR pada PDF, dan mengonversi teks PDF yang dipindai.'
og_title: Cara OCR PDF di Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  headline: How to OCR PDF in Python – Complete Guide
  type: TechArticle
- description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  name: How to OCR PDF in Python – Complete Guide
  steps:
  - name: Initialized an OCR engine.
    text: Initialized an OCR engine.
  - name: Set the language (optional but recommended).
    text: Set the language (optional but recommended).
  - name: Limited the page range to speed things up.
    text: Limited the page range to speed things up.
  - name: Loaded the PDF file.
    text: Loaded the PDF file.
  - name: Ran OCR on the document.
    text: Ran OCR on the document.
  - name: '**Extracted text from PDF** for immediate use.'
    text: '**Extracted text from PDF** for immediate use.'
  - name: Exported detailed results to **convert scanned PDF text** into JSON.
    text: Exported detailed results to **convert scanned PDF text** into JSON.
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Cara OCR PDF di Python – Panduan Lengkap
url: /id/python-java/general/how-to-ocr-pdf-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR PDF di Python – Panduan Lengkap

Pernah bertanya‑tanya **bagaimana cara OCR PDF** tanpa harus bersusah payah? Anda tidak sendirian; banyak pengembang mengalami kendala yang sama ketika ingin mengubah halaman yang dipindai menjadi teks yang dapat dicari. Kabar baiknya? Dengan beberapa baris Python Anda dapat memuat PDF untuk OCR, menjalankan OCR pada halaman PDF, dan mengambil string bersih yang dapat diedit dalam hitungan detik.

Dalam tutorial ini kami akan menelusuri contoh dunia nyata yang menunjukkan secara tepat cara OCR dokumen PDF, mengekstrak teks dari halaman PDF, dan bahkan mengonversi teks PDF yang dipindai menjadi hasil berstruktur JSON. Tanpa basa‑basi, hanya skrip yang dapat langsung Anda gunakan dalam proyek hari ini.

## Apa yang Anda Butuhkan

- Python 3.8+ (versi terbaru apa saja)
- Library `ocr` (atau wrapper yang kompatibel – kami mengasumsikan paket `ocr` generik yang mengikuti API yang ditunjukkan)
- PDF ber‑halaman‑banyak yang dipindai dan ingin Anda proses
- IDE atau editor pilihan Anda (VS Code, PyCharm, bahkan editor teks sederhana)

Itu saja. Jika Anda sudah memiliki semua itu, Anda siap mulai mengekstrak teks dari file PDF seperti seorang profesional.

## Langkah 1 – Siapkan Mesin OCR (How to OCR PDF)

Langkah pertama: buat instance mesin OCR. Anggap mesin sebagai otak yang akan membaca setiap piksel pada dokumen Anda.

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

> **Tips pro:** Menginisialisasi mesin tidak memakan banyak sumber daya, tetapi jika Anda berencana memproses puluhan PDF sekaligus, gunakan kembali objek `engine` yang sama untuk menghemat memori.

![Diagram of the OCR pipeline illustrating how to OCR PDF](/images/ocr-pdf-workflow.png "How to OCR PDF workflow")

## Langkah 2 – Pilih Bahasa yang Tepat (Run OCR on PDF)

Jika pemindaian Anda berbahasa Inggris, tetapkan bahasa secara eksplisit. Melewatkan langkah ini membuat mesin menebak, yang dapat memperlambat proses dan kadang kurang akurat.

```python
# Step 2 (optional): Set language to English
engine.language = ocr.Language.ENGLISH
```

Kenapa harus begitu? Karena memberi tahu mesin untuk **run OCR on PDF** dengan bahasa yang diketahui secara signifikan meningkatkan tingkat pengenalan—terutama untuk dokumen dengan istilah teknis.

## Langkah 3 – Fokus pada Halaman Tertentu (Load PDF for OCR)

Memproses arsip 500‑halaman yang besar bisa berlebihan jika Anda hanya membutuhkan beberapa bab pertama. Anda dapat membatasi rentang halaman seperti ini:

```python
# Step 3 (optional): Process only pages 1‑5
engine.pdf_page_range = (1, 5)
```

Penyesuaian kecil ini memberi tahu mesin untuk **load PDF for OCR** tetapi hanya menyentuh halaman yang Anda perlukan, menghemat waktu dan siklus CPU.

## Langkah 4 – Muat Dokumen Anda (Load PDF for OCR)

Sekarang arahkan mesin ke file yang sebenarnya. Pastikan path sudah benar; jika tidak, Anda akan mendapatkan `FileNotFoundError`.

```python
# Step 4: Load the multi‑page PDF file
engine.load_from_file("YOUR_DIRECTORY/multipage-document.pdf")
```

Pada titik ini mesin telah **loaded the PDF for OCR**, mengurai struktur internal, dan siap memulai pekerjaan berat.

## Langkah 5 – Jalankan Pengenalan (Run OCR on PDF)

Inilah saat keajaiban terjadi. Pemanggilan `recognize()` memindai setiap piksel, menerapkan model bahasa, dan mengembalikan objek hasil yang kaya.

```python
# Step 5: Run OCR on the loaded document
pdf_result = engine.recognize()
```

Di balik layar, mesin **runs OCR on PDF** halaman, membangun lapisan teks, dan bahkan menyimpan skor kepercayaan untuk setiap kata.

## Langkah 6 – Ambil Seluruh Teks (Extract Text from PDF)

Sebagian besar kasus penggunaan hanya membutuhkan teks polos. Atribut `text` memberikan Anda string gabungan dari semua yang dilihat mesin.

```python
# Step 6: Retrieve the combined text of the entire PDF
print("Full PDF text:\n", pdf_result.text)
```

Sekarang Anda telah berhasil **extracted text from PDF**—siap dimasukkan ke indeks pencarian, basis data, atau sekadar `print()`.

## Langkah 7 – Periksa Hasil Detail (Convert Scanned PDF Text)

Jika Anda membutuhkan lebih dari sekadar string mentah—misalnya kotak pembatas atau skor kepercayaan—gunakan ekspor JSON. Ini pada dasarnya **converting scanned PDF text** menjadi format yang dapat dibaca mesin.

```python
# Step 7: View detailed OCR results for each page in JSON
print(pdf_result.to_json(indent=2))
```

JSON mencakup array per‑halaman, setiap entri berisi teks yang dikenali, lokasinya pada halaman, dan metrik kepercayaan. Sempurna untuk pemrosesan lanjutan seperti ekstraksi entitas atau penyorotan khusus.

## Kesalahan Umum dan Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi Cepat |
|-------|----------------|-----------|
| **Karakter sampah** | Bahasa salah atau font hilang | Tetapkan `engine.language` secara eksplisit ke bahasa yang tepat. |
| **Halaman hilang** | `pdf_page_range` terlalu sempit | Periksa kembali tuple `(start, end)` sesuai dokumen Anda. |
| **Kinerja melambat** | PDF besar diproses sekaligus | Bagi PDF menjadi bagian‑bagian atau proses halaman secara paralel menggunakan `concurrent.futures`. |
| **Output kosong** | Salah ketik path file atau PDF tidak dapat dibaca | Pastikan file ada dan tidak diproteksi password. |

Menangani hal‑hal ini sejak awal menghemat jam‑jam debugging di kemudian hari.

## Memperluas Contoh

- **Pemrosesan batch:** Loop melalui direktori PDF, gunakan kembali instance `engine` yang sama.
- **Output khusus:** Tulis `pdf_result.text` ke file `.txt`, atau alirkan langsung ke mesin pencari seperti Elasticsearch.
- **Ekstraksi gambar:** Beberapa library OCR menyediakan gambar per halaman; Anda dapat mengekstraknya untuk verifikasi visual.

Berikut cuplikan kecil yang menunjukkan cara memproses folder secara batch:

```python
import pathlib, json

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    engine.load_from_file(str(pdf_path))
    result = engine.recognize()
    (pdf_folder / f"{pdf_path.stem}.txt").write_text(result.text)
    (pdf_folder / f"{pdf_path.stem}.json").write_text(result.to_json(indent=2))
    print(f"Processed {pdf_path.name}")
```

## Ringkasan – Apa yang Telah Kita Bahas

Kami memulai dengan pertanyaan **how to OCR PDF** di Python, kemudian:

1. Menginisialisasi mesin OCR.  
2. Menetapkan bahasa (opsional tetapi disarankan).  
3. Membatasi rentang halaman untuk mempercepat proses.  
4. Memuat file PDF.  
5. Menjalankan OCR pada dokumen.  
6. **Extracting text from PDF** untuk penggunaan langsung.  
7. Mengekspor hasil detail untuk **convert scanned PDF text** ke JSON.

Semua langkah ini memberi Anda fondasi kuat untuk mengubah PDF yang dipindai menjadi konten yang dapat dicari dan diedit.

## Langkah Selanjutnya

- Coba bahasa lain (`ocr.Language.SPANISH`, `ocr.Language.FRENCH`) untuk melihat bagaimana mesin menangani dokumen multibahasa.  
- Bereksperimen dengan pengaturan `engine.dpi` jika pemindaian Anda beresolusi rendah—DPI yang lebih tinggi dapat meningkatkan akurasi.  
- Padukan output OCR dengan library pemrosesan bahasa alami seperti spaCy untuk mengekstrak entitas, tanggal, atau frasa kunci secara otomatis.

Punya pertanyaan tentang **load PDF for OCR** atau mengalami kendala saat **run OCR on PDF**? Tinggalkan komentar di bawah, dan kami akan membantu memecahkan masalah bersama. Selamat coding, dan nikmati mengubah pemindaian yang membandel menjadi emas yang dapat dicari!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang memperluas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}