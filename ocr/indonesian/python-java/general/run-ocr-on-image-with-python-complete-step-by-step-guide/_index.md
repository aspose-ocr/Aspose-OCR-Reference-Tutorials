---
category: general
date: 2026-06-06
description: Jalankan OCR pada gambar menggunakan Python dan lihat skor kepercayaan.
  Pelajari cara memfilter kata dengan kepercayaan rendah, mengatur ambang batas, dan
  menangani kasus tepi.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: id
og_description: Jalankan OCR pada gambar di Python, periksa tingkat kepercayaan, dan
  saring kata‑kata dengan kepercayaan rendah. Tutorial ini memandu Anda melalui contoh
  lengkap yang dapat dijalankan.
og_title: Jalankan OCR pada Gambar dengan Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Jalankan OCR pada Gambar dengan Python – Panduan Lengkap Langkah demi Langkah
url: /id/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar dengan Python – Panduan Lengkap Langkah‑per‑Langkah

Pernahkah Anda **menjalankan OCR pada gambar** tetapi tidak yakin bagaimana cara mendapatkan teks yang dapat diandalkan darinya? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika kata‑kata yang diekstrak tampak tidak stabil dan nilai skor kepercayaan menjadi misteri.  

Dalam panduan ini kami akan langsung menyajikan solusi yang dapat bekerja: Anda akan melihat cara **menjalankan OCR pada gambar**, membaca nilai kepercayaan keseluruhan, dan mengekstrak kata‑kata dengan kepercayaan rendah yang mungkin memerlukan peninjauan manual. Pada akhir tutorial Anda akan memiliki skrip yang dapat digunakan kembali, memahami mengapa setiap baris penting, dan mengetahui cara menyesuaikan ambang kepercayaan untuk proyek Anda sendiri.

## Apa yang Dibahas dalam Tutorial Ini

Kami akan menelusuri seluruh alur kerja—dari memuat gambar hingga mencetak laporan rapi tentang kata‑kata yang berada di bawah ambang kepercayaan 80 %. Sepanjang perjalanan kami akan membahas:

* Memilih mesin OCR yang solid (kami akan menggunakan **EasyOCR**, sebuah perpustakaan OCR Python yang populer)  
* Menafsirkan atribut `confidence` yang dikembalikan oleh setiap hasil OCR  
* Menyaring kata‑kata dengan **ambang kepercayaan OCR** khusus  
* Memperluas skrip untuk pemrosesan batch atau mesin alternatif seperti **pytesseract**  

Tidak diperlukan pengalaman OCR sebelumnya, cukup familiar dengan Python dan lingkungan kerja (Python 3.9+ disarankan).  

Siap mengubah tangkapan layar yang buram menjadi teks bersih yang dapat dicari? Mari kita mulai.

---

## ## Cara Menjalankan OCR pada Gambar dengan Python

Inti tutorial adalah potongan kode tiga langkah yang mencerminkan kode yang sudah Anda lihat. Di bawah ini kami akan memecah setiap baris, menjelaskan alasannya, dan kemudian memberikan skrip lengkap yang siap disalin‑tempel.

### Langkah 1: Instal dan Impor Mesin OCR

Pertama, pastikan perpustakaan OCR tersedia. **EasyOCR** bekerja langsung untuk banyak bahasa dan memberikan nilai kepercayaan per kata.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Mengapa EasyOCR?* Ia menyertakan model deep‑learning yang telah dilatih pada dataset beragam, sehingga Anda biasanya mendapatkan nilai kepercayaan lebih tinggi dibandingkan mesin Tesseract yang lebih lama, terutama pada gambar dengan kualitas campuran.

> **Pro tip:** Jika Anda berada di lingkungan terbatas (misalnya, kontainer Docker kecil), `pytesseract` mungkin lebih ringan, tetapi Anda akan kehilangan sebagian akurasi modern yang diberikan EasyOCR.

### Langkah 2: Jalankan OCR pada Gambar

Sekarang kita benar‑benarnya **menjalankan OCR pada gambar**. Metode `recognize_image` dari contoh asli digantikan dengan pemanggilan `readtext` milik EasyOCR, yang mengembalikan daftar tuple `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Setiap entri dalam `ocr_results` terlihat seperti:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Elemen ketiga (`0.92` pada contoh) adalah nilai kepercayaan yang berkisar antara 0 hingga 1.

### Langkah 3: Ringkas Kepercayaan Keseluruhan

Berbeda dengan potongan kode sebelumnya yang mencetak satu atribut `confidence`, EasyOCR memberikan kepercayaan per kata. Untuk mendapatkan gambaran keseluruhan, kami akan menghitung rata‑rata nilai tersebut:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Mengapa rata‑rata?* Ini memberi Anda cek kesehatan cepat—jika kepercayaan keseluruhan di bawah, misalnya, 70 %, Anda mungkin perlu meningkatkan kualitas gambar (pencahayaan lebih baik, pra‑pemrosesan, dll.).

### Langkah 4: Daftar Kata‑kata dengan Kepercayaan Rendah

Berikutnya adalah bagian yang secara langsung menjawab permintaan “daftar kata yang kepercayaan nya di bawah ambang yang diinginkan”. Kami akan menetapkan **ambang kepercayaan OCR** sebesar 0.80 (80 %) secara default, tetapi Anda dapat menyesuaikannya.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

Loop ini mencetak setiap kata yang tidak lolos, bersamaan dengan persentase kepercayaannya. Ini adalah analog tepat dari loop asli `for recognized_word in recognition_result.words`, tetapi kini bekerja dengan format keluaran EasyOCR.

---

## ## Memahami Skor Kepercayaan OCR

Kepercayaan bukanlah angka ajaib; itu adalah perkiraan model tentang seberapa yakin ia terhadap transkripsi tertentu. Berikut beberapa hal yang perlu diingat:

| Situasi | Kepercayaan Umum | Apa yang Harus Dilakukan |
|-----------|-------------------|------------|
| Pemindaian jelas beresolusi tinggi | 0.95 – 1.00 | Tidak perlu pekerjaan tambahan |
| Sedikit blur atau pencahayaan tidak merata | 0.80 – 0.94 | Pertimbangkan pra‑pemrosesan ringan (peningkatan kontras) |
| Noise berat, teks miring | < 0.70 | Terapkan pra‑pemrosesan gambar (deskew, denoise) atau beralih ke mesin OCR lain |

> **Waspada:** Beberapa bahasa (misalnya tulisan tangan kursif) secara alami menghasilkan skor lebih rendah. Sesuaikan ambang sesuai kebutuhan.

### Kasus Pinggir & Variasi

1. **Pemrosesan Batch** – Jika Anda perlu **menjalankan OCR pada gambar** secara massal, bungkus logika di atas dalam loop yang mengiterasi sebuah direktori.  
2. **Banyak Bahasa** – Berikan daftar seperti `['en', 'fr']` ke `easyocr.Reader` dan mesin akan mendeteksi keduanya.  
3. **Mesin Alternatif** – Ingin mencoba **pytesseract**? Ganti blok pembaca dengan:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Anda kemudian harus mengagregasi kepercayaan per‑karakter menjadi nilai per‑kata—sedikit lebih rumit tetapi memungkinkan.

4. **Trik Pra‑pemrosesan** – Menerapkan filter OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) dapat meningkatkan kepercayaan pada pemindaian yang berisik.  

---

## ## Skrip Lengkap Siap‑Jalankan

Berikut adalah file Python lengkap yang dapat Anda letakkan dalam proyek. Simpan sebagai `ocr_report.py` dan jalankan dengan `python ocr_report.py`. Pastikan jalur gambar mengarah ke berkas yang nyata.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Output yang diharapkan** (angka Anda akan berbeda):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Jika setiap kata melewati ambang 80 % Anda akan melihat pesan ramah “All words meet the confidence threshold.” sebagai gantinya.

---

## ## Pertanyaan yang Sering Diajukan (FAQ)

**T: Apakah ini bekerja dengan PDF?**  
J: Tidak secara langsung. Konversi setiap halaman PDF menjadi gambar terlebih dahulu (misalnya dengan `pdf2image`) lalu masukkan PNG/JPEG ke dalam skrip.

**T: Nilai kepercayaan saya semua rendah—apa yang bisa saya lakukan?**  
J: Coba pra‑pemrosesan gambar: tingkatkan kontras, hilangkan noise latar, atau putar gambar ke posisi horizontal. EasyOCR juga menerima parameter `contrast_ths` yang dapat Anda sesuaikan.

**T: Bisakah saya mengekspor hasil ke CSV?**  
J: Tentu. Setelah loop kata‑kata berkepercayaan rendah, tulis `ocr_results` ke `csv.DictWriter` dimana setiap baris berisi `text`, `confidence`, dan koordinat bounding‑box.

**T: Apakah ada versi yang dipercepat GPU?**  
J: EasyOCR secara otomatis menggunakan CUDA jika GPU yang kompatibel dan PyTorch terpasang. Verifikasi dengan `torch.cuda.is_available()` sebelum menjalankan skrip.

---

## Kesimpulan

Kami baru saja **menjalankan OCR pada gambar** menggunakan Python, memeriksa kepercayaan keseluruhan, dan memisahkan kata‑kata berkepercayaan rendah yang memerlukan peninjauan manual.

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menetapkan Nilai Ambang pada Pengakuan Gambar OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Cara Menggunakan Aspose OCR untuk Hasil JSON dalam Pengakuan Gambar](/ocr/english/net/text-recognition/get-result-as-json/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}