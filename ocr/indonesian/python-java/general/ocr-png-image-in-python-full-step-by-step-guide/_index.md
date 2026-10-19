---
category: general
date: 2026-06-06
description: OCR gambar PNG dengan Python – pelajari cara mengekstrak teks dari gambar,
  jalankan contoh OCR Python, dan bahkan baca teks bahasa Yunani kuno dengan mudah.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: id
og_description: OCR gambar PNG di Python dijelaskan. Panduan ini menunjukkan cara
  mengekstrak teks dari gambar, menjalankan contoh OCR Python, dan membaca bahasa
  Yunani kuno dengan mudah.
og_title: OCR Gambar PNG di Python – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR Gambar PNG di Python – Panduan Lengkap Langkah demi Langkah
url: /id/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG Image di Python – Panduan Langkah‑demi‑Langkah Lengkap

Pernah bertanya-tanya bagaimana cara **OCR PNG image** langsung dari skrip Python? Mungkin Anda memiliki folder penuh naskah kuno yang dipindai dan Anda perlu **extract text from image** tanpa harus mengetik semuanya secara manual. Kabar baiknya, Anda tidak memerlukan gelar PhD dalam computer vision—hanya beberapa baris kode dan pustaka yang tepat, dan Anda akan membaca bahasa Yunani kuno dalam hitungan detik.

Dalam tutorial ini kami akan membahas **python OCR example** yang mengenali teks dari PNG, mengatur bahasa ke Greek polytonic, dan mencetak hasilnya. Pada akhir tutorial Anda akan tahu persis cara **recognize image text**, menangani jebakan umum, dan menyesuaikan skrip untuk bahasa atau format gambar lain.

## Apa yang Akan Anda Pelajari

- Instal dan konfigurasikan pustaka OCR Python (pytesseract + Tesseract OCR)
- Buat instance mesin OCR dan muat file PNG
- Atur bahasa pengenalan ke Greek polytonic sehingga Anda dapat **read ancient greek**
- Keluarkan teks yang dikenali dan selesaikan masalah umum
- Perluas skrip untuk memproses batch‑multiple PNG atau beralih ke bahasa lain

### Prasyarat

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Sintaks modern dan petunjuk tipe |
| `pytesseract` package | Pembungkus tipis di sekitar mesin Tesseract |
| Tesseract OCR binaries (≥ 5.0) | Mesin sebenarnya yang melakukan pekerjaan berat |
| Greek language data (`grc.traineddata`) | Diperlukan untuk **read ancient greek** dengan benar |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Target kami untuk demo **ocr png image** |

Anda dapat menginstal sisi Python dengan:

```bash
pip install pytesseract Pillow
```

Dan di Ubuntu/macOS Anda akan menambahkan mesin itu sendiri:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Jangan lupa mengunduh data terlatih Greek polytonic:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Path mungkin berbeda; sesuaikan `TESSDATA_PREFIX` jika diperlukan.)*

---

## OCR PNG Image: Buat Instance Mesin

Hal pertama yang kita butuhkan adalah objek yang berkomunikasi dengan Tesseract. Pada `pytesseract` mesin diakses melalui fungsi tingkat modul, tetapi demi kejelasan kami akan membungkusnya dalam kelas kecil. Ini mencerminkan konsep “engine” yang Anda lihat pada cuplikan asli.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Mengapa membungkusnya?**  
- Menjaga API publik tetap identik dengan cuplikan yang Anda mulai, sehingga migrasi menjadi mudah.  
- Memungkinkan kami menambahkan logging atau penanganan error nanti tanpa mengubah alur utama.  
- Menunjukkan praktik OOP yang baik—sesuatu yang dihargai oleh pengembang senior.

---

## Ekstrak Teks dari Gambar: Atur Bahasa ke Greek Polytonic

Sekarang kita memiliki mesin, kita perlu memberi tahu bahasa apa yang diharapkan. Greek polytonic menggunakan diakritik yang tidak tercakup dalam data “greek” standar, jadi kami mengarahkan Tesseract ke file terlatih `grc`.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Jika Anda ingin **extract text from image** dalam bahasa lain, cukup ganti `"grc"` dengan `"eng"` untuk Bahasa Inggris, `"fra"` untuk Bahasa Prancis, dll. Baris yang sama berfungsi untuk bahasa apa pun yang telah Anda instal.

## Kenali Teks Gambar: Jalankan OCR pada PNG

Dengan bahasa yang sudah diatur, kami memasukkan PNG ke dalam mesin. Contoh asli menggunakan path yang di‑hard‑code; kami akan membuatnya sedikit lebih fleksibel dengan menggunakan objek `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Tips & Kasus Tepi**

- **File not found** – bungkus pemanggilan dalam `try/except FileNotFoundError` untuk memberikan pesan yang ramah.
- **Low‑resolution PNG** – pertimbangkan pra‑pemrosesan (mis., mengubah ukuran, binarisasi) dengan Pillow sebelum OCR.
- **Non‑Greek text** – Tesseract tetap akan mencoba mendekode, tetapi akurasi turun drastis. Selalu cocokkan bahasanya.

## Keluarkan Teks yang Dikenali

Akhirnya, kami mencetak hasilnya. Dalam proyek nyata Anda mungkin menulis ke basis data, CSV, atau bahkan mengirimnya ke pipeline terjemahan.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Saat Anda menjalankan skrip terhadap pemindaian bersih dari sebuah prasasti Yunani kuno, Anda akan melihat sesuatu seperti:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Jika output terlihat berantakan, periksa kembali bahwa file **greek.traineddata** berada di folder yang tepat dan PNG tidak terlalu berisik.

---

## Contoh Kerja Penuh (Semua Langkah dalam Satu Skrip)

Berikut adalah program lengkap yang siap dijalankan. Simpan sebagai `ocr_greek.py` dan jalankan `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Output yang Diharapkan** (dipotong untuk singkat):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Jika Anda melihat karakter Yunani yang tepat, selamat—Anda telah berhasil melakukan operasi **ocr png image** di Python!

---

## Pertanyaan Umum & Tips Pro

### Bagaimana cara meningkatkan akurasi pada PNG yang berisik?

- Ubah gambar menjadi skala abu‑abu: `img = img.convert('L')`
- Terapkan ambang biner: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Perbesar dengan `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Langkah‑langkah ini sering mengubah mimpi buruk **recognize image text** menjadi hasil yang bersih.

### Bisakah saya memproses seluruh folder PNG?

Tentu saja. Bungkus pemanggilan `recognize_image` dalam loop `for` pada `Path.glob("*.png")`. Simpan setiap hasil dalam kamus atau tulis ke CSV untuk analisis selanjutnya.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Bagaimana jika saya hanya perlu mengekstrak angka?

Berikan string **config** khusus ke `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

Dengan cara itu Anda dapat **extract text from image** file yang berisi tabel, nomor seri, atau timestamp.

### Apakah ada cara untuk mendapatkan skor kepercayaan?

Ya—gunakan `pytesseract.image_to_data` yang mengembalikan TSV dengan kepercayaan per kata. Anda dapat menyaring token dengan kepercayaan rendah sebelum menyusun string akhir.

---

## Memperluas Tutorial

Sekarang Anda telah menguasai dasar‑dasarnya, pertimbangkan untuk menjelajahi topik terkait berikut:

- **Batch OCR with multiprocessing** – mempercepat korpora besar PNG.
- **Hybrid OCR + NLP pipelines** – secara otomatis menerjemahkan Greek kuno yang diekstrak ke dalam Bahasa Inggris modern.
- **Alternative engines** – coba `easyocr` atau metode berbasis `opencv` untuk kasus penggunaan khusus.
- **Cloud OCR services** – Google Vision, Azure Computer Vision, atau AWS Textract untuk skala tanpa server.

Masing‑masing ini dibangun di atas **python ocr example** inti yang baru saja kami bahas, sehingga Anda akan merasa nyaman menyelam lebih dalam.

---

## Kesimpulan

Kami telah mengambil cuplikan sederhana dan mengubahnya menjadi alur kerja **ocr png image** yang kuat di Python. Dengan membuat `OcrEngine`, mengatur bahasa ke Greek polytonic, memasukkan PNG, dan mencetak hasilnya, Anda kini tahu cara **extract text from image** file, **recognize image text**, dan bahkan **read ancient greek**.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑demi‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara Mengatur Nilai Ambang pada Pengenalan Gambar OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [mengenali teks gambar dengan Aspose OCR untuk banyak bahasa](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}