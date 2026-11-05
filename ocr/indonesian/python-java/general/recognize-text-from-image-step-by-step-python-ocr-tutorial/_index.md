---
category: general
date: 2026-03-26
description: Mengenali teks dari gambar dengan cepat dengan mempelajari cara memuat
  gambar untuk OCR dan mengekstrak data dari wilayah tertentu. Ikuti panduan praktis
  ini.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: id
og_description: Mengenali teks dari gambar dalam Python dengan memuat gambar untuk
  OCR, menentukan wilayah minat, dan mengekstrak teks bersih. Pelajari alur kerja
  lengkap.
og_title: Mengenali Teks dari Gambar – Panduan Lengkap OCR Python
tags:
- OCR
- Python
- Image Processing
title: Mengenali teks dari gambar – Tutorial OCR Python Langkah demi Langkah
url: /id/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar – Panduan Lengkap OCR dengan Python

Pernah perlu **mengenali teks dari gambar** tetapi tidak tahu harus mulai dari mana? Mungkin Anda memiliki formulir yang dipindai, kwitansi, atau tangkapan layar dan hanya ingin mengambil kata‑kata di dalam kotak tertentu. Kabar baiknya, dengan beberapa baris Python Anda dapat memuat gambar untuk OCR, memfokuskan pada satu wilayah, dan mengambil teks yang tepat—tanpa menyalin secara manual.

Dalam tutorial ini kita akan melewati seluruh proses: memuat gambar, mendefinisikan region of interest (ROI), menjalankan mesin OCR, dan mencetak hasilnya. Pada akhir tutorial Anda dapat menyisipkan potongan kode ini ke proyek apa pun yang membutuhkan ekstraksi teks dari bagian spesifik gambar. Tanpa pipeline pemrosesan gambar yang rumit, hanya kode bersih yang dapat dijalankan hari ini.

## Prasyarat

- Python 3.8+ terpasang  
- Paket `ocr` (atau perpustakaan OCR kompatibel lainnya) – instal dengan `pip install ocr-lib` (ganti dengan nama paket yang Anda gunakan)  
- Gambar PNG/JPEG yang berisi formulir yang ingin Anda baca  
- Familiaritas dasar dengan fungsi dan kelas Python  

Jika Anda sudah nyaman dengan hal‑hal di atas, bagus—Anda dapat melanjutkan. Jika belum, siapkan kopi cepat dan pastikan semua item di atas siap; langkah‑langkah selanjutnya mengasumsikan semuanya sudah tersedia.

## Langkah 1: Buat Instance Mesin OCR – Inti “mengenali teks dari gambar”

Hal pertama yang kita butuhkan adalah objek yang tahu cara berkomunikasi dengan mesin OCR. Anggap saja ini sebagai otak yang nanti akan **mengenali teks dari gambar**.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **Mengapa ini penting:** Menginisialisasi mesin sekali memungkinkan Anda menggunakan kembali pengaturan (seperti paket bahasa) pada banyak gambar, yang meningkatkan performa dan menjaga kode tetap rapi.

## Langkah 2: Muat Gambar untuk OCR – Membawa Gambar ke Memori

Sekarang kita benar‑benar **memuat gambar untuk OCR**. Perpustakaan menyediakan metode statis yang nyaman untuk membaca file dan mengembalikan objek yang dapat dipahami mesin.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **Tips pro:** Jika gambar Anda besar, pertimbangkan untuk mengubah ukurannya sebelum dimuat. Gambar yang lebih kecil mempercepat OCR tanpa mengorbankan akurasi untuk kebanyakan teks cetak.

## Langkah 3: Definisikan Region of Interest (ROI) OCR

Seringkali Anda tidak membutuhkan seluruh halaman—hanya kotak spesifik tempat pengguna mengisi data. Mendefinisikan **region of interest OCR** memberi tahu mesin untuk mengabaikan sisanya, yang mengurangi noise dan mempercepat proses.

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **Mengapa fokus pada ROI?**  
> - **Kecepatan:** Mesin memindai lebih sedikit piksel.  
> - **Akurasi:** Grafik latar belakang di luar ROI dapat membingungkan pengenalan karakter.  
> - **Kesederhanaan:** Anda mendapatkan string bersih yang persis sesuai dengan bidang yang Anda butuhkan.

## Langkah 4: Jalankan Proses OCR – Saatnya Membuktikan

Dengan semua persiapan selesai, kita akhirnya **mengenali teks dari gambar** di dalam ROI yang telah didefinisikan.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

Jika mesin mendukung banyak wilayah, `ocr_result` akan berisi daftar; dalam kasus ROI tunggal ini ia berupa objek sederhana dengan metode `get_text()`.

## Langkah 5: Ekstrak dan Cetak Teks – Mendapatkan Output Akhir

Sekarang kita ambil string mentah dari objek hasil dan menampilkannya. Di sinilah Anda dapat menyalurkan output ke basis data, file CSV, atau logika downstream lainnya.

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**Output yang diharapkan** (contoh untuk bidang nama yang telah diisi):

```
Text inside ROI:
 John Doe
```

Jika mesin OCR mengembalikan spasi ekstra atau baris baru, Anda dapat membersihkannya dengan `.strip()` atau ekspresi reguler.

## Menangani Kasus Edge Umum

| Situasi                                 | Apa yang Harus Dilakukan                                                   |
|-----------------------------------------|----------------------------------------------------------------------------|
| **Gambar resolusi rendah**              | Perbesar dengan `Pillow` (`Image.resize`) sebelum memuat.                  |
| **Teks miring atau berputar**           | Terapkan koreksi rotasi (`ocr.Imaging.Image.rotate`).                     |
| **Banyak bahasa**                       | Atur paket bahasa pada mesin: `ocr_engine.set_language('eng+spa')`.      |
| **Tidak ada ROI yang didefinisikan**   | Lewati `add_region_of_interest`; mesin akan memproses seluruh gambar.    |
| **Karakter tak terduga (mis., koma)**   | Proses pasca‑string: `extracted_text.replace(',', '')`.                  |

Tips ini membuat pipeline **memuat gambar untuk OCR** Anda tetap kuat meski materi sumber tidak sempurna.

## Contoh Lengkap yang Berfungsi – Salin, Tempel, Jalankan

Berikut adalah skrip lengkap yang dapat Anda letakkan dalam file `.py` dan jalankan. Skrip ini mencakup semua impor, penanganan error, dan helper kecil yang memverifikasi keberadaan gambar.

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

Menjalankan skrip ini akan mencetak string yang telah dibersihkan dari ROI, memberikan Anda data siap pakai.

## Kesimpulan

Anda kini memiliki metode yang jelas, end‑to‑end untuk **mengenali teks dari gambar** dengan pertama‑tama **memuat gambar untuk OCR**, mendefinisikan **region of interest OCR** yang tepat, dan akhirnya mengekstrak teks bersih. Pendekatan ini bekerja dengan perpustakaan OCR Python apa pun yang mengikuti pola di atas, dan Anda dapat dengan mudah memperluasnya untuk menangani banyak ROI, bahasa berbeda, atau langkah pra‑pemrosesan.

Selanjutnya, Anda dapat menjelajahi:

- **pra‑pemrosesan gambar untuk OCR** (thresholding, denoising) guna meningkatkan akurasi pada pemindaian berisik.  
- Menggunakan hasil **ekstrak teks dari ROI** untuk mengisi DataFrame pandas untuk analisis data massal.  
- Beralih ke layanan OCR berbasis cloud (Google Vision, Azure Computer Vision) bila Anda memerlukan keandalan lebih tinggi pada skala besar.

Cobalah, sesuaikan koordinat persegi panjang agar cocok dengan formulir Anda, dan saksikan otomatisasi bekerja. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}