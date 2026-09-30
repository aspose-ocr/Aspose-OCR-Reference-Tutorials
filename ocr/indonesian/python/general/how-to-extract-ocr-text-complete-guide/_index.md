---
category: general
date: 2026-02-22
description: Pelajari cara mengekstrak teks OCR dan meningkatkan akurasi OCR dengan
  pemrosesan pasca‑AI. Bersihkan teks OCR dengan mudah di Python menggunakan contoh
  langkah‑demi‑langkah.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: id
og_description: Temukan cara mengekstrak teks OCR, meningkatkan akurasi OCR, dan membersihkan
  teks OCR menggunakan alur kerja Python sederhana dengan pemrosesan AI pasca‑pengolahan.
og_title: Cara Mengekstrak Teks OCR – Panduan Langkah demi Langkah
tags:
- OCR
- AI
- Python
title: Cara Mengekstrak Teks OCR – Panduan Lengkap
url: /id/python/general/how-to-extract-ocr-text-complete-guide/
---

= re.sub(r"\s+", " ", txt).strip` and then blank line then `{{< /blocks/...`. The code block is not closed with triple backticks in original; maybe truncated. We must preserve original exactly. So we keep as is.

Now translate.

Let's produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekstrak Teks OCR – Tutorial Pemrograman Lengkap

Pernah bertanya‑tanya **bagaimana mengekstrak OCR** dari dokumen yang dipindai tanpa berakhir dengan sekumpulan typo dan baris yang rusak? Anda tidak sendirian. Dalam banyak proyek dunia nyata, output mentah dari mesin OCR terlihat seperti paragraf yang berantakan, dan membersihkannya terasa seperti pekerjaan rumah.

Kabar baiknya? Dengan mengikuti panduan ini Anda akan melihat cara praktis untuk mengambil data OCR terstruktur, menjalankan post‑processor AI, dan mendapatkan **teks OCR bersih** yang siap untuk analisis lanjutan. Kami juga akan menyentuh teknik untuk **meningkatkan akurasi OCR** sehingga hasilnya dapat diandalkan pada percobaan pertama.

Dalam beberapa menit ke depan kami akan membahas semua yang Anda perlukan: pustaka yang diperlukan, skrip lengkap yang dapat dijalankan, dan tips menghindari jebakan umum. Tanpa jalan pintas “lihat dokumentasinya”—hanya solusi lengkap yang dapat Anda salin‑tempel dan jalankan.

## Apa yang Anda Butuhkan

- Python 3.9+ (kode menggunakan type hints tetapi dapat berjalan pada versi 3.x yang lebih lama)
- Mesin OCR yang dapat mengembalikan hasil terstruktur (misalnya, Tesseract via `pytesseract` dengan flag `--psm 1`, atau API komersial yang menyediakan metadata blok/baris)
- Model post‑processing AI – untuk contoh ini kami akan mem‑mock‑nya dengan fungsi sederhana, tetapi Anda dapat menggantinya dengan `gpt‑4o-mini` dari OpenAI, Claude, atau LLM apa pun yang menerima teks dan mengembalikan output yang dibersihkan
- Beberapa baris gambar contoh (PNG/JPG) untuk diuji

Jika semua sudah siap, mari kita mulai.

## Cara Mengekstrak OCR – Pengambilan Awal

Langkah pertama adalah memanggil mesin OCR dan memintanya memberikan **representasi terstruktur** alih‑alih string polos. Hasil terstruktur mempertahankan batas blok, baris, dan kata, yang membuat proses pembersihan selanjutnya jauh lebih mudah.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **Mengapa ini penting:** Dengan mempertahankan blok dan baris, kita menghindari harus menebak di mana paragraf dimulai. Fungsi `recognize_structured` memberi kita hierarki bersih yang kemudian dapat kita berikan ke model AI.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Menjalankan potongan kode ini mencetak baris pertama persis seperti yang dilihat mesin OCR, yang sering berisi kesalahan pengenalan seperti “0cr” alih‑alih “OCR”.

## Tingkatkan Akurasi OCR dengan Post‑Processing AI

Setelah kita memiliki output terstruktur mentah, mari serahkan ke post‑processor AI. Tujuannya adalah **meningkatkan akurasi OCR** dengan memperbaiki kesalahan umum, menormalkan tanda baca, dan bahkan menyegmentasi ulang baris bila diperlukan.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **Pro tip:** Jika Anda tidak memiliki langganan LLM, Anda dapat mengganti pemanggilan dengan transformer lokal (misalnya, `sentence‑transformers` + model koreksi yang sudah di‑fine‑tune) atau bahkan pendekatan berbasis aturan. Ide utamanya adalah AI melihat setiap baris secara terpisah, yang biasanya cukup untuk **membersihkan teks OCR**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Sekarang Anda seharusnya melihat kalimat yang jauh lebih bersih—typo sudah diganti, spasi ekstra dihapus, dan tanda baca diperbaiki.

## Bersihkan Teks OCR untuk Hasil Lebih Baik

Bahkan setelah koreksi AI, Anda mungkin ingin menerapkan langkah sanitasi akhir: menghapus karakter non‑ASCII, menyatukan jeda baris, dan mengompres spasi ganda. Pass tambahan ini memastikan output siap untuk tugas downstream seperti NLP atau ingest ke basis data.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

Fungsi `final_cleanup` memberi Anda string polos yang dapat langsung dimasukkan ke indeks pencarian, model bahasa, atau ekspor CSV. Karena kami mempertahankan batas blok, struktur paragraf tetap terjaga.

## Kasus Pinggir & Skenario “What‑If”

- **Tata letak multi‑kolom:** Jika sumber Anda memiliki kolom, mesin OCR mungkin mencampur baris. Anda dapat mendeteksi koordinat kolom dari output TSV dan mengurutkan ulang baris sebelum mengirimnya ke AI.
- **Skrip non‑Latin:** Untuk bahasa seperti Mandarin atau Arab, ubah prompt LLM untuk meminta koreksi spesifik bahasa, atau gunakan model yang sudah di‑fine‑tune pada skrip tersebut.
- **Dokumen besar:** Mengirim setiap baris secara terpisah dapat lambat. Kelompokkan baris (misalnya, 10 per permintaan) dan biarkan LLM mengembalikan daftar baris yang sudah dibersihkan. Ingat untuk memperhatikan batas token.
- **Blok yang hilang:** Beberapa mesin OCR hanya mengembalikan daftar kata datar. Dalam kasus ini, Anda dapat membangun kembali baris dengan mengelompokkan kata‑kata yang memiliki nilai `line_num` serupa.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut satu file yang dapat Anda jalankan dari awal hingga akhir. Ganti placeholder dengan API key dan path gambar Anda sendiri.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}