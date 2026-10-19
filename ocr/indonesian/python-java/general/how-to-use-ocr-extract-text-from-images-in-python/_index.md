---
category: general
date: 2026-03-18
description: Cara menggunakan OCR untuk mengekstrak teks dari gambar – panduan cepat
  untuk mengenali teks dari file PNG dan memuat gambar untuk OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: id
og_description: Cara menggunakan OCR untuk mengekstrak teks dari gambar – pelajari
  cara mengenali teks dari PNG, memuat gambar untuk OCR, dan mengekstrak teks dengan
  skrip Python sederhana.
og_title: 'Cara Menggunakan OCR: Mengekstrak Teks dari Gambar dengan Python'
tags:
- OCR
- Python
- Image Processing
title: 'Cara Menggunakan OCR: Mengekstrak Teks dari Gambar dengan Python'
url: /id/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR: Mengekstrak Teks dari Gambar dengan Python

Pernah bertanya-tanya **bagaimana cara menggunakan OCR** ketika Anda memiliki screenshot berantakan atau kwitansi yang dipindai? Anda tidak sendirian—para pengembang terus-menerus perlu mengambil teks yang dapat dibaca dari gambar, terutama PNG yang berasal dari aplikasi seluler atau unggahan web. Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang dapat dijalankan yang menunjukkan cara **mengekstrak teks dari file gambar**, **mengenali teks dari aset PNG**, dan bahkan **memuat gambar untuk OCR** hanya dengan beberapa baris Python.

Kami akan membahas semuanya mulai dari menginstal pustaka yang tepat hingga menangani dokumen multibahasa, sehingga pada akhir Anda akan tahu persis *bagaimana mengekstrak teks* dari gambar apa pun yang Anda beri ke mesin. Tanpa referensi yang samar, hanya solusi langkah‑demi‑langkah yang jelas yang dapat Anda salin‑tempel dan jalankan.

## Apa yang Akan Anda Pelajari

Di beberapa bagian berikut kami akan:

1. Menyiapkan mesin OCR ringan (tanpa ketergantungan berat).  
2. Memuat file gambar—khususnya PNG—ke dalam mesin.  
3. Mengaktifkan deteksi bahasa otomatis sehingga mesin dapat menangani konten multibahasa.  
4. Menjalankan proses pengenalan dan mengambil hasil teks polos.  
5. Menyesuaikan alur kerja untuk kasus tepi seperti file yang hilang atau format yang tidak didukung.

Jika Anda nyaman dengan Python dasar, Anda siap. Tidak diperlukan pengalaman OCR sebelumnya, meskipun sekilas melihat dokumentasi pustaka tidak ada salahnya.

---

![Cara menggunakan OCR pada gambar PNG](placeholder.png "Cara menggunakan OCR pada gambar PNG – panduan langkah demi langkah")

## Cara Menggunakan OCR – Memuat Gambar dan Mengenali Teks {#how-to-use-ocr}

### Langkah 1: Instal pustaka OCR

Hal pertama yang perlu dilakukan, Anda memerlukan paket Python yang menyediakan kelas `OcrEngine`. Untuk tujuan tutorial ini kami akan menggunakan paket fiktif namun ilustratif **SimpleOCR**, yang dapat Anda instal via pip:

```bash
pip install simple-ocr
```

> **Pro tip:** Jika Anda bekerja di dalam lingkungan virtual (sangat disarankan), aktifkan terlebih dahulu sebelum menjalankan perintah instalasi. Ini menjaga ketergantungan proyek Anda tetap rapi.

### Langkah 2: Impor mesin dan buat sebuah instance

Membuat mesin semudah memanggil konstruktornya. Anggap mesin sebagai “otak” yang nanti akan memproses gambar yang Anda berikan.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Mengapa kita membuat instance baru setiap kali? Karena isolasi. Mesin yang baru menjamin tidak ada status sisa dari run sebelumnya yang mencemari pengenalan saat ini, yang sangat penting ketika Anda memproses banyak file dalam satu batch.

### Langkah 3: Muat gambar yang ingin Anda proses

Sekarang kita benar‑benar **memuat gambar untuk OCR**. Metode `setImageFromFile` menerima path ke gambar raster apa pun; kami akan menunjuk ke PNG bernama `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Jika file tidak ditemukan, `SimpleOCR` akan melempar `FileNotFoundError` yang jelas. Anda dapat menangkapnya untuk memberikan pesan error yang ramah:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Langkah 4: Aktifkan deteksi bahasa otomatis

Sebagian besar mesin OCR modern dilengkapi paket bahasa. Dengan memberikan `"multilingual"` kami memberi tahu mesin untuk mencium teks dan secara otomatis memilih model bahasa yang tepat. Ini sangat berguna ketika PNG Anda berisi campuran bahasa Inggris dan Spanyol, misalnya.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Jika Anda sudah mengetahui bahasa sebelumnya, Anda dapat mengganti `"multilingual"` dengan locale spesifik seperti `"eng"` atau `"spa"` untuk mempercepat proses.

### Langkah 5: Jalankan proses pengenalan

Inilah bagian yang melakukan pekerjaan berat. `recognize()` memindai gambar, menerapkan segmentasi, menjalankan jaringan saraf, dan membangun buffer teks secara internal.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Di balik layar mesin melakukan:

- **Pra‑pemrosesan** (deskewing, binarisasi)  
- **Analisis tata letak** (mendeteksi kolom, tabel)  
- **Klasifikasi karakter** (menggunakan model deep‑learning)  

Semua itu diabstraksikan, itulah mengapa Anda hanya memerlukan satu baris kode.

### Langkah 6: Ambil dan cetak teks yang dikenali

Akhirnya, kami mengambil objek hasil dan mengekstrak string polos. Inilah bagian di mana Anda benar‑benar **mengekstrak teks dari gambar**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Output yang diharapkan** (dipotong untuk singkat):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Jika gambar tidak mengandung karakter yang dapat dikenali, `text` akan menjadi string kosong. Anda dapat melindungi terhadap hal itu:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Mengekstrak Teks dari Gambar – Menangani Kasus Tepi Umum

### Banyak bahasa dalam satu file

Ketika dokumen mencampur bahasa, pengaturan `"multilingual"` biasanya bekerja dengan baik. Namun, jika Anda melihat kesalahan pengenalan, Anda dapat secara manual menentukan daftar fallback:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Format non‑PNG

Meskipun fokus kami adalah **mengenali teks dari PNG**, `SimpleOCR` juga menerima JPEG, BMP, dan TIFF. Cukup ubah ekstensi file di `setImageFromFile`. Untuk tumpukan TIFF, Anda mungkin perlu memilih halaman tertentu:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### File besar dan penggunaan memori

Jika Anda memproses pemindaian gigapiksel, pertimbangkan untuk mengubah ukuran sebelum OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Mengubah ukuran mengurangi tekanan memori sambil mempertahankan detail yang cukup untuk pengenalan yang akurat.

### Debugging gagal memuat

Kadang‑kadang gambar terlihat baik secara mata tetapi rusak secara internal. Aktifkan logging verbose untuk melihat apa yang dilihat mesin:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Skrip Lengkap yang Siap Dijalan

Berikut adalah program lengkap yang menyatukan semua bagian. Salin ke file bernama `ocr_demo.py`, sesuaikan placeholder `YOUR_DIRECTORY`, dan jalankan `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Menjalankan skrip ini seharusnya menghasilkan versi teks polos dari apa pun yang ada di dalam `mixed_doc.png`. Jangan ragu mengganti file dengan gambar lain—**cara mengekstrak teks** bekerja dengan cara yang sama.

---

## Kesimpulan

Kami baru saja menelusuri **cara menggunakan OCR** di Python untuk **mengekstrak teks dari file gambar**, khususnya berfokus pada **mengenali teks dari PNG** dan langkah‑langkah praktis untuk **memuat gambar untuk OCR**. Potongan kode di atas adalah solusi mandiri: instal paket, beri file, aktifkan deteksi multibahasa, jalankan mesin, dan ambil hasilnya.

Dari sini Anda dapat:

- Mengintegrasikan skrip ke layanan web yang menerima unggahan pengguna.  
- Memproses batch folder PDF yang dikonversi ke PNG.  
- Menambahkan pasca‑pemrosesan (misalnya pembersihan regex, pemeriksaan ejaan) untuk meningkatkan akurasi.

Ingat, kualitas OCR bergantung pada kejernihan gambar, paket bahasa yang tepat, dan kadang‑kadang sedikit pra‑pemrosesan—jadi bereksperimenlah

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}