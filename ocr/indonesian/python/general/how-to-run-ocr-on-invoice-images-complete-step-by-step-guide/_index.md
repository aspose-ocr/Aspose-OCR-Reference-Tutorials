---
category: general
date: 2026-01-12
description: Cara menjalankan OCR dan mengekstrak teks dari gambar faktur menggunakan
  Aspose OCR dan model ringan Hugging Face. Pelajari cara mengunduh model, memperbaiki
  kesalahan OCR, dan melakukan OCR pada gambar.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: id
og_description: Cara menjalankan OCR pada gambar faktur, mengekstrak teks, dan memperbaiki
  kesalahan dengan LLM Hugging Face. Ikuti panduan lengkap ini untuk hasil yang sempurna.
og_title: Cara Menjalankan OCR pada Gambar Faktur – Tutorial Lengkap
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Cara Menjalankan OCR pada Gambar Faktur – Panduan Langkah-demi-Langkah Lengkap
url: /id/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR pada Gambar Faktur – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya‑tanya **cara menjalankan OCR** pada faktur yang dipindai dan mendapatkan teks bersih yang dapat dicari tanpa menghabiskan berjam‑jam membersihkannya? Anda tidak sendirian. Dalam banyak proyek dunia nyata, output OCR mentah penuh dengan kesalahan pengenalan—misalnya “O” untuk “0”, “l” untuk “1”, atau bahkan kata‑kata yang seluruhnya kacau. Kabar baik? Dengan beberapa baris Python Anda tidak hanya dapat **melakukan OCR pada gambar** tetapi juga secara otomatis **memperbaiki kesalahan OCR** menggunakan model ringan dari Hugging Face.

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui: mulai dari memuat gambar faktur, mengekstrak teks mentah, mengunduh model terkuantisasi, hingga memoles hasil sehingga Anda mendapatkan transkripsi sempurna yang siap diproses lebih lanjut. Pada akhir tutorial Anda akan dapat **mengekstrak teks dari faktur** dalam format PDF atau PNG dengan satu skrip yang dapat diulang.

## Prasyarat & Penyiapan

Sebelum melanjutkan, pastikan Anda memiliki:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.9+ | Sintaks modern dan tipe hint |
| `aspose-ocr` package | Menyediakan `ocr.OcrEngine` yang digunakan dalam contoh |
| `aspose-ai` package | Menyediakan post‑processor `AsposeAI` |
| Akses ke GPU (opsional) | Mempercepat lapisan LLM; jika tidak, CPU tetap dapat digunakan |
| Koneksi internet (untuk pertama kali) | Diperlukan untuk **mengunduh model Hugging Face** secara otomatis |

Anda dapat menginstal pustaka yang diperlukan dengan:

```bash
pip install aspose-ocr aspose-ai
```

> **Tips pro:** Jika Anda berencana menjalankan LLM di GPU, instal `torch` dengan dukungan CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Setelah lingkungan siap, mari masuk ke kode.

---

## Langkah 1 – Inisialisasi Mesin OCR dan Muat Gambar Faktur Anda

Hal pertama yang harus Anda lakukan adalah membuat instance mesin OCR Aspose dan menunjuk ke file yang ingin diproses. Langkah ini merupakan fondasi **cara menjalankan OCR** pada gambar apa pun.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Mengapa ini penting:** `load_image` menerima PNG, JPEG, TIFF, bahkan halaman PDF, memungkinkan Anda **melakukan OCR pada gambar** terlepas dari formatnya.

---

## Langkah 2 – Jalankan OCR Dasar untuk Menangkap Teks Mentah

Setelah gambar dimuat, mesin dapat menghasilkan transkripsi mentah. Output ini sering berisik, itulah mengapa kami nanti akan menjalankan langkah koreksi.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Output mentah tipikal mungkin terlihat seperti:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Perhatikan angka nol (`0`) di tempat seharusnya huruf “O”? Itulah jenis kesalahan yang akan kami perbaiki nanti.

---

## Langkah 3 – Konfigurasikan AI Post‑Processor dengan LLM Ringan

Sekarang kami membawa **model Hugging Face yang diunduh** yang cukup kecil untuk dijalankan pada perangkat keras sederhana namun cukup kuat untuk memahami bahasa faktur. Contoh ini menggunakan model Qwen 2.5 3B‑Instruct GGUF, terkuantisasi ke `int8` untuk jejak memori yang sangat kecil.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Mengapa model ini?** Kuantisasi `int8` mengecilkan file menjadi ~1,2 GB, sehingga dapat dijalankan pada kebanyakan laptop. Lapisan GPU mempercepat inferensi, tetapi kode akan otomatis beralih ke CPU bila tidak ada GPU.

---

## Langkah 4 – Jalankan Koreksi Berbasis LLM pada Hasil OCR Mentah

Dengan model yang siap, kami memasukkan teks mentah ke post‑processor. LLM akan menulis ulang transkripsi, memperbaiki glitch OCR umum dan menormalkan angka.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Output bersih yang diharapkan:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Anda dapat melihat angka nol telah berubah kembali menjadi huruf “O”, dan “Am0unt” kini menjadi “Amount”. Inilah inti **memperbaiki kesalahan OCR** secara otomatis.

---

## Langkah 5 – Lepaskan Sumber Daya dan Bersihkan

Model bahasa besar dapat menahan memori GPU, jadi sebaiknya bebaskan sumber daya setelah selesai.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Jika Anda berencana memproses banyak faktur secara batch, Anda dapat mempertahankan model tetap dimuat dan hanya membebaskannya di akhir skrip.

---

## Contoh Skrip Lengkap

Menggabungkan semuanya, berikut satu skrip yang dapat Anda simpan sebagai file `.py` dan jalankan:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Menjalankan skrip akan menghasilkan output serupa dengan blok “AI‑corrected” yang ditunjukkan sebelumnya. Ganti jalur gambar dengan faktur atau kwitansi lain untuk **mengekstrak teks dari faktur** secara massal.

---

## Pertanyaan yang Sering Diajukan & Kasus Khusus

### Bagaimana jika saya tidak memiliki GPU?

Parameter `gpu_layers` bersifat opsional. Atur ke `0` atau hapus, dan model akan berjalan sepenuhnya di CPU. Harapkan inferensi yang lebih lambat—sekitar 2–3 detik per halaman pada laptop modern.

### Faktur saya berupa PDF multi‑halaman. Bagaimana cara menanganinya?

Konversi setiap halaman menjadi gambar terpisah (misalnya dengan `pdf2image`) dan lakukan loop pada halaman‑halaman tersebut dengan skrip yang sama. Mesin OCR dapat memproses tiap gambar secara independen, dan LLM akan memperbaiki tiap blok teks.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Unduhan model gagal karena firewall?

Unduh model secara manual dari Hugging Face model hub, ekstrak ke folder lokal, dan arahkan `hugging_face_repo_id` ke jalur lokal tersebut:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Seberapa akurat koreksinya?

Untuk faktur berbahasa Inggris standar, LLM memperbaiki >95 % kesalahan OCR umum. Catatan tulisan tangan yang kompleks mungkin masih memerlukan tinjauan manual.

---

## Tips & Trik untuk Penggunaan Produksi

- **Pemrosesan batch:** Bungkus langkah 2‑4 dalam sebuah fungsi dan berikan daftar jalur file. Gunakan kembali instance `AsposeAI` yang sama untuk menghindari pemuatan model berulang.
- **Logging:** Ganti `print` dengan modul `logging` Python untuk merekam output mentah dan bersih demi jejak audit.
- **Penanganan error:** Bungkus panggilan OCR dengan blok `try/except`. Jika sebuah gambar gagal, catat nama file dan lanjutkan.
- **Optimasi performa:** Bereksperimenlah dengan `gpu_layers`. Lebih banyak lapisan di GPU mempercepat inferensi tetapi meningkatkan penggunaan VRAM.

---

## Kesimpulan

Kami telah membahas **cara menjalankan OCR** pada gambar faktur dari awal hingga akhir, menunjukkan cara **melakukan OCR pada gambar**, **mengunduh model Hugging Face**, dan **memperbaiki kesalahan OCR** secara otomatis. Skrip lengkap memperlihatkan alur kerja praktis yang dapat Anda integrasikan ke dalam pipeline otomatisasi berbasis Python mana pun.

Langkah selanjutnya? Coba perluas pipeline untuk **mengekstrak bidang kunci** (nomor faktur, tanggal, total) menggunakan ekspresi reguler pada teks yang telah diperbaiki, atau alirkan output bersih ke basis data untuk pencarian. Anda juga dapat bereksperimen dengan LLM ringan lain dari Hugging Face jika memerlukan bahasa atau pengetahuan domain yang berbeda.

Selamat coding, semoga hasil OCR Anda selalu jernih! 

![cara menjalankan OCR pada gambar faktur](ocr_invoice_example.png "cara menjalankan OCR pada faktur")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}