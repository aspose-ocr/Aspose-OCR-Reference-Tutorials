---
category: general
date: 2026-08-12
description: Tambahkan pemeriksa ejaan ke pipeline AI Anda dan pelajari cara mengatur
  post‑processor, menambahkan post‑processing, serta menerapkan pemeriksaan ejaan
  di Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add spell checker
- add post processing
- use post processor
- apply spell checking
- how to set post processor
language: id
lastmod: 2026-08-12
og_description: Tambahkan pemeriksa ejaan ke pipeline AI Anda. Panduan ini menunjukkan
  cara mengatur pemroses pasca, menambahkan pemrosesan pasca, dan menerapkan pemeriksaan
  ejaan dalam beberapa menit.
og_image_alt: Diagram illustrating how to add spell checker as a post processor in
  an AI pipeline
og_title: Tambahkan pemeriksa ejaan ke pipeline AI – tutorial Python lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Add spell checker to your AI pipeline and learn how to set post processor,
    add post processing, and apply spell checking in Python.
  headline: Add spell checker to an AI pipeline – step‑by‑step guide
  type: TechArticle
- description: Add spell checker to your AI pipeline and learn how to set post processor,
    add post processing, and apply spell checking in Python.
  name: Add spell checker to an AI pipeline – step‑by‑step guide
  steps:
  - name: Why this works
    text: '* **`SpellChecker`** encapsulates the logic for detecting and correcting
      misspelled tokens. * **`set_post_processor`** tells the pipeline to invoke the
      supplied object after the primary model finishes inference. * The configuration
      dictionary lets you customize behavior (language, custom dictionarie'
  - name: What the wrapper does
    text: 1. **Runs the original inference** and captures the raw output. 2. **Detects
      the appropriate entry point** (`process` method or callable) on the supplied
      processor. 3. **Calls the processor** with the result and any options you provided.
  - name: Handling edge cases
    text: '| Situation | Recommended approach | |----------------------------------------|--------------------------------------------------------------------|
      | Input contains domain‑specific terms | Provide a custom dictionary via the
      `options` parameter. | | Processor raises an exception | Wrap the call in '
  type: HowTo
tags:
- AI pipeline
- Python
- post‑processing
title: Tambahkan pemeriksa ejaan ke pipeline AI – panduan langkah demi langkah
url: /id/python/general/add-spell-checker-to-an-ai-pipeline-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan pemeriksa ejaan ke pipeline AI – panduan langkah demi langkah

Jika Anda perlu **menambahkan pemeriksa ejaan** ke pipeline AI, tutorial ini menunjukkan secara tepat cara melakukannya. Anda akan melihat cara mengatur post processor, menambahkan post processing, dan menerapkan pemeriksaan ejaan dengan kode yang minimal.

Panduan ini mencakup semua hal mulai dari menginstal pustaka pemeriksaan ejaan khusus hingga menghubungkannya ke pipeline yang sudah ada. Pada akhir artikel Anda dapat menjalankan contoh end‑to‑end lengkap yang memperbaiki kesalahan ejaan dalam teks yang dihasilkan.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* Python 3.9 atau yang lebih baru terpasang.
* Objek pipeline AI yang mendukung post‑processing (misalnya, `TransformerPipeline` dari pustaka `transformers`).
* Akses ke paket `my_spellchecker` atau modul pemeriksaan ejaan yang kompatibel.

Anda tidak memerlukan pengetahuan mendalam tentang internal pipeline; langkah‑langkah di bawah ini menangani semua detail integrasi yang diperlukan.

## Cara menambahkan pemeriksa ejaan sebagai post processor

Ide dasarnya adalah membuat instance dari kelas pemeriksaan ejaan dan mendaftarkannya ke pipeline menggunakan metode `set_post_processor`. Metode ini menerima objek processor dan kamus konfigurasi opsional.

```python
# Step 1: Import the custom spell checker class
from my_spellchecker import SpellChecker

# Step 2: Create an instance of the spell checker
spell_checker = SpellChecker()

# Step 3: Attach the spell checker as a post‑processor to the AI pipeline,
#         providing any necessary options (e.g., language)
ai.set_post_processor(spell_checker, {"lang": "en"})
```

### Mengapa ini berhasil

* **`SpellChecker`** mengenkapsulasi logika untuk mendeteksi dan memperbaiki token yang salah eja.  
* **`set_post_processor`** memberi tahu pipeline untuk memanggil objek yang diberikan setelah model utama selesai melakukan inferensi.  
* Kamus konfigurasi memungkinkan Anda menyesuaikan perilaku (bahasa, kamus khusus, dll.) tanpa mengubah kode processor.

## Menambahkan post processing ke pipeline AI Anda

Jika pipeline Anda belum menyediakan metode `set_post_processor`, Anda dapat memperluasnya dengan subclassing atau menggunakan fungsi pembungkus. Di bawah ini adalah pembungkus generik yang bekerja dengan pipeline apa pun yang dapat dipanggil.

```python
def add_post_processor(pipeline, processor, options=None):
    """
    Registers a post‑processor on a generic pipeline.
    """
    def wrapped(*args, **kwargs):
        # Run the original pipeline
        result = pipeline(*args, **kwargs)
        # Apply the post‑processor if it implements `process`
        if hasattr(processor, "process"):
            return processor.process(result, **(options or {}))
        # Fallback: assume processor is a callable
        return processor(result, **(options or {}))

    return wrapped

# Example usage with a Hugging Face pipeline
from transformers import pipeline as hf_pipeline

# Create the base pipeline (e.g., text generation)
base = hf_pipeline("text-generation", model="gpt2")

# Wrap it with the spell‑checking post processor
ai = add_post_processor(base, spell_checker, {"lang": "en"})
```

### Apa yang dilakukan pembungkus

1. **Menjalankan inferensi asli** dan menangkap output mentah.  
2. **Mendeteksi titik masuk yang tepat** (`process` method atau callable) pada processor yang diberikan.  
3. **Memanggil processor** dengan hasil dan opsi apa pun yang Anda berikan.  

Pola ini memungkinkan Anda **menggunakan post processor** yang tidak dirancang khusus untuk pipeline, memberi Anda fleksibilitas penuh untuk menambahkan pemeriksaan ejaan atau logika khusus lainnya.

## Menggunakan post processor untuk pemeriksaan ejaan

Setelah processor terpasang, Anda dapat memanggil pipeline seperti biasa. Langkah pemeriksaan ejaan dijalankan secara otomatis setelah model menghasilkan teks.

```python
# Generate text that may contain spelling errors
raw_output = ai("Write a short paragraph about climate change.")

print("Raw output:", raw_output)
print("Corrected output:", ai.last_result)  # Assuming the wrapper stores the final result
```

**Output yang diharapkan (contoh):**

```
Raw output: ['Climte change is a global issue that affects all nations.']
Corrected output: ['Climate change is a global issue that affects all nations.']
```

Perhatikan bagaimana kata yang salah eja *“Climte”* menjadi *“Climate”* setelah pemeriksa ejaan dijalankan. Ini menunjukkan bahwa langkah **apply spell checking** bekerja secara transparan.

### Menangani kasus tepi

| Situasi                               | Pendekatan yang disarankan                                               |
|----------------------------------------|--------------------------------------------------------------------|
| Input mengandung istilah khusus domain   | Berikan kamus khusus melalui parameter `options`.          |
| Processor menghasilkan pengecualian          | Bungkus pemanggilan dalam blok `try/except` dan kembali ke hasil mentah. |
| Dibutuhkan beberapa post processor    | Rantai mereka dengan menumpuk pemanggilan `add_post_processor` atau dengan membuat processor komposit. |

## Cara mengatur opsi post processor secara dinamis

Anda mungkin perlu mengubah pengaturan bahasa atau kamus saat runtime. Metode `set_post_processor` dapat dipanggil lagi dengan konfigurasi baru, menimpa yang sebelumnya.

```python
# Switch to French spell checking
ai.set_post_processor(spell_checker, {"lang": "fr"})
```

Memanggil metode untuk kedua kalinya **how to set post processor** menggantikan konfigurasi lama, memastikan bahwa generasi selanjutnya menggunakan model bahasa yang baru.

## Tips pro: menguji integrasi pemeriksaan ejaan Anda

Tes otomatis menjamin bahwa pemeriksa ejaan tetap berfungsi setelah perubahan kode.

```python
import unittest

class TestSpellCheckerIntegration(unittest.TestCase):
    def test_correction(self):
        result = ai("The qick brown fox.")
        self.assertIn("quick", result[0].lower())

if __name__ == "__main__":
    unittest.main()
```

Menjalankan tes ini mengonfirmasi bahwa langkah **add spell checker** secara tepat memodifikasi output.

## Ringkasan

Panduan ini menunjukkan cara **menambahkan pemeriksa ejaan** ke pipeline AI, cara **menambahkan post processing**, dan cara **menggunakan post processor** untuk **apply spell checking**. Anda belajar cara **how to set post processor** opsi, menangani kasus tepi, dan memvalidasi integrasi dengan unit test.

Dari sini Anda dapat:

* Perluas pola ini ke tugas post‑processing lain seperti penyaringan kata kasar atau analisis sentimen.  
* Jelajahi fitur lanjutan pustaka `my_spellchecker`, seperti saran yang sadar konteks.  
* Gabungkan beberapa post processor untuk pipeline output yang lebih kaya.

Eksperimen dengan konfigurasi yang berbeda dan bagikan temuan Anda dengan komunitas. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Tingkatkan Akurasi OCR dengan Pemeriksaan Ejaan pada Gambar](/ocr/english/net/ocr-optimization/result-correction-with-spell-checking/)
- [OCR Post Processing – Dapatkan Pilihan Karakter](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Cara Menggunakan AspOCR: Praproses Filter OCR Gambar untuk .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}