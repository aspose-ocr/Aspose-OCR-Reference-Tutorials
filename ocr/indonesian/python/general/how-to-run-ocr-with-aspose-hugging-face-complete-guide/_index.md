---
category: general
date: 2026-04-29
description: Pelajari cara menjalankan OCR pada pemindaian Anda, gunakan model Hugging
  Face secara otomatis, dan kenali teks dari pemindaian dengan Aspose OCR dalam hitungan
  menit.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: id
og_description: Cara menjalankan OCR pada pemindaian menggunakan Aspose OCR, secara
  otomatis mengunduh model Hugging Face, dan mendapatkan teks yang bersih serta berpunctuation.
og_title: Cara Menjalankan OCR dengan Aspose & Hugging Face – Panduan Lengkap
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Cara Menjalankan OCR dengan Aspose & Hugging Face – Panduan Lengkap
url: /id/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR dengan Aspose & Hugging Face – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara menjalankan OCR** pada tumpukan dokumen yang dipindai tanpa menghabiskan berjam-jam mengatur pengaturan? Anda tidak sendirian. Dalam banyak proyek, pengembang perlu **mengenali teks dari pemindaian** dengan cepat, namun mereka terhambat oleh unduhan model dan proses pasca‑pemrosesan.  

Kabar baik: tutorial ini menunjukkan solusi siap‑jalankan yang **menggunakan model Hugging Face**, secara otomatis mengunduhnya, dan menambahkan tanda baca sehingga outputnya terbaca seperti ditulis manusia. Pada akhir tutorial, Anda akan memiliki skrip yang memproses setiap gambar dalam sebuah folder dan menaruh file `.txt` bersih di samping setiap pemindaian.

## Apa yang Anda Butuhkan

- Python 3.8+ (kode menggunakan f‑strings, jadi versi yang lebih lama tidak akan cukup)
- `aspose-ocr` package (pasang via `pip install aspose-ocr`)
- Akses internet untuk unduhan model pertama kali  
- Folder berisi pemindaian gambar (`.png`, `.jpg`, atau `.tif`)

Itu saja—tidak ada binari tambahan, tidak ada penyesuaian model manual. Mari kita mulai.

![contoh cara menjalankan OCR](https://example.com/ocr-demo.png "contoh cara menjalankan OCR")

## Langkah 1: Impor Kelas Aspose OCR & Siapkan Lingkungan

Kita mulai dengan mengambil kelas yang diperlukan dari pustaka Aspose OCR. Mengimpor semuanya di awal membuat skrip rapi dan memudahkan menemukan ketergantungan yang hilang.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*Mengapa ini penting*: `OcrEngine` melakukan pekerjaan berat, sementara `AsposeAI` memungkinkan kita menyambungkan model bahasa besar untuk post‑processing yang lebih cerdas. Jika Anda melewatkan impor, sisa kode tidak akan dapat dikompilasi—jadi jangan lupa.

## Langkah 2: Konfigurasikan Model Hugging Face yang Sadar GPU  

Sekarang kita memberi tahu Aspose dari mana mengambil model dan berapa banyak lapisan yang harus dijalankan di GPU. Flag `allow_auto_download="true"` melakukan bagian **mengunduh model secara otomatis** untuk Anda.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **Tip pro**: Jika Anda tidak memiliki GPU, setel `gpu_layers=0`. Model akan beralih ke CPU, yang lebih lambat tetapi tetap berfungsi.

### Mengapa Memilih Model Hugging Face?

Hugging Face menyimpan koleksi besar LLM siap‑pakai. Dengan menunjuk ke `Qwen/Qwen2.5-3B-Instruct-GGUF`, Anda mendapatkan model yang kompak dan disetel instruksi yang dapat menambahkan tanda baca, memperbaiki spasi, dan bahkan memperbaiki kesalahan OCR minor. Inilah esensi **menggunakan model hugging face** dalam praktik.

## Langkah 3: Inisialisasi Mesin AI dan Aktifkan Post‑Processing Tanda Baca  

Mesin AI bukan hanya untuk obrolan mewah—di sini kami menambahkan *penambah tanda baca* yang membersihkan output OCR mentah.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*Apa yang terjadi?* Panggilan `set_post_processor` mendaftarkan post‑processor bawaan yang dijalankan setelah mesin OCR selesai. Ia mengambil string mentah dan menyisipkan koma, titik, serta huruf kapital di tempat yang tepat, membuat teks akhir jauh lebih mudah dibaca.

## Langkah 4: Buat Mesin OCR dan Lampirkan Mesin AI  

Menghubungkan mesin AI ke mesin OCR memberi kita satu objek yang dapat membaca karakter sekaligus memoles hasilnya.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

Jika Anda melewatkan langkah ini, OCR tetap akan berfungsi, tetapi Anda akan kehilangan peningkatan tanda baca—sehingga output akan terlihat seperti rangkaian kata.

## Langkah 5: Proses Setiap Gambar dalam Folder  

Berikut inti tutorial. Kami melakukan loop pada setiap gambar, menjalankan OCR, menerapkan post‑processor, dan menulis teks yang sudah dibersihkan ke file `.txt` berdampingan.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### Apa yang Diharapkan

Menjalankan skrip akan mencetak sesuatu seperti:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

Setiap baris memberi Anda skor kepercayaan (pemeriksaan cepat) dan membuat `invoice_001.png.txt`, `receipt_2024.tif.txt`, dll., yang berisi teks berpunctuation, dapat dibaca manusia.

### Kasus Pinggir & Variasi

- **Pemindaian non‑Inggris**: Ganti `hugging_face_repo_id` ke model multibahasa (mis., `microsoft/Multilingual-LLM-GGUF`).
- **Batch besar**: Bungkus loop dalam `concurrent.futures.ThreadPoolExecutor` untuk pemrosesan paralel, tetapi perhatikan batas memori GPU.
- **Post‑processing kustom**: Ganti `"punctuation_adder"` dengan skrip Anda sendiri jika Anda memerlukan pembersihan khusus domain (mis., menghapus nomor faktur).

## Langkah 6: Bersihkan Sumber Daya  

Saat pekerjaan selesai, membebaskan sumber daya mencegah kebocoran memori, terutama penting jika Anda menjalankan ini dalam layanan yang berjalan lama.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

Mengabaikan langkah ini dapat meninggalkan memori GPU tergantung, yang akan mengganggu jalannya selanjutnya.

## Ringkasan: Cara Menjalankan OCR End‑to‑End  

Dalam hanya beberapa baris, kami telah menunjukkan **cara menjalankan OCR** pada folder pemindaian, **menggunakan model Hugging Face** yang mengunduh dirinya sendiri pada pertama kali, dan **mengenali teks dari pemindaian** dengan tanda baca yang ditambahkan secara otomatis. Skrip lengkap siap untuk disalin‑tempel, menyesuaikan jalur Anda, dan dijalankan.

## Langkah Selanjutnya & Topik Terkait  

- **Post‑processing batch**: Jelajahi `ocr_engine.run_batch_postprocessor` untuk penanganan massal yang lebih cepat.  
- **Model alternatif**: Coba keluarga `openai/whisper` jika Anda membutuhkan speech‑to‑text bersamaan dengan OCR.  
- **Integrasi dengan basis data**: Simpan teks yang diekstrak di SQLite atau Elasticsearch untuk arsip yang dapat dicari.  

Rasakan **bebas** untuk bereksperimen—ganti model, ubah `gpu_layers`, atau tambahkan post‑processor Anda sendiri. Fleksibilitas **Aspose OCR** yang digabungkan **dengan hub model Hugging Face** menjadikan ini **dasar yang serbaguna** untuk proyek **digitalisasi dokumen** apa pun.

---

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa dokumentasi Aspose OCR untuk opsi konfigurasi yang lebih mendalam.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}