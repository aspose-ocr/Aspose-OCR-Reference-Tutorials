---
category: general
date: 2026-09-22
description: Pelajari cara menjalankan OCR pada gambar menggunakan Aspose OCR, mengonfigurasi
  model OCR, mengekstrak teks dari faktur, dan meningkatkan akurasi OCR dalam Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from invoice
- improve OCR accuracy
- configure OCR model
language: id
lastmod: 2026-09-22
og_description: Jalankan OCR pada gambar dengan Aspose OCR, konfigurasikan model OCR,
  ekstrak teks dari faktur, dan tingkatkan akurasi OCR dalam tutorial lengkap langkah
  demi langkah.
og_image_alt: Screenshot showing raw OCR and AI‑enhanced text extracted from an invoice
  image
og_title: Jalankan OCR pada gambar dengan Aspose OCR – panduan lengkap Python
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to run OCR on image using Aspose OCR, configure the OCR model,
    extract text from invoice and improve OCR accuracy in Python.
  headline: How to run OCR on image with Aspose OCR and boost accuracy
  type: TechArticle
tags:
- Aspose OCR
- Python
- AI post‑processing
title: Cara menjalankan OCR pada gambar dengan Aspose OCR dan meningkatkan akurasi
url: /id/python/general/how-to-run-ocr-on-image-with-aspose-ocr-and-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menjalankan OCR pada gambar dengan Aspose OCR dan meningkatkan akurasi

Jika Anda perlu **menjalankan OCR pada gambar** file di Python, panduan ini menunjukkan alur kerja lengkap yang siap produksi. Anda akan melihat cara mengonfigurasi model OCR, mengekstrak teks dari foto faktur, dan meningkatkan akurasi OCR dengan post‑processor AI Aspose.

Memproses faktur yang dipindai adalah titik sakit yang umum—OCR mentah sering menghasilkan kata yang salah eja atau angka yang terputus. Pada akhir tutorial ini Anda akan memiliki skrip siap‑jalankan yang menghasilkan ekstraksi teks yang lebih bersih dan dapat diandalkan, serta Anda akan memahami mengapa setiap langkah konfigurasi penting.

## Prasyarat

* Python 3.8 atau yang lebih baru terpasang.
* Lisensi Aspose OCR yang aktif (versi percobaan gratis dapat digunakan untuk evaluasi).
* Gambar contoh faktur (misalnya `sample_invoice.png`) ditempatkan di direktori yang diketahui.
* Familiaritas dasar dengan pemasangan paket Python.

Tidak ada dependensi tingkat sistem tambahan yang diperlukan; SDK menangani pengunduhan model secara otomatis.

## Langkah 1: Instal paket Aspose OCR

Hal pertama yang harus Anda lakukan adalah menambahkan pustaka Aspose OCR ke lingkungan Anda. Paket ini menyertakan model AI dan post‑processor yang akan Anda perlukan nanti.

```bash
pip install aspose-ocr
```

Menjalankan perintah ini menginstal `asposeocr`, yang menyediakan kelas `AsposeAI` yang digunakan untuk **mengonfigurasi model OCR** seperti pengunduhan otomatis dan eksekusi hanya CPU.

## Langkah 2: Konfigurasikan model OCR (opsional tetapi disarankan)

Penyetelan halus model meningkatkan kecepatan dan akurasi, terutama ketika Anda menjalankan OCR pada gambar faktur yang mengandung banyak angka dan karakter khusus. Kode berikut menunjukkan pengaturan yang paling berguna:

```python
import asposeocr as ocr   # import the Aspose OCR package

# Create an AsposeAI instance with default logging
ai = ocr.AsposeAI()

# Enable automatic model download, force CPU execution, and enlarge the context window
ai.allow_auto_download = "true"   # download missing model files automatically
ai.gpu_layers = 0                 # use CPU only – avoids GPU‑related errors on most machines
ai.context_size = 2048           # larger context improves correction quality
```

*Mengapa flag ini?*  
* `allow_auto_download` memastikan model OCR tersedia bahkan pada mesin baru.  
* `gpu_layers = 0` menghilangkan kebutuhan akan GPU yang kompatibel dengan CUDA, yang tidak dimiliki banyak pengembang.  
* `context_size` mengontrol berapa banyak token di sekitarnya yang dipertimbangkan AI saat memperbaiki kesalahan; jendela yang lebih besar sering **meningkatkan akurasi OCR** pada teks padat seperti faktur.

## Langkah 3: Inisialisasi mesin AI

Inisialisasi memvalidasi bahwa file model siap dan memuatnya ke memori. Melewatkan langkah ini dapat menyebabkan kesalahan runtime saat Anda memanggil post‑processor nanti.

```python
# Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")
```

Jika mesin gagal, pengecualian akan memberi tahu Anda tepat di mana masalah terjadi, menghemat waktu debugging.

## Langkah 4: Jalankan mesin OCR standar pada gambar

Sekarang Anda dapat **menjalankan OCR pada gambar** file. Kelas `OcrEngine` melakukan ekstraksi teks mentah tanpa koreksi berbasis AI.

```python
# Path to the invoice image you want to process
image_path = "YOUR_DIRECTORY/sample_invoice.png"

# Perform raw OCR
ocr_result = ocr.OcrEngine().recognize_image(image_path)
```

`ocr_result.text` berisi string polos yang dikenali oleh mesin OCR. Untuk faktur tipikal, Anda mungkin melihat digit yang hilang, tanda baca yang salah tempat, atau kata yang terputus.

## Langkah 5: Terapkan post‑processor AI untuk meningkatkan akurasi OCR

Post‑processor AI Aspose menganalisis output mentah dan memperbaiki kesalahan OCR umum (mis., “5um” → “Sum”). Menjalankan langkah ini adalah kunci untuk **meningkatkan akurasi OCR** pada dokumen keuangan.

```python
# Apply the AI post‑processor
cleaned_result = ai.run_postprocessor(ocr_result)
```

Post‑processor menggunakan konfigurasi yang Anda tetapkan pada Langkah 2, sehingga `context_size` yang lebih besar berkontribusi pada koreksi yang lebih dapat diandalkan.

## Langkah 6: Ekstrak teks dari faktur dan tampilkan hasil

Pada titik ini Anda memiliki dua versi teks yang diekstrak: output OCR mentah dan versi yang ditingkatkan AI. Mencetak keduanya memungkinkan Anda memverifikasi perbaikan dan juga memberi kesempatan untuk mencatat data asli untuk keperluan audit.

```python
# Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)

print("\n=== AI‑enhanced ===")
print(cleaned_result.text)
```

**Output tipikal**

```
=== Raw OCR ===
Inv0ice No: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00

=== AI‑enhanced ===
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Perhatikan bagaimana langkah AI memperbaiki kebingungan nol‑satu dan memperbaiki format jumlah—tepat jenis perbaikan yang Anda butuhkan saat **mengekstrak teks dari faktur**.

## Langkah 7: Lepaskan sumber daya

Akhirnya, bebaskan sumber daya native yang digunakan oleh mesin AI. Ini sangat penting dalam layanan yang berjalan lama atau pekerjaan batch.

```python
# Release resources when finished
ai.free_resources()
```

Mengabaikan pemanggilan ini dapat menyebabkan kebocoran memori karena model yang mendasarinya berjalan dalam kode native.

## Skrip lengkap yang dapat Anda salin‑tempel

Berikut adalah program lengkap yang dapat dijalankan yang menggabungkan setiap langkah yang dijelaskan di atas. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya ke file gambar Anda.

```python
import asposeocr as ocr   # import the Aspose OCR package

# Step 1: Create an AsposeAI instance (default logging)
ai = ocr.AsposeAI()

# Step 2: (Optional) Tune the model configuration for this demo
#   • Enable automatic download of the model if missing
#   • Use CPU only (no GPU layers)
#   • Increase context size for better correction quality
ai.allow_auto_download = "true"
ai.gpu_layers = 0
ai.context_size = 2048

# Step 3: Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")

# Step 4: Run the standard OCR engine on an image
image_path = "YOUR_DIRECTORY/sample_invoice.png"
ocr_result = ocr.OcrEngine().recognize_image(image_path)

# Step 5: Apply the AI post‑processor to improve the raw OCR output
cleaned_result = ai.run_postprocessor(ocr_result)

# Step 6: Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)
print("\n=== AI‑enhanced ===")
print(cleaned_result.text)

# Step 7: Release resources when finished
ai.free_resources()
```

Simpan ini sebagai `process_invoice.py` dan jalankan:

```bash
python process_invoice.py
```

Anda akan melihat teks mentah dan yang telah dikoreksi dicetak ke konsol, mengonfirmasi bahwa Anda telah berhasil **menjalankan OCR pada gambar**, **mengonfigurasi model OCR**, dan **meningkatkan akurasi OCR** untuk tugas ekstraksi faktur Anda.

## Pertanyaan umum dan kasus tepi

| Question | Answer |
|----------|--------|
| *Bagaimana jika model gagal diunduh?* | Pastikan mesin Anda memiliki akses internet dan flag `allow_auto_download` disetel ke `"true"`. Anda juga dapat mengunduh model secara manual dari portal Aspose dan mengarahkan `AsposeAI` ke folder lokal melalui `ai.model_path = "path/to/model"` |
| *Bisakah saya menjalankannya di GPU?* | Ya. Setel `ai.gpu_layers` ke bilangan bulat positif (mis., `2`) dan instal pustaka CUDA yang sesuai. Eksekusi GPU mempercepat batch besar tetapi memerlukan GPU yang kompatibel. |
| *Bagaimana cara memproses banyak faktur dalam sebuah folder?* | Bungkus logika inti dalam loop yang mengiterasi `os.listdir(folder)`. Ingatlah untuk memanggil `ai.free_resources()` hanya setelah loop selesai, bukan setelah setiap file, agar model tetap dimuat. |
| *Apakah post‑processor aman untuk faktur non‑Inggris?* | Model default dilatih pada teks bahasa Inggris. Untuk bahasa lain, unduh paket bahasa yang sesuai dan setel `ai.language = "fr"` (atau kode ISO yang tepat). |
| *Bagaimana jika hasil OCR kosong?* | Pastikan `image_path` mengarah ke gambar yang dapat dibaca dan file tidak rusak. Anda juga dapat meningkatkan `ai.context_size` untuk memberi model lebih banyak konteks pada pemindaian kualitas rendah. |

## Langkah selanjutnya

Sekarang Anda dapat **menjalankan OCR pada gambar** dan secara andal **mengekstrak teks dari faktur**, pertimbangkan ekstensi berikut:

* **Pemrosesan batch** – gabungkan skrip dengan `multiprocessing` untuk menangani ribuan faktur secara paralel.
* **Validasi data** – gunakan ekspresi reguler untuk memverifikasi nomor faktur, tanggal, dan nilai moneter setelah ekstraksi.
* **Integrasi dengan basis data** – simpan teks yang sudah dibersihkan langsung ke PostgreSQL atau MongoDB untuk analitik selanjutnya.
* **Penyetelan model khusus** – jika Anda memiliki dataset proprietari yang besar, latih model khusus domain dan arahkan `ai.model_path` ke sana untuk akurasi yang lebih tinggi.

Dengan bereksperimen dengan ide-ide ini, Anda akan mengubah demo OCR sederhana menjadi pipeline pemrosesan dokumen yang kuat yang memenuhi persyaratan produksi.

---

*Anda sekarang tahu cara menjalankan OCR pada file gambar dengan Aspose OCR, mengonfigurasi model OCR untuk kinerja optimal, dan meningkatkan akurasi OCR menggunakan post‑processor AI. Terapkan langkah-langkah ini ke alur kerja pemrosesan faktur Anda sendiri dan nikmati ekstraksi teks yang lebih bersih dan dapat diandalkan.*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menjalankan OCR pada Faktur – Mengekstrak Teks dari Gambar dengan Python](/ocr/english/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/)
- [Mengekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Konversi Gambar ke Teks: Mengekstrak Teks dari Gambar Menggunakan Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}