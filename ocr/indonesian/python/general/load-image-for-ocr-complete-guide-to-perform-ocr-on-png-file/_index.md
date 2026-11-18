---
category: general
date: 2026-06-25
description: Muat gambar untuk OCR dan lakukan OCR pada PNG dengan tutorial Python
  langkah demi langkah menggunakan aocr. Pelajari debugging, logging, dan praktik
  terbaik.
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: id
og_description: Muat gambar untuk OCR dan lakukan OCR pada PNG menggunakan aocr. Panduan
  ini memandu Anda melalui pencatatan, pemuatan gambar, dan pengenalan dengan kode
  lengkap.
og_title: Muat Gambar untuk OCR – Tutorial Python Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Muat Gambar untuk OCR – Panduan Lengkap Melakukan OCR pada File PNG
url: /id/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memuat Gambar untuk OCR – Panduan Lengkap Melakukan OCR pada File PNG

Pernah perlu **memuat gambar untuk OCR** tetapi tidak yakin cara menyiapkan debugging yang tepat? Anda tidak sendirian. Dalam banyak proyek, rintangan pertama adalah memasukkan PNG ke dalam mesin sambil tetap dapat melihat apa yang terjadi di balik layar.  

Dalam tutorial ini kami akan memandu Anda melalui semua yang diperlukan untuk **melakukan OCR pada PNG** menggunakan pustaka `aocr` – mulai dari menyiapkan logger untuk output detail hingga benar‑benar mengenali teks. Pada akhir tutorial Anda akan memiliki skrip yang dapat dipakai ulang dan dapat dimasukkan ke proyek Python mana pun, serta memahami mengapa setiap bagian penting.

## Apa yang Akan Anda Pelajari

- Cara menginisialisasi logger `aocr` sehingga Anda dapat melacak setiap langkah.
- Kode tepat untuk **memuat gambar untuk OCR** dengan `aocr.OcrEngine`.
- Cara mengonfigurasi level logging untuk mendapatkan informasi debug yang terperinci.
- Menjalankan mesin untuk **melakukan OCR pada PNG** dan mengambil hasilnya.
- Tips menangani jebakan umum seperti file yang hilang atau format yang tidak didukung.

Tidak diperlukan pengalaman sebelumnya dengan `aocr`; hanya instalasi Python 3 yang berfungsi dan sebuah gambar yang ingin Anda baca. Mari kita mulai.

![contoh memuat gambar untuk OCR](assets/load-image-ocr.png "Ilustrasi memuat gambar untuk OCR dalam Python")

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.8+ | `aocr` menargetkan interpreter modern dan menggunakan tipe petunjuk. |
| `aocr` library installed (`pip install aocr`) | Tanpa paket ini kelas yang kami gunakan tidak akan ada. |
| A PNG image you want to read | Tutorial ini berfokus pada **perform OCR on PNG**, jadi PNG sangat penting. |
| Write permission to a log directory | Logger perlu membuat `ocr_debug.log`. |

Jika Anda belum memiliki salah satu dari ini, instal sekarang – hanya memerlukan satu menit.

```bash
pip install aocr
```

## Langkah 1: Memuat Gambar untuk OCR – Inisialisasi Logging

Sebelum Anda menyentuh gambar, siapkan logger terlebih dahulu. Debugging OCR bisa menjadi mimpi buruk jika Anda tidak tahu apa yang sedang dilakukan mesin. Kelas `aocr.Logging` menulis semuanya ke file, dan dengan mengatur level ke `DEBUG` Anda akan melihat setiap panggilan internal.

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**Mengapa ini penting:**  
Jika mesin OCR tidak dapat menemukan file atau format gambar tidak didukung, logger akan menangkap jejak tumpukan pengecualian. Hal ini menyelamatkan Anda dari tebakan‑tebakan tak berujung nanti.

## Langkah 2: Melakukan OCR pada PNG – Konfigurasi Mesin

Setelah logger siap, sambungkan ke mesin OCR. Langkah ini mengikat keduanya sehingga setiap aksi mesin tercatat.

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**Pro tip:**  
Anda dapat menggunakan kembali instance `ocr_engine` yang sama untuk beberapa gambar. Cukup ingat untuk membersihkan status sebelumnya jika Anda memproses batch.

## Langkah 3: Memuat Gambar untuk OCR – Memasukkan File PNG

Berikut inti tutorial: sebenarnya **memuat gambar untuk OCR**. Metode `load_image` menerima jalur file; secara internal ia akan mendekode PNG menjadi bitmap yang dapat dipahami mesin.

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### Kasus Tepi yang Perlu Diwaspadai

1. **File Tidak Ditemukan** – Jika jalurnya salah, `aocr` akan mengeluarkan `FileNotFoundError`. Logger akan mencatatnya, tetapi Anda juga dapat menangkapnya:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **Format Tidak Didukung** – Meskipun PNG umumnya didukung, file yang rusak dapat memicu `UnsupportedFormatError`. Dalam kasus ini, pertimbangkan mengonversi gambar ke PNG bersih dengan Pillow sebelum memuatnya.

## Langkah 4: Melakukan OCR pada PNG – Jalankan Pengakuan

Setelah gambar berada di memori, Anda akhirnya dapat **melakukan OCR pada PNG**. Metode `recognize` meluncurkan pipeline mesin (pra‑pemrosesan, segmentasi, klasifikasi) dan mengisi objek hasil.

```python
# Execute the OCR process
ocr_engine.recognize()
```

Setelah pemanggilan ini, mesin menyimpan teks yang dikenali. Anda dapat mengaksesnya melalui atribut `result`:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**Mengapa Anda harus memeriksa hasil:**  
Beberapa mesin OCR mengembalikan string kosong untuk gambar dengan kontras rendah. Melihat hasil secara langsung memungkinkan Anda memutuskan apakah perlu pra‑pemrosesan (misalnya, meningkatkan kontras) sebelum menjalankan kembali.

## Langkah 5: Membungkus Semua – Fungsi yang Dapat Digunakan Ulang

Menggabungkan semua bagian ke dalam satu fungsi memudahkan pemanggilan dari skrip lain atau layanan web. Ini juga menunjukkan cara **memuat gambar untuk OCR** dan **melakukan OCR pada PNG** dalam satu paket rapi.

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

Menjalankan skrip akan menghasilkan `ocr_debug.log` yang detail di folder `logs`, kemudian mencetak teks yang dikenali ke konsol. Anda kini memiliki utilitas **perform OCR on PNG** yang dapat di‑import di tempat lain.

## Pertanyaan Umum & Gotchas

- **Apakah saya perlu mengonversi PNG ke format lain?**  
  Biasanya tidak. `aocr` menangani PNG secara native, tetapi jika gambar sangat besar (>10 MP) Anda mungkin ingin menurunkan resolusi terlebih dahulu untuk mempercepat proses.

- **Bagaimana jika file log menjadi terlalu besar?**  
  Rotasikan log setelah setiap run atau batasi level ke `INFO` setelah Anda yakin pipeline berfungsi.

- **Bisakah saya memproses banyak gambar dalam loop?**  
  Tentu saja. Cukup panggil `ocr_png` untuk setiap file; fungsi tersebut membuat logger baru setiap kali, menjaga log tetap terisolasi.

- **Apakah ada cara mendapatkan kotak pembatas alih‑alih teks biasa?**  
  Ya – `engine.result` juga berisi `boxes` dan `confidences`. Jelajahi dokumentasi `aocr` untuk `result.boxes` jika Anda memerlukan informasi tata letak.

## Kesimpulan

Anda kini tahu cara **memuat gambar untuk OCR** dan **melakukan OCR pada PNG** menggunakan pustaka `aocr`, lengkap dengan setup logging yang kuat sehingga debugging menjadi mudah. Fungsi contoh mengenkapsulasi seluruh alur kerja, sehingga Anda dapat menambahkannya ke proyek apa pun dan mulai mengekstrak teks segera.

Langkah selanjutnya? Coba beri mesin gambar tipe lain (JPEG, TIFF) untuk melihat bagaimana akurasi berubah, atau bereksperimen dengan teknik pra‑pemrosesan seperti thresholding untuk meningkatkan hasil pada pemindaian berisik. Dan jika Anda penasaran tentang mengekstrak data terstruktur (tabel, formulir), lihat bagian `aocr` tentang analisis tata letak – mereka sangat cocok dengan apa yang baru saja Anda bangun.

Selamat coding, semoga pipeline OCR Anda selalu bebas error!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara OCR Gambar – Lakukan OCR pada Gambar dalam Pengakuan Gambar OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}