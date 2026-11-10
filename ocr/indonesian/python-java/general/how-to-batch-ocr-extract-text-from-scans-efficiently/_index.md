---
category: general
date: 2026-04-26
description: Cara melakukan OCR batch pada dokumen Anda dan mengekstrak teks dari
  pemindaian menggunakan Python. Pelajari pemrosesan batch langkah demi langkah dengan
  OcrEngine untuk output JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: id
og_description: Cara melakukan OCR batch pada file hasil scan Anda dan mengekstrak
  teks dari pemindaian dalam satu skrip. Kode lengkap, tips, dan penanganan kasus
  tepi.
og_title: Cara Batch OCR – Panduan Python Cepat
tags:
- OCR
- Python
- Automation
title: Cara OCR Massal – Ekstrak Teks dari Scan Secara Efisien
url: /id/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR – Ekstrak Teks dari Scan Secara Efisien

Pernah bertanya-tanya **bagaimana cara batch OCR** tumpukan PDF yang dipindai tanpa kehilangan akal? Anda bukan satu-satunya—para pengembang terus bertanya, *“Bagaimana saya bisa mengekstrak teks dari scan sekaligus?”* Kabar baiknya, beberapa baris Python dapat mengubah pekerjaan membosankan itu menjadi alur kerja otomatis yang mulus.

Dalam tutorial ini kami akan membahas solusi lengkap yang siap dijalankan yang **mengekstrak teks dari scan**, menyimpan hasilnya sebagai JSON, dan memberikan pemeriksaan cepat di akhir. Tanpa layanan eksternal, tanpa sulap—hanya Python biasa, kelas `OcrEngine`, dan sedikit pengaturan folder.

## Apa yang Akan Anda Dapatkan

- Script yang berfungsi penuh yang **batch OCR** pada folder gambar apa pun.  
- Penjelasan jelas tentang *mengapa* setiap baris ada, bukan hanya *apa* yang dilakukannya.  
- Tips untuk menangani folder kosong, file non‑gambar, dan batch besar.  
- Cara untuk memverifikasi bahwa output JSON memang berisi teks yang diekstrak.  

### Prasyarat (minimum yang diperlukan)

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.8+ | Sintaks modern & petunjuk tipe |
| `OcrEngine` library (atau pembungkus yang kompatibel) | Fungsi inti OCR |
| Direktori dengan file gambar hasil scan (PNG, JPG, TIFF) | Data masukan |
| Izin menulis untuk folder output | Menyimpan hasil JSON |

Jika Anda sudah memiliki ini, bagus—mari kita mulai.

![alur kerja batch OCR](image-placeholder.png){alt="alur kerja batch OCR"}

## Langkah 1 – Inisialisasi Mesin OCR (cara batch OCR)

Sebelum kita dapat memproses apa pun, kita memerlukan instance mesin OCR. Anggaplah itu sebagai “otak” yang akan membaca setiap gambar dan menghasilkan teks. Menginisialisasinya sekali dan menggunakannya kembali di seluruh batch adalah pola paling efisien.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Mengapa menggunakan kembali instance yang sama?**  
> Membuat mesin baru untuk setiap file akan berulang kali memuat model berat ke memori, secara dramatis memperlambat batch. Satu instance menjaga model tetap di RAM dan memungkinkan Anda memproses ribuan gambar tanpa perlambatan yang terlihat.

## Langkah 2 – Arahkan ke Folder Scan Anda (ekstrak teks dari scan)

Scan Anda berada di suatu tempat di disk. Mari beri tahu skrip di mana menemukannya. Menggunakan path absolut menghindari kejutan “file tidak ditemukan” ketika skrip dijalankan dari direktori kerja yang berbeda.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Tips pro:**  
> Jika Anda menggunakan Windows, garis miring maju (`/`) berfungsi dengan baik dengan `os.path.abspath`, sehingga Anda tidak perlu meloloskan backslash.

## Langkah 3 – Pilih Lokasi Hasil JSON

Anda mungkin menginginkan folder rapi untuk hasil OCR. Memisahkan output dari sumber memudahkan pembersihan nanti atau memasukkan JSON ke pipeline lain.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Mengapa membuat folder secara programatis?**  
> Ini memastikan skrip tidak akan crash jika direktori tidak ada, dan `exist_ok=True` membuat operasi menjadi idempotent—menjalankan skrip berulang kali tanpa error.

## Langkah 4 – Jalankan Proses Batch (cara batch OCR)

Sekarang inti permasalahan: memberi tahu `ocr_engine` untuk menelusuri setiap file di `input_dir`, menjalankan OCR, dan menuliskan JSON ke `output_dir`. Flag `format="json"` memberi tahu mesin untuk menyerialisasi hasil dalam format terstruktur yang disukai alat downstream.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Apa yang terjadi di balik layar?

1. **Penemuan file** – Mesin memindai `input_folder` secara rekursif, mengabaikan file tersembunyi.  
2. **Validasi file** – Hanya ekstensi gambar yang didukung (`.png`, `.jpg`, `.tif`, dll.) yang diberikan ke model OCR.  
3. **Eksekusi OCR** – Setiap gambar dikirim ke mesin OCR; teks, skor kepercayaan, dan data tata letak ditangkap.  
4. **Serialisasi JSON** – Hasil ditulis ke file dengan nama dasar yang sama tetapi ekstensi `.json` di `output_folder`.  

> **Penanganan kasus tepi:**  
> - **Folder kosong:** Mesin mencatat “No files found” dan kembali dengan lancar.  
> - **Gambar rusak:** Mesin melewati file, mencatat entri error di `batch_errors.log`, dan melanjutkan.  
> - **Batch besar (10k+ file):** Penggunaan memori tetap rendah karena setiap gambar diproses secara independen.

## Langkah 5 – Konfirmasi Konversi Selesai

Pernyataan `print` sederhana memberikan umpan balik langsung di konsol. Untuk pipeline produksi Anda mungkin menggantinya dengan pemanggilan logging atau notifikasi email.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Ketika Anda melihat baris itu, Anda dapat memeriksa folder `json_output` dengan aman. Setiap file JSON akan tampak kira-kira seperti ini:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Anda sekarang dapat memasukkan file JSON ini ke dalam basis data, indeks pencarian, atau alat analitik downstream apa pun.

## Pertanyaan yang Sering Diajukan (dan jawaban cepat)

**Q: Bagaimana jika saya perlu memproses PDF alih-alih gambar?**  
A: Ubah setiap halaman PDF menjadi gambar terlebih dahulu (mis., menggunakan `pdf2image`) dan letakkan file PNG/JPG yang dihasilkan di `input_dir`. Logika batch OCR tetap tidak berubah.

**Q: Bisakah saya mengubah format output menjadi teks biasa?**  
A: Tentu saja. Ganti `format="json"` dengan `format="txt"` dan mesin akan menulis file `.txt` yang hanya berisi teks yang diekstrak.

**Q: Scan saya berada di beberapa sub‑folder—apakah skrip akan menelusuri?**  
A: Ya. `batch_process` menelusuri pohon direktori secara default. Jika Anda menginginkan output datar, set `flatten=True` (jika perpustakaan mendukungnya) atau lakukan post‑process pada nama file JSON.

**Q: Bagaimana cara menangani skrip non‑Latin?**  
A: Inisialisasi `OcrEngine` dengan parameter bahasa, misalnya `OcrEngine(lang="spa+eng")`. Loop batch itu sendiri tidak memerlukan perubahan apa pun.

## Tips Pro & Kesalahan Umum

- **Ukuran batch penting:** Jika Anda melihat lonjakan CPU, batasi proses dengan `time.sleep(0.1)` sederhana antara file.  
- **Logging:** Ganti pemanggilan `print` dengan modul `logging` Python untuk menangkap timestamp dan level error.  
- **Tabrakan penamaan file:** Jika dua scan memiliki nama dasar yang sama tetapi berada di sub‑folder berbeda, file JSON akan menimpa satu sama lain. Tambahkan hash dari path relatif ke nama output untuk menghindarinya.  
- **Memory leak:** Beberapa back‑end OCR menyimpan sumber daya native. Panggil `ocr_engine.close()` di akhir skrip Anda jika perpustakaan menyediakan metode pembersihan.

## Skrip Lengkap – Siap Salin & Tempel

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Output konsol yang diharapkan**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Anda dapat memverifikasi JSON dengan membuka file apa pun di `json_output` menggunakan editor teks atau memuatnya di Python:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Anda akan melihat teks mentah hasil OCR yang dicetak ke konsol.

## Kesimpulan

Kami baru saja membahas **cara batch OCR** seluruh direktori gambar yang dipindai dan **mengekstrak teks dari scan** ke dalam file JSON yang bersih dan dapat dibaca mesin. Pendekatannya sengaja sederhana: siapkan mesin sekali, arahkan ke folder, dan biarkan perpustakaan menangani pekerjaan berat. Dari sini Anda dapat:

- Menghubungkan JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}