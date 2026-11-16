---
category: general
date: 2026-06-22
description: Tutorial python batch OCR yang menunjukkan cara menjalankan OCR multithread
  pada folder gambar PNG menggunakan Tesseract dan pathlib. Pelajari OCR gambar batch
  cepat dengan Python.
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: id
og_description: Tutorial batch OCR Python membimbing Anda melalui skrip lengkap yang
  dapat dijalankan, yang memproses banyak PNG dengan Tesseract menggunakan beberapa
  thread.
og_title: Tutorial OCR Batch Python – OCR Multithreaded Cepat untuk Gambar PNG
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'Tutorial OCR batch Python: Memproses Banyak PNG Secara Efisien'
url: /id/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – OCR Multithreaded Cepat untuk Gambar PNG

Pernah bertanya-tanya bagaimana cara **python batch ocr tutorial** melalui ratusan screenshot PNG tanpa membuat CPU Anda meleleh? Anda bukan satu-satunya. Baik Anda mendigitalkan formulir yang dipindai, mengekstrak teks dari kwitansi, atau membangun arsip yang dapat dicari, pipeline batch OCR yang solid menghemat waktu berjam‑jam.

Dalam panduan ini kami akan membuat skrip kecil namun kuat yang mengumpulkan setiap `*.png` dalam sebuah folder, menyerahkannya ke Tesseract melalui prosesor multithreaded, dan menaruh hasil teks biasa ke dalam direktori output yang rapi. Tanpa pustaka misterius—hanya `pathlib`, `concurrent.futures`, dan `pytesseract` yang selalu dapat diandalkan. Pada akhir tutorial Anda akan memiliki **python batch ocr tutorial** yang dapat Anda salin‑tempel ke proyek mana pun.

## Apa yang Akan Anda Pelajari

- Cara mengumpulkan file gambar dengan **pathlib image handling**  
- Menyiapkan **multithreaded OCR in Python** worker pool  
- Menyetel **OCR thread count optimization** untuk inti CPU Anda  
- Menyimpan setiap hasil dengan skema penamaan yang jelas untuk pencarian nanti  
- Menjalankan semuanya sebagai skrip tunggal yang berdiri sendiri  

## Prasyarat (Apa yang Anda Butuhkan)

| Persyaratan | Mengapa Penting |
|-------------|-----------------|
| Python 3.9+ | Sintaks modern (`pathlib`, f‑strings) |
| Tesseract 5.x terinstal dan dapat diakses di `PATH` | Mesin OCR di balik `pytesseract` |
| `pytesseract` (`pip install pytesseract`) | Pembungkus Python untuk Tesseract |
| `Pillow` (`pip install pillow`) | Memuat gambar untuk Tesseract |
| Sebuah folder berisi file PNG yang ingin Anda proses | Target **tesseract OCR batch processing** kami |

> **Tip Pro:** Jika Anda menggunakan Windows, tambahkan `C:\Program Files\Tesseract-OCR` ke `PATH` sistem Anda sehingga `pytesseract` dapat menemukan executable secara otomatis.

---

## Langkah 1 – Kumpulkan Semua Gambar PNG (Menggunakan pathlib)

Hal pertama yang harus dilakukan: kita membutuhkan daftar setiap gambar yang akan diproses OCR. `pathlib` membuat ini menjadi satu baris kode dan menjaga agar kode tetap OS‑agnostic.

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*Mengapa `pathlib`?* Ia mengabstraksi perbedaan antara backslash Windows dan slash Unix, memungkinkan skrip yang sama berjalan di mana saja. Ini adalah landasan **pathlib image handling** dalam tutorial kami.

---

## Langkah 2 – Definisikan Kelas Pemroses Batch OCR Sederhana

Berikut adalah wrapper ringan yang menyembunyikan boilerplate threading. Ia mencerminkan pseudo‑code yang Anda lihat sebelumnya tetapi sepenuhnya fungsional.

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**Penjelasan pilihan utama**

- **ThreadPoolExecutor** memberi kami multithreading sejati untuk tugas I/O‑bound seperti membaca file dan memanggil binary Tesseract eksternal.  
- Metode `set_thread_count` adalah tempat Anda dapat bereksperimen dengan **OCR thread count optimization**; lebih banyak thread biasanya berarti throughput lebih cepat sampai inti CPU Anda jenuh.  
- Setiap gambar menghasilkan file `.txt` yang dinamai sesuai PNG asli—sempurna untuk pengindeksan atau pencarian di kemudian hari.

---

## Langkah 3 – Sambungkan Semua Bersama

Sekarang kita menginstansiasi processor, menyesuaikan jumlah thread, menunjuk ke folder output kami, dan akhirnya memberikan daftar gambar.

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

Menjalankan skrip akan menghasilkan output serupa dengan:

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

Setiap `.txt` berisi output OCR mentah. Buka file apa pun dan Anda akan melihat teks yang diekstrak siap untuk diindeks, analisis sentimen, atau apa pun yang akan datang selanjutnya.

---

## Langkah 4 – Kesalahan Umum & Cara Menghindarinya

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| File `.txt` kosong | Tesseract tidak menemukan data bahasa atau gambar terlalu gelap | Instal paket bahasa (`tesseract-ocr-eng`) dan pra‑proses gambar (tingkatkan kontras). |
| `UnicodeDecodeError` saat membaca hasil | Output mengandung karakter non‑UTF‑8 | Tulis file dengan `encoding="utf-8"` (sudah ada dalam kode) atau gunakan `errors="ignore"` sebagai solusi cepat. |
| Lonjakan CPU, tidak ada peningkatan kecepatan | Jumlah thread melebihi inti fisik | Kurangi `set_thread_count` menjadi `os.cpu_count()` atau lebih rendah. |
| `FileNotFoundError` saat membuka gambar | Path berisi karakter non‑ASCII di Windows | Tambahkan prefix `r` pada string atau gunakan objek `pathlib` langsung (seperti yang kami lakukan). |

---

## Langkah 5 – Memperluas Tutorial (Langkah Selanjutnya)

- **Tambahkan pra‑pemrosesan gambar** dengan OpenCV (`cv2`) untuk meningkatkan akurasi OCR (mis., deskew, threshold).  
- **Paralelisasi lintas mesin** menggunakan `multiprocessing` atau antrian tugas sederhana seperti RabbitMQ untuk beban kerja besar.  
- **Integrasikan dengan mesin pencari** (Elasticsearch) agar teks yang diekstrak dapat dicari secara real‑time.  
- **Ganti Tesseract dengan API OCR cloud** (Google Vision, Azure Computer Vision) jika Anda memerlukan akurasi lebih tinggi pada teks tulisan tangan.

Semua ide ini dibangun di atas fondasi yang kini Anda miliki: **python batch ocr tutorial** yang bersih dan siap pakai.

---

## Kesimpulan

Anda baru saja membangun **python batch ocr tutorial** lengkap yang:

1. **Mengumpulkan** setiap PNG dengan **pathlib image handling**.  
2. **Menyetel** sebuah **multithreaded OCR in Python** worker pool.  
3. **Mengoptimalkan** jumlah thread untuk perangkat keras Anda (**OCR thread count optimization**).  
4. **Menulis** setiap hasil ke folder khusus (**tesseract OCR batch processing**).  

Skrip ini siap dimasukkan ke dalam pipeline apa pun, apakah Anda memproses kwitansi, dokumen hukum, atau gunung screenshot. Mainkan jumlah thread, tambahkan pra‑pemrosesan gambar, atau hubungkan output ke basis data—pilihan ada di tangan Anda.

Ada pertanyaan? Silakan beri komentar di bawah, dan selamat coding!

![Diagram alur tutorial python batch ocr memproses banyak file PNG secara paralel](/images/python-batch-ocr-workflow.png){.center width=600 alt="alur kerja tutorial python batch ocr"}

---


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Tutorial Aspose OCR – Pengenalan Karakter Optik](/ocr/english/)
- [Cara Batch OCR Gambar dengan List di Aspose.OCR untuk .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}