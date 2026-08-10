---
category: general
date: 2026-06-22
description: Buat PDF yang dapat dicari dengan Python menggunakan OCR – pelajari cara
  mengonversi gambar menjadi PDF, mengenali teks PDF, dan mengotomatiskan alur kerja
  Anda.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text pdf
- python ocr pdf
language: id
og_description: Buat PDF yang dapat dicari di Python menggunakan OCR. Ikuti tutorial
  langkah demi langkah ini untuk mengonversi gambar menjadi PDF, mengenali teks PDF,
  dan mengotomatiskan pemrosesan dokumen.
og_title: Buat PDF yang dapat dicari di Python – Panduan OCR Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  headline: Create searchable PDF in Python – Complete OCR Guide
  type: TechArticle
- description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  name: Create searchable PDF in Python – Complete OCR Guide
  steps:
  - name: Initialise the OCR engine
    text: The first thing you do is spin up an `OcrEngine` object. Think of it as
      turning on a scanner that’s ready to read your image.
  - name: Load the image you want to convert
    text: Next we feed the engine with an image stream. The `ImageStream.from_file`
      helper reads the file and wraps it in a format the OCR engine understands.
  - name: Tell the engine to output a searchable PDF
    text: By default many OCR SDKs output plain text. We need to switch the output
      format to PDF so the resulting file is both visual and searchable.
  - name: Prepare an in‑memory stream for the PDF data
    text: Instead of writing directly to disk, we capture the PDF in a `MemoryStream`.
      This keeps I/O fast and lets you pipe the bytes elsewhere (e.g., upload to S3)
      if you wish.
  - name: Run the recognition and write the PDF
    text: Now the heavy lifting happens. The `recognize` call reads the image, runs
      OCR, and streams the searchable PDF into `pdf_stream`.
  - name: Save the generated PDF to a file
    text: Finally, we dump the bytes from the memory stream onto disk. The resulting
      file can be opened in Adobe Reader, Preview, or any PDF viewer with full‑text
      search.
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Buat PDF yang Dapat Dicari di Python – Panduan OCR Lengkap
url: /id/python-java/general/create-searchable-pdf-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang dapat dicari di Python – Panduan OCR Lengkap

Pernahkah Anda perlu **membuat PDF yang dapat dicari** dari kontrak yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami hal yang sama saat pertama kali mencoba mengubah gambar bitmap menjadi dokumen yang dapat dicari teks. Kabar baiknya, dengan skrip Python kecil Anda dapat **mengonversi gambar ke PDF**, membiarkan mesin OCR mengenali setiap kata, dan menghasilkan file yang sepenuhnya dapat dicari.

Dalam tutorial ini kami akan membahas seluruh proses, mulai dari menginstal pustaka yang tepat hingga menangani kasus tepi seperti dokumen multi‑halaman. Pada akhir tutorial Anda akan dapat **ocr image to pdf**, **recognize text pdf**, dan mengintegrasikan alur kerja ke dalam pipeline otomatisasi yang lebih besar.

## Apa yang Anda butuhkan

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.8 atau lebih baru | Sintaks modern dan petunjuk tipe yang lebih baik |
| `ocr` Python package (atau SDK OCR yang kompatibel) | Menyediakan `OcrEngine`, `ImageStream`, dan output PDF |
| Gambar yang dipindai (JPEG, PNG, atau TIFF) | Sumber yang akan Anda konversi |
| Akses menulis ke folder untuk PDF output | Agar Anda dapat menyimpan file yang dihasilkan |

Jika Anda belum menginstal SDK, jalankan:

```bash
pip install ocr-sdk   # replace with the actual package name
```

> **Tips pro:** Gunakan lingkungan virtual (`python -m venv .venv`) untuk menjaga ketergantungan tetap rapi.

## Ikhtisar alur kerja

1. **Buat instance mesin OCR** – otak di balik pengenalan.  
2. **Muat gambar** yang ingin Anda proses.  
3. **Konfigurasikan mesin** untuk menghasilkan PDF yang dapat dicari bukan teks biasa.  
4. **Siapkan aliran dalam memori** yang akan menampung byte PDF.  
5. **Jalankan pengenalan** – mesin membaca gambar, mengekstrak teks, dan menulis PDF.  
6. **Simpan PDF ke disk** sehingga Anda dapat membukanya di viewer apa pun.

Itulah seluruh cerita dalam enam baris kode. Mari kita uraikan setiap langkah.

---

## Buat PDF yang dapat dicari – Tutorial OCR Python Langkah‑per‑Langkah

### Langkah 1: Inisialisasi mesin OCR

Hal pertama yang Anda lakukan adalah membuat objek `OcrEngine`. Anggaplah itu seperti menyalakan pemindai yang siap membaca gambar Anda.

```python
import ocr

# Initialise the OCR engine – this is where all the magic begins
engine = ocr.OcrEngine()
```

> **Mengapa ini penting:** Menginstansiasi mesin mengalokasikan buffer internal dan memuat data bahasa. Melewatkan langkah ini akan menyebabkan error `NoneType` nanti ketika Anda mencoba mengatur gambar.

### Langkah 2: Muat gambar yang ingin Anda konversi

Selanjutnya kami memberi mesin aliran gambar. Helper `ImageStream.from_file` membaca file dan membungkusnya dalam format yang dipahami mesin OCR.

```python
# Load the source image – replace the path with your own file
image_path = "YOUR_DIRECTORY/contract.jpg"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

> **Kasus tepi:** Jika sumber Anda adalah TIFF multi‑halaman, gunakan `ocr.MultiPageImageStream.from_file` sebagai gantinya. Mesin akan memperlakukan setiap halaman sebagai halaman PDF terpisah secara otomatis.

### Langkah 3: Beritahu mesin untuk menghasilkan PDF yang dapat dicari

Secara default banyak SDK OCR menghasilkan teks biasa. Kita perlu mengubah format output menjadi PDF sehingga file yang dihasilkan bersifat visual dan dapat dicari.

```python
# Configure the engine to produce a searchable PDF
engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
```

> **Apa yang terjadi di balik layar?** Mesin kini menyematkan lapisan teks tak terlihat di belakang bitmap, memungkinkan Anda mencari kata seperti pada PDF asli.

### Langkah 4: Siapkan aliran dalam memori untuk data PDF

Alih-alih menulis langsung ke disk, kami menangkap PDF dalam `MemoryStream`. Ini menjaga I/O tetap cepat dan memungkinkan Anda mengalirkan byte ke tempat lain (mis., mengunggah ke S3) jika diinginkan.

```python
# Create a memory buffer that will receive the PDF bytes
pdf_stream = ocr.MemoryStream()
```

### Langkah 5: Jalankan pengenalan dan tulis PDF

Sekarang pekerjaan berat terjadi. Panggilan `recognize` membaca gambar, menjalankan OCR, dan menyalurkan PDF yang dapat dicari ke dalam `pdf_stream`.

```python
# Perform OCR and write the searchable PDF into the memory stream
engine.recognize(pdf_stream)
```

> **Jebakan umum:** Lupa memanggil `engine.recognize` akan membuat `pdf_stream` kosong, dan mencoba menyimpannya akan memunculkan `ValueError`. Selalu periksa `pdf_stream.length` jika Anda perlu memverifikasi bahwa data telah dihasilkan.

### Langkah 6: Simpan PDF yang dihasilkan ke file

Akhirnya, kami menuliskan byte dari aliran memori ke disk. File yang dihasilkan dapat dibuka di Adobe Reader, Preview, atau viewer PDF apa pun dengan pencarian teks penuh.

```python
output_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Write the PDF bytes to a file
with open(output_path, "wb") as f:
    f.write(pdf_stream.to_bytes())
print(f"✅ Searchable PDF saved to {output_path}")
```

> **Hasil yang akan Anda lihat:** Buka PDF, tekan `Ctrl+F`, ketik kata yang muncul dalam pemindaian asli, dan lihat viewer menyorotnya secara instan. Itu adalah ciri khas **PDF yang dapat dicari**.

## Konversi gambar ke PDF – Menyesuaikan pengaturan untuk hasil terbaik

Jika tujuan utama Anda hanya **mengonversi gambar ke PDF** tanpa OCR, Anda dapat melewatkan langkah 3 dan mengatur format output ke `ocr.OutputFormat.IMAGE_PDF`. Mesin akan menyematkan bitmap sebagai halaman PDF tanpa lapisan teks tersembunyi.

```python
engine.get_settings().set_output_format(ocr.OutputFormat.IMAGE_PDF)
```

Gunakan mode ini ketika Anda membutuhkan replika visual yang akurat tetapi tidak peduli dengan kemampuan pencarian—mungkin untuk tujuan arsip di mana OCR tidak diperlukan.

## Kenali PDF Teks – Menambahkan paket bahasa dan kontrol DPI

Untuk pengalaman **recognize text PDF** yang kuat, pertimbangkan penyesuaian opsional berikut:

```python
settings = engine.get_settings()
settings.set_language("eng+spa")          # English + Spanish support
settings.set_dpi(300)                     # Higher DPI improves accuracy
settings.enable_auto_rotate(True)         # Auto‑rotate skewed scans
```

> **Mengapa mengatur DPI?** Resolusi yang lebih tinggi memberi mesin OCR lebih banyak piksel untuk dianalisis, mengurangi kesalahan pengenalan pada pemindaian berkualitas rendah.

## PDF OCR Python – Mengintegrasikan ke pipeline yang lebih besar

Sekarang Anda dapat **python ocr pdf** dalam beberapa baris, bayangkan menyematkan logika ini ke dalam API Flask:

```python
from flask import Flask, request, send_file
import io, ocr

app = Flask(__name__)

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["image"]
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_bytes(file.read()))
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
    pdf_stream = ocr.MemoryStream()
    engine.recognize(pdf_stream)

    return send_file(
        io.BytesIO(pdf_stream.to_bytes()),
        mimetype="application/pdf",
        as_attachment=True,
        download_name="searchable.pdf"
    )
```

Endpoint kecil ini memungkinkan klien mengirim POST gambar dan menerima **PDF yang dapat dicari** secara instan—sempurna untuk layanan pemrosesan dokumen SaaS.

## Kesalahan umum saat Anda **ocr image to pdf**

| Gejala | Penyebab kemungkinan | Perbaikan |
|--------|----------------------|-----------|
| Halaman PDF kosong | Gambar tidak dimuat (`engine.set_image` dipanggil dengan path yang salah) | Verifikasi path dan gunakan `os.path.abspath` |
| Tidak ada teks yang dapat dicari | Format output masih diatur ke `IMAGE_PDF` | Secara eksplisit panggil `set_output_format(ocr.OutputFormat.PDF)` |
| Karakter kacau | Paket bahasa salah | Muat bahasa yang benar dengan `settings.set_language("eng")` |
| Pemrosesan lambat pada file besar | Menggunakan DPI default (72) pada gambar resolusi tinggi | Tingkatkan DPI ke 300 atau proses halaman secara batch satu per satu |

## Contoh lengkap yang dapat dijalankan (siap salin‑tempel)

```python
import ocr

def create_searchable_pdf(image_path: str, output_path: str) -> None:
    """
    Convert a scanned image to a searchable PDF using the ocr SDK.
    """
    # 1️⃣ Initialise engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # 3️⃣ Set output to searchable PDF
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)

    # Optional: improve accuracy
    settings = engine.get_settings()
    settings.set_language("eng")   # adjust as needed
    settings.set_dpi(300)

    # 4️⃣ Prepare in‑memory stream
    pdf_stream = ocr.MemoryStream()

    # 5️⃣ Run OCR
    engine.recognize(pdf_stream)

    # 6️⃣ Persist PDF
    with open(output_path, "wb") as f:
        f.write(pdf_stream.to_bytes())
    print(f"✅ Searchable PDF created at: {output_path}")

if __name__ == "__main__":
    create_searchable_pdf(
        image_path="YOUR_DIRECTORY/contract.jpg",
        output_path="YOUR_DIRECTORY/contract_searchable.pdf"
    )
```

Jalankan skrip, buka PDF yang dihasilkan, dan coba cari kata yang Anda tahu muncul dalam pemindaian asli. Jika semuanya berjalan lancar, Anda baru saja menguasai **create searchable pdf** dengan Python.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **create searchable PDF** menggunakan pustaka OCR Python: menginisialisasi mesin, memuat gambar, mengonfigurasi output PDF, men‑stream hasil, dan akhirnya menyimpannya ke disk. Anda juga telah melihat cara **convert image to PDF**, menyesuaikan **

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Kenali Teks PDF – Operasi OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/)
- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Konversi Gambar ke PDF C# – Simpan Hasil OCR Multi‑halaman](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}