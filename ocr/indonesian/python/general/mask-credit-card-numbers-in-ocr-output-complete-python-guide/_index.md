---
category: general
date: 2026-04-26
description: Sembunyikan nomor kartu kredit dengan cepat menggunakan post‑processing
  OCR AsposeAI. Pelajari kepatuhan PCI, penyamaran dengan ekspresi reguler, dan sanitasi
  data dalam tutorial langkah demi langkah.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: id
og_description: Menyamarkan nomor kartu kredit dalam hasil OCR dengan AsposeAI. Tutorial
  ini mencakup kepatuhan PCI, penyamaran dengan ekspresi reguler, dan sanitasi data.
og_title: Menyamarkan Nomor Kartu Kredit – Panduan Lengkap Pemrosesan Pasca OCR dengan
  Python
tags:
- OCR
- Python
- security
title: Menyamarkan Nomor Kartu Kredit dalam Output OCR – Panduan Python Lengkap
url: /id/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyamarkan Nomor Kartu Kredit – Panduan Python Lengkap

Pernahkah Anda perlu **menyamarkan nomor kartu kredit** dalam teks yang berasal langsung dari mesin OCR? Anda bukan satu-satunya. Dalam industri yang diatur, mengungkapkan PAN (Primary Account Number) lengkap dapat menimbulkan masalah dengan auditor kepatuhan PCI. Kabar baik? Dengan beberapa baris Python dan hook post‑processing AsposeAI, Anda dapat secara otomatis menyembunyikan delapan digit tengah dan tetap aman.

Dalam tutorial ini kami akan membahas skenario dunia nyata: menjalankan OCR pada gambar struk, lalu menerapkan fungsi **OCR post‑processing** khusus yang menyanitasi data PCI apa pun. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat ditempatkan ke dalam alur kerja AsposeAI mana pun, serta beberapa tip praktis untuk menangani kasus pinggir dan menskalakan solusi.

## Apa yang Akan Anda Pelajari

- Cara mendaftarkan post‑processor khusus dengan **AsposeAI**.
- Mengapa pendekatan **regular expression masking** cepat dan dapat diandalkan.
- Dasar‑dasar **PCI compliance** terkait sanitasi data.
- Cara memperluas pola untuk berbagai format kartu atau nomor internasional.
- Output yang diharapkan dan cara memverifikasi bahwa penyamaran berhasil.

> **Prasyarat** – Anda harus memiliki lingkungan Python 3 yang berfungsi, paket Aspose.AI for OCR terpasang (`pip install aspose-ocr`), dan contoh gambar (misalnya `receipt.png`) yang berisi nomor kartu kredit. Tidak ada layanan eksternal lain yang diperlukan.

---

## Langkah 1: Definisikan Post‑Processor yang Menyamarkan Nomor Kartu Kredit

Inti solusi berada dalam fungsi kecil yang menerima hasil OCR, menjalankan rutin **regular expression masking**, dan mengembalikan teks yang telah disanitasi.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Mengapa ini berhasil:**  
- Regex `(\d{4})\d{8}(\d{4})` cocok tepat dengan 16 digit berurutan, format umum untuk Visa, MasterCard, dan banyak lainnya.  
- Dengan menangkap empat digit pertama dan terakhir (`\1` dan `\2`) kami mempertahankan cukup informasi untuk debugging sambil mematuhi aturan **PCI compliance** yang melarang penyimpanan PAN lengkap.  
- Substitusi `\1****\2` menyembunyikan delapan digit tengah yang sensitif, mengubah `1234567812345678` menjadi `1234****5678`.

> **Pro tip:** Jika Anda perlu mendukung nomor American Express 15‑digit, tambahkan pola kedua seperti `r'(\d{4})\d{6}(\d{5})'` dan jalankan kedua penggantian secara berurutan.

---

## Langkah 2: Inisialisasi Mesin AsposeAI

Sebelum kita dapat menempelkan post‑processor kami, kita memerlukan sebuah instance dari mesin OCR. AsposeAI menyertakan model OCR dan API sederhana untuk pemrosesan khusus.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Mengapa inisialisasi di sini?**  
Membuat objek `AsposeAI` sekali dan menggunakannya kembali pada banyak gambar mengurangi beban. Mesin juga menyimpan cache model bahasa, yang mempercepat panggilan berikutnya—berguna saat Anda memindai batch struk.

---

## Langkah 3: Daftarkan Fungsi Penyaringan Kustom

AsposeAI menyediakan metode `set_post_processor` yang memungkinkan Anda menyambungkan callable apa pun. Kami mengirim fungsi `mask_pci` bersama kamus pengaturan opsional (kosong untuk saat ini).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Apa yang terjadi di balik layar?**  
Ketika Anda kemudian memanggil `run_postprocessor`, AsposeAI akan menyerahkan hasil OCR mentah ke `mask_pci`. Fungsi tersebut menerima objek ringan (`data`) yang berisi teks yang dikenali, dan Anda mengembalikan string baru. Desain ini menjaga inti OCR tetap tidak tersentuh sambil memungkinkan Anda menegakkan kebijakan **data sanitization** di satu tempat.

---

## Langkah 4: Jalankan OCR pada Gambar Resi

Sekarang mesin tahu cara membersihkan output, kami memberikannya sebuah gambar. Untuk keperluan tutorial ini kami mengasumsikan Anda sudah memiliki objek `engine` yang dikonfigurasi dengan bahasa dan pengaturan resolusi yang tepat.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tip:** Jika Anda belum memiliki objek yang sudah dikonfigurasi, Anda dapat membuatnya dengan:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

Pemanggilan `recognize_image` mengembalikan objek yang atribut `text`‑nya berisi string mentah yang belum disamarkan.

---

## Langkah 5: Terapkan Post‑Processor yang Terdaftar

Dengan data OCR mentah di tangan, kami menyerahkannya ke instance AI. Mesin secara otomatis menjalankan fungsi `mask_pci` yang kami daftarkan sebelumnya.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Mengapa menggunakan `run_postprocessor` alih‑alih memanggil fungsi secara manual?**  
Hal ini menjaga alur kerja tetap konsisten, terutama ketika Anda memiliki beberapa post‑processor (misalnya pemeriksaan ejaan, deteksi bahasa). AsposeAI menempatkannya dalam urutan pendaftaran, menjamin output yang deterministik.

---

## Langkah 6: Verifikasi Output yang Disanitasi

Akhirnya, mari cetak teks yang telah disanitasi dan pastikan bahwa semua nomor kartu kredit telah disamarkan dengan benar.

```python
print(final_result.text)
```

**Output yang diharapkan** (kutipan):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Jika struk tidak mengandung nomor kartu, teks tetap tidak berubah—tidak ada yang perlu disamarkan, tidak ada yang perlu dikhawatirkan.

---

## Menangani Kasus Pinggir dan Variasi Umum

### Banyak Nomor Kartu dalam Satu Dokumen
Jika sebuah struk mencakup lebih dari satu PAN (misalnya kartu loyalitas plus kartu pembayaran), regex dijalankan secara global, menyamarkan semua kecocokan secara otomatis. Tidak perlu kode tambahan.

### Format Non‑Standar
Kadang OCR menyisipkan spasi atau tanda hubung (`1234 5678 1234 5678` atau `1234-5678-1234-5678`). Perluas pola untuk mengabaikan karakter tersebut:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Penambahan `[ -]?` memungkinkan spasi atau tanda hubung opsional di antara blok digit.

### Kartu Internasional
Untuk PAN 19‑digit yang digunakan di beberapa wilayah, Anda dapat memperluas pola:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Ingat bahwa **PCI compliance** tetap mengharuskan penyamaran digit tengah, terlepas dari panjangnya.

### Mencatat Nilai yang Disamarkan (Opsional)
Jika Anda memerlukan jejak audit, kirimkan flag melalui `custom_settings` dan sesuaikan fungsi:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Kemudian daftarkan dengan:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste Ready)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Menjalankan skrip ini pada struk yang berisi `4111111111111111` akan menghasilkan:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Itulah seluruh pipeline—dari OCR mentah hingga **data sanitization**—dibungkus dalam beberapa baris Python yang bersih.

---

## Kesimpulan

Kami baru saja menunjukkan cara **menyamarkan nomor kartu kredit** dalam hasil OCR menggunakan hook post‑processing AsposeAI, rutin regular‑expression yang ringkas, dan beberapa tip praktik terbaik untuk **PCI compliance**. Solusinya sepenuhnya mandiri, bekerja dengan gambar apa pun yang dapat dibaca mesin OCR, dan dapat diperluas untuk mencakup format kartu yang lebih kompleks atau kebutuhan pencatatan.

Siap untuk langkah selanjutnya? Cobalah menggabungkan penyamaran ini dengan rutinitas **penyisipan ke database** yang hanya menyimpan empat digit terakhir untuk referensi, atau integrasikan **batch processor** yang memindai seluruh folder struk semalaman. Anda juga dapat menjelajahi tugas **OCR post‑processing** lain seperti standarisasi alamat atau deteksi bahasa—semuanya mengikuti pola yang sama seperti yang kami gunakan di sini.

Ada pertanyaan tentang kasus pinggir, kinerja, atau cara menyesuaikan kode untuk perpustakaan OCR lain? Tinggalkan komentar di bawah, dan mari teruskan diskusi. Selamat coding, dan tetap aman!  

![Diagram yang menggambarkan cara kerja penyamaran nomor kartu kredit dalam pipeline OCR](https://example.com/images/ocr-mask-flow.png "Diagram alur penyamaran post‑processing OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}