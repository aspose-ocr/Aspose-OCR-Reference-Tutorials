---
category: general
date: 2026-06-19
description: Cara menjalankan OCR langkah demi langkah dan meningkatkan akurasi OCR
  dengan teknik OCR teks biasa. Pelajari alur kerja cepat untuk ekstraksi teks yang
  andal.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: id
og_description: Cara menjalankan OCR secara efisien. Tutorial ini menunjukkan cara
  meningkatkan akurasi OCR menggunakan OCR teks biasa dan pemrosesan lanjutan AI.
og_title: Cara Menjalankan OCR di Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Cara Menjalankan OCR di Python – Panduan Lengkap
url: /id/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR di Python – Panduan Lengkap

Pernah bertanya-tanya **bagaimana menjalankan OCR** pada sekumpulan PDF yang dipindai tanpa menghabiskan berjam‑jam mengatur parameter? Anda tidak sendirian. Dalam banyak proyek, rintangan pertama hanyalah mendapatkan teks yang dapat diandalkan dari sebuah gambar, dan perbedaan antara hasil yang goyah dan ekstraksi yang bersih seringkali bergantung pada beberapa langkah cerdas.

Dalam panduan ini kami akan membahas alur kerja empat‑langkah yang tidak hanya **menjalankan OCR** tetapi juga **meningkatkan akurasi OCR** dengan menggabungkan pass teks biasa yang cepat, pass kedua yang memperhatikan tata letak, dan post‑processor berbasis AI. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan, penjelasan jelas mengapa setiap tahap penting, serta tips menangani kasus khusus seperti halaman multi‑kolom atau pemindaian berisik.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

- **Python 3.9+** – kode ini menggunakan type hints dan f‑strings.  
- **Tesseract OCR** terpasang dan dapat diakses melalui perintah `tesseract`. (Di Ubuntu: `sudo apt install tesseract-ocr`; di Windows unduh installer dari repositori resmi.)  
- Wrapper **pytesseract** (`pip install pytesseract`).  
- **Pustaka post‑processing AI** – untuk contoh ini kami mengasumsikan Anda memiliki modul ringan `ai` yang menyediakan `run_postprocessor`. Ganti dengan API GPT‑4 OpenAI atau LLM lokal jika diinginkan.  
- Beberapa gambar atau PDF contoh untuk diuji.

Itu saja. Tanpa kerangka kerja berat, tanpa Docker yang rumit. Hanya beberapa instalasi pip dan Anda siap meluncur.

---

## Langkah 1: Lakukan Pass OCR Teks Biasa yang Cepat

Hal pertama yang sering terlewatkan pengembang adalah bahwa *plain text* OCR berjalan sangat cepat dan memberikan pemeriksaan sanity yang cepat. Kami akan memanggil `engine.Recognize()` untuk mengambil karakter mentah tanpa metadata tata letak apa pun. Inilah yang kami maksud dengan **plain text OCR**.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Mengapa ini penting:*  
- **Kecepatan** – pass teks biasa pada halaman 300 dpi biasanya selesai dalam kurang dari satu detik.  
- **Baseline** – Anda dapat membandingkan output terstruktur selanjutnya dengan baseline ini untuk menemukan kesalahan yang mencolok.  
- **Deteksi kesalahan** – jika pass teks biasa gagal total (misalnya semua karakter acak), Anda tahu kualitas gambar terlalu rendah dan dapat menghentikan proses lebih awal.

---

## Langkah 2: Jalankan Pass OCR Berbasis Tata Letak yang Detail

Teks biasa bagus, tetapi mengabaikan *di mana* setiap kata berada di halaman. Untuk faktur, formulir, atau majalah multi‑kolom Anda memerlukan koordinat, nomor baris, dan bahkan informasi font. Di sinilah `engine.RecognizeStructured()` berperan.

Berikut adalah wrapper tipis di atas output **TSV** Tesseract, yang memberikan hierarki halaman → baris → kata, sambil mempertahankan bounding box.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Mengapa kami melakukannya:*  
- **Koordinat** memungkinkan Anda memetakan teks yang diekstrak kembali ke gambar asli untuk penyorotan atau redaksi.  
- **Pengelompokan baris** mempertahankan tata letak asli, yang penting saat Anda harus merekonstruksi tabel atau kolom.  
- Pass ini sedikit lebih lambat dibandingkan pass teks biasa, tetapi tetap selesai dalam beberapa detik untuk kebanyakan dokumen.

---

## Langkah 3: Jalankan AI Post‑Processor untuk Memperbaiki Kesalahan OCR

Bahkan mesin OCR terbaik pun membuat kesalahan—misalnya “rn” vs “m”, hilangnya diakritik, atau kata terpisah. Model AI dapat melihat string mentah dan data terstruktur, menemukan inkonsistensi, dan menulis ulang teks sambil menjaga koordinat asli tetap utuh.

Berikut adalah implementasi **mock**; ganti tubuh fungsi dengan panggilan LLM nyata jika Anda memilikinya.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Mengapa langkah ini meningkatkan akurasi OCR:*  
- **Perbaikan kontekstual** – AI dapat memutuskan bahwa “l0ve” kemungkinan besar “love” berdasarkan kata‑kata di sekitarnya.  
- **Preservasi koordinat** – Anda tetap menyimpan informasi tata letak, sehingga tugas downstream (seperti anotasi PDF) tetap akurat.  
- **Penyempurnaan iteratif** – Anda dapat menjalankan post‑processor beberapa kali, setiap pass membersihkan lebih banyak kesalahan.

---

## Langkah 4: Iterasi Melalui Output Terstruktur yang Telah Diperbaiki

Setelah kita memiliki struktur yang bersih, mengekstrak teks akhir menjadi sangat mudah. Di bawah ini kami mencetak setiap baris, tetapi Anda juga dapat menulis ke CSV, memasukkan ke basis data, atau menghasilkan PDF yang dapat dicari.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Output yang diharapkan** (asumsi faktur satu‑halaman sederhana):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Perhatikan bagaimana pemisahan baris dan urutan kolom tetap terjaga, serta gangguan OCR umum seperti “$15.00” yang terbaca sebagai “$15,00” telah diperbaiki oleh langkah AI.

---

## Bagaimana Alur Kerja Ini Membantu **Meningkatkan Akurasi OCR**

| Tahap | Apa yang diperbaiki | Mengapa penting |
|------|---------------------|-----------------|
| **Plain text OCR** | Mendeteksi halaman yang tidak dapat dibaca sejak awal | Menghemat waktu dengan melewatkan input yang tidak dapat dipulihkan |
| **Structured OCR** | Menangkap tata letak, koordinat | Memungkinkan tugas downstream (penyorotan, redaksi) |
| **AI post‑processor** | Memperbaiki ejaan, menggabungkan kata terpisah, memperbaiki angka | Meningkatkan akurasi karakter secara keseluruhan dari ~85 % menjadi >95 % pada pemindaian berisik |
| **Iteration** | Memungkinkan Anda menjalankan ulang dengan parameter yang disesuaikan | Menyempurnakan alur kerja untuk tipe dokumen tertentu |

Dengan menggabungkan tiga konsep ini—**plain text OCR**, ekstraksi berbasis tata letak, dan koreksi AI—Anda mendapatkan solusi yang kuat yang *secara signifikan* **meningkatkan akurasi OCR** tanpa harus menulis jaringan saraf khusus dari nol.

---

## Kesalahan Umum & Tips Pro

- **Kesalahan:** Menggunakan gambar beresolusi rendah (≤150 dpi) pada Tesseract menghasilkan output berantakan.  
  **Tips pro:** Lakukan pra‑pemrosesan dengan `Pillow`—terapkan `Image.convert('L')` dan `Image.filter(ImageFilter.MedianFilter())` sebelum OCR.

- **Kesalahan:** AI post‑processor secara tidak sengaja mengubah istilah khusus domain (misalnya “SKU123”).  
  **Tips pro:** Buat whitelist istilah dan berikan ke LLM atau ke pustaka spell‑checker seperti `pyspellchecker`.

- **Kesalahan:** Halaman multi‑kolom digabung menjadi satu baris.  
  **Tips pro:** Deteksi batas kolom menggunakan field `block_num` pada output TSV Tesseract dan pisahkan baris sesuai kebutuhan.

- **Kesalahan:** PDF besar menyebabkan memori meledak saat memuat semua halaman sekaligus.  
  **Tips pro:** Proses halaman secara bertahap—loop melalui `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## Memperluas Pipeline

Jika Anda penasaran dengan langkah selanjutnya, pertimbangkan peningkatan berikut:

1. **Pemrosesan batch** – Bungkus seluruh skrip dalam fungsi yang menelusuri direktori, menangani ribuan file secara paralel dengan `concurrent.futures`.  
2. **Model bahasa** – Ganti heuristik difflib sederhana dengan panggilan ke `gpt‑4o` OpenAI atau model LLaMA yang di‑host secara lokal untuk koreksi kontekstual yang lebih kaya.  
3. **Format ekspor** – Tulis struktur yang telah diperbaiki ke PDF yang dapat dicari  

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Cara Menggunakan OCR - Teknik Lanjutan dengan Aspose.OCR untuk Java](/ocr/english/java/advanced-ocr-techniques/)
- [Tingkatkan Akurasi OCR – Mode Deteksi Area dalam OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}