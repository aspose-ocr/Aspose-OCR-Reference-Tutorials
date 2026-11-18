---
category: general
date: 2026-04-26
description: Mengenali teks tulisan tangan menggunakan mesin OCR Python. Pelajari
  cara mengekstrak teks dari gambar, mengaktifkan mode tulisan tangan, dan membaca
  catatan tulisan tangan dengan cepat.
draft: false
keywords:
- recognize handwritten text
- extract text from image
- read handwritten notes
- turn on handwritten mode
- create OCR engine python
language: id
og_description: Mengenali teks tulisan tangan dengan Python. Tutorial ini menunjukkan
  cara mengekstrak teks dari gambar, mengaktifkan mode tulisan tangan, dan membaca
  catatan tulisan tangan menggunakan mesin OCR sederhana.
og_title: Mengenali teks tulisan tangan di Python – Panduan OCR Lengkap
tags:
- OCR
- Python
- Handwriting Recognition
title: Mengenali teks tulisan tangan di Python – Tutorial Mesin OCR
url: /id/python/general/recognize-handwritten-text-in-python-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks tulisan tangan di Python – Tutorial Mesin OCR

Pernah butuh **mengenali teks tulisan tangan** tetapi merasa terjebak pada “dari mana saya mulai?”? Anda tidak sendirian. Baik Anda mendigitalkan coretan rapat atau mengambil data dari formulir yang dipindai, mendapatkan hasil OCR yang dapat diandalkan bisa terasa seperti mengejar unicorn.  

Berita baik: dengan hanya beberapa baris Python Anda dapat **extract text from image** file, **turn on handwritten mode**, dan akhirnya **read handwritten notes** tanpa mencari perpustakaan yang obscure. Dalam panduan ini kami akan melangkah melalui seluruh proses, dari pengaturan gaya **create OCR engine python** hingga mencetak hasil di layar.

## Apa yang Akan Anda Pelajari

- Cara membuat instance **create OCR engine python** menggunakan paket `ocr`.  
- Pengaturan bahasa mana yang memberi Anda dukungan tulisan tangan bawaan.  
- Pemanggilan tepat untuk **turn on handwritten mode** sehingga mesin tahu Anda menangani tulisan kursif.  
- Cara memberi gambar catatan dan **recognize handwritten text** darinya.  
- Tips untuk menangani berbagai format gambar, memecahkan masalah umum, dan memperluas solusi.

Tanpa basa-basi, tanpa dead‑ends “see the docs”—hanya skrip lengkap yang dapat dijalankan yang dapat Anda salin‑tempel dan uji hari ini.

## Prasyarat

1. Python 3.8+ terpasang (kode menggunakan f‑strings).  
2. Pustaka `ocr` hipotetik (`pip install ocr‑engine` – ganti dengan nama paket nyata yang Anda gunakan).  
3. File gambar yang jelas dari catatan tulisan tangan (JPEG, PNG, atau TIFF).  
4. Sedikit rasa ingin tahu—semua hal lainnya dibahas di bawah.

> **Pro tip:** Jika gambar Anda berisik, jalankan langkah pra‑pemrosesan cepat dengan Pillow (mis., `Image.open(...).convert('L')`) sebelum mengirimnya ke mesin OCR. Ini sering meningkatkan akurasi.

## Cara mengenali teks tulisan tangan dengan Python

Berikut adalah skrip lengkap yang **creates OCR engine python** objects, configures them for handwriting, and prints the extracted string. Simpan sebagai `handwriting_ocr.py` dan jalankan dari terminal Anda.

```python
# handwriting_ocr.py
import ocr                     # The OCR library that provides OcrEngine
import os

def main():
    # Step 1: Create an OCR engine instance
    # This is the core object that will do all the heavy lifting.
    ocr_engine = ocr.OcrEngine()

    # Step 2: Choose a language that includes handwritten support.
    # EXTENDED_LATIN covers most Western alphabets and knows how to
    # handle cursive strokes.
    ocr_engine.set_language(ocr.Language.EXTENDED_LATIN)

    # Step 3: Turn on handwritten mode.
    # Without this flag the engine assumes printed text and will miss
    # most of the nuances in a scribble.
    ocr_engine.enable_handwritten_mode(True)

    # Step 4: Define the path to your handwritten image.
    # Replace the placeholder with the actual location of your file.
    image_path = os.path.join("YOUR_DIRECTORY", "handwritten_note.jpg")

    # Basic validation – makes debugging easier.
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 5: Recognize text from the image.
    # The recognize_image method returns a result object that holds
    # both the raw text and confidence scores.
    handwritten_result = ocr_engine.recognize_image(image_path)

    # Step 6: Display the extracted text.
    # This is where you finally **read handwritten notes** programmatically.
    print("=== Extracted Text ===")
    print(handwritten_result.text)

if __name__ == "__main__":
    main()
```

### Output yang Diharapkan

Ketika skrip berhasil dijalankan, Anda akan melihat sesuatu seperti:

```
=== Extracted Text ===
Meeting notes:
- Discuss quarterly targets
- Assign tasks to Alice & Bob
- Follow‑up email by Friday
```

Jika mesin OCR tidak dapat mendeteksi karakter apa pun, bidang `text` akan menjadi string kosong. Dalam kasus itu, periksa kembali kualitas gambar atau coba pemindaian dengan resolusi lebih tinggi.

## Penjelasan Langkah‑per‑Langkah

### Langkah 1 – instance **create OCR engine python**

Kelas `OcrEngine` adalah titik masuk. Anggaplah seperti buku catatan kosong—tidak ada yang terjadi sampai Anda memberi tahu bahasa yang diharapkan dan apakah Anda menangani tulisan tangan.

### Langkah 2 – Pilih bahasa yang mendukung tulisan tangan

`ocr.Language.EXTENDED_LATIN` bukan hanya “English”. Ia menggabungkan sekumpulan skrip berbasis Latin dan, yang penting, menyertakan model yang dilatih pada contoh tulisan kursif. Melewatkan langkah ini sering menghasilkan output berantakan karena mesin default ke model teks cetak.

### Langkah 3 – **turn on handwritten mode**

Memanggil `enable_handwritten_mode(True)` mengubah flag internal. Mesin kemudian beralih ke jaringan saraf yang disetel untuk spasi tidak teratur dan lebar goresan variabel yang Anda lihat pada catatan dunia nyata. Lupa baris ini adalah kesalahan umum; mesin akan memperlakukan coretan Anda sebagai noise.

### Langkah 4 – Beri gambar dan **recognize handwritten text**

`recognize_image` melakukan pekerjaan berat: ia mempraproses bitmap, menjalankannya melalui model tulisan tangan, dan mengembalikan objek dengan atribut `text`. Anda juga dapat memeriksa `handwritten_result.confidence` jika membutuhkan metrik kualitas.

### Langkah 5 – Cetak hasil dan **read handwritten notes**

`print(handwritten_result.text)` adalah cara paling sederhana untuk memverifikasi bahwa Anda berhasil **extract text from image**. Dalam produksi Anda mungkin akan menyimpan string ke basis data atau mengirimnya ke layanan lain.

## Menangani Kasus Edge & Variasi Umum

| Situasi | Apa yang Harus Dilakukan |
|-----------|------------|
| **Gambar diputar** | Gunakan Pillow untuk memutar (`Image.rotate(angle)`) sebelum memanggil `recognize_image`. |
| **Kontras rendah** | Ubah menjadi grayscale dan terapkan threshold adaptif (`Image.point(lambda p: p > 128 and 255)`). |
| **Beberapa halaman** | Loop melalui daftar path file dan gabungkan hasil. |
| **Skrip non‑Latin** | Ganti `EXTENDED_LATIN` dengan `ocr.Language.CHINESE` (atau yang sesuai) dan pertahankan `enable_handwritten_mode(True)`. |
| **Kekhawatiran performa** | Gunakan kembali instance `ocr_engine` yang sama untuk banyak gambar; menginisialisasinya setiap kali menambah overhead. |

### Pro tip tentang penggunaan memori

Jika Anda memproses ratusan catatan dalam satu batch, panggil `ocr_engine.dispose()` setelah selesai. Ini membebaskan sumber daya native yang mungkin dipegang oleh wrapper Python.

## Ringkasan Visual Cepat

![contoh mengenali teks tulisan tangan](https://example.com/handwritten-note.png "contoh mengenali teks tulisan tangan")

*Gambar di atas menunjukkan catatan tulisan tangan tipikal yang dapat diubah skrip kami menjadi teks biasa.*

## Contoh Kerja Penuh (Skrip Satu‑File)

Untuk mereka yang suka kesederhanaan copy‑paste, berikut seluruhnya lagi tanpa komentar penjelasan:

```python
import ocr, os

ocr_engine = ocr.OcrEngine()
ocr_engine.set_language(ocr.Language.EXTENDED_LATIN)
ocr_engine.enable_handwritten_mode(True)

img = os.path.join("YOUR_DIRECTORY", "handwritten_note.jpg")
if not os.path.isfile(img):
    raise FileNotFoundError(f"Image not found: {img}")

result = ocr_engine.recognize_image(img)
print("=== Extracted Text ===")
print(result.text)
```

Jalankan dengan:

```bash
python handwriting_ocr.py
```

Anda sekarang harus melihat output **recognize handwritten text** di konsol Anda.

## Kesimpulan

Kami baru saja membahas semua yang Anda butuhkan untuk **recognize handwritten text** di Python—dimulai dari pemanggilan **create OCR engine python** yang baru, memilih bahasa yang tepat, **turn on handwritten mode**, dan akhirnya **extract text from image** untuk **read handwritten notes**.  

Dalam satu skrip mandiri Anda dapat beralih dari foto buram coretan rapat ke teks bersih yang dapat dicari. Selanjutnya, pertimbangkan mengirim output ke pipeline bahasa alami, menyimpannya di indeks yang dapat dicari, atau bahkan mengirimnya kembali ke layanan transkripsi untuk menghasilkan suara.

### Kemana Selanjutnya?

- **Pemrosesan batch:** Bungkus skrip dalam loop untuk menangani folder pemindaian.  
- **Penyaringan kepercayaan:** Gunakan `result.confidence` untuk membuang bacaan berkualitas rendah.  
- **Pustaka alternatif:** Jika `ocr` tidak cocok, jelajahi `pytesseract` dengan `--psm 13` untuk mode tulisan tangan.  
- **Integrasi UI:** Gabungkan dengan Flask atau FastAPI untuk menawarkan layanan unggah berbasis web.

Memiliki pertanyaan tentang format gambar tertentu atau butuh bantuan menyetel model? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}