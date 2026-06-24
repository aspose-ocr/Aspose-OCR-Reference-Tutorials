---
category: general
date: 2026-06-16
description: Ekstrak teks dari file TIFF menggunakan OCR Python. Pelajari cara mengubah
  TIFF menjadi teks langkah demi langkah, menangani dokumen multi‑halaman dengan mudah.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: id
og_description: Ekstrak teks dari file TIFF dengan Python OCR. Ikuti panduan ini untuk
  mengonversi TIFF menjadi teks, menangani pemindaian multi‑halaman, dan mendapatkan
  hasil yang bersih.
og_title: Ekstrak Teks dari TIFF – Panduan Python Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Ekstrak Teks dari TIFF – Panduan Python Lengkap
url: /id/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari TIFF – Panduan Python Lengkap

Pernah perlu **mengekstrak teks dari TIFF** tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami kendala ini saat menangani arsip yang dipindai atau dokumen lama. Kabar baiknya? Dengan beberapa baris Python Anda dapat **mengonversi TIFF ke teks** dalam sekejap, bahkan ketika file berisi puluhan halaman.

Dalam tutorial ini kita akan membahas contoh dunia nyata: memuat TIFF multi‑halaman, mengatur bahasa OCR ke Prancis, dan mengambil teks yang dikenali dari setiap halaman. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan, memahami mengapa setiap langkah penting, dan tahu cara menyesuaikannya untuk bahasa atau format gambar lain.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- Python 3.8 atau yang lebih baru terpasang.
- Paket `ocr` (atau perpustakaan OCR kompatibel lain yang menyediakan kelas `OcrEngine`). Anda dapat menginstalnya dengan `pip install ocr-lib`—ganti dengan nama paket yang sebenarnya Anda gunakan.
- File TIFF multi‑halaman (misalnya `french-scans.tif`) yang ingin Anda proses.
- Familiaritas dasar dengan scripting Python.

Tidak ada dependensi berat, tidak ada layanan eksternal—hanya Python murni dan mesin OCR.

---

## Langkah 1: Siapkan Mesin OCR untuk **Ekstrak Teks dari TIFF**

Hal pertama yang harus dilakukan—kita memerlukan instance mesin OCR dan memberi tahu bahasa yang akan digunakan. Dalam kasus ini materi sumbernya berbahasa Prancis, jadi kita akan mengatur bahasa tersebut.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Mengapa ini penting:**  
Pengaturan bahasa secara drastis meningkatkan akurasi. Karakter Prancis seperti “é” atau “ç” akan terbaca sebagai simbol generik jika mesin default ke bahasa Inggris. Dengan secara eksplisit memilih Prancis, kita memberi mesin peta karakter yang tepat.

> **Tip pro:** Jika Anda memproses dokumen dalam beberapa bahasa, Anda dapat mengubah `engine.language` secara dinamis sebelum setiap pemanggilan `recognize()`.

---

## Langkah 2: Muat TIFF Multi‑Halaman yang Ingin Anda **Konversi TIFF ke Teks**

Sebuah TIFF dapat menyimpan beberapa frame—anggap setiap frame sebagai halaman terpisah. Perpustakaan OCR mengabstraksikannya untuk kita, jadi kita cukup menunjuk ke file tersebut.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Peringatan kasus tepi:**  
Jika jalur file salah atau TIFF rusak, metode `load_from_file` akan melemparkan pengecualian. Bungkus dengan blok `try/except` untuk kode produksi:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Langkah 3: Jalankan OCR pada Seluruh Dokumen – Inti dari **Ekstrak Teks dari TIFF**

Sekarang biarkan mesin melakukan magisnya. Pemanggilan `recognize()` memproses setiap halaman sekaligus dan mengembalikan objek hasil yang kaya.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Apa yang terjadi di balik layar?**  
Mesin menelusuri setiap frame, menerapkan pra‑pemrosesan (penyelarasan, binarisasi), menjalankan jaringan saraf, dan mengagregasi output. Karena kita memanggil `recognize()` hanya sekali, perpustakaan dapat berbagi sumber daya antar halaman, yang lebih cepat daripada melakukan loop manual.

---

## Langkah 4: Ambil Teks yang Diakui dari Hasil JSON – **Konversi TIFF ke Teks** Halaman per Halaman

Objek hasil dapat diserialisasi ke JSON. Di dalam JSON tersebut Anda akan menemukan array `pages`, masing‑masing berisi field `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Sekarang kita memiliki daftar Python bersih di mana setiap elemen berkorespondensi dengan output OCR sebuah halaman.

---

## Langkah 5: Cetak atau Simpan Teks untuk Setiap Halaman – Potongan Akhir dari **Ekstrak Teks dari TIFF**

Mari kita loop melalui halaman‑halaman dan menampilkan teks yang diekstrak. Anda juga dapat menulis setiap halaman ke file `.txt` terpisah jika lebih suka.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Output yang Diharapkan (contoh)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Jika OCR berhasil, Anda akan melihat blok kalimat Prancis yang bersih untuk setiap halaman. Jika Anda melihat karakter kacau, periksa kembali pengaturan bahasa atau pertimbangkan meningkatkan resolusi gambar sebelum OCR.

---

## Menangani Masalah Umum Saat Anda **Mengonversi TIFF ke Teks**

| Masalah | Mengapa Terjadi | Solusi Cepat |
|-------|----------------|-----------|
| **Array `pages` kosong** | TIFF tidak dimuat dengan benar atau tidak memiliki frame. | Verifikasi jalur file dan pastikan TIFF bukan PNG satu‑halaman yang disamarkan sebagai TIFF. |
| **Karakter sampah** | Bahasa tidak cocok atau kualitas gambar rendah. | Atur `engine.language` yang tepat dan pra‑proses gambar (misalnya, tingkatkan DPI). |
| **Memori melambung pada TIFF besar** | Memuat semua halaman sekaligus mengonsumsi RAM. | Proses secara bertahap: muat satu frame, kenali, lalu buang sebelum melanjutkan ke berikutnya. |
| **Kesalahan Unicode saat mencetak** | Encoding konsol tidak mendukung karakter aksen. | Gunakan `print(page["text"].encode('utf-8').decode('utf-8'))` atau konfigurasikan terminal Anda untuk UTF‑8. |

---

## Memperluas Skrip: Dari **Ekstrak Teks dari TIFF** ke Pemrosesan Batch

Setelah Anda memiliki fondasi yang kuat, pertimbangkan langkah selanjutnya berikut:

1. **Konversi batch** – Bungkus seluruh alur dalam fungsi `def ocr_tiff(path):` dan iterasi melalui direktori berisi file TIFF.
2. **Output ke file** – Alih-alih mencetak, tulis teks tiap halaman ke `page_{i}.txt` atau gabungkan semuanya ke dalam satu dokumen.
3. **Mesin OCR alternatif** – Jika Anda membutuhkan akurasi lebih tinggi, ganti `ocr.OcrEngine()` dengan Tesseract (`pytesseract`) atau Azure Cognitive Services—tetap gunakan logika “ekstrak teks dari TIFF” yang sama.
4. **Pasca‑pemrosesan** – Jalankan pemeriksaan ejaan, deteksi bahasa, atau pembersihan regex untuk merapikan output OCR mentah.

---

## Skrip Lengkap, Siap‑Jalankan

Berikut adalah kode lengkap, siap untuk disalin‑tempel. Skrip ini mencakup penanganan kesalahan dasar dan penyimpanan opsional teks tiap halaman ke file terpisah.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Jalankan skrip ini, arahkan `tiff_file` ke dokumen Anda, dan saksikan konsol terisi dengan kalimat Prancis yang bersih. Jika Anda menyediakan `out_folder`, Anda juga akan menemukan serangkaian file `page_#.txt` siap untuk diproses lebih lanjut.

---

## Kesimpulan

Kita baru saja **mengekstrak teks dari file TIFF** menggunakan alur kerja OCR Python yang sederhana, dan kini Anda tahu cara **mengonversi TIFF ke teks** secara andal. Dari menginisialisasi mesin dengan bahasa yang tepat hingga melintasi hasil JSON tiap halaman, setiap langkah dijelaskan beserta “mengapa” di baliknya, sehingga Anda dapat menyesuaikan pola ini untuk bahasa lain, format gambar lain, atau pekerjaan batch yang lebih besar.

Apa selanjutnya? Coba ganti backend OCR dengan Tesseract, bereksperimen dengan paket bahasa yang berbeda, atau integrasikan output ke basis data yang dapat dicari. Langit adalah batasnya ketika Anda dapat mengubah gambar yang dipindai menjadi teks yang dapat dicari.

Silakan tinggalkan komentar jika Anda menemukan kendala atau memiliki ide untuk peningkatan lebih lanjut. Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}