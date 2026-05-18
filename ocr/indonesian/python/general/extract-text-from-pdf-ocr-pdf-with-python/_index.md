---
category: general
date: 2026-04-29
description: Ekstrak teks dari PDF menggunakan Aspose OCR di Python. Pelajari pemrosesan
  PDF OCR batch, konversi teks PDF yang dipindai, dan tangani halaman dengan kepercayaan
  rendah.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: id
og_description: Ekstrak teks dari PDF dengan Aspose OCR di Python. Panduan ini menunjukkan
  pemrosesan OCR PDF secara batch, mengonversi teks PDF yang dipindai, dan menangani
  hasil dengan kepercayaan rendah.
og_title: Ekstrak Teks dari PDF – OCR PDF dengan Python
tags:
- OCR
- Python
- PDF processing
title: Ekstrak Teks dari PDF – OCR PDF dengan Python
url: /id/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari PDF – OCR PDF dengan Python

Pernah perlu **mengekstrak teks dari PDF** tetapi file tersebut hanya berupa gambar yang dipindai? Anda tidak sendirian—banyak pengembang mengalami hal yang sama saat mencoba mengubah PDF menjadi data yang dapat dicari. Kabar baiknya? Dengan Aspose OCR untuk Python Anda dapat mengonversi teks PDF yang dipindai dalam beberapa baris kode, bahkan menjalankan **pemrosesan batch OCR PDF** ketika Anda memiliki puluhan file untuk diproses.

Dalam tutorial ini kami akan membahas seluruh alur kerja: menyiapkan pustaka, menjalankan OCR pada satu PDF, memperluas ke batch, dan menangani halaman dengan kepercayaan rendah sehingga Anda tahu kapan diperlukan tinjauan manual. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang mengekstrak teks dari PDF yang dipindai apa pun, dan Anda akan memahami alasan di balik setiap langkah.

## Apa yang Anda Butuhkan

- Python 3.8 atau lebih baru (kode menggunakan f‑strings, jadi 3.6+ dapat bekerja, tetapi 3.8+ disarankan)
- Lisensi Aspose OCR untuk Python atau kunci percobaan gratis (Anda dapat mendapatkannya dari situs web Aspose)
- Sebuah folder dengan satu atau lebih PDF yang dipindai yang ingin Anda proses
- Sebuah ruang disk yang cukup untuk laporan *.txt* yang dihasilkan

Itu saja—tidak ada ketergantungan eksternal yang berat, tidak ada akrobatik OpenCV. Mesin OCR Aspose melakukan pekerjaan berat untuk Anda.

## Menyiapkan Lingkungan

Pertama, instal paket Aspose OCR dari PyPI:

```bash
pip install aspose-ocr
```

Jika Anda memiliki file lisensi (`Aspose.OCR.lic`), letakkan di root proyek Anda dan aktifkan seperti berikut:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Pro tip:** Simpan file lisensi di luar kontrol versi; tambahkan ke `.gitignore` untuk menghindari paparan tidak sengaja.

## Melakukan OCR pada Satu PDF

Sekarang mari kita ekstrak teks dari satu PDF yang dipindai. Langkah‑langkah inti adalah:

1. Buat instance `OcrEngine`.
2. Arahkan ke file PDF.
3. Dapatkan `OcrResult` untuk setiap halaman.
4. Tulis output teks biasa ke disk.
5. Hapus (dispose) engine untuk membebaskan sumber daya native.

Berikut adalah skrip lengkap yang dapat dijalankan:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Apa yang akan Anda lihat:** Untuk setiap halaman skrip mencetak sesuatu seperti `Page 1: confidence 97.45%`. Jika sebuah halaman berada di bawah ambang 80 %, sebuah peringatan muncul, memberi tahu Anda bahwa OCR mungkin telah melewatkan karakter.

### Mengapa Ini Berfungsi

- **`OcrEngine`** adalah gerbang ke pustaka Aspose OCR native; ia menangani segala hal mulai dari pra‑pemrosesan gambar hingga pengenalan karakter.
- **`extract_from_pdf`** secara otomatis meraster setiap halaman PDF, sehingga Anda tidak perlu mengonversi PDF menjadi gambar secara manual.
- **Skor kepercayaan** memungkinkan Anda mengotomatisasi pemeriksaan kualitas—penting ketika Anda memproses dokumen hukum atau medis di mana akurasi sangat penting.

## Pemrosesan Batch OCR PDF dengan Python

Sebagian besar proyek dunia nyata melibatkan lebih dari satu file. Mari kita perpanjang skrip satu‑file menjadi pipeline **pemrosesan batch OCR PDF** yang menelusuri sebuah direktori, memproses setiap PDF, dan menyimpan hasilnya di sub‑folder yang sesuai.

Berikut kode contoh:

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Bagaimana Ini Membantu

- **Skalabilitas:** Fungsi ini menelusuri folder sekali, membuat sub‑folder output khusus untuk setiap PDF. Ini menjaga keteraturan ketika Anda memiliki puluhan dokumen.
- **Dapat digunakan kembali:** `ocr_pdf_file` dapat dipanggil dari skrip lain (mis., layanan web) karena merupakan fungsi murni.
- **Penanganan error:** Skrip mencetak pesan ramah jika folder input kosong, menyelamatkan Anda dari kegagalan diam.

## Mengonversi Teks PDF yang Dipindai – Menangani Kasus Pinggir

Meskipun kode di atas berfungsi untuk kebanyakan PDF, Anda mungkin menemui beberapa keanehan:

| Situation | Why It Happens | How to Mitigate |
|-----------|----------------|-----------------|
| **PDF terenkripsi** | PDF dilindungi kata sandi. | Berikan kata sandi ke `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Dokumen multi‑bahasa** | Aspose OCR secara default ke bahasa Inggris. | Atur `ocr_engine.language = "spa"` untuk bahasa Spanyol, atau berikan daftar untuk bahasa campuran. |
| **PDF sangat besar (>500 halaman)** | Penggunaan memori melonjak karena setiap halaman dimuat ke RAM. | Proses PDF dalam potongan menggunakan `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` dan lakukan loop. |
| **Kualitas pemindaian buruk** | DPI rendah atau banyak noise mengurangi kepercayaan. | Pra‑proses PDF dengan `engine.image_preprocessing = True` atau tingkatkan DPI melalui `engine.dpi = 300`. |

> **Perhatian:** Mengaktifkan pra‑pemrosesan gambar dapat meningkatkan waktu CPU secara signifikan. Jika Anda menjalankan batch malam, jadwalkan cukup waktu atau jalankan pekerja terpisah.

## Memverifikasi Output

Setelah skrip selesai, Anda akan menemukan struktur folder seperti berikut:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Buka file `.txt` apa pun; Anda akan melihat teks bersih ber‑encoding UTF‑8 yang mencerminkan konten yang dipindai asli. Jika Anda melihat karakter yang kacau, periksa kembali pengaturan bahasa PDF dan pastikan paket font yang tepat terpasang di mesin.

## Membersihkan Sumber Daya

Aspose OCR bergantung pada DLL native, jadi penting untuk memanggil `engine.dispose()` setelah selesai. Lupa langkah ini dapat menyebabkan kebocoran memori, terutama pada pekerjaan batch yang berjalan lama.

```python
# Always the last line of your script
engine.dispose()
```

## Contoh End‑to‑End Lengkap

Menggabungkan semuanya, berikut contoh lengkap satu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}