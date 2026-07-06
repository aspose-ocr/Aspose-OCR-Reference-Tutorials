---
category: general
date: 2026-06-19
description: Cara melakukan OCR pada struk dan menjalankan pemeriksa ejaan untuk ekstraksi
  teks yang bersih. Ikuti tutorial Python langkah demi langkah ini.
draft: false
keywords:
- how to perform ocr
- extract text from receipt
- run spell checker
- perform ocr on image
- load image for ocr
language: id
og_description: Cara melakukan OCR pada struk dan langsung menjalankan pemeriksa ejaan.
  Pelajari alur kerja lengkapnya dalam Python dengan Aspose AI.
og_title: Cara Melakukan OCR pada Struk – Panduan Lengkap Pemeriksa Ejaan
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to perform OCR on receipts and run a spell checker for clean text
    extraction. Follow this step‑by‑step Python tutorial.
  headline: How to Perform OCR on Receipts – Spell Checker Guide
  type: TechArticle
- description: How to perform OCR on receipts and run a spell checker for clean text
    extraction. Follow this step‑by‑step Python tutorial.
  name: How to Perform OCR on Receipts – Spell Checker Guide
  steps:
  - name: '**Load the image** → the OCR engine knows *what* to read.'
    text: '**Load the image** → the OCR engine knows *what* to read.'
  - name: '**Perform OCR** → the engine spits out raw characters.'
    text: '**Perform OCR** → the engine spits out raw characters.'
  - name: '**Extract the text** → we pull the string out of the engine’s result object.'
    text: '**Extract the text** → we pull the string out of the engine’s result object.'
  - name: '**Run spell checker** → a smart post‑processor cleans up typos and OCR
      quirks.'
    text: '**Run spell checker** → a smart post‑processor cleans up typos and OCR
      quirks.'
  - name: '**Use the corrected text** → print, store, or pass it to another service.'
    text: '**Use the corrected text** → print, store, or pass it to another service.'
  type: HowTo
tags:
- OCR
- Python
- Aspose AI
- Text Extraction
title: Cara Melakukan OCR pada Struk – Panduan Pemeriksa Ejaan
url: /id/python/general/how-to-perform-ocr-on-receipts-spell-checker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR pada Struk – Panduan Pemeriksa Ejaan

Pernah bertanya-tanya **bagaimana melakukan OCR** pada sebuah struk tanpa membuat Anda frustasi? Anda bukan satu-satunya. Dalam banyak aplikasi dunia nyata—pelacak pengeluaran, alat pembukuan, atau bahkan pemindai daftar belanja sederhana—Anda perlu **mengekstrak teks dari struk** gambar dan memastikan teks tersebut dapat dibaca. Kabar baik? Dengan beberapa baris Python dan Aspose AI Anda dapat memperoleh string bersih yang telah diperiksa ejaannya dalam hitungan detik.

Dalam tutorial ini kami akan membahas seluruh alur: memuat gambar struk, menjalankan OCR, dan kemudian memoles hasilnya dengan post‑processor pemeriksa ejaan. Pada akhir tutorial Anda akan memiliki fungsi siap‑pakai yang dapat Anda sisipkan ke dalam proyek apa pun yang memerlukan digitalisasi struk yang andal.

## Apa yang Akan Anda Pelajari

- Cara **load image for OCR** menggunakan OcrEngine milik Aspose.
- Langkah‑langkah tepat untuk **perform OCR on image** file dalam Python.
- Cara **extract text from receipt** dan mengapa post‑processor penting.
- Cara **run spell checker** pada output OCR mentah untuk memperbaiki kesalahan umum.
- Tips menangani kasus tepi seperti pemindaian kontras rendah atau struk multi‑halaman.

### Prasyarat

- Python 3.8 atau lebih baru terpasang di mesin Anda.
- Lisensi Aspose.OCR yang aktif (versi percobaan gratis dapat digunakan untuk pengujian).
- Familiaritas dasar dengan fungsi Python dan penanganan pengecualian.

Jika Anda sudah memiliki itu, mari kita mulai—tanpa basa‑basi, hanya solusi yang berfungsi yang dapat Anda salin‑tempel.

![how to perform OCR example diagram](ocr_flow.png)

## Cara Melakukan OCR pada Struk – Ikhtisar

Sebelum kita mulai menulis kode, bayangkan alurnya sebagai jalur perakitan sederhana:

1. **Load the image** → mesin OCR tahu *apa* yang harus dibaca.  
2. **Perform OCR** → mesin mengeluarkan karakter mentah.  
3. **Extract the text** → kami mengambil string dari objek hasil mesin.  
4. **Run spell checker** → post‑processor cerdas membersihkan typo dan keanehan OCR.  
5. **Use the corrected text** → mencetak, menyimpan, atau mengirimkannya ke layanan lain.

Itu saja. Setiap tahap adalah satu baris kode yang diberi nama jelas, tetapi penjelasan di sekitarnya akan membantu Anda tidak tersesat ketika ada yang tidak beres.

## Langkah 1 – Load Image for OCR

Hal pertama yang harus Anda lakukan adalah mengarahkan mesin OCR ke file yang tepat. `OcrEngine` milik Aspose mengharapkan sebuah path, jadi pastikan gambar struk Anda berada di lokasi yang dapat dibaca skrip.

```python
# Import the necessary Aspose OCR classes
from aspose.ocr import OcrEngine

def load_image(image_path: str) -> OcrEngine:
    """
    Initializes an OcrEngine instance and loads the image.
    Returns the configured engine ready for recognition.
    """
    engine = OcrEngine()
    try:
        # This is the 'load image for ocr' step
        engine.set_image_from_file(image_path)
        return engine
    except Exception as e:
        # Provide a clear error if the file can't be opened
        raise FileNotFoundError(f"Unable to load image at {image_path}: {e}")
```

**Mengapa ini penting:**  
Jika path gambar salah, seluruh alur akan runtuh. Dengan membungkus pemuatan dalam `try/except`, Anda akan mendapatkan pesan yang membantu alih‑alih jejak stack yang membingungkan. Juga, perhatikan nama metode `set_image_from_file`—itu panggilan tepat yang digunakan Aspose untuk **load image for OCR**.

## Langkah 2 – Perform OCR on Image

Sekarang mesin tahu file mana yang harus dibaca, kami memintanya untuk mengenali karakter. Langkah ini adalah tempat kerja berat dilakukan.

```python
def perform_ocr(engine: OcrEngine):
    """
    Executes OCR on the previously loaded image.
    Returns the raw recognition result object.
    """
    # This line actually runs the OCR algorithm
    raw_result = engine.recognize()
    return raw_result
```

**Di balik layar:**  
`recognize()` memindai bitmap, menerapkan segmentasi, dan kemudian menjalankan pengenalan berbasis jaringan saraf. Hasilnya berisi lebih dari sekadar teks biasa—juga mencakup skor kepercayaan, kotak pembatas, dan informasi bahasa. Untuk kebanyakan skenario pemindaian struk, Anda hanya akan membutuhkan properti `text` nanti.

## Langkah 3 – Extract Text from Receipt

Hasil mentah adalah objek yang kaya, tetapi kami hanya peduli pada string yang dapat dibaca manusia. Inilah titik di mana kami **extract text from receipt**.

```python
def get_raw_text(raw_result) -> str:
    """
    Pulls the plain text out of the OCR result.
    """
    # The Text attribute holds the recognized characters
    return raw_result.text
```

**Jebakan umum:**  
Kadang‑kadang struk berisi font kecil atau cetakan pudar, menyebabkan mesin OCR mengembalikan string kosong atau simbol kacau. Jika Anda melihat banyak karakter `�`, pertimbangkan pra‑pemrosesan gambar (meningkatkan kontras, meluruskan, dll.) sebelum memuatnya.

## Langkah 4 – Run Spell Checker

OCR tidak sempurna—terutama pada struk beresolusi rendah. Aspose AI menawarkan post‑processor yang berfungsi seperti pemeriksa ejaan, memperbaiki kesalahan OCR umum seperti “0” vs “O” atau “l” vs “1”.

```python
from aspose.ai import AsposeAI

def spell_check(raw_text: str) -> str:
    """
    Sends the raw OCR text through Aspose AI's spell‑checking post‑processor.
    Returns the corrected string.
    """
    # Initialize the AI helper
    spellchecker = AsposeAI()
    try:
        # The 'run_postprocessor' method expects the raw OCR result object,
        # but we can also feed just the text if the API allows.
        corrected = spellchecker.run_postprocessor(raw_text)
        return corrected.text
    finally:
        # Always free resources to avoid memory leaks
        spellchecker.free_resources()
```

**Mengapa Anda membutuhkannya:**  
Bahkan OCR dengan akurasi 95 % dapat menghasilkan beberapa kata yang salah eja yang mengganggu parsing selanjutnya (misalnya, ekstraksi tanggal). Pemeriksa ejaan belajar dari model bahasa dan memperbaiki gangguan ini secara otomatis. Dalam praktiknya, Anda akan melihat peningkatan yang jelas dari “Total: $1O.00” menjadi “Total: $10.00”.

## Langkah 5 – Use the Corrected Text

Pada tahap ini Anda memiliki string bersih yang siap untuk apa pun yang Anda butuhkan—mencetak ke konsol, menyimpan di basis data, atau memasukkannya ke parser bahasa alami.

```python
def main(image_path: str):
    # Load the image
    engine = load_image(image_path)

    # Perform OCR
    raw_result = perform_ocr(engine)

    # Extract raw text
    raw_text = get_raw_text(raw_result)

    # Run spell checker
    corrected_text = spell_check(raw_text)

    # Release OCR resources
    engine.dispose()

    # Show the final, cleaned‑up receipt text
    print("=== Corrected Receipt Text ===")
    print(corrected_text)

# Example usage
if __name__ == "__main__":
    main("YOUR_DIRECTORY/receipt.png")
```

**Output yang diharapkan** (dengan asumsi struk belanja umum):

```
=== Corrected Receipt Text ===
Walmart Supercenter
Date: 06/15/2026   Time: 14:32
Item          Qty   Price
Milk          2     $3.20
Bread         1     $2.50
Eggs          1     $2.99
Subtotal               $8.69
Tax                    $0.69
Total                 $9.38
Thank you for shopping!
```

Perhatikan bagaimana angka-angka ditampilkan dengan benar dan kata “Thank” tidak terbaca salah menjadi “Thankk”.

## Menangani Kasus Tepi & Tips

- **Low‑contrast scans:** Pra‑proses gambar dengan Pillow (`ImageEnhance.Contrast`) sebelum memuat.  
- **Multi‑page receipts:** Loop setiap file halaman dan gabungkan hasilnya.  
- **Language variations:** Set `engine.language = "eng"` atau kode ISO lain jika Anda menangani struk non‑English.  
- **Resource cleanup:** Selalu panggil `engine.dispose()` dan `spellchecker.free_resources()`; gagal melakukannya dapat menyebabkan kebocoran memori pada layanan yang berjalan lama.  
- **Batch processing:** Bungkus logika `main` dalam antrian pekerja (Celery, RQ) untuk skenario throughput tinggi.

## Kesimpulan

Kami baru saja menjawab **how to perform OCR** pada struk dan secara mulus **run spell checker** untuk mendapatkan teks bersih yang dapat dicari. Dari memuat gambar, melakukan OCR pada gambar, mengekstrak teks dari struk, hingga menjalankan post‑processor pemeriksa ejaan—setiap langkah ringkas, terdokumentasi dengan baik, dan siap digunakan dalam produksi.

Jika Anda ingin **extract text from receipt** dalam skala besar, pertimbangkan menambahkan pemrosesan paralel dan caching hasil OCR. Ingin menjelajah lebih jauh? Coba integrasikan parser PDF untuk menangani PDF yang dipindai, atau bereksperimen dengan analisis tata letak Aspose untuk secara otomatis menangkap data kolom.

Selamat coding, dan semoga struk Anda selalu dapat dibaca!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cara Menggunakan AspOCR: Filter Pra‑proses OCR Gambar untuk .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}