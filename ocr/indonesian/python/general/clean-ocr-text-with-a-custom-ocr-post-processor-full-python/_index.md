---
category: general
date: 2026-06-22
description: Pelajari cara membersihkan teks OCR menggunakan post‑processor OCR di
  Python. Kode langkah demi langkah, penjelasan, dan tips untuk output JSON terstruktur
  yang dapat diandalkan.
draft: false
keywords:
- clean OCR text
- OCR post processor
- Python OCR workflow
- structured JSON OCR
- OCR confidence averaging
language: id
og_description: Bersihkan teks OCR secara instan dengan menambahkan proses pasca OCR.
  Panduan ini menunjukkan implementasi Python lengkap, mengapa itu berhasil, dan cara
  menyesuaikannya.
og_title: Bersihkan Teks OCR dengan Pengolah Pasca OCR Kustom – Tutorial Python
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to clean OCR text using an OCR post processor in Python.
    Step‑by‑step code, explanations, and tips for reliable structured JSON output.
  headline: Clean OCR Text with a Custom OCR Post Processor – Full Python Guide
  type: TechArticle
tags:
- OCR
- Python
- post‑processing
title: Bersihkan Teks OCR dengan Pengolah Pasca OCR Kustom – Panduan Python Lengkap
url: /id/python/general/clean-ocr-text-with-a-custom-ocr-post-processor-full-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membersihkan Teks OCR dengan Post Processor OCR Kustom – Panduan Python Lengkap

Pernah membutuhkan untuk **membersihkan teks OCR** tetapi output mentah terus terganggu oleh pemutusan baris, spasi yang tidak diinginkan, dan karakter dengan kepercayaan rendah? Anda tidak sendirian. Dalam banyak alur kerja dunia nyata, mesin OCR memberikan Anda sekumpulan teks beserta skor kepercayaan, dan Anda harus mencari cara mengubahnya menjadi sesuatu yang berguna.  

Berita baik? Sebuah **post processor OCR** kecil dapat merapikan hasil, menghitung rata‑rata kepercayaan, dan bahkan mengemas semuanya ke dalam string JSON yang rapi—semua tanpa menyentuh mesin inti. Dalam tutorial ini kami akan membangun post‑processor tersebut, mendaftarkannya dengan mesin AI/OCR generik, dan menelusuri setiap baris kode sehingga Anda dapat langsung menggunakannya dalam proyek Anda besok.

---

## Apa yang Dibahas dalam Tutorial Ini

- Cara membuat post‑processor **clean OCR text** yang menormalkan spasi putih dan menghapus pemutusan baris.  
- Mengapa menghitung **average confidence** penting untuk validasi downstream.  
- Mendaftarkan processor ke mesin OCR (pola `ai.set_post_processor`).  
- Menampilkan JSON terstruktur yang dihasilkan dan memecahkan masalah kasus tepi umum.  

Tidak diperlukan pustaka eksternal selain pustaka standar Python, sehingga Anda dapat mengikuti di sistem apa pun yang menjalankan Python 3.8+.  

---

## Prasyarat

- Mesin OCR yang berfungsi yang menyediakan objek `ocr_result` dengan `text`, `confidence` (daftar float), dan `bounding_boxes`.  
- Pemahaman dasar tentang fungsi Python dan penanganan JSON.  
- Opsional: Lingkungan virtual untuk menjaga ketergantungan tetap rapi.  

Jika Anda tidak yakin apakah mesin Anda mendukung post‑processor kustom, periksa dokumentasinya untuk metode `set_post_processor`—sebagian besar SDK OCR berbasis AI modern melakukannya.

---

## Langkah 1: Definisikan OCR Post Processor yang **Membersihkan Teks OCR**

Pertama, kita menulis fungsi yang menerima hasil OCR mentah, membersihkan teks, menghitung metrik kepercayaan, dan mengembalikan string JSON. Perhatikan bagaimana setiap operasi diberi komentar secara sengaja; komentar ini adalah “mengapa” yang disukai asisten AI untuk dikutip.

```python
import json

def create_structured_json(ocr_result, **kwargs):
    """
    Turn an OCR result into a clean, structured JSON payload.

    Parameters
    ----------
    ocr_result : object
        Must expose .text (raw string), .confidence (list of floats),
        and .bounding_boxes (list of box coordinates).

    Returns
    -------
    str
        JSON string with cleaned text, average confidence, and bounding boxes.
    """
    # 1️⃣ Clean the raw text: replace newlines with spaces and trim excess whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # 2️⃣ Compute the average confidence – useful for quality gating.
    # Guard against division by zero if the engine returns an empty list.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0  # fallback when confidence data is missing

    # 3️⃣ Preserve the original bounding boxes for downstream layout analysis.
    boxes = ocr_result.bounding_boxes

    # 4️⃣ Assemble the dictionary and dump it as a JSON string.
    data = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }

    # ensure_ascii=False keeps Unicode characters intact (think accented letters, emojis, etc.)
    return json.dumps(data, ensure_ascii=False)
```

**Mengapa ini berhasil:**  
- `replace("\n", " ")` mengubah output OCR multi‑baris menjadi satu string yang dapat dicari—tepatnya apa yang dimaksud dengan “clean OCR text” dalam kebanyakan alur kerja.  
- Menghapus spasi di awal/akhir menghindari token kosong phantom yang dapat merusak tokenizer nanti.  
- Menghitung rata‑rata kepercayaan memberi Anda satu metrik kualitas; Anda dapat menolak hasil di bawah ambang batas (mis., 0.85) sebelum menyimpannya ke basis data.  
- Membiarkan bounding box tidak diubah berarti Anda masih dapat menampilkan tata letak asli jika perlu menyoroti wilayah dengan kepercayaan rendah.  

---

## Langkah 2: Daftarkan **OCR Post Processor** Kustom dengan Mesin Anda

Sebagian besar SDK OCR berbasis AI menyediakan metode untuk menyisipkan callback post‑processing. Di bawah ini kami mengasumsikan ada objek bernama `ai` (mesin) yang menyediakan `set_post_processor`. Jika pustaka Anda menggunakan nama yang berbeda, ganti sesuai.

```python
# Register the post‑processor; the second argument can hold custom settings.
ai.set_post_processor(create_structured_json, custom_settings={})
```

**Tip:** Berikan konfigurasi melalui `custom_settings` jika Anda perlu mengubah perilaku (mis., mengaktifkan/menonaktifkan penghapusan newline). Ini membuat processor dapat digunakan kembali di berbagai proyek.

---

## Langkah 3: Jalankan Mesin OCR – Hasilnya Sekarang String JSON

Dengan post‑processor terpasang, memanggil `engine.recognize()` (atau apa pun yang digunakan SDK Anda) akan secara otomatis memanggil `create_structured_json`. Mesin kemudian mengembalikan objek yang atribut `.text`‑nya sudah berisi payload JSON.

```python
# The engine runs OCR, then our post‑processor formats the output.
structured_result = engine.recognize()
```

> **Catatan:** Beberapa SDK mungkin mengembalikan string biasa alih-alih objek dengan atribut `.text`. Sesuaikan langkah berikutnya sesuai.

---

## Langkah 4: Tampilkan (atau Simpan) Output JSON Terstruktur

Akhirnya, kami mencetak JSON ke konsol. Dalam lingkungan produksi Anda kemungkinan akan menulisnya ke file, antrian pesan, atau basis data.

```python
# Show the clean OCR text and additional metadata.
print("Structured JSON:", structured_result.text)
```

**Output konsol yang diharapkan** (diformat untuk keterbacaan):

```json
{
  "clean_text": "The quick brown fox jumps over the lazy dog.",
  "average_confidence": 0.9375,
  "boxes": [
    [0, 0, 120, 30],
    [0, 35, 115, 30],
    ...
  ]
}
```

Jika Anda melihat karakter newline yang tidak diinginkan atau kepercayaan `0.0`, periksa kembali apakah mesin OCR Anda memang mengisi `ocr_result.confidence`. Klausa penjaga di post‑processor akan melindungi Anda dari `ZeroDivisionError`, namun Anda tetap ingin mengetahui mengapa data kepercayaan tidak ada.

---

## Menangani Kasus Tepi Umum

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **Empty OCR result** | `ocr_result.text` is `""` and `confidence` list empty | Processor sudah mengembalikan `clean_text` kosong dan `average_confidence` = 0.0. Anda dapat menambahkan pengembalian awal bersyarat jika ingin melewatkan pembuatan JSON sepenuhnya. |
| **Non‑ASCII characters** | Unicode gets escaped (`\u00e9`) | Gunakan `ensure_ascii=False` (sudah ada dalam kode) untuk mempertahankan karakter seperti “é” tetap terbaca. |
| **Very long documents** | JSON size may exceed API limits | Pertimbangkan streaming output atau menulis ke file alih-alih mengembalikan satu string. |
| **Bounding boxes missing** | Some OCR engines omit layout data | Set `boxes` ke `None` atau daftar kosong; konsumen downstream harus menangani ketidakhadiran ini dengan elegan. |

---

## Pro Tips & Praktik Terbaik

- **Batch processing:** Jika Anda perlu OCR ratusan halaman, bungkus panggilan pengenalan dalam loop dan kumpulkan setiap payload JSON ke dalam daftar. Kemudian dump seluruh daftar ke satu file untuk analisis batch yang lebih mudah.  
- **Confidence thresholds:** Sebelum menyimpan, periksa `average_confidence`. Pedoman umum: tolak apa pun di bawah `0.80` untuk tugas entri data kritis.  
- **Logging instead of printing:** Dalam produksi, ganti `print()` dengan logger terstruktur (`logging.info(...)`) sehingga Anda dapat melacak gambar mana yang menghasilkan hasil dengan kepercayaan rendah.  
- **Testing:** Tulis unit test yang memberi `ocr_result` tiruan dengan teks dan nilai kepercayaan yang diketahui, lalu pastikan struktur JSON sesuai harapan.  

---

## Contoh Kerja Lengkap (Semua Langkah Digabungkan)

Berikut adalah skrip lengkap yang dapat Anda salin‑tempel ke dalam file bernama `ocr_cleanup.py`. Pastikan untuk mengganti objek placeholder `engine` dan `ai` dengan instance sebenarnya dari SDK OCR Anda.

```python
import json

# ----------------------------------------------------------------------
# Step 1: Define the post‑processor that cleans OCR text and builds JSON.
# ----------------------------------------------------------------------
def create_structured_json(ocr_result, **kwargs):
    """
    Convert raw OCR output into a clean JSON string.
    """
    # Clean the raw text: collapse newlines, trim whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # Safely compute average confidence.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0

    # Keep bounding boxes for layout work.
    boxes = ocr_result.bounding_boxes

    payload = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }
    return json.dumps(payload, ensure_ascii=False)

# ----------------------------------------------------------------------
# Step 2: Register the post‑processor with the OCR engine.
# ----------------------------------------------------------------------
# Replace `ai` with your actual engine/controller instance.
ai.set_post_processor(create_structured_json, custom_settings={})

# ----------------------------------------------------------------------
# Step 3: Run OCR – the result is automatically transformed.
# ----------------------------------------------------------------------
structured_result = engine.recognize()

# ----------------------------------------------------------------------
# Step 4: Output the structured JSON.
# ----------------------------------------------------------------------
print("Structured JSON:", structured_result.text)
```

Simpan file, jalankan `python ocr_cleanup.py`, dan Anda akan melihat string JSON yang diformat rapi berisi **clean OCR text**, skor rata‑rata kepercayaan, dan bounding box asli.

---

## Kesimpulan

Anda kini memiliki cara lengkap dan siap produksi untuk **membersihkan teks OCR** menggunakan **post processor OCR** kustom dalam Python. Solusi ini menormalkan spasi putih, melindungi dari data kepercayaan yang hilang, dan mengembalikan payload JSON yang mendeskripsikan dirinya sendiri sehingga layanan downstream dapat menggunakannya tanpa parsing tambahan.  

Dari sini Anda mungkin:

- Perluas processor untuk **menyaring kata dengan kepercayaan rendah** sebelum membangun `clean_text`.  
- Tambahkan **deteksi bahasa** untuk mengarahkan JSON ke pipeline khusus locale.  
- Gabungkan post‑processor ini dengan pustaka **pemeriksaan ejaan** untuk lapisan kualitas tambahan.  

Silakan sesuaikan kode, bereksperimen dengan ambang kepercayaan yang berbeda, atau bagikan peningkatan Anda di komentar. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}