---
category: general
date: 2026-06-28
description: Lakukan OCR pada gambar menggunakan Aspose AI dan ekstrak teks polos
  dari gambar dalam hanya beberapa baris kode Python. Tutorial langkah demi langkah
  untuk integrasi cepat.
draft: false
keywords:
- perform OCR on image
- extract plain text from image
- Aspose AI OCR
- Python OCR tutorial
- spell‑check post‑processor
- OCR result handling
language: id
og_description: Lakukan OCR pada gambar dengan Aspose AI dan ekstrak teks biasa dari
  gambar dengan mudah. Pelajari alur kerja lengkap dalam tutorial singkat ini.
og_title: Lakukan OCR pada Gambar dengan Aspose AI – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose AI and extract plain text from image
    in just a few lines of Python. Step‑by‑step tutorial for fast integration.
  headline: Perform OCR on Image with Aspose AI – Complete Guide
  type: TechArticle
- questions:
  - answer: Aspose’s OCR engine works best with 300 dpi or higher. If you’re dealing
      with lower quality scans, consider pre‑processing the image (e.g., sharpening,
      binarisation) before feeding it to `engine.set_image`.
    question: What if the image is low‑resolution?
  - answer: Yes. Loop over a list of image files, re‑using the same `engine` and `ai`
      instances. Just remember to call `engine.set_image` for each new file.
    question: Can I process multiple pages?
  - answer: Only on the first run, when the AI model is downloaded. After that, everything
      runs offline from the cached directory you specified.
    question: Do I need an internet connection?
  - answer: 'Pass a language code in the options dictionary, e.g., `ai.set_post_processor(AIProcessor.SpellCheck,
      {"lang": "fr"})` for French.'
    question: How do I change the language of the spell‑check?
  type: FAQPage
tags:
- OCR
- Python
- Aspose
- AI
title: Lakukan OCR pada Gambar dengan Aspose AI – Panduan Lengkap
url: /id/python/general/perform-ocr-on-image-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar dengan Aspose AI – Panduan Lengkap

Pernah bertanya-tanya bagaimana **melakukan OCR pada file gambar** tanpa harus berurusan dengan pustaka berat? Dalam banyak aplikasi dunia nyata Anda hanya perlu mengambil teks dari faktur yang dipindai atau struk, lalu mungkin membersihkannya dengan pemeriksa ejaan. Kabar baiknya, Aspose AI membuat ini menjadi sangat mudah, dan Anda juga dapat **mengekstrak teks biasa dari gambar** dalam satu skrip yang dapat dibaca.

Dalam tutorial ini kita akan melangkah melalui seluruh alur: memuat gambar, menjalankan OCR, mendapatkan hasil mentah dan terstruktur, menerapkan post‑processor pemeriksa ejaan bawaan, dan akhirnya membersihkan sumber daya. Pada akhir tutorial Anda akan memiliki contoh Python siap‑jalankan yang dapat Anda sisipkan ke dalam proyek Anda sendiri.

## Apa yang Akan Anda Pelajari

- Cara menginisialisasi mesin Aspose OCR dan memberinya file gambar.  
- Perbedaan antara output string biasa dan `OcrResult` terstruktur yang mempertahankan tata letak.  
- Cara menghubungkan jembatan Aspose AI, mengunduh model secara otomatis, dan menunjuk ke folder cache khusus.  
- Menggunakan post‑processor pemeriksa ejaan untuk **mengekstrak teks biasa dari gambar** dengan ejaan yang diperbaiki sambil mempertahankan kotak pembatas.  
- Tips praktik terbaik untuk melepaskan sumber daya AI dan menghindari kebocoran memori.  

Tidak diperlukan pengalaman sebelumnya dengan Aspose—hanya lingkungan Python 3 yang berfungsi dan gambar pilihan Anda. Mari kita mulai.

![Contoh Lakukan OCR pada gambar](image.png "Diagram yang menunjukkan alur OCR – lakukan OCR pada gambar")

## Langkah 1 – Inisialisasi Mesin OCR dan Muat Gambar Anda

Hal pertama yang perlu Anda lakukan adalah menghidupkan mesin OCR dan menunjuk ke gambar yang ingin Anda baca. Anggap mesin ini sebagai pemindai yang mengubah piksel menjadi karakter.

```python
# Step 1: Initialise the OCR engine and load the image
engine = OcrEngine()
engine.set_image(Image.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Mengapa ini penting:** `OcrEngine()` membuat sesi baru, sementara `set_image` memberi tahu mesin file mana yang harus dianalisis. Jika Anda melewatkan langkah ini, pemanggilan `recognize` berikutnya akan menghasilkan pengecualian karena tidak ada yang diproses.

## Langkah 2 – Lakukan OCR dan Dapatkan Kedua Hasil: Teks Biasa dan Terstruktur

Sekarang kita benar‑benar **melakukan OCR pada gambar**. Aspose memberikan dua jenis output:

1. `plain_text` – string sederhana, sempurna ketika Anda hanya membutuhkan kata‑kata.  
2. `structured` – objek `OcrResult` yang menyimpan jeda baris, kotak pembatas, dan metadata tata letak lainnya.

```python
# Step 2: Perform OCR – obtain plain text and structured result
plain_text = engine.recognize()                # plain string
structured = engine.recognize_structured()    # OcrResult with layout info
```

> **Pro tip:** Gunakan `plain_text` ketika Anda hanya peduli pada karakter (misalnya, mencari dalam dokumen). Gunakan `structured` ketika Anda perlu memetakan teks kembali ke posisi aslinya, seperti menyorot kesalahan pada pemindaian asli.

## Langkah 3 – Inisialisasi Jembatan Aspose AI (Unduh Model pada Penggunaan Pertama)

Aspose AI adalah otak yang menggerakkan post‑processor pemeriksa ejaan. Pada kali pertama Anda menjalankannya, model akan diunduh secara otomatis. Anda juga dapat menyediakan folder khusus untuk menyimpan cache model, yang mempercepat eksekusi berikutnya.

```python
# Step 3: Initialise the Aspose AI bridge (model will be downloaded on first use)
# Optional: specify a custom directory for the cached model
ai_config = AsposeAIModelConfig()
ai_config.directory_model_path = "YOUR_DIRECTORY/models"
ai = AsposeAI(ai_config)
```

> **Mengapa ini penting:** Menyimpan model dalam cache menghindari panggilan jaringan berulang dan membuat aplikasi Anda tetap responsif, terutama di lingkungan produksi.

## Langkah 4 – Daftarkan Post‑Processor Pemeriksa Ejaan Bawaan

Aspose menyertakan processor pemeriksa ejaan yang berguna dan bekerja pada string biasa maupun hasil OCR terstruktur. Daftarkan sekali, dan Anda siap membersihkan kesalahan ketik yang dihasilkan OCR.

```python
# Step 4: Register the built‑in spell‑check post‑processor
ai.set_post_processor(AIProcessor.SpellCheck, {})
```

> **Catatan:** Kamus kosong `{}` adalah tempat Anda dapat memasukkan kamus khusus atau pengaturan bahasa jika memerlukan kontrol lebih.

## Langkah 5 – Terapkan Pemeriksa Ejaan pada Teks OCR Biasa

Di sinilah kita **mengekstrak teks biasa dari gambar** dan sekaligus memperbaiki kesalahan ejaan. Metode `run_postprocessor` mengambil string mentah dan mengembalikan versi yang telah dibersihkan.

```python
# Step 5: Apply spell‑check to the plain OCR text
corrected_text = ai.run_postprocessor(plain_text)
print("Corrected:", corrected_text)
```

**Output yang diharapkan (contoh):**

```
Corrected: Invoice Number 2023‑07‑15
Date: 07/15/2023
Total Amount: $1,250.00
```

> **Mengapa ini penting:** Mesin OCR sering salah mengenali karakter seperti “0” vs “O” atau “1” vs “l”. Langkah pemeriksa ejaan memperbaiki hal tersebut, memberikan data yang lebih bersih untuk pemrosesan selanjutnya.

## Langkah 6 – Terapkan Pemeriksa Ejaan pada Hasil OCR Terstruktur (Mempertahankan Kotak Pembatas)

Jika Anda perlu mempertahankan tata letak asli—misalnya, menyorot kata yang telah diperbaiki pada dokumen yang dipindai—Anda dapat memberi hasil terstruktur ke post‑processor yang sama. Objek yang dikembalikan tetap berisi informasi baris.

```python
# Step 6: Apply spell‑check to the structured OCR result (preserves bounding boxes)
corrected_struct = ai.run_postprocessor(structured)
for line in corrected_struct.Lines:
    print(line.Text)
```

**Contoh output konsol:**

```
Invoice Number 2023‑07‑15
Date: 07/15/2023
Total Amount: $1,250.00
```

> **Pro tip:** Karena koleksi `Lines` menyimpan koordinat `BoundingBox`, Anda kini dapat menumpangkan teks yang telah diperbaiki kembali ke gambar asli menggunakan pustaka grafis apa pun (Pillow, OpenCV, dll.).

## Langkah 7 – Lepaskan Sumber Daya AI Setelah Selesai

Kebocoran memori adalah pembunuh diam layanan yang berjalan lama. Selalu bebaskan sumber daya AI setelah pekerjaan selesai.

```python
# Step 7: Release AI resources when done
ai.free_resources()
```

> **Mengapa ini penting:** `free_resources()` menutup thread latar belakang dan menghapus model dari memori, menjaga aplikasi Anda tetap ringan.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip lengkap yang dapat Anda salin‑tempel dan jalankan (ganti `YOUR_DIRECTORY` dengan jalur yang sebenarnya):

```python
from aspose.ocr import OcrEngine, Image
from aspose.ai import AsposeAI, AsposeAIModelConfig, AIProcessor

# Initialise OCR engine
engine = OcrEngine()
engine.set_image(Image.from_file("YOUR_DIRECTORY/invoice.png"))

# Perform OCR
plain_text = engine.recognize()
structured = engine.recognize_structured()

# Initialise Aspose AI bridge
ai_config = AsposeAIModelConfig()
ai_config.directory_model_path = "YOUR_DIRECTORY/models"
ai = AsposeAI(ai_config)

# Register spell‑check post‑processor
ai.set_post_processor(AIProcessor.SpellCheck, {})

# Correct plain text
corrected_text = ai.run_postprocessor(plain_text)
print("Corrected:", corrected_text)

# Correct structured result
corrected_struct = ai.run_postprocessor(structured)
for line in corrected_struct.Lines:
    print(line.Text)

# Clean up
ai.free_resources()
```

Jalankan skrip, dan Anda akan melihat output yang telah diperbaiki tercetak di konsol. Itulah seluruh alur kerja **melakukan OCR pada gambar** dari awal hingga akhir.

## Pertanyaan Umum & Kasus Edge

- **Bagaimana jika gambar beresolusi rendah?**  
  Mesin OCR Aspose bekerja paling baik dengan 300 dpi atau lebih. Jika Anda berurusan dengan pemindaian kualitas rendah, pertimbangkan pra‑pemrosesan gambar (misalnya, penajaman, binarisasi) sebelum memberikannya ke `engine.set_image`.

- **Bisakah saya memproses beberapa halaman?**  
  Ya. Lakukan iterasi pada daftar file gambar, gunakan kembali instance `engine` dan `ai` yang sama. Jangan lupa memanggil `engine.set_image` untuk setiap file baru.

- **Apakah saya memerlukan koneksi internet?**  
  Hanya pada kali pertama, ketika model AI diunduh. Setelah itu, semuanya berjalan offline dari direktori cache yang Anda tentukan.

- **Bagaimana cara mengubah bahasa pemeriksa ejaan?**  
  Berikan kode bahasa pada kamus opsi, misalnya `ai.set_post_processor(AIProcessor.SpellCheck, {"lang": "fr"})` untuk bahasa Prancis.

## Kesimpulan

Anda kini tahu persis cara **melakukan OCR pada gambar** dengan Aspose AI dan cara **mengekstrak teks biasa dari gambar** sambil secara otomatis memperbaiki kesalahan OCR umum. Tutorial ini mencakup inisialisasi mesin, hasil biasa vs terstruktur, caching model, integrasi pemeriksa ejaan, dan pembersihan sumber daya yang tepat.  

Selanjutnya Anda dapat menjelajahi penambahan kamus khusus, mengalirkan teks yang telah diperbaiki ke pipeline NLP selanjutnya, atau merender kotak pembatas kembali ke pemindaian asli untuk verifikasi visual. Kemungkinan sangat banyak, dan basis kode yang baru Anda bangun merupakan fondasi yang kuat.

Jangan ragu bereksperimen—ganti gambar, ubah pengaturan post‑processor, atau rangkaikan modul AI tambahan. Jika mengalami kendala, tinggalkan komentar di bawah; selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut membahas topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}