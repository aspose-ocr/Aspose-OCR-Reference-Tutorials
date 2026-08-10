---
category: general
date: 2026-07-18
description: Jalankan OCR pada gambar menggunakan Aspose OCR di Python. Pelajari cara
  mengekstrak teks biasa dari gambar, terapkan pemrosesan pasca‑AI, dan dapatkan hasil
  bersih dengan cepat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract plain text from image
- Aspose OCR Python
- AI post‑processor OCR
- image text extraction
language: id
lastmod: 2026-07-18
og_description: Jalankan OCR pada gambar dengan Aspose OCR dan Python. Tutorial ini
  menunjukkan cara mengekstrak teks biasa dari gambar dan meningkatkan akurasi menggunakan
  pemroses AI.
og_image_alt: Screenshot showing run OCR on image results in Python console
og_title: Jalankan OCR pada Gambar – Panduan Python Lengkap dengan Aspose AI
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Run OCR on image using Aspose OCR in Python. Learn to extract plain
    text from image, apply AI post‑processing, and get clean results fast.
  headline: Run OCR on Image with Aspose AI – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI
title: Jalankan OCR pada Gambar dengan Aspose AI – Tutorial Python Lengkap
url: /id/python/general/run-ocr-on-image-with-aspose-ai-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar dengan Aspose AI – Tutorial Python Lengkap

Pernah bertanya-tanya bagaimana cara **run OCR on image** file tanpa berurusan dengan API tingkat‑rendah? Anda tidak sendirian. Dalam banyak proyek—pemrosesan faktur, pemindaian struk, atau mendigitalkan dokumen lama—mendapatkan teks bersih yang dapat dicari dari sebuah gambar adalah langkah pertama, dan seringkali yang paling sulit.

Pada panduan ini kami akan membahas contoh langsung yang tidak hanya **run OCR on image** tetapi juga menunjukkan cara **extract plain text from image** menggunakan mesin OCR Aspose, kemudian memoles hasilnya dengan post‑processor AI kecil. Pada akhir Anda akan memiliki skrip siap‑jalankan, pemahaman jelas tentang setiap bagian, dan beberapa tips untuk menghindari jebakan umum.

![Contoh Run OCR pada Gambar](/images/run-ocr-on-image.png){: .align-center alt="Output konsol Run OCR pada gambar yang menunjukkan teks asli dan teks yang ditingkatkan AI"}

## Apa yang Anda Butuhkan

- Python 3.8+ terinstal (kode ini bekerja di Windows, macOS, dan Linux).
- Lisensi aktif Aspose OCR untuk Python atau percobaan gratis (paketnya adalah `aspose-ocr` di PyPI).
- File gambar contoh (misalnya, faktur atau struk yang dipindai) disimpan secara lokal.
- Opsional: mesin dengan GPU jika Anda berencana mengubah pengaturan `gpu_layers` nanti.

Itu saja—tanpa mesin OCR berat, tanpa panggilan cloud eksternal, hanya satu instalasi pip dan beberapa baris kode.

## Langkah 1: Instal Paket Aspose OCR

Buka terminal dan jalankan:

```bash
pip install aspose-ocr
```

Paket ini mengunduh mesin OCR inti serta namespace ringan `aspose.ocr` yang akan kami gunakan sepanjang tutorial.

## Langkah 2: Impor Kelas yang Diperlukan

Kami mulai dengan mengimpor dua kelas utama: `AsposeAI` untuk post‑processing yang ditingkatkan AI dan `OcrEngine` untuk ekstraksi teks sebenarnya.

```python
# Step 1: Import required classes
from aspose.ocr import AsposeAI, OcrEngine
```

*Mengapa ini penting*: `OcrEngine` melakukan pekerjaan berat dalam mengenali glif, sementara `AsposeAI` memungkinkan kami menyisipkan logika khusus—seperti mengkapitalisasi setiap kata—tanpa menulis ulang inti OCR.

## Langkah 3: Buat Instance AsposeAI (Logger Opsional)

Jika Anda menginginkan logging yang detail, Anda dapat memberikan logger khusus, tetapi default sudah cukup untuk kebanyakan kasus.

```python
# Step 2: Create an AsposeAI instance (optional custom logger can be supplied)
ai = AsposeAI()
```

## Langkah 4: Sesuaikan Model Dasar (Opsional)

Aspose OCR dilengkapi dengan model bahasa default, tetapi Anda dapat mengarahkannya ke repositori HuggingFace atau memaksa eksekusi CPU. Di bawah ini kami mengaktifkan unduhan otomatis dan memilih model `gpt2` kecil—hanya untuk menggambarkan pengaturan yang dapat Anda ubah.

```python
# Step 3: (Optional) Adjust the underlying model configuration
ai.config.allow_auto_download = "true"          # permit automatic model download
ai.config.hugging_face_repo_id = "openai/gpt2"   # specify the HuggingFace model
ai.config.gpu_layers = 0                        # force CPU execution
```

> **Tip pro:** Jika Anda memiliki GPU yang mendukung CUDA, naikkan `gpu_layers` ke `1` atau `2` untuk peningkatan kecepatan yang terlihat.

## Langkah 5: Daftarkan Post‑Processor Sederhana

Tujuan kami adalah **extract plain text from image** dan kemudian membuatnya terlihat lebih bagus. Berikut fungsi kecil yang mengkapitalisasi setiap kata. Anda dapat menggantinya dengan pemeriksaan ejaan, deteksi bahasa, atau bahkan panggilan LLM lengkap.

```python
# Step 4: Register a simple post‑processor that capitalizes each word
def capitalize_words(text, settings):
    """Capitalize every word in the OCR output."""
    return " ".join(word.capitalize() for word in text.split())

# Attach the processor to the AsposeAI instance
ai.set_post_processor(capitalize_words, custom_settings={})
```

Dictionary `custom_settings` memungkinkan Anda mengirimkan parameter tambahan nanti—berguna saat Anda mengembangkan processor.

## Langkah 6: Muat Gambar dan Jalankan OCR

Sekarang kami akhirnya **run OCR on image**. Kami akan mengambil dua jenis output:

1. **Plain text** – string mentah tanpa informasi tata letak.
2. **Structured text** – sadar tata letak, mempertahankan kolom dan tabel.

```python
# Step 5: Load an image and obtain OCR results (plain and layout‑aware)
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()                     # raw text
structured_text = ocr_engine.recognize_structured()    # layout‑aware text
```

> **Mengapa keduanya?** `plain_text` sempurna untuk pencarian cepat, sementara `structured_text` unggul ketika Anda perlu membangun kembali tabel atau menjaga kesejajaran kolom.

## Langkah 7: Tingkatkan Output OCR dengan AI Post‑Processor

Dengan hasil OCR di tangan, kami menyerahkannya ke `AsposeAI.run_postprocessor`. Di sinilah fungsi `capitalize_words` sebelumnya dijalankan.

```python
# Step 6: Enhance the OCR outputs using the AI post‑processor
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)
```

Jika Anda memutuskan nanti untuk mengganti post‑processor dengan sesuatu yang lebih canggih—misalnya korektor tata bahasa—cukup ganti fungsi pada langkah 5 dan sisa pipeline tetap sama.

## Langkah 8: Lihat Hasilnya

Mari cetak semuanya berdampingan sehingga Anda dapat membandingkan OCR mentah dengan versi yang ditingkatkan AI.

```python
# Step 7: Display original and enhanced texts
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)
```

### Output yang Diharapkan

```
Original plain text: invoice #12345 date 01/02/2024 total $123.45
AI‑enhanced plain text: Invoice #12345 Date 01/02/2024 Total $123.45

Original structured text: invoice #12345
date 01/02/2024
total $123.45
AI‑enhanced structured text: Invoice #12345
Date 01/02/2024
Total $123.45
```

Perhatikan bagaimana AI post‑processor mengubah kata semua‑huruf kecil menjadi kapital, membuat teks jauh lebih mudah dibaca. Anda dapat menerapkan transformasi apa pun yang diinginkan—ini hanya bukti konsep.

## Langkah 9: Bersihkan Sumber Daya

Aspose memuat file model besar ke memori. Saat selesai, bebaskan mereka untuk menghindari kebocoran memori, terutama pada layanan yang berjalan lama.

```python
# Step 8: Release model resources when done
ai.free_resources()
```

## Pertanyaan Umum & Kasus Edge

| Question | Answer |
|----------|--------|
| **Bisakah saya menjalankan OCR pada beberapa gambar dalam loop?** | Tentu saja. Cukup instantiate `OcrEngine` sekali, panggil `load_image` di dalam loop, dan gunakan kembali instance `AsposeAI` yang sama untuk post‑processing. |
| **Bagaimana jika gambar beresolusi rendah?** | Lakukan pra‑proses dengan OpenCV (misalnya, `cv2.resize` dan `cv2.threshold`) sebelum mengirimkannya ke `OcrEngine`. |
| **Apakah saya memerlukan GPU?** | Tidak diperlukan. Mode CPU default bekerja baik untuk kebanyakan dokumen. Atur `ai.config.gpu_layers` > 0 hanya jika Anda memiliki GPU yang kompatibel dan membutuhkan kecepatan. |
| **Bagaimana cara extract plain text from image dalam bahasa lain?** | Ubah `ocr_engine.language = "fr"` (atau kode ISO‑639‑1 apa pun) sebelum memanggil `recognize`. Post‑processor yang sama tetap akan dijalankan, tetapi Anda mungkin memerlukan logika khusus bahasa. |

## Skrip Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan:

```python
# Full script: run OCR on image, extract plain text, and apply AI post‑processing

from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Initialize AsposeAI
ai = AsposeAI()
ai.config.allow_auto_download = "true"
ai.config.hugging_face_repo_id = "openai/gpt2"
ai.config.gpu_layers = 0   # set >0 for GPU

# 2️⃣ Register post‑processor (capitalizes each word)
def capitalize_words(text, settings):
    return " ".join(word.capitalize() for word in text.split())

ai.set_post_processor(capitalize_words, custom_settings={})

# 3️⃣ Load image and run OCR
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()
structured_text = ocr_engine.recognize_structured()

# 4️⃣ Enhance outputs
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)

# 5️⃣ Print results
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)

# 6️⃣ Clean up
ai.free_resources()
```

Simpan ini sebagai `run_ocr_on_image.py`, ganti path placeholder dengan gambar Anda yang sebenarnya, dan jalankan `python run_ocr_on_image.py`. Anda akan melihat output sebelum/setelah seperti contoh di atas.

## Kesimpulan

Kami telah berhasil **run OCR on image** file menggunakan Aspose OCR, menunjukkan cara **extract plain text from image**, dan memperlihatkan cara ringan untuk meningkatkan keterbacaan dengan AI post‑processor. Pola inti—OCR

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}