---
category: general
date: 2026-06-22
description: Cara mengubah bahasa di mesin OCR dengan cepat. Pelajari cara mengatur
  bahasa OCR Arab (ar) menggunakan kode sederhana dan hindari jebakan umum.
draft: false
keywords:
- how to change language
- ocr language arabic
- how to set OCR
- change OCR language
- set language OCR
language: id
og_description: Cara mengubah bahasa pada mesin OCR dijelaskan di kalimat pertama.
  Ikuti tutorial ini untuk mengatur bahasa OCR Arab dengan cepat.
og_title: Cara Mengubah Bahasa di OCR – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  headline: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  type: TechArticle
- description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  name: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  steps:
  - name: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
    text: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
  - name: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
    text: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
  - name: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
    text: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
  type: HowTo
tags:
- OCR
- multilingual
- programming
title: Cara Mengubah Bahasa di OCR – Mengatur Bahasa Arab Langkah demi Langkah
url: /id/python-java/general/how-to-change-language-in-ocr-set-arabic-language-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengubah Bahasa di OCR – Panduan Pemrograman Lengkap

Mengubah bahasa pada mesin OCR sering menjadi kendala ketika Anda mulai menangani dokumen multibahasa. Dalam tutorial ini kami akan memandu Anda melalui langkah‑langkah tepat untuk mengatur bahasa OCR ke bahasa Arab, lengkap dengan contoh kode yang dapat dijalankan dan penjelasan untuk setiap baris. Jika Anda pernah bertanya-tanya *“bagaimana cara mengatur OCR* ke skrip yang berbeda tanpa merusak alur kerja*, Anda berada di tempat yang tepat*.

Kami akan membahas semua yang Anda perlukan: pustaka yang diperlukan, cara memperoleh instance mesin OCR, cara mengakses pengaturannya, dan akhirnya cara mengubah bahasa OCR dengan aman. Pada akhir tutorial Anda akan dapat beralih dari bahasa Inggris ke bahasa Arab (atau bahasa lain yang didukung) dengan satu pemanggilan metode. Tanpa sulap, hanya kode yang jelas dan beberapa tip praktis.

## Prasyarat

- Python 3.8+ (atau versi terbaru lainnya)
- Sebuah pustaka OCR yang menyediakan objek pengaturan – contoh ini menggunakan **pytesseract** yang dibungkus dalam kelas pembantu kecil, tetapi pola yang sama berlaku untuk mesin lain seperti EasyOCR atau Microsoft Computer Vision SDK.
- Data bahasa Arab terpasang untuk mesin OCR (`ara.traineddata` untuk Tesseract).  
  *Pro tip:* di Ubuntu Anda dapat memasangnya dengan `sudo apt-get install tesseract-ocr-ara`.

## Cara Mengubah Bahasa di OCR – Gambaran Umum

Mengubah bahasa pada dasarnya adalah tarian tiga langkah:

1. **Ambil instance mesin OCR** – biasanya ini adalah objek singleton atau dibuat lewat factory.
2. **Tarik objek pengaturan** – kebanyakan pustaka menyimpan bahasa, DPI, dan opsi lain dalam wadah konfigurasi terpisah.
3. **Setel kode bahasa** – untuk bahasa Arab kode ISO‑639‑2‑nya adalah `"ar"`.

Di bawah ini adalah skrip minimal yang sepenuhnya dapat dijalankan dan mendemonstrasikan langkah‑langkah tersebut.

![How to change language in OCR screenshot](image-placeholder.png "How to change language in OCR example")

## Langkah 1: Buat atau Dapatkan Instance Mesin OCR

Pertama kita membutuhkan sebuah mesin. Pada proyek nyata mesin mungkin dibuat di tempat lain dan diteruskan; untuk kejelasan kami akan menginstansiasinya di sini.

```python
# step1_engine.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    """A thin wrapper around pytesseract to expose a settings object."""
    def __init__(self):
        # pytesseract itself doesn't expose a mutable settings object,
        # so we store options in a dict that we later pass to image_to_string().
        self._options = {"lang": "eng"}  # default to English

    def get_settings(self):
        """Return a Settings object that can modify OCR options."""
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        """Run OCR on the given image using current options."""
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        """Convert the internal options dict to a Tesseract command line."""
        # Example: '-l eng' or '-l ar+eng' for multiple languages
        lang_option = self._options.get("lang", "eng")
        return f"-l {lang_option}"
```

**Mengapa kami membungkus mesin** – banyak SDK OCR (termasuk Tesseract) mengharapkan bahasa diberikan sebagai string pada setiap pemanggilan. Dengan mengenkapsulasi opsi dalam objek pengaturan kami mendapatkan API yang bersih, *how to set OCR*‑style yang mencerminkan cuplikan kode asli yang Anda berikan.

## Langkah 2: Akses Objek Pengaturan Mesin

Sekarang setelah kita memiliki mesin, kita mengambil pengaturannya. Ini mencerminkan baris kedua dari contoh asli (`settings = engine.get_settings()`).

```python
# step2_settings.py
class OcrSettings:
    """Provides getters and setters for OCR configuration."""
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        """
        Change OCR language.
        :param lang_code: ISO‑639‑2 language code, e.g., 'ar' for Arabic.
        """
        # Validate the language code – a tiny safety net.
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        """Return the currently configured language code."""
        return self._engine._options.get("lang", "eng")
```

Di sini kami mengekspos bahasa **how to set OCR** melalui `set_language`. Metode ini juga melakukan pemeriksaan dasar, yang merupakan kebiasaan pemrograman defensif yang baik.

## Langkah 3: Atur Bahasa OCR ke Bahasa Arab (ocr language arabic)

Akhirnya kami memanggil metode dengan kode Arab `"ar"`. Inilah inti dari operasi *change OCR language*.

```python
# step3_change_language.py
from step1_engine import SimpleOCREngine

# Obtain the OCR engine instance (could be a singleton in a larger app)
engine = SimpleOCREngine()

# Access the settings object
settings = engine.get_settings()

# Set the OCR language to Arabic – this is the "how to change language" line.
settings.set_language("ar")

# Optional: verify the change
print("Current OCR language:", settings.get_language())

# Run OCR on a sample Arabic image (replace with your own path)
# result = engine.recognize("sample_arabic.png")
# print("OCR Output:", result)
```

**Output yang Diharapkan**

```
Current OCR language: ar
```

Jika Anda meng-uncomment pemanggilan `recognize` dan menunjukkannya ke gambar Arab yang nyata, Anda akan melihat karakter Arab tercetak di konsol (asalkan data bahasa sudah terpasang).

## Cara Mengatur OCR untuk Beberapa Bahasa

Kadang‑kadang Anda memerlukan *ocr language arabic* **plus** bahasa Inggris, terutama untuk dokumen campuran. Metode `set_language` dapat menerima daftar yang dipisahkan dengan `+`:

```python
settings.set_language("ar+eng")
print("Now recognizing both Arabic and English:", settings.get_language())
```

*Edge case*: Jika paket bahasa yang diminta tidak terpasang, Tesseract akan melempar error seperti `Error opening language file`. Untuk menghindari crash, Anda dapat menangkap pengecualian dan kembali ke bahasa default.

```python
try:
    settings.set_language("ar")
except Exception as e:
    print("Failed to set Arabic language:", e)
    settings.set_language("eng")  # fallback
```

## Mengubah Bahasa OCR Secara Dinamis pada Runtime

Dalam banyak aplikasi pengguna memilih bahasa dari dropdown. Karena pengaturan berada di dalam objek mesin, Anda dapat beralih bahasa secara langsung tanpa harus membuat ulang mesin.

```python
def switch_language(lang_code: str):
    settings.set_language(lang_code)
    print(f"OCR language switched to {lang_code}")

# Example usage:
switch_language("fr")   # switch to French
switch_language("ar")   # back to Arabic
```

Pola ini memenuhi kebutuhan *set language OCR* sambil menjaga kode tetap rapi.

## Kesalahan Umum dan Pro Tips

| Kesalahan | Apa yang Terjadi | Solusi |
|-----------|------------------|--------|
| Paket bahasa tidak ada | Tesseract mengembalikan “Failed loading language ‘ar’” | Pasang data bahasa (`sudo apt-get install tesseract-ocr-ara` atau unduh dari repositori). |
| Menggunakan kode ISO yang salah | Tidak ada output atau karakter kacau | Verifikasi kode (`ar` untuk Arab, `eng` untuk Inggris, `chi_sim` untuk Mandarin Sederhana). |
| Lupa membangun ulang konfigurasi | Mesin masih menggunakan bahasa lama | Selalu panggil `engine._build_config()` (ditangani secara internal saat Anda memanggil `recognize`). |
| Mengirimkan daftar alih-alih string | TypeError | Gunakan `"ar+eng"` sebagai satu string, bukan `["ar", "eng"]`. |

## Contoh Lengkap yang Berfungsi (Semua Bagian Bersatu)

```python
# full_example.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    def __init__(self):
        self._options = {"lang": "eng"}

    def get_settings(self):
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        return f"-l {self._options.get('lang', 'eng')}"

class OcrSettings:
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        return self._engine._options.get("lang", "eng")

# ---------- Usage ----------
engine = SimpleOCREngine()
settings = engine.get_settings()

# Change to Arabic (how to change language)
settings.set_language("ar")
print("Current OCR language:", settings.get_language())

# Uncomment and point to a real Arabic image to test OCR
# output = engine.recognize("sample_arabic.png")
# print("OCR result:", output)
```

Jalankan skrip dengan `python full_example.py`. Jika semuanya sudah disiapkan, Anda akan melihat:

```
Current OCR language: ar
```

…dan output OCR untuk gambar Arab Anda jika Anda mengaktifkan dua baris terakhir.

## Kesimpulan

Anda kini tahu **cara mengubah bahasa di mesin OCR**, khususnya cara mengatur bahasa OCR ke bahasa Arab menggunakan pola yang bersih dan dapat digunakan kembali. Panduan ini menjelaskan cara memperoleh mesin, mengakses pengaturannya, dan akhirnya menerapkan perubahan bahasa—mencakup skenario *ocr language arabic* serta kasus penggunaan *change OCR language* yang lebih luas.  

Langkah selanjutnya? Coba tambahkan dukungan untuk lebih banyak bahasa, bereksperimen dengan string multi‑bahasa (`"ar+eng"`), atau integrasikan logika ini ke dalam layanan web yang memungkinkan pengguna mengunggah dokumen dalam skrip apa pun. Jika Anda penasaran tentang *set language OCR* di pustaka lain (EasyOCR, Google Vision

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cara Mengekstrak OCR – Konfigurasi OCR](/ocr/english/net/ocr-configuration/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}