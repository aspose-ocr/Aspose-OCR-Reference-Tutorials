---
category: general
date: 2026-06-25
description: Cara menggunakan OCR di Python – pelajari cara memuat gambar untuk OCR,
  mengenali teks dalam wilayah, dan mengekstrak teks wilayah dengan cepat.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: id
og_description: Cara menggunakan OCR di Python – panduan langkah demi langkah untuk
  memuat gambar, mengenali teks di wilayah tertentu, dan mengekstrak nomor faktur.
og_title: 'Cara Menggunakan OCR Python: Memuat Gambar dan Mengekstrak Teks Wilayah'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Cara Menggunakan OCR Python: Memuat Gambar dan Mengekstrak Teks Wilayah'
url: /id/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR Python: Memuat Gambar dan Mengekstrak Teks Wilayah

**How to use OCR in Python** lebih sederhana daripada yang Anda pikirkan. Pernah menatap faktur yang dipindai dan bertanya-tanya bagaimana cara mengambil hanya nomor faktur tanpa harus mem‑parsing seluruh halaman? Anda tidak sendirian—banyak pengembang mengalami kendala itu saat pertama kali mencoba optical character recognition. Dalam panduan ini kami akan menjelaskan cara memuat gambar untuk OCR, mendefinisikan sebuah persegi panjang, mengenali teks di wilayah tersebut, dan akhirnya mengekstrak teks wilayah. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang mengisolasi potongan teks apa pun yang Anda butuhkan.

> *Pro tip:* Jika Anda bekerja dengan PDF, konversi setiap halaman menjadi gambar terlebih dahulu—sebagian besar pustaka OCR menangani PNG/JPEG dengan paling baik.

## Apa yang Anda Butuhkan

- Python 3.8+ (rilis stabil terbaru disarankan)  
- Sebuah pustaka OCR yang menyediakan kelas `OcrEngine` (misalnya **ocr** dari `pip install ocr-lib`)  
- Contoh gambar—di sini kami akan menggunakan `invoice.png` yang ditempatkan di folder yang Anda kontrol  
- Familiaritas dasar dengan persegi panjang (x, y, lebar, tinggi)  

Tidak ada dependensi berat, tidak memerlukan GPU—hanya pekerjaan CPU biasa, yang membuatnya mudah dipindahkan.

---

## Cara Menggunakan OCR: Menginisialisasi Engine (Langkah 1)

Sebelum teks apa pun dapat dibaca, Anda memerlukan sebuah instance engine OCR. Anggaplah itu sebagai otak yang akan menganalisis pola piksel.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Mengapa ini penting:* Menginisialisasi engine memuat model bahasa dan mengatur konfigurasi default. Melewatkan langkah ini akan memunculkan pengecualian saat Anda memanggil `recognize_region`.

## Memuat Gambar untuk OCR (Langkah 2)

Sekarang engine sudah siap, kami memberikannya sebuah gambar. Metode `Image.load` dari pustaka menangani format umum dan menormalkan bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Jika file tidak ditemukan, Python akan melempar `FileNotFoundError`. Pastikan path bersifat absolut atau relatif terhadap direktori kerja skrip Anda.  

*Kasus khusus:* Beberapa engine OCR mengharapkan gambar grayscale. Jika Anda melihat akurasi yang buruk, konversi gambar terlebih dahulu:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Mengenali Teks di Wilayah (Langkah 3)

Mendefinisikan wilayah adalah tempat Anda memberi tahu engine *di mana* harus mencari. `Rectangle` menerima nilai floating‑point untuk presisi sub‑piksel, yang berguna saat menangani pemindaian resolusi tinggi.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – sudut kiri‑atas persegi panjang (dalam piksel)  
- **width, height** – ukuran kotak  

Anda mungkin bertanya-tanya bagaimana menemukan angka-angka ini. Cara cepatnya adalah membuka gambar di editor apa pun (misalnya GIMP atau Paint.NET) dan gunakan alat seleksi untuk membaca koordinat.  

*Mengapa tidak langsung OCR seluruh halaman?* Membatasi area mengurangi noise, mempercepat proses, dan secara dramatis meningkatkan akurasi untuk bidang kecil seperti nomor faktur.

---

## Cara Mengekstrak Teks Wilayah (Langkah 4)

Dengan wilayah yang sudah ditetapkan, minta engine untuk mengenali hanya bagian itu. Objek hasil berisi teks mentah dan skor kepercayaan.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Jika engine OCR mendukung banyak bahasa, Anda dapat memberikan kode bahasa opsional:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Kesalahan umum:* Beberapa engine mengembalikan daftar kata alih‑alih satu string. Dalam kasus tersebut, gabungkan mereka:

```python
text = " ".join(region_result.words)
```

---

## Mengeluarkan Nomor Faktur yang Diekstrak (Langkah 5)

Akhirnya, cetak—atau simpan—teks yang diekstrak. Anda juga dapat memproses string lebih lanjut untuk menghapus spasi berlebih atau karakter non‑numerik.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Menjalankan skrip dengan persegi panjang yang teralign dengan benar seharusnya menghasilkan sesuatu seperti:

```
Invoice number: 20231578
```

Jika Anda mendapatkan karakter sampah, periksa kembali koordinat persegi panjang atau pertimbangkan meningkatkan resolusi gambar.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip mandiri yang dapat Anda salin‑tempel dan jalankan:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Simpan file sebagai `extract_invoice.py`, ganti `YOUR_DIRECTORY` dengan folder yang sebenarnya, dan jalankan:

```bash
python extract_invoice.py
```

Anda akan melihat nomor faktur tercetak di konsol.

---

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana jika nomor faktur dicetak dengan font yang bergaya?**  
A: Sebagian besar engine OCR modern menangani berbagai jenis font, namun Anda dapat meningkatkan akurasi dengan melatih model bahasa khusus atau melakukan pra‑pemrosesan gambar (misalnya, menerapkan filter ambang).

**Q: Bisakah saya mengekstrak beberapa bidang sekaligus?**  
A: Tentu saja. Definisikan daftar objek `Rectangle`—satu per bidang—dan lakukan loop di atasnya, menyimpan setiap hasil dalam kamus.

**Q: Apakah ini bekerja pada PDF multi‑halaman?**  
A: Konversi setiap halaman menjadi gambar terlebih dahulu (menggunakan `pdf2image` atau serupa), lalu terapkan ekstraksi berbasis wilayah yang sama per halaman.

---

## Kesimpulan

Dalam tutorial ini kami membahas **cara menggunakan OCR** di Python untuk memuat gambar, mengenali teks di wilayah tertentu, dan mengekstrak teks wilayah tersebut—sempurna untuk mengambil nomor faktur, ID pesanan, atau potongan data kecil lainnya dari dokumen yang dipindai. Dengan mengisolasi area yang diminati Anda memperoleh kecepatan, akurasi, dan lebih sedikit kerepotan pasca‑pemrosesan.

Siap untuk langkah selanjutnya? Cobalah memperluas skrip untuk menangani **load image for OCR** dari folder faktur batch, atau bereksperimen dengan **recognize text in region** untuk bidang berbeda seperti tanggal dan total. Pola yang sama berlaku—hanya ubah koordinat persegi panjang.

Jika Anda mengalami kendala atau memiliki ide perbaikan, tinggalkan komentar di bawah. Selamat coding, dan semoga pipeline OCR Anda selalu akurat!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara Mengekstrak Teks dari Gambar dengan Menyiapkan Persegi Panjang di OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Cara Menggunakan AspOCR: Filter Pra‑proses Gambar OCR untuk .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}