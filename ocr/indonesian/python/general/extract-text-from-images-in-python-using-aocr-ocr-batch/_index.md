---
category: general
date: 2026-06-25
description: Ekstrak teks dari gambar dengan pustaka Python aocr – pelajari OCR batch,
  atur mode pengenalan menjadi cetak, dan tambahkan postprocessor AI.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: id
og_description: Ekstrak teks dari gambar menggunakan pustaka Python aocr. Tutorial
  ini menunjukkan OCR batch, mode pengenalan cetak, dan postprocessor AI opsional.
og_title: Ekstrak Teks dari Gambar dengan Python – Panduan Lengkap Batch aocr
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Ekstrak Teks dari Gambar di Python Menggunakan aocr OCR Batch
url: /id/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Python Menggunakan aocr OCR Batch

Pernah perlu **mengekstrak teks dari gambar** tetapi merasa kewalahan dengan puluhan langkah kecil? Anda tidak sendirian. Baik Anda mendigitalkan formulir yang dipindai, mengambil data dari struk, atau membangun arsip yang dapat dicari, mendapatkan hasil OCR yang handal dalam skala besar bisa terasa seperti mendaki bukit curam.

Kabar baiknya? Dengan **library aocr** Anda dapat membuat **batch OCR Python** lengkap hanya dengan beberapa baris kode. Dalam panduan ini kami akan menunjukkan cara membuat batch OCR, memuat semua gambar yang didukung dari sebuah folder, memilih **mode pengenalan printed** yang tepat, dan bahkan menambahkan **AI postprocessor** untuk meningkatkan akurasi. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang mengekstrak teks dari gambar dan memberi tahu berapa banyak teks yang berhasil diambil per file.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mengimpor paket `aocr`.
- Menyiapkan `OcrBatch` untuk menangani ribuan file secara otomatis.
- Memilih mode pengenalan optimal untuk dokumen tercetak.
- (Opsional) Menyambungkan AI post‑processor untuk membersihkan hasil yang berisik.
- Menampilkan setiap jalur file bersamaan dengan panjang teks yang diekstrak.
- Tips menangani kasus tepi seperti format tidak didukung atau halaman kosong.

### Prasyarat

- Python 3.8 atau lebih baru terpasang di mesin Anda.  
- Familiaritas dasar dengan scripting Python (loop, import, dll.).  
- Akses ke folder berisi gambar hasil pemindaian (PNG, JPG, TIFF, dll.).  

Jika Anda sudah memiliki semua itu, mari mulai—tanpa layanan eksternal diperlukan.

## Langkah 1: Instal Library aocr

Langkah pertama. Paket `aocr` tidak termasuk dalam library standar, jadi Anda harus mengunduhnya dari PyPI.

```bash
pip install aocr
```

> **Pro tip:** Gunakan lingkungan virtual (`python -m venv .venv`) untuk menjaga dependensi tetap terisolasi.  

Setelah terinstal, Anda dapat mengimpor kelas inti.

```python
# core imports
import aocr
```

## Langkah 2: Buat Instance OCR Batch

`OcrBatch` adalah mesin utama yang akan menjelajahi direktori Anda dan melacak setiap file gambar. Anggap saja sebagai konveyor yang mengirimkan gambar ke mesin OCR.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

Pada titik ini batch masih kosong, tetapi kami akan mengisinya pada langkah berikutnya.

## Langkah 3: Tambahkan Semua Gambar yang Didukung dari Folder (Secara Rekursif)

Kemungkinan Anda memiliki struktur folder bersarang—mungkin satu sub‑folder per klien atau per bulan. Metode `add_folder` akan menelusuri pohon tersebut untuk Anda, mengambil setiap gambar yang dapat dibacanya.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Ganti `"YOUR_DIRECTORY/scanned_forms/"` dengan jalur yang sebenarnya di sistem Anda. Setelah pemanggilan ini `ocr_batch.file_paths` berisi daftar nama file absolut, dan batch tahu persis berapa banyak item yang akan diproses.

## Langkah 4: Pilih Mode Pengenalan untuk Teks Tercetak

Mesin `aocr` mendukung beberapa mode (handwritten, printed, mixed). Karena kita berurusan dengan formulir tercetak yang bersih, atur mode sesuai. Bendera kecil ini dapat meningkatkan akurasi secara dramatis karena mesin tidak perlu heuristik berat untuk skrip kursif.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Mengapa penting:** Teks tercetak memiliki baseline dan bentuk karakter yang konsisten, memungkinkan model OCR menerapkan kamus karakter yang lebih ketat. Jika Anda membiarkan mode pada “auto”, Anda mungkin mendapatkan noise tambahan pada pemindaian beresolusi rendah.

## Langkah 5: (Opsional) Tambahkan AI Post‑Processor

Jika hasil pemindaian Anda buram, kontras rendah, atau menggunakan font tidak biasa, AI post‑processor dapat membersihkan output OCR mentah sebelum Anda mengirimkannya ke sistem downstream. Metode `set_ai_postprocessor` mengharapkan objek yang mengimplementasikan antarmuka `process(text: str) -> str`.

Berikut contoh minimal menggunakan kelas fiktif `SimpleCleaner`. Pada praktiknya Anda dapat memasang transformer HuggingFace, model bahasa khusus, atau bahkan pemeriksa ejaan berbasis aturan.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Jika Anda melewatkan langkah ini, batch akan mengembalikan string OCR mentah saja.

## Langkah 6: Jalankan OCR pada Seluruh Batch dan Kumpulkan Hasil

Sekarang pekerjaan berat dimulai. Metode `run` akan melintasi setiap file, menjalankan mesin OCR, melewatkan output melalui AI post‑processor (jika ada), dan mengembalikan daftar string—satu per gambar.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Karena metode ini mengembalikan list Python biasa, Anda dapat memperlakukannya seperti koleksi lain—menyimpannya, menulis ke CSV, atau memasukkannya ke database.

## Langkah 7: Tampilkan Setiap Jalur File dengan Panjang Teks yang Diekstrak

Pengecekan cepat adalah mencetak berapa banyak karakter yang diekstrak dari setiap file. Jika sebuah halaman kosong atau OCR gagal, Anda akan melihat panjang `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Output tipikal terlihat seperti:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Melihat flag `0` secara langsung memberi tahu file mana yang perlu diperiksa kembali (mungkin rusak atau bukan gambar sama sekali).

## Menangani Kasus Tepi Umum

### 1. Tipe File Tidak Didukung

`aocr` secara diam-diam melewati file yang tidak dapat didekode. Jika Anda curiga ada PDF atau BMP yang tercampur, filter terlebih dahulu:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Batch Besar dan Konsumsi Memori

Menjalankan ribuan pemindaian beresolusi tinggi dapat meningkatkan penggunaan memori. Kurangi dampaknya dengan memproses dalam potongan:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Halaman Kosong atau Kontras Rendah

Jika sebuah halaman menghasilkan kurang dari 10 karakter, Anda mungkin ingin menandainya untuk review manual:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip yang dapat Anda salin‑tempel dan jalankan langsung. Simpan sebagai `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Output yang diharapkan** (dipotong untuk singkat):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Jalankan dengan:

```bash
python batch_ocr.py
```

Jika semuanya sudah diatur dengan benar, Anda akan melihat satu baris untuk setiap gambar, masing‑masing melaporkan jumlah karakter teks yang diekstrak.

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja pada PDF?**  
J: Tidak secara langsung. `aocr` hanya menangani gambar raster. Konversi PDF ke PNG/TIFF terlebih dahulu (misalnya dengan `pdf2image`).

**T: Bisakah saya mengubah mode pengenalan ke handwritten?**  
J: Tentu—ganti saja `aocr.RecognitionMode.PRINTED` dengan `aocr.RecognitionMode.HANDWRITTEN`. Expect waktu proses yang lebih lama namun hasil lebih baik pada catatan kursif.

**T: Bagaimana jika saya membutuhkan dukungan multibahasa?**  
J: Library ini dilengkapi paket bahasa. Instal modul bahasa yang diinginkan (`pip install aocr-lang-fr` untuk bahasa Prancis, dll.) dan set `ocr_batch.language = "fr"` sebelum menjalankan.

## Langkah Selanjutnya dan Topik Terkait

- **Pemrosesan paralel:** Bungkus eksekusi batch dalam `concurrent.futures.ThreadPoolExecutor` untuk memanfaatkan banyak core CPU.  
- **Menyimpan hasil:** Tulis `ocr_results` ke CSV atau database SQLite untuk analitik downstream.  
- **Integrasi dengan AI cloud:** Ganti `SimpleCleaner` dengan model transformer dari HuggingFace untuk koreksi ejaan mutakhir.  
- **Fine‑tuning aocr:** Jika Anda memiliki set font khusus, jelajahi `aocr.Trainer` untuk meningkatkan akurasi mode printed.

---

Itu saja—Anda kini memiliki dasar yang kuat


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang berhubungan erat dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}