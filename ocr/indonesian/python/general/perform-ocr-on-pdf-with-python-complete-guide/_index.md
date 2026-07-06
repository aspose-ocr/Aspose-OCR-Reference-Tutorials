---
category: general
date: 2026-06-25
description: Lakukan OCR pada PDF menggunakan Python—pelajari cara memuat PDF untuk
  OCR, mengekstrak teks dari halaman PDF, dan meninjau teks yang dikenali secara efisien.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: id
og_description: Lakukan OCR pada PDF dengan Python. Panduan ini menunjukkan cara memuat
  PDF untuk OCR, mengekstrak teks dari halaman PDF, dan meninjau teks yang dikenali
  dengan cepat.
og_title: Lakukan OCR pada PDF dengan Python – Tutorial Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Lakukan OCR pada PDF dengan Python – Panduan Lengkap
url: /id/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada PDF dengan Python – Panduan Lengkap

Pernah perlu **melakukan OCR pada PDF** tetapi tidak yakin harus mulai dari mana? Mungkin Anda memiliki tumpukan kontrak yang dipindai, atau satu buku panduan tebal yang menolak bekerja dengan pengekstrak teks biasa Anda. Singkatnya, Anda ingin **memuat PDF untuk OCR**, mengambil teksnya, dan mendapatkan pratinjau cepat—semua tanpa menghabiskan memori mesin Anda.

Nah, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan membahas skrip Python yang berfungsi penuh yang **mengekstrak teks dari halaman PDF**, menunjukkan cara **meninjau teks yang dikenali**, dan bahkan menangani masalah klasik **bagaimana OCR PDF besar** secara efisien.

Pada akhir tutorial Anda akan memiliki program siap‑jalankan, pemahaman jelas tentang setiap pengaturan, dan beberapa tips untuk menghindari jebakan umum yang sering membuat pemula tersandung.

---

## Apa yang Akan Anda Pelajari

- Cara **memuat PDF untuk OCR** menggunakan pustaka `aocr`.
- Langkah‑langkah tepat untuk **melakukan OCR pada PDF** halaman demi halaman.
- Cara **mengekstrak teks dari halaman PDF** sambil menjaga penggunaan memori tetap terkendali.
- Cara **meninjau teks yang dikenali** untuk memeriksa hasil secara cepat.
- Strategi menangani **PDF besar** tanpa menghabiskan RAM.

> **Tip:** Panduan ini mengasumsikan Anda telah menginstal Python 3.9+ dan memiliki pemahaman dasar tentang lingkungan virtual. Jika Anda baru mengenal Python, siapkan virtualenv terlebih dahulu—percaya saya, ini menghemat banyak sakit kepala nantinya.

---

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Paket Python `aocr` (atau mesin OCR kompatibel lainnya) | Menyediakan kelas `OcrEngine` yang digunakan di seluruh skrip. |
| `pip` dan lingkungan virtual | Menjaga dependensi terisolasi dari Python sistem Anda. |
| Ruang disk yang cukup untuk ekstrak gambar sementara | Beberapa mesin OCR menulis gambar halaman ke disk sebelum diproses. |
| Opsional: `tqdm` untuk bilah progres | Meningkatkan pengalaman pengguna saat menangani **bagaimana OCR PDF besar**. |

Instal kebutuhan dasar dengan:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Jika PDF Anda dilindungi kata sandi, Anda harus menyediakan kata sandi tersebut nanti—lihat bagian “Kasus Khusus”.

---

## Langkah 1: Lakukan OCR pada PDF – Menyiapkan Mesin OCR

Langkah pertama, kita perlu membuat instance mesin OCR. Anggap saja ini sebagai otak yang akan membaca gambar tiap halaman dan menghasilkan teks biasa.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **Mengapa mengatur `max_memory_mb`?**  
> Mesin OCR sering menyimpan gambar halaman di RAM. Dengan membatasi memori, Anda mencegah skrip crash pada kontrak 500 halaman.

---

## Langkah 2: Memuat PDF untuk OCR dan Mengonfigurasi Pengaturan

Sekarang kita benar‑benar **memuat PDF untuk OCR**. Path dapat berupa absolut atau relatif; pastikan file tersebut ada.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Jika PDF terenkripsi, `engine.load_pdf` biasanya akan melemparkan pengecualian. Dalam kasus itu Anda dapat memanggil `engine.load_pdf(pdf_path, password="secret")`—lebih lanjut nanti.

---

## Langkah 3: Mengekstrak Teks dari Halaman PDF – Loop Inti

Di sinilah kita **melakukan OCR pada PDF** halaman demi halaman. Kami juga akan **meninjau teks yang dikenali** untuk beberapa ratus karakter pertama agar Anda dapat memverifikasi semuanya berjalan baik.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Pro tip:** Bilah progres `tqdm` memberi Anda isyarat visual, sangat berguna saat menangani **bagaimana OCR PDF besar** yang memerlukan menit untuk diproses.

---

## Langkah 4: Menggabungkan Semua – Skrip Siap‑Jalankan

Berikut contoh lengkap yang dapat dijalankan. Simpan sebagai `pdf_ocr.py` dan jalankan dengan `python pdf_ocr.py path/to/your/file.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Output yang Diharapkan (kutipan)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Anda akan melihat pratinjau singkat untuk tiap halaman, diikuti dengan konfirmasi akhir bahwa file teks yang digabungkan telah ditulis.

---

## Kasus Khusus & Tips Praktis

| Situasi | Apa yang Harus Dilakukan |
|---------|--------------------------|
| **PDF terenkripsi** | Berikan kata sandi: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **PDF sangat besar (> 1000 halaman)** | Tingkatkan `max_memory_mb` dengan hati‑hati, atau proses dalam potongan (misalnya 200 halaman sekaligus). |
| **Konten campuran (cetak + tulisan tangan)** | Ganti `engine.recognition_mode` menjadi `aocr.RecognitionMode.MIXED` jika pustaka mendukungnya. |
| **Font hilang atau kualitas scan buruk** | Pra‑proses halaman dengan pustaka peningkatan gambar (mis., Pillow) sebelum memanggil `recognize()`. |
| **Crash karena kehabisan memori** | Kurangi `preview_len` atau tulis teks tiap halaman langsung ke disk alih‑alih menyimpannya semua dalam list. |

---

## Cara OCR PDF Besar Secara Efisien – Strategi Lanjutan

Saat menangani **bagaimana OCR PDF besar**, kecepatan dan stabilitas menjadi krusial. Berikut beberapa trik yang dapat Anda tambahkan ke skrip:

1. **Paralelisasi per halaman** – Gunakan `concurrent.futures.ThreadPoolExecutor` jika mesin OCR aman untuk thread.
2. **Cache gambar menengah** – Beberapa mesin memungkinkan Anda menyimpan halaman raster ke SSD, secara dramatis mengurangi beban CPU pada pemrosesan ulang.
3. **Tulis output secara batch** – Alih‑alih menambahkan ke list Python, buka file output sekali dan tulis teks tiap halaman segera setelah siap.
4. **Sesuaikan DPI** – Menurunkan DPI saat rasterisasi mengurangi memori tetapi dapat memengaruhi akurasi; temukan titik optimal (biasanya 200‑300 DPI).

Berikut cuplikan singkat yang menunjukkan cara memparalelkan langkah OCR (opsional, hapus komentar untuk menggunakannya):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Ingat: paralelisme dapat meningkatkan penggunaan CPU, jadi pantau suhu sistem Anda pada proses yang lama.

---

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menggunakan skrip ini dengan pustaka OCR lain seperti Tesseract?**  
J: Tentu saja. Ganti pemanggilan `aocr` dengan `pytesseract.image_to

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cara Mengekstrak Teks Gambar dari Stream Menggunakan Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Cara mengekstrak teks dari gambar dari URL menggunakan Aspose.OCR untuk Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}