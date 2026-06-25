---
category: general
date: 2026-06-25
description: Dapatkan karakter yang didukung OCR dengan cepat menggunakan pustaka
  aocr. Pelajari cara menampilkan daftar karakter OCR, mengatur bahasa, dan men-debug
  mesin OCR Anda di Python.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: id
og_description: Dapatkan karakter yang didukung OCR dengan aocr. Panduan ini menunjukkan
  cara menampilkan daftar karakter OCR, memilih bahasa, dan menangani kasus tepi dalam
  Python.
og_title: Dapatkan Karakter yang Didukung OCR di Python – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Dapatkan Karakter yang Didukung OCR di Python – Panduan Lengkap
url: /id/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Karakter OCR yang Didukung di Python – Panduan Lengkap

Pernah bertanya-tanya bagaimana **mendapatkan karakter OCR yang didukung** untuk bahasa tertentu saat Anda bereksperimen dengan mesin OCR? Anda tidak sendirian. Baik Anda sedang membangun pemindai struk atau parser dokumen multibahasa, mengetahui tepatnya glyph apa yang dapat dikenali mesin Anda sangat membantu. Dalam tutorial ini kami akan membahas seluruh proses—menginstal pustaka, mengonfigurasi bahasa, dan akhirnya mencantumkan karakter‑karakter tersebut—sehingga Anda dapat men-debug dan menyempurnakan pipeline OCR dalam hitungan menit.

Kami akan menggunakan pustaka **aocr**, sebuah mesin OCR Python ringan yang memudahkan kueri kemampuan bahasa. Pada akhir panduan ini Anda akan dapat **mencantumkan karakter OCR**, beralih antara **bahasa OCR yang didukung**, dan bahkan menemukan celah cakupan sebelum mengganggu produksi.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* Python 3.8 atau lebih baru (paket aocr tidak lagi mendukung 3.7)
* Terminal atau command prompt dengan akses internet
* Familiaritas dasar dengan scripting Python (jika Anda pernah menulis `print()`, Anda sudah siap)

Tidak ada dependensi eksternal yang berat—hanya paket pip `aocr`.

---

## Instal Pustaka aocr (Mesin OCR Python)

Hal pertama yang Anda butuhkan adalah instalasi **mesin OCR Python** yang berfungsi. Paket aocr tersedia di PyPI, jadi satu perintah pip sudah cukup:

```bash
pip install aocr
```

Jika Anda menggunakan lingkungan virtual (sangat disarankan), aktifkan dulu:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** Pin versi (`pip install aocr==1.2.4`) untuk menghindari perubahan API yang tak terduga di kemudian hari.

---

## Pilih Bahasa (Bahasa OCR yang Didukung)

aocr dilengkapi dengan beberapa paket bahasa bawaan. Setiap paket mendefinisikan kumpulan titik kode Unicode yang dapat dikenali mesin. Untuk mengkueri paket‑paket tersebut Anda perlu menyetel atribut `language` pada instance engine.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Anda dapat mengganti `aocr.Language.ENGLISH` dengan nilai enum lain (`FRENCH`, `GERMAN`, dll.). Jika Anda mencoba menetapkan bahasa yang tidak termasuk dalam paket, aocr akan mengeluarkan `ValueError`. Karena itu ada baiknya memeriksa daftar **bahasa OCR yang didukung** terlebih dahulu:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Ambil Set Karakter (Dapatkan Karakter OCR yang Didukung)

Sekarang masuk ke inti tutorial: sebenarnya **mendapatkan karakter OCR yang didukung**. Engine menyediakan metode praktis bernama `get_supported_characters()` yang mengembalikan daftar string satu‑karakter.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Di balik layar, aocr membaca file JSON yang dibundel bersama paket bahasa dan mengonversi setiap titik kode Unicode menjadi string Python. Hasilnya deterministik, artinya Anda akan mendapatkan daftar yang sama setiap kali menjalankan skrip pada versi bahasa yang sama.

---

## Tampilkan Berapa Banyak Karakter yang Didukung

Mengetahui jumlahnya membantu Anda cepat menilai luasnya cakupan. Untuk bahasa Inggris, biasanya Anda akan melihat beberapa ribu karakter (termasuk tanda baca dan digit).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

Pemanggilan `len()` bersifat O(1) karena Python menyimpan panjang daftar secara internal, sehingga tidak ada penalti performa meskipun alfabetnya besar.

---

## Pratinjau 100 Karakter Pertama yang Didukung

Pemeriksaan visual singkat dapat mengungkap apakah engine menyertakan simbol yang Anda perlukan (misalnya tanda Euro atau kutipan pintar). Mari cetak seratus karakter pertama:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

Operasi `join` menggabungkan irisan menjadi satu string, yang lebih mudah dibaca dibandingkan mencetak daftar Python.

---

## Skrip Lengkap – Semua Langkah dalam Satu Tempat

Berikut contoh lengkap yang dapat dijalankan dan menggabungkan semua langkah. Simpan sebagai `list_supported_chars.py` dan jalankan `python list_supported_chars.py` dari terminal Anda.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Output yang diharapkan (dipotong untuk singkat):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Jumlah tepatnya mungkin sedikit berbeda tergantung versi aocr, tetapi Anda akan selalu melihat alfabet panjang ditambah tanda baca umum.

---

## Menangani Kasus Edge

### Bagaimana jika paket bahasa tidak ada?

Jika Anda meminta bahasa yang tidak dibundel, `aocr.Language` tidak akan memiliki enum tersebut, dan Anda akan mendapatkan `AttributeError`. Lindungi kode dengan pemeriksaan sederhana:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Daftar karakter kosong

Beberapa bahasa niche mungkin mengembalikan daftar kosong bila data pelatihan yang mendasarinya tidak lengkap. Dalam skenario ini, Anda dapat beralih ke default (misalnya, Inggris) atau mengeluarkan peringatan:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Normalisasi Unicode

Daftar dapat berisi karakter gabungan (misalnya “é” sebagai `e` + aksen akut). Jika proses hilir Anda mengharapkan glyph yang sudah terkomposisi, jalankan langkah normalisasi:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Pro Tips untuk Proyek Dunia Nyata

* **Cache daftar karakter** – Jika Anda memproses ribuan gambar, memanggil `get_supported_characters()` pada setiap iterasi menambah beban yang tidak perlu. Simpan daftar dalam variabel level modul atau serialisasikan ke JSON untuk dipakai kembali.
* **Validasi lintas bahasa** – Saat Anda mendukung banyak bahasa dalam satu aplikasi, intersect set karakter untuk menemukan subset bersama. Ini membantu merancang elemen UI yang konsisten di semua locale.
* **Debug kegagalan OCR** – Jika engine salah mengklasifikasikan glyph, bandingkan karakter yang bermasalah dengan output `list_supported_chars`. Jika tidak ada, Anda telah menemukan celah cakupan yang mungkin memerlukan pelatihan khusus.
* **Kombinasikan dengan font khusus** – aocr menghormati rentang Unicode, tetapi kualitas rendering dapat berbeda antar font. Uji karakter yang didukung dengan font yang akan Anda gunakan di produksi untuk menghindari kejutan.

---

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan aocr versi 2.x?**  
J: Ya, metode `get_supported_characters()` stabil di antara 1.x dan 2.x. Satu‑satunya perubahan adalah enum bahasa dipindahkan ke `aocr.languages`.

**T: Bisakah saya mendapatkan titik kode Unicode untuk setiap karakter?**  
J: Tentu. Gunakan `ord(ch)` dalam list comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**T: Bagaimana dengan skrip kanan‑ke‑kiri seperti Arab?**  
J: aocr menyertakan enum `ARABIC`. Daftar karakter akan berisi glyph Arab, tetapi Anda mungkin perlu mengaktifkan rendering RTL di UI hilir Anda.

---

## Kesimpulan

Anda kini tahu **cara mendapatkan karakter OCR yang didukung** menggunakan pustaka aocr di Python, cara beralih antara **bahasa OCR yang didukung**, dan mengapa **mencantumkan karakter OCR** penting untuk pipeline pengenalan teks yang handal. Dengan skrip lengkap dan tips di atas, Anda dapat dengan cepat memverifikasi cakupan bahasa, men-debug glyph yang hilang, dan membangun aplikasi berbasis OCR yang lebih cerdas.

Siap untuk langkah selanjutnya? Cobalah menggabungkan daftar karakter ini dengan filter daftar kata khusus, atau bereksperimen dengan mesin OCR lain (Tesseract, EasyOCR) dan bandingkan hasilnya. Semakin banyak Anda menjelajah, semakin baik solusi OCR Anda.

Selamat coding, semoga set karakter Anda selalu lengkap!

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}