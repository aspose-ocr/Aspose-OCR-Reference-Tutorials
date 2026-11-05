---
category: general
date: 2026-06-28
description: Cara melakukan OCR batch di Python—mengekstrak teks dari gambar dan mengonversi
  halaman yang dipindai menjadi teks menggunakan pemrosesan OCR batch.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: id
og_description: Pelajari cara melakukan OCR batch di Python, mengekstrak teks dari
  gambar, dan mengonversi halaman yang dipindai menjadi teks dengan pemrosesan OCR
  batch yang efisien.
og_title: Cara Melakukan OCR Batch di Python – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Cara Batch OCR di Python – Panduan Lengkap untuk Mengekstrak Teks dari Gambar
url: /id/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di Python – Panduan Lengkap untuk Mengekstrak Teks dari Gambar

Jika Anda bertanya-tanya **bagaimana melakukan batch OCR di Python**, Anda berada di tempat yang tepat. Tutorial ini menunjukkan cara cepat untuk **mengekstrak teks dari gambar** dan **mengonversi halaman yang dipindai menjadi teks** menggunakan satu instance mesin OCR. Tidak lagi menyalin‑tempel satu file demi satu file—biarkan kode melakukan pekerjaan berat.

Kami akan membahas semua yang Anda perlukan: menginstal pustaka, memuat seluruh folder pemindaian, menjalankan pemrosesan batch OCR, dan menangani hasil dengan elegan. Pada akhir tutorial Anda akan memiliki skrip yang dapat digunakan kembali yang mengubah tumpukan PNG atau JPEG menjadi file teks yang dapat dicari dalam hitungan detik.

## Apa yang Anda Butuhkan

* Python 3.9+ terinstal (kode ini juga berfungsi pada 3.8, tetapi 3.9+ memberikan fitur typing terbaru).
* Sebuah pustaka OCR modern—di sini kami menggunakan **Aspose.OCR for Python via .NET**, yang mengekspos kelas `OcrEngine` seperti yang ditunjukkan dalam cuplikan asli.  
  ```bash
  pip install aspose-ocr
  ```
* Sebuah folder berisi halaman yang dipindai (`page1.png`, `page2.png`, …). Apa pun yang dapat dibuka Pillow akan berfungsi, jadi PDF, TIFF, atau BMP juga dapat digunakan.
* Sedikit rasa ingin tahu—jika Anda belum pernah mengotomatisasi image‑to‑text sebelumnya, Anda akan segera melihat mengapa batch OCR menjadi pengubah permainan.

> **Pro tip:** Jika Anda lebih suka pustaka murni Python, ganti `OcrEngine` dengan `pytesseract.image_to_string`. Logika di sekitarnya tetap sama.

## Cara Batch OCR di Python – Panduan Langkah‑per‑Langkah

Berikut adalah skrip lengkap yang dapat dijalankan. Setiap baris diberi komentar sehingga Anda dapat melihat *mengapa* setiap bagian penting, bukan hanya *apa* yang dilakukannya.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Output yang Diharapkan

Menjalankan skrip terhadap folder dengan tiga pemindaian PNG menghasilkan sesuatu seperti:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

Pratinjau menampilkan 200 karakter pertama dari setiap halaman, dan teks lengkap berada di direktori `ocr_output`.

## Mengekstrak Teks dari Gambar Menggunakan Satu Engine

Mengapa kita membuat **satu** `OcrEngine` dan menggunakannya kembali? Menginstansiasi engine dapat mahal karena memuat paket bahasa dan DLL native. Dengan berbagi instance yang sama di seluruh batch, Anda:

* **Menghemat memori** – hanya satu set sumber daya yang berada di RAM.
* **Meningkatkan kecepatan** – engine tetap hangat, menghindari inisialisasi berulang.
* **Menjaga konsistensi** – pengaturan pengenalan yang sama diterapkan pada setiap halaman, yang penting ketika Anda ingin **mengekstrak teks dari gambar** yang memiliki tata letak serupa.

Jika Anda perlu menyesuaikan pengenalan (mis., mengaktifkan pemeriksaan ejaan atau mengubah bahasa), lakukan itu *sebelum* memanggil `recognize_batch`. Semua halaman berikutnya akan mewarisi pengaturan tersebut secara otomatis.

## Mengonversi Halaman yang Dipindai menjadi Teks secara Efisien

Inti permasalahan—**mengonversi halaman yang dipindai menjadi teks**—diselesaikan oleh `engine.recognize_batch(images)`. Di balik layar pustaka memproses setiap gambar dalam pool thread latar belakang, sehingga Anda mendapatkan skala hampir linear pada mesin multi‑core. Beberapa hal yang perlu diingat:

* **Kualitas gambar penting** – 300 dpi atau lebih menghasilkan hasil terbaik. Jika pemindaian Anda beresolusi rendah, pertimbangkan up‑sampling dengan Pillow sebelum memberi ke engine.
* **Warna vs. grayscale** – mesin OCR biasanya bekerja lebih cepat pada grayscale 8‑bit. Anda dapat menambahkan langkah pra‑pemrosesan:
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Dukungan bahasa** – Aspose.OCR mendukung lebih dari 40 bahasa. Atur `engine.language = "eng"` atau `"fra"` sebelum pemanggilan batch jika Anda tidak bekerja dengan bahasa Inggris.

## Praktik Terbaik Pemrosesan Batch OCR

Meskipun kode di atas sudah singkat, batch OCR tingkat produksi sering memerlukan beberapa langkah pengamanan tambahan:

| Masalah | Pendekatan yang Disarankan |
|---------|----------------------------|
| **Batch besar ( > 500 file )** | Bagi menjadi potongan 100–200 gambar untuk menjaga jejak memori tetap kecil. |
| **File rusak atau tidak didukung** | Helper `load_images` sudah menangkap pengecualian dan mencatat peringatan; Anda juga dapat menulis fallback untuk melewatkan atau memindahkan file yang buruk. |
| **Pemantauan progres** | Bungkus `recognize_batch` dalam loop yang mengembalikan setelah setiap gambar jika pustaka menyediakan callback per‑gambar. |
| **Pasca‑pemrosesan** | Jalankan pemeriksaan ejaan atau pembersihan regex pada string hasil untuk meningkatkan kemampuan pencarian selanjutnya. |
| **Paralelisme** | Jika Anda memiliki setup multi‑node, distribusikan folder ke pekerja dan gabungkan output `.txt` di akhir. |

Tips ini membantu Anda menskalakan **pemrosesan batch OCR** dari beberapa halaman menjadi ribuan tanpa membuat skrip Anda crash.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan ini langsung dengan PDF?**  
A: Tentu saja. Konversi setiap halaman PDF menjadi gambar terlebih dahulu (mis., menggunakan `pdf2image`) dan berikan daftar hasilnya ke `recognize_batch`. Sisa pipeline tetap tidak berubah.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Ekstrak Teks dari Gambar Menggunakan Operasi OCR pada Folder](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Cara Mengekstrak Teks dari Arsip ZIP Menggunakan Aspose.OCR untuk .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}