---
category: general
date: 2026-06-16
description: Definisikan wilayah minat dalam OCR untuk mengekstrak teks bahasa Spanyol
  dari kartu identitas. Pelajari cara memuat gambar untuk OCR dan menentukan ROI secara
  efisien.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: id
og_description: Tentukan wilayah minat dalam OCR untuk mengekstrak teks bahasa Spanyol
  dari kartu identitas. Panduan langkah demi langkah tentang memuat gambar dan menentukan
  ROI.
og_title: Tentukan wilayah minat dalam OCR – Tutorial Python Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Mendefinisikan wilayah minat dalam OCR – Tutorial Python Lengkap
url: /id/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definisikan wilayah minat dalam OCR – Tutorial Python Lengkap

Pernah bertanya-tanya bagaimana cara **define region of interest in OCR** sehingga Anda hanya membaca bagian gambar yang benar‑benar Anda perlukan? Dalam tutorial ini kami akan memandu Anda langkah demi langkah, serta menunjukkan cara **load image for OCR** dan mengekstrak teks bahasa Spanyol dari kartu identitas hanya dengan beberapa baris Python.  

Jika Anda pernah menatap pemindaian yang berisik dan berpikir, “Harus ada cara yang lebih bersih untuk mengambil bidang nama,” Anda berada di tempat yang tepat. Pada akhir tutorial Anda akan dapat mengambil teks kartu identitas yang Anda butuhkan tanpa terganggu oleh latar belakang yang berantakan.

## Apa yang Akan Anda Pelajari

- Mengapa Anda harus **define region of interest** sebelum menjalankan OCR.  
- Langkah‑langkah tepat untuk **load image for OCR** menggunakan pembungkus OCR Python yang populer.  
- Cara **how to specify ROI** dengan koordinat piksel.  
- Cara **extract id card text** secara andal, bahkan ketika bahasa sumbernya adalah Spanyol.  
- Tips untuk menangani kasus tepi seperti kartu yang diputar atau pemindaian dengan kontras rendah.  

Tidak diperlukan keahlian OCR sebelumnya—hanya lingkungan Python 3 yang berfungsi dan file JPEG kartu identitas yang ingin Anda uji.

---

![Define region of interest illustration](placeholder.png){alt="Contoh definisi wilayah minat yang menunjukkan persegi panjang yang disorot pada gambar kartu identitas"}

## Langkah 1: Instal dan Impor Pustaka OCR

Pertama-tama, Anda memerlukan pustaka yang menyediakan kelas `OcrEngine` serupa dengan cuplikan yang Anda lihat. Untuk panduan ini kami akan menggunakan paket fiktif `ocr`, tetapi konsep yang sama berlaku untuk `pytesseract`, `easyocr`, atau pembungkus apa pun yang memungkinkan Anda mengatur bahasa dan ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro tip:* Jika Anda menggunakan `pytesseract`, kelas `Rectangle` menjadi tuple sederhana `(left, top, width, height)`. Sisa alur tetap sama.

## Langkah 2: Muat Gambar untuk OCR

Sekarang kita **load image for OCR**. Mesin mengharapkan objek `ocr.Image`, jadi kami menunjuk ke file yang berisi kartu identitas. Pastikan path tersebut absolut atau relatif terhadap direktori kerja skrip Anda.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Jika gambar terlalu besar, pertimbangkan untuk mengubah ukurannya terlebih dahulu; mesin OCR bekerja lebih cepat pada gambar dengan lebar di bawah 1500 px.

## Langkah 3: Cara Menentukan ROI (Define Region of Interest)

Inilah inti dari tutorial: **how to specify ROI**. Wilayah minat hanyalah sebuah persegi panjang yang memberi tahu mesin OCR, “Hanya lihat di dalam batas piksel ini.” Anggaplah seperti menggambar kotak di sekitar bidang nama pada kartu identitas.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Mengapa angka‑angka itu? Pada gambar contoh kami, nama berada kira‑kira 120 px dari tepi kiri dan 80 px dari atas. Sesuaikan angka tersebut agar cocok dengan tata letak kartu yang Anda proses.  

*Edge case:* Jika kartu diputar 90°, tukar `width` dan `height` serta sesuaikan `left`/`top` secara tepat, atau pra‑putar gambar dengan Pillow sebelum memberikannya ke mesin.

## Langkah 4: Lakukan OCR Dalam ROI

Dengan ROI yang ditentukan, mesin akan mengabaikan semua hal di luar persegi panjang. Ini tidak hanya mempercepat pemrosesan tetapi juga mengurangi positif palsu yang disebabkan oleh grafik latar belakang.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

Pemanggilan `recognize()` mengembalikan objek yang berisi teks yang dikenali, skor kepercayaan, dan kotak pembatas untuk setiap kata.

## Langkah 5: Ekstrak Teks Kartu Identitas (dan Verifikasi Output Bahasa Spanyol)

Akhirnya, kami **extract id card text** dari hasil ROI dan mencetaknya. Karena kami telah mengatur bahasa ke Spanyol sebelumnya, mesin OCR akan menerapkan kamus khusus bahasa, meningkatkan akurasi untuk karakter aksen seperti “ñ” atau “á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Output yang Diharapkan

```
ROI text: JUAN PÉREZ GARCÍA
```

Jika Anda melihat karakter yang kacau, periksa kembali bahwa gambar memang berbahasa Spanyol dan bahwa file data bahasa pustaka OCR telah terpasang.

## Kesalahan Umum & Cara Menghindarinya

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| String kosong dikembalikan | ROI tidak berpotongan dengan teks apa pun | Verifikasi koordinat dengan penampil gambar; gunakan `engine.debug_draw_roi()` jika tersedia. |
| Banyak karakter sampah | Paket bahasa salah | Pasang kembali data bahasa Spanyol atau beralih ke `ocr.Language.AUTO`. |
| Skor kepercayaan rendah | Gambar buram atau kontras rendah | Pra‑proses dengan OpenCV – terapkan `cv2.GaussianBlur` dan `cv2.threshold`. |
| OCR berjalan pada seluruh gambar meskipun ROI telah ditetapkan | Menggunakan versi pustaka yang lebih lama | Perbarui ke paket `ocr` terbaru; versi lama mengabaikan ROI. |

## Memperluas Contoh: Multiple ROIs

Terkadang Anda perlu mengambil lebih dari satu bidang (mis., nama dan nomor ID). Polanya tetap sama: ubah `engine.region_of_interest` dan panggil `recognize()` lagi.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Anda juga dapat memproses batch daftar persegi panjang jika pustaka mendukungnya, yang menghemat satu siklus ke mesin OCR.

## Skrip Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip siap‑jalankan yang **defines region of interest**, **loads image for OCR**, dan **extracts Spanish text** dari kartu identitas.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Jalankan skrip dan Anda akan melihat nama tercetak di konsol. Ganti nilai persegi panjang untuk menargetkan bidang lain, dan Anda akan memiliki utilitas yang dapat digunakan kembali untuk dokumen tipe kartu identitas apa pun.

## Langkah Selanjutnya

- **Batch processing:** Loop over folder kartu identitas dan simpan setiap nama yang diekstrak ke file CSV.  
- **Language detection:** Biarkan pengguna memilih bahasa secara dinamis; `ocr.Language.AUTO` dapat berguna.  
- **Post‑processing:** Terapkan pola regex untuk membersihkan kesalahan OCR umum (mis., ganti “0” dengan “O” ketika muncul dalam nama).  

Dengan menguasai cara **define region of interest** Anda telah membuka cara yang kuat untuk **extract id card text** dengan cepat dan akurat, terutama saat menangani dokumen berbahasa Spanyol.

---

### TL;DR

Kami menunjukkan cara **define region of interest in OCR**, **load image for OCR**, dan **how to specify ROI** untuk **extract spanish text image** dari kartu identitas. Contoh lengkap berjalan dalam waktu kurang dari satu menit dan dapat disesuaikan dengan tata letak apa pun dengan beberapa penyesuaian koordinat. Cobalah, ubah persegi panjang, dan saksikan OCR fokus seperti laser.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengekstrak Teks dari Gambar dengan Menyiapkan Persegi Panjang dalam OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}