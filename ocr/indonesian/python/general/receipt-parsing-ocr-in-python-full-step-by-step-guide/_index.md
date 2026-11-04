---
category: general
date: 2026-06-28
description: Pemrosesan OCR struk dalam Python menjadi mudah – pelajari cara mengekstrak
  data struk, memuat OCR gambar, dan lihat contoh lengkap OCR Python.
draft: false
keywords:
- receipt parsing OCR
- how to extract receipt
- python ocr example
- load image ocr
- how to ocr receipt
language: id
og_description: 'Pemrosesan struk OCR di Python: pelajari cara mengekstrak data struk,
  memuat OCR gambar, dan menjalankan contoh OCR Python lengkap dalam hitungan menit.'
og_title: Parsing Resi OCR dengan Python – Panduan Langkah‑Demi‑Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Receipt parsing OCR in Python made easy – learn how to extract receipt
    data, load image OCR, and see a complete python OCR example.
  headline: Receipt Parsing OCR in Python – Full Step‑By‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- receipt parsing
- image processing
title: Parsing Struk OCR di Python – Panduan Lengkap Langkah demi Langkah
url: /id/python/general/receipt-parsing-ocr-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsing Resi OCR di Python – Panduan Langkah‑ demi‑Langkah Lengkap

Pernah bertanya-tanya bagaimana mengubah resi supermarket yang buram menjadi JSON yang bersih dan dapat dicari? **Receipt parsing OCR** adalah jawabannya, dan Anda tidak memerlukan gelar PhD dalam computer vision untuk membuatnya bekerja. Dalam tutorial ini kami akan membahas contoh **python ocr example** praktis yang memuat gambar, menjalankan pengenalan teks terstruktur, dan menghasilkan string JSON yang diformat dengan rapi—sempurna untuk dimasukkan ke dalam perangkat lunak pembukuan atau pipeline analitik. Kami juga akan menjawab pertanyaan penting: **how to extract receipt** data secara andal, bahkan ketika pemindaian tidak sempurna. Pada akhir tutorial Anda akan memiliki skrip yang dapat digunakan kembali dan dapat dimasukkan ke dalam proyek Python apa pun, baik Anda sedang membangun aplikasi keuangan pribadi atau sistem pelacakan pengeluaran tingkat perusahaan.

## Apa yang Akan Anda Pelajari

* Cara menyiapkan engine OCR ringan di Python.  
* Langkah tepat untuk **load image OCR** pada file resi.  
* Cara memanggil metode pengenalan terstruktur dan mengubah hasilnya menjadi JSON.  
* Tips menangani kasus tepi umum—resi yang diputar, kontras rendah, dan karakter Unicode.  
* Contoh kode lengkap yang siap disalin‑tempel yang dapat Anda jalankan hari ini.

### Prasyarat

* Python 3.8 atau yang lebih baru terinstal di mesin Anda.  
* Sebuah perpustakaan OCR yang menyediakan kelas `OcrEngine` dan helper `Image` (banyak perpustakaan menyediakan API serupa; untuk panduan ini kami mengasumsikan pembungkus generik).  
* Gambar resi (`receipt.png`) ditempatkan dalam folder yang dapat Anda referensikan.  
* Opsional namun disarankan: `pip install pillow` untuk penanganan gambar dan ketergantungan tambahan yang dibutuhkan perpustakaan OCR Anda.

Jika Anda belum memiliki salah satu dari ini, instal sekarang—tidak sulit, cukup satu baris perintah untuk kebanyakan paket.

---

## Receipt Parsing OCR – Langkah 1: Instal dan Impor Modul yang Diperlukan

Pertama-tama, mari siapkan lingkungan Python. Kami akan mengimpor `json` untuk serialisasi dan kelas khusus OCR.

```python
# Step 1: Import required modules
import json                     # Built‑in JSON handling
from ocr_library import OcrEngine, Image   # Replace with your actual library
```

*Mengapa ini penting*: Mengimpor di bagian atas menjaga skrip tetap rapi dan memastikan engine OCR tersedia di seluruh skrip. Jika Anda lupa mengimpor `json`, pemanggilan `json.dumps` nanti akan menghasilkan `NameError`.

**Pro tip**: Jika perpustakaan OCR Anda berada di namespace yang berbeda (misalnya, `easyocr` atau `pytesseract`), sesuaikan baris impor sesuai. Sisanya tutorial tetap sama.

---

## Cara Mengekstrak Data Resi – Langkah 2: Buat Instance Engine OCR

Sekarang kita mengaktifkan engine. Anggap `OcrEngine()` sebagai otak yang akan membaca resi.

```python
# Step 2: Create an OCR engine instance
engine = OcrEngine()
```

Sebagian besar SDK OCR modern memungkinkan Anda mengkonfigurasi paket bahasa atau mode deteksi di sini. Untuk resi tipikal, Anda akan menginginkan bahasa Inggris (atau bahasa resi) dan mode “structured” jika tersedia.

> **Catatan**: Jika perpustakaan Anda memerlukan kunci lisensi, berikan sebagai argumen: `engine = OcrEngine(api_key="YOUR_KEY")`.

---

## Load Image OCR – Langkah 3: Arahkan Engine ke Resi Anda

Dengan engine siap, kita perlu memberi file gambar kepadanya. Di sinilah **load image OCR** berperan.

```python
# Step 3: Load the image to be processed
engine.set_image(Image.from_file("YOUR_DIRECTORY/receipt.png"))
```

*Apa yang terjadi*: `Image.from_file` membaca PNG (atau JPG, TIFF, dll.) dan membungkusnya dalam format yang dipahami engine OCR. Jika resi Anda berupa PDF, konversi halaman pertama menjadi gambar terlebih dahulu—banyak perpustakaan menyediakan helper `pdf2image`.

**Kasus khusus**: Resi yang dipindai terbalik masih dapat dibaca jika Anda memutarnya:

```python
# Optional: auto‑rotate if needed
image = Image.from_file("YOUR_DIRECTORY/receipt.png")
image = image.rotate(180) if image.is_upside_down() else image
engine.set_image(image)
```

---

## Cara OCR Resi – Langkah 4: Jalankan Pengenalan Teks Terstruktur

Sekarang keajaiban terjadi. Kami meminta engine melakukan pemindaian terstruktur, yang berusaha mengelompokkan item, total, dan tanggal.

```python
# Step 4: Perform structured text recognition
result = engine.recognize_structured()
```

Jika perpustakaan OCR Anda hanya menawarkan metode `recognize()` biasa, Anda masih dapat mengekstrak bidang secara manual, tetapi `recognize_structured()` biasanya mengembalikan kamus dengan kunci seperti `items`, `total`, dan `date`.

---

## Contoh Python OCR – Langkah 5: Konversi Hasil ke JSON

Objek hasil mentah biasanya merupakan kelas khusus. Mengkonversinya menjadi dict Python biasa memudahkan serialisasi.

```python
# Step 5: Convert the recognition result to a nicely formatted JSON string
json_str = json.dumps(result.to_dict(), ensure_ascii=False, indent=2)
```

*Mengapa `ensure_ascii=False`?* Resi dapat berisi simbol mata uang (€, £) atau karakter beraksen. Flag ini mempertahankannya alih‑alih mengubah menjadi `\u00e9`.

---

## Cara Mengekstrak Resi – Langkah 6: Output Representasi JSON

Akhirnya, kami mencetak (atau menulis) JSON sehingga Anda dapat mengirimkannya ke database, spreadsheet, atau API.

```python
# Step 6: Output the JSON representation of the recognized data
print(json_str)
```

**Output yang diharapkan** (dicetak rapi untuk kemudahan membaca):

```json
{
  "merchant": "Coffee House",
  "date": "2024-03-15",
  "items": [
    {"name": "Latte", "quantity": 1, "price": "3.50"},
    {"name": "Bagel", "quantity": 2, "price": "4.00"}
  ],
  "subtotal": "7.50",
  "tax": "0.60",
  "total": "8.10"
}
```

Jika Anda melihat dict kosong atau bidang yang hilang, periksa kembali bahwa gambar resi jelas dan engine OCR diatur ke bahasa yang tepat.

---

## Pro Tips & Kesalahan Umum (Bagian Bonus)

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Gambar buram atau kontras rendah** | OCR kesulitan dengan noise | Pra‑proses dengan OpenCV: `cv2.threshold` atau `cv2.bilateralFilter` |
| **Resi yang diputar** | Engine mengasumsikan teks dalam posisi tegak | Deteksi orientasi dengan `engine.detect_orientation()` atau putar secara manual (lihat Langkah 3) |
| **Karakter non‑Latin** | Paket bahasa salah | Inisialisasi engine dengan `language="spa"` untuk bahasa Spanyol, dll. |
| **Resi besar menyebabkan error memori** | Seluruh gambar dimuat sekaligus | Potong ke wilayah yang diinginkan: `engine.set_image(image.crop((x, y, w, h)))` |

---

## Apa Selanjutnya? Perluas Alur Kerja

Anda baru saja menguasai **receipt parsing OCR** di Python. Berikut beberapa ide untuk mempertahankan momentum:

* **Batch processing** – iterasi folder berisi gambar resi dan tambahkan setiap JSON ke file utama.  
* **Database insertion** – gunakan `sqlite3` atau `SQLAlchemy` untuk menyimpan setiap resi sebagai baris.  
* **Machine‑learning enrichment** – masukkan item yang diekstrak ke dalam model kategorisasi untuk penandaan pengeluaran.  

Semua ini dibangun di atas langkah inti yang kami bahas, dan masing‑masing akan melibatkan pola **python ocr example** yang sama: load → recognize → serialize → store.

---

## Kesimpulan

Dalam panduan ini kami membahas alur kerja **receipt parsing OCR** lengkap di Python, menunjukkan secara tepat **how to extract receipt** informasi, cara **load image OCR**, dan memberikan contoh **python ocr example** yang dapat dijalankan hari ini. Dengan mengikuti enam langkah—install, import, instantiate, load, recognize, dan serialize—Anda kini memiliki fondasi kuat untuk proyek pemrosesan resi apa pun. Silakan bereksperimen: coba engine OCR yang berbeda, sesuaikan pra‑proses, atau tambahkan penanganan error untuk bidang yang hilang. Tidak ada batasan ketika Anda menggabungkan OCR yang handal dengan fleksibilitas Python. Punya pertanyaan atau variasi menarik pada resep ini? Tinggalkan komentar di bawah dan mari teruskan diskusi.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}