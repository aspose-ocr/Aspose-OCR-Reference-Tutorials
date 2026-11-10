---
category: general
date: 2026-07-05
description: Buat PDF yang dapat dicari dengan Python. Pelajari cara melakukan OCR
  pada PNG yang dipindai, mengonversi PDF gambar yang dipindai, dan mendapatkan PDF
  yang dapat dicari dalam hitungan menit.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: id
og_description: Buat PDF yang dapat dicari dengan cepat. Panduan ini menunjukkan cara
  melakukan OCR pada PNG, mengonversi PDF gambar yang dipindai, dan menghasilkan PDF
  yang dapat dicari menggunakan Python.
og_title: Buat PDF yang Dapat Dicari dari Gambar Pindai – Tutorial OCR Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Buat PDF yang Dapat Dicari dari Gambar Pindai – Panduan Lengkap OCR dengan
  Python
url: /id/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari Gambar Pindai – Panduan Lengkap OCR Python

Pernah bertanya-tanya bagaimana cara **membuat PDF yang dapat dicari** dari gambar pindai tanpa harus membayar perangkat lunak mahal? Anda tidak sendirian. Di banyak kantor, PDF datang sebagai gambar datar—sulit untuk dicari, tidak dapat disalin‑tempel, dan menjadi mimpi buruk untuk audit kepatuhan. Kabar baik? Dengan beberapa baris Python Anda dapat mengubah PNG statis itu menjadi PDF yang sepenuhnya dapat dicari, dan prosesnya lebih mudah daripada yang Anda kira.

Dalam tutorial ini kami akan membahas contoh **pengenalan OCR** secara lengkap, mencakup semua hal mulai dari menginstal pustaka yang tepat hingga menulis file PDF akhir. Pada akhir tutorial Anda akan tahu persis cara **mengonversi file PDF gambar pindai**, cara **ocr pdf secara programatik**, dan Anda akan memiliki skrip yang dapat digunakan kembali yang dapat Anda masukkan ke dalam proyek apa pun.

## Apa yang Akan Anda Pelajari

- Menginstal dan mengkonfigurasi pustaka OCR Python (kami akan menggunakan `pytesseract` dan `pdf2image`).
- Menginisialisasi mesin OCR dan mengatur bahasa.
- Memuat PNG yang dipindai (atau gambar apa pun) dan menjalankan OCR padanya.
- Mengonversi hasil OCR menjadi **PDF yang dapat dicari** (array byte) dan menyimpannya.
- Tips untuk menangani dokumen multi‑halaman, bahasa yang berbeda, dan jebakan umum.

Tidak diperlukan pengalaman sebelumnya dengan OCR—hanya lingkungan Python 3 yang berfungsi dan sedikit rasa ingin tahu.

---

## Buat PDF yang Dapat Dicari – Ikhtisar

Berikut adalah diagram alur tingkat tinggi dari langkah‑langkah yang akan kami terapkan.  

![Create searchable PDF workflow diagram](https://example.com/flowchart.png "Create searchable PDF workflow diagram")

*Alt text: Diagram alur pembuatan PDF yang dapat dicari yang menunjukkan inisialisasi mesin, pemuatan gambar, pengenalan OCR, konversi PDF, dan penulisan file.*

---

## Langkah 1: Inisialisasi Mesin OCR (how to ocr pdf)

Mengapa kita perlu menginisialisasi apa pun? Mesin OCR adalah otak yang menginterpretasikan pola piksel menjadi karakter. Dengan membuat sebuah instance mesin dan secara eksplisit mengatur bahasa, kita memberi tahu pustaka alfabet apa yang diharapkan, yang secara dramatis meningkatkan akurasi.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro tip:** Jika Anda perlu melakukan OCR pada dokumen dalam beberapa bahasa, instal paket bahasa yang sesuai untuk Tesseract dan berikan daftar seperti `"eng+spa"` ke `ocr_language`.

---

## Langkah 2: Muat Gambar Pindai (convert scanned image pdf)

Bagian selanjutnya dari teka‑teki adalah memasukkan data gambar ke dalam Python. Baik Anda memiliki PNG tunggal atau TIFF multi‑halaman, kelas `PIL.Image` dapat membukanya. Jika Anda memulai dari PDF yang sudah berisi gambar pindai, `pdf2image` akan mengonversi setiap halaman menjadi gambar untuk kita.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Mengapa ini penting:** Memuat gambar sebagai objek Pillow memberi kami akses ke data piksel mentahnya, yang dibutuhkan mesin OCR. Melewatkan langkah ini dan memberikan byte mentah secara langsung akan menyebabkan kesalahan.

---

## Langkah 3: Lakukan Pengenalan OCR pada Gambar (ocr recognition example)

Sekarang bagian yang menyenangkan—membiarkan mesin membaca teks. `pytesseract.image_to_pdf_or_hocr` mengembalikan aliran byte PDF yang sudah berisi lapisan teks tak terlihat, yang persis apa yang kita butuhkan untuk **PDF yang dapat dicari**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Kasus khusus:** Jika gambar Anda memiliki kontras rendah, pertimbangkan untuk menerapkan ambang sederhana sebelum OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Langkah pra‑pemrosesan kecil ini dapat meningkatkan akurasi secara dramatis.

---

## Langkah 4: Tulis Byte PDF ke File (convert png searchable pdf)

Pustaka OCR memberikan kita array byte—anggaplah itu sebagai konten mentah file PDF. Semua yang perlu kita lakukan sekarang adalah menulis byte tersebut ke disk.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Apa yang akan Anda lihat:** Buka file hasilnya di penampil PDF apa pun dan coba cari kata yang Anda tahu muncul dalam gambar asli. Sorotan harus langsung melompat ke lokasi tersebut, membuktikan bahwa lapisan teks tak terlihat berfungsi.

---

## Langkah 5: Memperluas ke Dokumen Multi‑Halaman (convert scanned image pdf)

Kontrak dunia nyata sering kali mencakup beberapa halaman. Untuk **mengonversi file PDF gambar pindai** yang berisi beberapa halaman, lakukan loop melalui setiap halaman, lakukan OCR, dan gabungkan PDF yang dihasilkan.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Mengapa menggabungkan?** Setiap panggilan ke `image_to_pdf_or_hocr` menghasilkan PDF mandiri. Menggabungkannya memastikan dokumen akhir mempertahankan urutan halaman asli.

---

## Kesalahan Umum & Cara Memperbaikinya

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Tidak ada teks yang dapat dicari setelah membuka PDF | Tesseract tidak menemukan karakter apa pun (output kosong) | Periksa kualitas gambar, tingkatkan DPI, atau terapkan pra‑pemrosesan (kontras, binarisasi). |
| karakter kacau (mis., �) | Paket bahasa salah atau font yang hilang | Instal data bahasa yang benar (`tesseract‑lang‑eng`) dan pastikan `ocr_language` cocok. |
| Ukuran file PDF sangat besar (>10 MB untuk gambar satu halaman) | Menggunakan PNG lossless sebagai sumber; OCR menambahkan gambar resolusi penuh | Turunkan skala gambar sebelum OCR (`image.thumbnail((1240, 1754))` untuk A4). |
| Skrip crash di Windows dengan “tesseract.exe not found” | Binary Tesseract tidak ada di PATH | Tambahkan `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (sesuaikan path). |

---

## Skrip Lengkap, Siap‑Jalankan

Menggabungkan semuanya, berikut satu file yang dapat Anda salin‑tempel dan jalankan:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Simpan ini sebagai `create_searchable_pdf.py`, ganti placeholder dengan jalur yang sebenarnya, dan jalankan:

```bash
python create_searchable_pdf.py
```

Anda seharusnya melihat sebuah

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Konversi Gambar ke PDF C# – Simpan Hasil OCR Multi‑halaman](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR Mengenali Dokumen PDF dalam Aspose.OCR untuk Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}