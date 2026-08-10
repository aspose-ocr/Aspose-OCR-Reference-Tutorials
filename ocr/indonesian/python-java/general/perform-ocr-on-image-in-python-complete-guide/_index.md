---
category: general
date: 2026-06-22
description: Lakukan OCR pada gambar menggunakan Python dalam beberapa baris saja.
  Pelajari cara memuat gambar untuk OCR, mengenali teks dari PNG, dan menggunakan
  mesin OCR secara efisien.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: id
og_description: Lakukan OCR pada gambar dengan cepat menggunakan Python. Tutorial
  ini menunjukkan cara memuat gambar untuk OCR, mengenali teks dari PNG, dan menggunakan
  mesin OCR dengan tingkat kepercayaan.
og_title: Lakukan OCR pada Gambar dengan Python – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Lakukan OCR pada Gambar di Python – Panduan Lengkap
url: /id/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar di Python – Panduan Lengkap

Pernah perlu **melakukan OCR pada file gambar** tapi terhenti di baris kode pertama? Anda tidak sendirian. Dalam panduan ini kami akan menunjukkan cara **memuat gambar untuk OCR**, menyiapkan **mesin OCR** yang ringan, dan akhirnya **mengenali teks dari PNG** hanya dengan beberapa perintah.

Kami akan membahas semuanya mulai dari menginstal pustaka hingga menyesuaikan whitelist sehingga hanya digit dan huruf kapital yang lolos pemindaian. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang dapat Anda sisipkan ke proyek mana pun—tanpa misteri, tanpa tambahan yang tidak perlu.

## Apa yang Akan Anda Pelajari

- Cara **menggunakan mesin OCR** secara programatis di Python.  
- Langkah‑langkah tepat untuk **memuat gambar untuk OCR** dari folder lokal.  
- Mengapa dan bagaimana membatasi pengenalan ke set karakter khusus.  
- Cara **mengenali teks dari PNG** dan menangani hasilnya dengan aman.  

**Prasyarat:** Python 3.7+ terpasang, terminal yang Anda kuasai, dan sebuah gambar (misalnya `serial-number.png`) yang ingin Anda baca. Tidak diperlukan pengalaman OCR sebelumnya.

---

## Lakukan OCR pada Gambar – Inisialisasi Mesin OCR

Hal pertama yang harus Anda lakukan adalah membuat instance mesin OCR. Anggap mesin sebagai otak yang akan menganalisis piksel dan mengubahnya menjadi karakter.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Mengapa ini penting:* Tanpa mesin tidak ada yang memproses gambar. Kelas `OcrEngine` menggabungkan semua pekerjaan berat—pra‑pemrosesan, segmentasi, dan klasifikasi karakter—ke dalam satu objek yang dapat Anda gunakan kembali.

---

## Muat Gambar untuk OCR – Sediakan File PNG

Setelah mesin ada, Anda perlu memberinya gambar yang ingin dibaca. Pustaka mengharapkan objek `ImageStream`, yang dapat Anda buat langsung dari jalur file.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Tips profesional:* Simpan gambar dalam format kontras tinggi (teks hitam di latar putih) dan hindari artefak kompresi; hal ini dapat mengacaukan algoritma OCR.

---

## Batasi Karakter – Whitelist Digit dan Huruf Kapital

Seringkali Anda hanya peduli pada subset karakter—misalnya, nomor seri yang hanya berisi A‑Z dan 0‑9. Dengan mengatur whitelist Anda memberi tahu mesin untuk mengabaikan semua hal lain, yang secara dramatis meningkatkan akurasi.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*Apa yang terjadi di balik layar?* Mesin membangun filter yang membuang glyph yang tidak ada dalam whitelist sebelum tahap klasifikasi akhir. Ini sangat berguna ketika gambar mengandung noise atau teks dekoratif yang tidak diperlukan.

---

## Kenali Teks dari PNG – Jalankan Proses OCR

Dengan mesin yang sudah dipersiapkan dan gambar yang dimuat, Anda akhirnya dapat **melakukan OCR pada gambar**. Pemanggilan `recognize()` menjalankan seluruh pipeline dan mengembalikan objek hasil.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Jika Anda penasaran tentang kinerjanya, metode ini biasanya selesai dalam beberapa ratus milidetik untuk PNG berukuran 300 × 200 px pada laptop modern.

---

## Output dan Verifikasi – Dapatkan Teks yang Dikenali

Langkah terakhir adalah mengekstrak teks polos dari objek hasil. Apa pun yang tidak cocok dengan whitelist secara otomatis diabaikan, sehingga Anda mendapatkan string bersih siap diproses lebih lanjut.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Output tipikal:* `AB12C3D4E5` (asumsi gambar berisi nomor seri tersebut).  

Jika output kosong atau kacau, periksa kembali kualitas gambar dan whitelist; jebakan umum adalah secara tidak sengaja menghilangkan karakter yang diperlukan.

---

## Kasus Pinggir & Kesalahan Umum

| Situasi | Apa yang Diperiksa | Perbaikan yang Disarankan |
|-----------|---------------------|---------------------------|
| **File tidak ditemukan** | Salah ketik jalur atau file hilang | Gunakan `os.path.abspath` untuk memverifikasi jalur lengkap sebelum memanggil `set_image`. |
| **Gambar kontras rendah** | Teks menyatu dengan latar | Terapkan ambang sederhana (`Pillow` atau `OpenCV`) sebelum memberi gambar ke mesin. |
| **Karakter tak terduga** | Whitelist terlalu ketat | Tambahkan karakter yang hilang ke string whitelist. |
| **Gambar besar** | Pengakuan lambat | Ubah ukuran gambar menjadi maksimal lebar 1024 px; kualitas OCR biasanya tetap tinggi. |

---

## Skrip Lengkap – Siap Dijalanin

Berikut adalah skrip lengkap, mandiri, yang menggabungkan semua bagian. Simpan sebagai `ocr_demo.py`, ganti `YOUR_DIRECTORY` dengan folder yang sebenarnya, dan jalankan `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Output konsol yang diharapkan* (ketika PNG berisi `SN12345`):

```
Recognized text: SN12345
```

---

## Kesimpulan

Anda kini tahu persis cara **melakukan OCR pada gambar** di Python, mulai dari **memuat gambar untuk OCR** hingga **mengenali teks dari PNG** dan akhirnya mengekstrak hasil bersih menggunakan **mesin OCR** yang dapat disesuaikan. Pendekatannya sederhana, dapat diperluas, dan langsung dapat dipakai untuk kebanyakan pemindaian gaya nomor seri.

Apa selanjutnya? Coba ganti whitelist dengan huruf kecil, bereksperimen dengan format gambar lain (JPEG, BMP), atau integrasikan skrip ke dalam pipeline pemrosesan batch. Pola yang sama—mesin → gambar → pengaturan → kenali → output—berlaku untuk hampir semua tugas OCR yang akan Anda temui.

Punya pertanyaan atau gambar aneh yang menolak bekerja? Tinggalkan komentar di bawah, dan selamat coding! 

![Diagram illustrating the steps to perform OCR on image using Python](https://example.com/ocr-flow.png "Diagram showing how to perform OCR on image with a Python OCR engine")


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}