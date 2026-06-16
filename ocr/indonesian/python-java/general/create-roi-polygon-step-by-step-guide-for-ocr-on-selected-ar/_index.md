---
category: general
date: 2026-03-26
description: Buat poligon ROI untuk menjalankan OCR pada area yang dipilih. Pelajari
  cara mendefinisikan beberapa wilayah, mendaftarkannya, dan mengekstrak teks dengan
  mesin OCR Python.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: id
og_description: Buat poligon ROI dan jalankan OCR pada area yang dipilih dengan mesin
  Python. Kode lengkap, penjelasan, dan tips disertakan.
og_title: Buat Poligon ROI – OCR Cepat pada Area yang Dipilih
tags:
- OCR
- Python
- Image Processing
title: Buat Poligon ROI – Panduan Langkah demi Langkah untuk OCR pada Area yang Dipilih
url: /id/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Poligon ROI – Tutorial Lengkap untuk OCR pada Area Terpilih

Pernah perlu **membuat poligon ROI** sehingga Anda dapat menjalankan OCR hanya pada bagian gambar yang penting? Mungkin Anda memindai struk dan hanya total yang penting, atau Anda memiliki formulir di mana hanya bidang tanda tangan yang perlu dibaca. Dalam kasus tersebut, **ocr pada area terpilih** menghemat waktu dan meningkatkan akurasi.  

Dalam panduan ini kami akan membahas semua yang Anda perlukan: mulai dari mendefinisikan dua poligon, mendaftarkannya ke mesin OCR, hingga mengambil teks yang dikenali dalam satu panggilan bersih. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan dan pemahaman kuat mengapa memfokuskan pada region of interest itu penting.

## Apa yang Akan Anda Pelajari

- Cara **membuat objek poligon ROI** menggunakan pustaka OCR tipikal.  
- Perbedaan antara mendefinisikan satu region dengan beberapa region.  
- Cara mendaftarkan region tersebut ke mesin sehingga `ocr pada area terpilih` dilakukan.  
- Output yang diharapkan dan cara mengatasi masalah umum (misalnya, ROI yang tumpang tindih, hasil kosong).

### Prasyarat

- Python 3.8+ terpasang.  
- Sebuah pustaka OCR yang menyediakan metode `Polygon`, `Point`, dan `add_region_of_interest` (contoh menggunakan modul fiktif `ocr`; ganti dengan SDK Anda yang sebenarnya, seperti pembungkus Tesseract‑Python atau EasyOCR).  
- Sebuah file gambar contoh (`sample.png`) yang berisi teks pada koordinat yang ditunjukkan di bawah.

> **Tips pro:** Jika Anda menggunakan pustaka nyata, pastikan gambar dimuat dalam ruang koordinat yang sama (origin di kiri‑atas, X meningkat ke kanan, Y meningkat ke bawah).  

---  

## Langkah 1: Impor Modul OCR dan Muat Gambar Anda  

Pertama, bawa paket OCR ke dalam ruang lingkup dan baca gambar yang ingin Anda proses.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Mengapa ini penting:* Mesin memerlukan data gambar sebelum Anda dapat menambahkan **poligon ROI** apa pun. Beberapa pustaka juga memungkinkan Anda mengirim gambar nanti, tetapi menginisialisasi lebih awal membuat alur kerja lebih rapi.

## Langkah 2: Definisikan Poligon ROI Pertama  

Sekarang kita buat region of interest pertama. Anggap saja Anda menggambar persegi panjang di sekitar header tabel.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Penjelasan:*  
- `ocr.Point(x, y)` menggunakan koordinat piksel.  
- Daftar titik diurutkan searah jarum jam, yang biasanya diharapkan oleh mesin.  
- Anda dapat menambahkan sebanyak mungkin titik untuk membuat bentuk tidak beraturan; persegi panjang hanyalah kasus khusus.

## Langkah 3: Definisikan Poligon ROI Tambahan (Opsional)  

Anda tidak harus berhenti pada satu saja. Berikut poligon kedua yang menangkap bidang tanda tangan di bagian bawah halaman.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Mengapa menambah lebih banyak?* Menjalankan **ocr pada area terpilih** untuk beberapa zona memungkinkan Anda mengekstrak potongan data yang berbeda dalam satu kali proses, yang jauh lebih cepat daripada memotong dan memproses tiap potongan secara terpisah.

## Langkah 4: Daftarkan ROI ke Mesin OCR  

Setelah poligon siap, beri tahu mesin area mana yang harus diperiksa.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Catatan penting:* Beberapa SDK mengharuskan Anda memanggil metode `clear_regions()` sebelum menambahkan yang baru jika Anda menggunakan kembali mesin untuk gambar lain.

## Langkah 5: Jalankan OCR dan Ambil Teks  

Akhirnya, jalankan proses pengenalan. Mesin hanya akan melihat ke dalam poligon yang baru saja kita tambahkan.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Output yang diharapkan** (asumsi `sample.png` berisi kata “Invoice Total: $123.45” di ROI pertama dan “Signature: John Doe” di ROI kedua):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Jika output kosong, periksa kembali bahwa koordinat memang memotong teks dan bahwa resolusi gambar cocok dengan sistem koordinat.

## Kasus Tepi & Kesalahan Umum  

| Situasi                                 | Hal yang Perlu Diperhatikan                     | Solusi / Pendekatan                              |
|----------------------------------------|--------------------------------------------------|---------------------------------------------------|
| **ROI yang tumpang tindih**            | Teks dapat dikembalikan dua kali.               | Jaga poligon tidak bersinggungan atau deduplikasi output. |
| **ROI di luar batas gambar**           | Mesin mungkin mengeluarkan error atau tidak mengembalikan apa‑apa. | Batasi koordinat ke `0 ≤ x < width`, `0 ≤ y < height`. |
| **ROI sangat kecil**                   | Akurasi OCR menurun karena piksel tidak cukup.   | Perbesar poligon beberapa piksel atau tingkatkan resolusi gambar terlebih dahulu. |
| **Bentuk tidak persegi panjang**       | Beberapa mesin hanya mendukung poligon konveks. | Pecah bentuk kompleks menjadi beberapa ROI konveks. |
| **Ukuran gambar berubah**              | Koordinat yang di‑hardcode menjadi tidak valid.  | Hitung koordinat ROI relatif terhadap dimensi gambar (misalnya, persentase). |

## Contoh Lengkap yang Berfungsi  

Berikut skrip lengkap yang dapat Anda salin‑tempel dan jalankan (ganti `ocr` dengan pustaka Anda yang sebenarnya).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Jalankan dengan `python ocr_roi_example.py` dan Anda akan melihat string yang diekstrak dari dua zona yang didefinisikan.

## Langkah Selanjutnya  

- **Generasi ROI dinamis:** Alih‑alih meng‑hardcode koordinat, gunakan pemrosesan gambar (misalnya, deteksi kontur OpenCV) untuk secara otomatis menemukan tabel atau bidang.  
- **Pasca‑pemrosesan:** Hilangkan spasi berlebih, terapkan regex, atau ubah angka ke tipe data yang tepat.  
- **Pemrosesan batch:** Loop melalui folder gambar, gunakan kembali definisi ROI yang sama jika tata letaknya konsisten.  

Jika Anda penasaran tentang **ocr pada area terpilih** untuk dokumen yang lebih kompleks—misalnya PDF multi‑halaman atau formulir yang dipindai—telusuri pustaka yang mendukung pendaftaran ROI per halaman.  

---  

### Gambaran Visual  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="create roi polygon example showing two selected areas"}

Diagram memperlihatkan bagaimana dua persegi panjang (biru dan hijau) dipetakan ke gambar di bawah, menyoroti tepat apa yang akan dibaca oleh mesin OCR.

---  

## Kesimpulan  

Kami baru saja **membuat objek poligon ROI**, mendaftarkannya ke mesin OCR, dan melakukan `ocr pada area terpilih` dalam skrip yang bersih dan dapat direproduksi. Dengan membatasi mesin ke zona yang Anda pedulikan, Anda mengurangi waktu pemrosesan, meningkatkan akurasi, dan membuat penanganan data selanjutnya jauh lebih sederhana.  

Cobalah dengan gambar Anda sendiri—ubah koordinat, tambahkan lebih banyak poligon, atau hubungkan output ke basis data. Langit adalah batasnya setelah Anda menguasai OCR berbasis region.  

Punya pertanyaan atau ingin berbagi kasus penggunaan menarik? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}