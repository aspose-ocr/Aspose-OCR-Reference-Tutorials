---
category: general
date: 2026-05-03
description: Ekstrak teks dari gambar dengan Python menggunakan Aspose OCR. Pelajari
  tutorial OCR Python langkah demi langkah dengan dukungan campuran Latin‑Cyrillic.
draft: false
keywords:
- extract text from image python
- Aspose OCR Python
- image to text conversion
- mixed language OCR
- Python OCR tutorial
language: id
og_description: Ekstrak teks dari gambar dengan Python secara cepat. Panduan ini menunjukkan
  cara menggunakan Aspose OCR di Python untuk gambar campuran Latin‑Cyrillic.
og_title: Ekstrak Teks dari Gambar Python – Panduan Lengkap Aspose OCR
tags:
- OCR
- Python
- Aspose
title: Ekstrak Teks dari Gambar dengan Python – Panduan Lengkap Aspose OCR
url: /id/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar Python – Panduan Lengkap Aspose OCR

Pernahkah Anda perlu **extract text from image python** tetapi tidak yakin pustaka mana yang dapat menangani campuran karakter Latin dan Cyrillic? Anda bukan satu-satunya—para pengembang terus-menerus menghadapi masalah itu saat melakukan OCR pada screenshot multibahasa.  

Kabar baiknya, Aspose OCR untuk Python membuat seluruh proses hampir tanpa rasa sakit. Dalam tutorial ini kami akan menjelaskan cara menginstal paket, menerapkan lisensi Anda, memuat gambar berbahasa campuran, dan akhirnya mengambil teks yang dikenali dengan beberapa baris kode. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang dapat Anda masukkan ke dalam proyek apa pun.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan **Aspose OCR Python** dalam lingkungan virtual.  
- Mengapa memberi petunjuk bahasa (seperti Latin dan Cyrillic) mempercepat deteksi.  
- Kode tepat yang diperlukan untuk **extract text from image python** dengan satu panggilan fungsi.  
- Jebakan umum saat menangani OCR berbahasa campuran dan cara menghindarinya.  

### Prasyarat

- Python 3.8 atau yang lebih baru terpasang di mesin Anda.  
- File lisensi Aspose OCR (`Aspose.OCR.Java.lic`). Versi percobaan gratis dapat digunakan untuk pengujian, tetapi file berlisensi menghilangkan watermark.  
- Gambar PNG/JPEG yang berisi karakter Latin dan Cyrillic (kami akan menyebutnya `mixed_latin_cyrillic.png`).  

Jika Anda telah mencentang kotak-kotak tersebut, Anda siap melanjutkan—tidak memerlukan kerangka kerja tambahan atau dependensi berat.

---

## Langkah 1 – Ekstrak Teks dari Gambar Python: Instal Aspose OCR

Hal pertama yang harus dilakukan: dapatkan pustaka dari PyPI dan pastikan lingkungan Anda dapat menemukan file lisensi.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the Aspose OCR package
pip install asposeocrcloud
```

> **Pro tip:** Jika Anda mengalami error izin, tambahkan `--user` ke perintah `pip install` atau jalankan terminal sebagai administrator.

Setelah paket berada di sistem Anda, kami akan mengimpornya dan mengarahkan mesin ke lisensi kami.

```python
import asposeocrcloud as ocr   # the library we just installed

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with the actual location of your .lic file
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")
```

Mengapa kami memerlukan lisensi pada tahap ini? Tanpa lisensi, mesin berjalan dalam **evaluation mode**, yang membatasi jumlah halaman dan menambahkan watermark pada output. Menyediakan lisensi di awal memastikan panggilan `recognize` selanjutnya mengembalikan teks bersih.

---

## Langkah 2 – Muat Gambar Anda dengan Konten Latin‑Cyrillic Campuran

Selanjutnya, kami memuat gambar ke memori. Aspose OCR bekerja dengan kelas `Image` miliknya, yang mengabstraksi format file yang mendasarinya.

```python
# Load the image that contains both Latin and Cyrillic characters
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")
```

Jika Anda bertanya-tanya apakah format lain berfungsi—ya, JPEG, BMP, TIFF, bahkan PDF didukung. Cukup ganti ekstensi file dan metode `from_file` akan menangani sisanya.

---

## Langkah 3 – Beri Petunjuk Bahasa untuk Deteksi Lebih Cepat (Opsional tetapi Membantu)

Ketika Anda mengetahui bahasa yang ada dalam gambar, Anda dapat memberi mesin petunjuk. Ini tidak wajib, tetapi **secara signifikan mengurangi waktu pemrosesan** dan meningkatkan akurasi untuk OCR berbahasa campuran.

```python
# Provide language hints: Latin and Cyrillic
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]
```

Daftar petunjuk menerima bahasa apa pun yang didukung oleh Aspose OCR (mis., `"Arabic"`, `"Japanese"`). Jika Anda melewatkan langkah ini, mesin akan mencoba setiap bahasa bawaan, yang dapat lebih lambat pada batch besar.

---

## Langkah 4 – Jalankan Mesin OCR dan Ekstrak Teks

Kini saatnya menguji: sebenarnya mengenali karakter. Metode `recognize` mengembalikan objek `OcrResult` yang berisi teks polos, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti.

```python
# Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)

# The recognised text is available via the .text attribute
extracted_text = ocr_result.text
```

> **Mengapa ini berhasil:** Di balik layar, Aspose OCR menggabungkan detektor teks jaringan saraf dengan classifier khusus bahasa. Dengan memberi objek `Image`, Anda menghindari kebutuhan pra‑pemrosesan manual seperti binarisasi.

---

## Langkah 5 – Lihat Teks yang Diekstrak

Akhirnya, mari cetak hasilnya ke konsol. Dalam aplikasi nyata Anda mungkin menuliskannya ke file, mengirimnya ke basis data, atau memasukkannya ke API terjemahan.

```python
print("Recognised text:")
print(extracted_text)
```

Saat Anda menjalankan skrip, Anda akan melihat sesuatu seperti:

```
Recognised text:
Hello мир! This is a test.
```

Output tersebut mengonfirmasi bahwa kami berhasil **extract text from image python**, menangani karakter Latin dan Cyrillic dalam satu proses.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah skrip lengkap yang dapat Anda salin‑tempel ke file bernama `extract_ocr.py`. Ganti saja jalur placeholder dengan direktori Anda yang sebenarnya.

```python
import asposeocrcloud as ocr   # package installed via pip

# ------------------------------------------------------------
# Step 1 – Initialise engine and apply license
# ------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")   # path to your license file

# ------------------------------------------------------------
# Step 2 – Load the image (mixed Latin‑Cyrillic)
# ------------------------------------------------------------
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")

# ------------------------------------------------------------
# Step 3 – (Optional) Hint the languages present
# ------------------------------------------------------------
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]

# ------------------------------------------------------------
# Step 4 – Run OCR
# ------------------------------------------------------------
ocr_result = ocr_engine.recognize(input_image)

# ------------------------------------------------------------
# Step 5 – Display the recognised text
# ------------------------------------------------------------
print("Recognised text:")
print(ocr_result.text)
```

Simpan file, aktifkan lingkungan virtual Anda, dan jalankan:

```bash
python extract_ocr.py
```

Anda akan melihat teks yang dikenali tercetak, mengonfirmasi skrip berfungsi dari awal hingga akhir.

---

## Pertanyaan yang Sering Diajukan & Kasus Pojok

**Bagaimana jika gambar blur?**  
Aspose OCR menyertakan de‑skewing dan pengurangan noise bawaan, tetapi untuk foto yang sangat terdegradasi Anda mungkin ingin pra‑memproses dengan OpenCV (mis., menerapkan Gaussian blur dan threshold). Kelas `Image` juga dapat menerima array NumPy, sehingga Anda dapat menambahkan filter khusus sebelum memanggil `recognize`.

**Bisakah saya memproses seluruh folder gambar?**  
Tentu saja. Bungkus logika dalam loop `for`, ubah `from_file` untuk membaca setiap nama file, dan simpan hasilnya dalam kamus. Ingat untuk menghormati batas laju API jika Anda menggunakan versi cloud.

**Apakah saya memerlukan lisensi terpisah untuk setiap bahasa?**  
Tidak, satu lisensi Aspose OCR mencakup semua bahasa yang didukung. Daftar `language_hints` hanyalah petunjuk untuk meningkatkan performa.

**Bagaimana dengan input PDF?**  
Ganti `Image.from_file` dengan `ocr.Image.from_file("document.pdf")`. Mesin OCR akan secara otomatis meraster setiap halaman dan mengembalikan teks yang digabungkan.

---

## Kesimpulan

Kami baru saja menunjukkan cara singkat dan siap produksi untuk **extract text from image python** menggunakan Aspose OCR. Langkah‑langkah—instal, lisensi, muat, beri petunjuk bahasa, kenali, dan tampilkan—mencakup semua yang Anda butuhkan untuk mendapatkan hasil yang dapat diandalkan untuk konten Latin‑Cyrillic campuran.  

Dari sini Anda dapat menjelajahi topik lanjutan seperti **image to text conversion** untuk pemrosesan batch, mengintegrasikan output dengan **Python OCR tutorial** tentang pemrosesan bahasa alami, atau bereksperimen dengan petunjuk bahasa lain untuk dokumen multibahasa. Tidak ada batasan, dan kode sudah ada di tangan Anda.

Memiliki kasus penggunaan lain atau mengalami masalah? Tinggalkan komentar, bagikan pengalaman Anda, dan mari teruskan diskusinya. Selamat coding!  

![Extract text from image python example](/images/extract-text-from-image-python.png "Screenshot showing OCR output – extract text from image python")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}