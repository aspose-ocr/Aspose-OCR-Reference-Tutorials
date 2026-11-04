---
category: general
date: 2026-03-28
description: Pelajari cara menjalankan OCR pada gambar, mengunduh model Hugging Face
  secara otomatis, membersihkan teks OCR, dan mengonfigurasi model LLM di Python menggunakan
  Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: id
og_description: Jalankan OCR pada gambar dan bersihkan outputnya menggunakan model
  Hugging Face yang diunduh secara otomatis. Panduan ini menunjukkan cara mengonfigurasi
  model LLM di Python.
og_title: Jalankan OCR pada Gambar – Tutorial Lengkap Aspose OCR Cloud
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Jalankan OCR pada Gambar dengan Aspose OCR Cloud – Panduan Langkah-demi-Langkah
  Lengkap
url: /id/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar – Tutorial Lengkap Aspose OCR Cloud

Pernahkah Anda perlu menjalankan OCR pada file gambar tetapi output mentahnya terlihat berantakan? Menurut pengalaman saya, titik sakit terbesar bukanlah pengenalan itu sendiri—melainkan pembersihan. Untungnya, Aspose OCR Cloud memungkinkan Anda menambahkan post‑processor LLM yang dapat *membersihkan teks OCR* secara otomatis. Dalam tutorial ini kita akan membahas semua yang Anda perlukan: mulai dari **mengunduh model Hugging Face** hingga mengonfigurasi LLM, menjalankan mesin OCR, dan akhirnya memoles hasilnya.

Pada akhir panduan ini Anda akan memiliki skrip siap‑jalankan yang:

1. Mengambil model Qwen 2.5 yang ringkas dari Hugging Face (diunduh otomatis untuk Anda).  
2. Mengonfigurasi model untuk menjalankan sebagian jaringan di GPU dan sisanya di CPU.  
3. Menjalankan mesin OCR pada gambar catatan tulisan tangan.  
4. Menggunakan LLM untuk membersihkan teks yang dikenali, memberikan output yang dapat dibaca manusia.

> **Prasyarat** – Python 3.8+, paket `asposeocrcloud`, GPU dengan setidaknya 4 GB VRAM (opsional tetapi disarankan), dan koneksi internet untuk pengunduhan model pertama.

---

## Apa yang Anda Butuhkan

- **Aspose OCR Cloud SDK** – instal melalui `pip install asposeocrcloud`.  
- **Sebuah gambar contoh** – misalnya `handwritten_note.jpg` yang ditempatkan di folder lokal.  
- **Dukungan GPU** – jika Anda memiliki GPU yang mendukung CUDA, skrip akan memindahkan 30 lapisan; jika tidak, akan otomatis kembali ke CPU.  
- **Izin menulis** – skrip menyimpan cache model di `YOUR_DIRECTORY`; pastikan folder tersebut ada.

---

## Langkah 1 – Mengonfigurasi Model LLM (unduh model Hugging Face)

Hal pertama yang kami lakukan adalah memberi tahu Aspose AI dari mana mengambil model. Kelas `AsposeAIModelConfig` menangani pengunduhan otomatis, kuantisasi, dan alokasi lapisan GPU.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Mengapa ini penting** – Mengkuantisasi ke `int8` secara drastis mengurangi penggunaan memori (≈ 4 GB vs 12 GB). Membagi model antara GPU dan CPU memungkinkan Anda menjalankan LLM 3 miliar parameter bahkan pada RTX 3060 yang sederhana. Jika Anda tidak memiliki GPU, setel `gpu_layers=0` dan SDK akan menjaga semuanya di CPU.

> **Tip:** Jalankan pertama kali akan mengunduh sekitar ~ 1,5 GB, jadi beri beberapa menit dan koneksi yang stabil.

---

## Langkah 2 – Menginisialisasi Mesin AI dengan Konfigurasi Model

Sekarang kami memulai mesin Aspose AI dan memberinya konfigurasi yang baru saja dibuat.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**Apa yang terjadi di balik layar?** SDK memeriksa `directory_model_path` untuk model yang sudah ada. Jika menemukan versi yang cocok, ia memuatnya secara instan; jika tidak, ia mengunduh file GGUF dari Hugging Face, mengekstraknya, dan menyiapkan pipeline inferensi.

---

## Langkah 3 – Membuat Mesin OCR dan Menambahkan Post‑Processor AI

Mesin OCR melakukan pekerjaan berat dalam mengenali karakter. Dengan menambahkan `ocr_ai.run_postprocessor` kami mengaktifkan **pembersihan teks OCR** secara otomatis setelah pengenalan.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Mengapa menggunakan post‑processor?** OCR mentah sering menyertakan pemisahan baris di tempat yang salah, tanda baca yang terdeteksi keliru, atau simbol yang tidak diinginkan. LLM dapat menulis ulang output menjadi kalimat yang tepat, memperbaiki ejaan, dan bahkan menebak kata yang hilang—pada dasarnya mengubah dump mentah menjadi prosa yang dipoles.

---

## Langkah 4 – Menjalankan OCR pada File Gambar

Setelah semuanya terhubung, saatnya memberi gambar ke mesin.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Kasus tepi:** Jika gambar berukuran besar (> 5 MP), Anda mungkin ingin mengubah ukurannya terlebih dahulu untuk mempercepat pemrosesan. SDK menerima objek Pillow `Image`, jadi Anda dapat melakukan pra‑proses dengan `PIL.Image.thumbnail()` bila diperlukan.

---

## Langkah 5 – Biarkan AI Membersihkan Teks yang Dikenali dan Tampilkan Kedua Versi

Akhirnya kami memanggil post‑processor yang telah kami lampirkan sebelumnya. Langkah ini menunjukkan kontras antara *sebelum* dan *sesudah* pembersihan.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Output yang Diharapkan

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Perhatikan bagaimana LLM telah:

- Memperbaiki kesalahan pengenalan OCR umum (`Th1s` → `This`).  
- Menghapus simbol yang tidak diinginkan (`&` → `and`).  
- Menormalkan pemisahan baris menjadi kalimat yang tepat.

---

## 🎨 Ikhtisar Visual (Alur Kerja Jalankan OCR pada Gambar)

![Jalankan OCR pada gambar workflow](run_ocr_on_image_workflow.png "Diagram yang menunjukkan alur kerja jalankan OCR pada gambar mulai dari pengunduhan model hingga output yang sudah dibersihkan")

Diagram di atas merangkum seluruh pipeline: **unduh model Hugging Face → konfigurasikan LLM → inisialisasi AI → mesin OCR → post‑processor AI → bersihkan teks OCR**.

---

## Pertanyaan Umum & Tips Pro

### Bagaimana jika saya tidak memiliki GPU?

Setel `gpu_layers=0` pada `AsposeAIModelConfig`. Model akan berjalan sepenuhnya di CPU, yang lebih lambat namun tetap berfungsi. Anda juga dapat beralih ke model yang lebih kecil (misalnya `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) agar waktu inferensi tetap wajar.

### Bagaimana cara mengubah model nanti?

Cukup perbarui `hugging_face_repo_id` dan jalankan kembali `ocr_ai.initialize(model_config)`. SDK akan mendeteksi perubahan versi, mengunduh model baru, dan menggantikan file cache.

### Bisakah saya menyesuaikan prompt post‑processor?

Ya. Kirimkan kamus ke `custom_settings` dengan kunci `prompt_template`. Contohnya:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Haruskah saya menyimpan teks yang sudah dibersihkan ke file?

Tentu saja. Setelah pembersihan Anda dapat menulis hasilnya ke file `.txt` atau `.json` untuk pemrosesan lebih lanjut:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Kesimpulan

Kami baru saja menunjukkan cara **menjalankan OCR pada gambar** dengan Aspose OCR Cloud, secara otomatis **mengunduh model Hugging Face**, secara ahli **mengonfigurasi pengaturan model LLM**, dan akhirnya **membersihkan teks OCR** menggunakan post‑processor LLM yang kuat. Seluruh proses dapat dimasukkan ke dalam satu skrip Python yang mudah dijalankan dan berfungsi baik pada mesin dengan GPU maupun hanya CPU.

Jika Anda sudah nyaman dengan pipeline ini, pertimbangkan untuk bereksperimen dengan:

- **LLM yang berbeda** – coba `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` untuk jendela konteks yang lebih besar.  
- **Pemrosesan batch** – iterasi melalui folder gambar dan gabungkan hasil yang sudah dibersihkan ke dalam CSV.  
- **Prompt khusus** – sesuaikan AI dengan domain Anda (dokumen hukum, catatan medis, dll.).

Silakan ubah nilai `gpu_layers`, ganti model, atau pasang prompt Anda sendiri. Langit adalah batasnya, dan kode yang Anda miliki sekarang adalah landasan peluncuran.

Selamat coding, semoga output OCR Anda selalu bersih! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}