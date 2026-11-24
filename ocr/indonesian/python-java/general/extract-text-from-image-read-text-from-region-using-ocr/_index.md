---
category: general
date: 2026-07-05
description: Ekstrak teks dari gambar menggunakan Python OCR. Pelajari cara memuat
  gambar untuk OCR, membaca teks dari area tertentu, dan mengekstrak teks dari faktur
  dengan beberapa baris kode.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: id
og_description: Ekstrak teks dari gambar dengan Python OCR. Panduan ini menunjukkan
  cara memuat gambar untuk OCR, membaca teks dari wilayah, dan mengekstrak teks dari
  faktur dengan cepat.
og_title: Ekstrak Teks dari Gambar – Baca Teks dari Area Menggunakan OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Ekstrak Teks dari Gambar – Baca Teks dari Wilayah Menggunakan OCR
url: /id/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar – Baca Teks dari Wilayah Menggunakan OCR

Pernah perlu **mengekstrak teks dari gambar** tetapi hanya bagian tertentu yang penting—seperti total pada faktur? Anda tidak sendirian. Dalam banyak proyek dunia nyata Anda akan menemukan kebutuhan untuk **membaca teks dari wilayah** alih‑alih memproses seluruh gambar. Untungnya, dengan beberapa baris Python Anda dapat memuat gambar untuk OCR, menentukan wilayah minat (ROI), dan mengambil tepat karakter yang Anda butuhkan.

Dalam tutorial ini kita akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan cara **memuat gambar untuk OCR**, menyiapkan ROI, dan akhirnya **mengekstrak teks dari faktur**. Pada akhir tutorial Anda akan memiliki potongan kode siap pakai yang bekerja dengan pustaka OCR populer yang mendukung pengenalan berbasis wilayah.

---

## Apa yang Anda Butuhkan

- Python 3.8+ (kode ini juga berfungsi pada 3.10)  
- Sebuah paket OCR yang menyediakan kelas `OcrEngine` (untuk demo kami menggunakan modul fiktif `ocr`; ganti dengan `pytesseract`, `easyocr`, atau pustaka lain yang mendukung ROI)  
- Gambar contoh—misalnya `invoice.png`—yang berisi teks cetak yang jelas  
- Pengetahuan dasar tentang fungsi dan kelas Python (tidak memerlukan latar belakang deep learning)

Jika Anda sudah memiliki semua itu, bagus—mari kita mulai. Jika belum, unduh Python terbaru dari python.org dan instal paket OCR via `pip install your-ocr-lib`.

---

![Contoh ekstrak teks dari gambar](extract-text-from-image.png "Ekstrak teks dari gambar – demo OCR berbasis wilayah")

*Gambar di atas menggambarkan wilayah (persegi merah) yang akan kita targetkan untuk **mengekstrak teks dari gambar**.*

---

## Langkah 1: Instal dan Impor Pustaka OCR

Pertama, pastikan pustaka OCR tersedia di lingkungan Anda. Pola impor di bawah ini bekerja untuk kebanyakan paket yang menyediakan kelas tingkat tinggi `OcrEngine`.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Tip profesional:** Jika Anda menggunakan `pytesseract`, Anda harus menginstal binary Tesseract secara terpisah dan mengatur `pytesseract.pytesseract.tesseract_cmd` ke jalurnya.

---

## Langkah 2: Buat Engine OCR dan Atur Bahasa

Membuat engine sangat mudah, tetapi menentukan bahasa secara signifikan meningkatkan akurasi, terutama untuk faktur yang berisi angka dan kata‑kata bahasa Inggris.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Mengapa kita melakukannya? Engine OCR menggunakan model bahasa untuk memprediksi karakter; memberi tahu bahwa bahasa yang diharapkan adalah Inggris mengurangi false positive seperti membaca “0” menjadi “O”.

---

## Langkah 3: Muat Gambar untuk OCR

Sekarang kita benar‑benar **memuat gambar untuk OCR**. Kebanyakan pustaka menerima jalur file atau objek gambar Pillow. Di sini kami menggunakan loader bawaan pustaka untuk kesederhanaan.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Pastikan jalurnya mengarah ke direktori yang tepat; kesalahan umum adalah lupa menambahkan jalur relatif ketika skrip dijalankan dari direktori kerja yang berbeda.

---

## Langkah 4: Tentukan Region of Interest (ROI)

Menentukan ROI adalah inti dari **membaca teks dari wilayah**. Anggap saja Anda menggambar persegi di sekitar bagian faktur yang berisi total pembayaran.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` dan `top` mewakili koordinat X dan Y dari sudut kiri‑atas persegi.  
- `width` dan `height` menentukan ukuran kotak.  
- Anda dapat bereksperimen dengan nilai‑nilai berbeda menggunakan penampil gambar yang menampilkan koordinat piksel.

> **Mengapa ROI penting:** Menjalankan OCR pada seluruh halaman membuang siklus CPU dan sering menambah noise dari teks, tabel, atau grafik yang tidak relevan. Dengan memfokuskan pada wilayah tertentu, Anda mendapatkan hasil yang lebih bersih dan pemrosesan yang lebih cepat.

---

## Langkah 5: Lakukan OCR pada Wilayah yang Ditentukan

Setelah semuanya siap, kita akhirnya **mengekstrak teks dari gambar**—tetapi hanya dalam ROI yang telah ditetapkan.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

Metode `recognize` mengembalikan objek yang biasanya berisi string mentah, skor kepercayaan, dan kadang‑kadang kotak pembatas untuk setiap kata. Untuk keperluan kami, kami hanya membutuhkan teks biasa.

---

## Langkah 6: Tampilkan Teks yang Diekstrak

Mari cetak hasilnya dan lihat apa yang didapatkan. Langkah ini memperlihatkan **ekstrak teks dari faktur** dalam skenario dunia nyata.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Output yang Diharapkan

```
Text inside ROI:
Total Amount: $1,245.67
```

Jika faktur Anda memiliki tata letak yang berbeda, Anda akan melihat teks apa pun yang berada di dalam persegi—mungkin nomor faktur, tanggal, atau referensi PO.

---

## Langkah 7: Bungkus Semua ke dalam Fungsi yang Dapat Digunakan Kembali (Opsional)

Agar solusi dapat dipakai kembali pada banyak faktur, enkapsulasi logika ke dalam fungsi. Ini juga memperlihatkan **ocr pada wilayah** sebagai utilitas generik.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Sekarang Anda dapat memanggil fungsi tersebut dengan faktur apa pun:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Output kosong** | ROI tidak benar‑benar mencakup teks (koordinat salah). | Periksa kembali nilai piksel dengan editor gambar; tambahkan overlay debug visual. |
| **Karakter sampah** | Resolusi gambar rendah atau kontras buruk. | Praproses gambar: konversi ke grayscale, terapkan threshold (`cv2.threshold`). |
| **Bahasa salah** | Engine default ke bahasa yang tidak memiliki set karakter yang dibutuhkan. | Secara eksplisit atur `ocr_engine.language` ke `ENGLISH` atau locale yang sesuai. |
| **Keterlambatan performa** | Menjalankan OCR pada gambar besar berulang‑ulang. | Ubah ukuran gambar sebelum memuat, atau proses hanya ROI dengan memotong terlebih dahulu. |

---

## Memperluas Contoh: Multiple ROIs

Kadang‑kadang faktur berisi beberapa bidang yang Anda perlukan—seperti **ekstrak teks dari faktur** untuk total pembayaran dan tanggal faktur. Anda dapat melakukan iterasi pada daftar persegi:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Pola ini menjaga kode tetap bersih dan memudahkan penambahan wilayah lain di kemudian hari.

---

## Kesimpulan

Kami baru saja membahas alur kerja lengkap end‑to‑end untuk **mengekstrak teks dari gambar** menggunakan OCR Python, dengan fokus pada wilayah tertentu. Dengan **memuat gambar untuk OCR**, menentukan **region of interest**, dan memanggil engine, Anda dapat secara andal **membaca teks dari wilayah**—sempurna untuk mengambil total dari faktur, tanggal dari struk, atau data terlokalisasi lainnya.  

Silakan bereksperimen


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)
- [Cara Mengekstrak Teks dari Gambar dengan Menyiapkan Persegi di OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}