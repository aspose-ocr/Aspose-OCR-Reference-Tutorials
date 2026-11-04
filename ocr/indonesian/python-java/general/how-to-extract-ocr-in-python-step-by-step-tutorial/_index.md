---
category: general
date: 2026-04-26
description: cara mengekstrak OCR dari gambar menggunakan Python – contoh OCR Python
  yang menunjukkan cara memuat gambar untuk OCR dan mengekstrak teks dari struk.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: id
og_description: cara mengekstrak OCR dari gambar menggunakan Python. Pelajari contoh
  OCR Python, muat gambar untuk OCR, dan ekstrak teks dari struk dalam hitungan menit.
og_title: Cara Mengekstrak OCR di Python – Panduan Lengkap
tags:
- OCR
- Python
- Image Processing
title: Cara mengekstrak OCR di Python – Tutorial Langkah demi Langkah
url: /id/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara mengekstrak ocr di Python – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara mengekstrak ocr** dari kwitansi yang buram atau faktur yang dipindai? Anda bukan satu-satunya—para pengembang terus menemui kendala ketika mereka membutuhkan teks bersih yang dapat dibaca mesin dari gambar. Kabar baiknya? Dengan hanya beberapa baris Python Anda dapat mengubah foto kwitansi menjadi teks dengan kepercayaan tinggi yang dapat dicari.

Dalam tutorial ini kami akan membahas **contoh python ocr** yang menunjukkan **cara memuat gambar untuk ocr**, menjalankan mesin, dan hanya menyimpan karakter yang memenuhi ambang kepercayaan 85 %. Pada akhir tutorial Anda akan dapat **mengekstrak teks dari kwitansi** tanpa harus mencari-cari dokumentasi atau menebak parameter API.

## Apa yang Anda Butuhkan

- Python 3.9 atau lebih baru (sintaks yang kami gunakan bekerja pada 3.8+)
- Paket `aocr` (atau perpustakaan OCR apa pun yang menyediakan kelas `OcrEngine`). Instal dengan:

```bash
pip install aocr
```

- Sebuah contoh gambar kwitansi (`receipt.png`) yang ditempatkan di folder yang dapat Anda referensikan.
- Editor teks atau IDE—VS Code, PyCharm, atau bahkan notebook sederhana sudah cukup.

Itu saja. Tanpa kerangka kerja berat, tanpa layanan eksternal, hanya Python murni.

![Hasil OCR kepercayaan tinggi – cara mengekstrak ocr dari kwitansi](/images/ocr-high-confidence.png)

*Image alt text: cara mengekstrak ocr dari kwitansi menggunakan Python OCR*

## Langkah 1 – Buat Instance Mesin OCR (cara mengekstrak ocr)

Hal pertama yang kami lakukan adalah memulai mesin OCR. Anggap saja sebagai otak yang akan membaca piksel untuk kita.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Mengapa?** Menginstansiasi `OcrEngine` memberi Anda objek konfigurasi baru. Anda kemudian dapat menyesuaikan model bahasa, pengaturan DPI, atau langkah pra‑pemrosesan—semua tanpa menyentuh loop pemrosesan inti.

## Langkah 2 – Muat Gambar untuk OCR

Selanjutnya kami mengarahkan mesin ke gambar yang ingin kami analisis. Di sinilah kata kunci **memuat gambar untuk ocr** berperan.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Tip pro:** Jika gambar Anda berada di direktori lain, gunakan `os.path.join` untuk membuat jalur yang independen platform.

**Mengapa memuat gambar dengan cara ini?** Helper `Image.load` membaca file ke dalam format yang dipahami mesin, menangani format umum (PNG, JPEG, TIFF) secara otomatis. Melewatkan langkah ini atau memberi byte mentah akan memunculkan `ValueError`.

## Langkah 3 – Jalankan Proses OCR

Sekarang kami benar‑benar menjalankan OCR. Metode `process` mengembalikan objek hasil yang kaya berisi simbol yang dikenali, skor kepercayaan, dan kotak pembatas.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**Apa yang terkandung dalam `ocr_result`?** Pada kebanyakan perpustakaan, ini meliputi:

- `text`: string mentah yang digabungkan.
- `symbol_confidences`: daftar tuple `(char, confidence)`.
- `boxes`: koordinat untuk setiap karakter (berguna untuk debugging visual).

Memiliki akses ke kepercayaan per‑karakter sangat penting untuk langkah berikutnya.

## Langkah 4 – Simpan Hanya Simbol Kepercayaan Tinggi (≥ 85 %)

Kwitansi sering memiliki noda, cetakan pudar, atau kebisingan latar belakang. Dengan menyaring simbol kepercayaan rendah, kita secara dramatis meningkatkan parsing selanjutnya.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Mengapa 85 %?** Secara empiris, ambang sekitar 0.85 menyeimbangkan recall dan precision untuk kebanyakan kwitansi cetak. Jika Anda melihat angka yang hilang, turunkan ambang; jika Anda mendapatkan teks tak terbaca, naikkan ambang.

## Langkah 5 – Keluarkan Teks Ekstrak Kepercayaan Tinggi

Akhirnya, kami mencetak (atau menyimpan) string yang telah dibersihkan. Ini adalah inti dari alur kerja **mengekstrak teks dari kwitansi** kami.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

Output tipikal terlihat seperti:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

Anda sekarang dapat memasukkan string ini ke penulis CSV, basis data, atau pipeline analitik selanjutnya mana pun.

## Skrip Lengkap, Siap‑Jalankan

Berikut adalah cuplikan kode lengkap yang dapat Anda salin‑tempel ke `ocr_receipt.py` dan jalankan segera.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

Simpan file, pastikan `receipt.png` ada, dan jalankan:

```bash
python ocr_receipt.py
```

Anda akan melihat teks kwitansi yang telah dibersihkan dicetak ke konsol.

## Kasus Pinggir & Skenario What‑If

| Situasi | Perbaikan yang Disarankan |
|-----------|----------------------------|
| **Kepercayaan sangat rendah di seluruh gambar** | Pra‑proses gambar: tingkatkan kontras, konversi ke grayscale, atau terapkan filter pengurangan noise (`cv2.GaussianBlur`). |
| **Karakter non‑Latin** | Berikan model bahasa ke `OcrEngine` (misalnya `ocr_engine.language = "spa"` untuk bahasa Spanyol). |
| **Beberapa kwitansi dalam satu gambar** | Jalankan OCR pada seluruh gambar, kemudian bagi hasilnya menggunakan ekspresi reguler yang mendeteksi `\n\n+` (baris ganda). |
| **Butuh teks OCR mentah juga** | Simpan `ocr_result.text` bersama versi yang telah disaring untuk debugging. |

Variasi ini memastikan pengetahuan **cara menggunakan OCR** Anda dapat berkembang melampaui kasus paling sederhana.

## Kesalahan Umum (Dan Cara Menghindarinya)

- **Lupa menginstal perpustakaan** – `pip install aocr` harus berhasil sebelum Anda mengimpor.
- **Menggunakan pemisah path yang salah** di Windows (`\` vs `/`). Gunakan `os.path.join`.
- **Menghard‑code ambang kepercayaan** tanpa pengujian – selalu lakukan pemeriksaan visual cepat pada beberapa kwitansi terlebih dahulu.
- **Mengabaikan normalisasi Unicode** – beberapa kwitansi mengandung karakter dash khusus; jalankan `unicodedata.normalize('NFKC', text)` jika Anda berencana menyimpan output.

## Langkah Selanjutnya – Melampaui Dasar

Sekarang Anda tahu **cara mengekstrak ocr** data dari satu kwitansi, Anda mungkin ingin:

1. **Proses batch folder kwitansi** – iterasi semua file PNG/JPG dan tulis setiap hasil ke CSV.
2. **Integrasikan dengan basis data** – simpan `high_confidence_text` di SQLite untuk pencarian cepat.
3. **Terapkan parsing bahasa alami** – gunakan regex atau `dateutil` untuk mengambil tanggal, total, dan jumlah pajak.
4. **Bereksperimen dengan perpustakaan alternatif** – `pytesseract`, `easyocr`, atau layanan cloud (Google Vision, Azure OCR) jika Anda membutuhkan dukungan multibahasa atau akurasi lebih tinggi.

Setiap topik ini secara alami menggabungkan kata kunci sekunder kami: *python ocr example*, *extract text from receipt*, *load image for ocr*, dan *how to use OCR*.

## Kesimpulan

Kami baru saja menelusuri contoh **python ocr** lengkap yang menunjukkan **cara mengekstrak ocr** teks dari gambar kwitansi, menyaring simbol kepercayaan rendah, dan menghasilkan hasil bersih. Langkah‑langkahnya sederhana, kodenya mandiri, dan pendekatannya cukup fleksibel untuk disesuaikan dengan proyek yang lebih besar.

Cobalah dengan kwitansi Anda sendiri, sesuaikan ambang kepercayaan, dan kemudian skala ke pemrosesan batch. Jika Anda menemukan keanehan—seperti logo yang pudar atau font yang tidak biasa—ingat tips kasus pinggir di atas. Selamat coding, semoga pipeline OCR Anda selalu akurat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}