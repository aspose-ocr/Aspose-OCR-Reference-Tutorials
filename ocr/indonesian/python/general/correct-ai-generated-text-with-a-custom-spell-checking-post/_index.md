---
category: general
date: 2026-08-15
description: Perbaiki teks yang dihasilkan AI secara instan dengan menerapkan pemeriksaan
  ejaan dalam Python. Pelajari post‑processor yang dapat digunakan kembali untuk membersihkan
  output LLM.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- correct AI generated text
- apply spell checking text
language: id
lastmod: 2026-08-15
og_description: Perbaiki teks yang dihasilkan AI dengan menambahkan post‑processor
  pemeriksa ejaan. Panduan ini menunjukkan cara mengintegrasikan koreksi AI dan menjaga
  output Anda tetap bersih.
og_image_alt: Diagram of an AI post‑processor pipeline that corrects generated text
og_title: Perbaiki teks yang dihasilkan AI – tambahkan pemeriksaan ejaan di Python
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Correct AI generated text instantly by applying spell checking text
    in Python. Learn a reusable post‑processor that cleans up LLM output.
  headline: Correct AI generated text with a custom spell‑checking post‑processor
  type: TechArticle
- description: Correct AI generated text instantly by applying spell checking text
    in Python. Learn a reusable post‑processor that cleans up LLM output.
  name: Correct AI generated text with a custom spell‑checking post‑processor
  steps:
  - name: Why this step matters
    text: '* **Encapsulation** – By isolating the correction logic, you can reuse
      it across multiple AI calls without duplicating code. * **Extensibility** –
      The `settings` parameter lets you later **apply spell checking text** with custom
      rules (e.g., a medical terminology list). * **Transparency** – Returnin'
  - name: What happens under the hood?
    text: 'When you call `ai.generate(prompt)`, the SDK now follows this flow:'
  - name: Tips for advanced use
    text: '* **Performance** – The built‑in correction is lightweight, but if you
      process thousands of responses per minute, consider batching or disabling it
      for short prompts. * **Logging** – Add a `print` or logger inside `spell_check_post_processor`
      to monitor how many corrections are applied per request. '
  type: HowTo
tags:
- AI post‑processor
- spell checking
- Python
title: Koreksi teks yang dihasilkan AI dengan post‑processor pemeriksaan ejaan khusus
url: /id/python/general/correct-ai-generated-text-with-a-custom-spell-checking-post/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Koreksi teks AI yang dihasilkan dengan post‑processor pemeriksaan ejaan khusus

Jika Anda perlu **mengoreksi teks AI yang dihasilkan**, panduan ini menunjukkan cara singkat untuk melakukannya di Python. Dengan **menerapkan pemeriksaan ejaan** sebagai post‑processor, Anda dapat secara otomatis membersihkan kesalahan ketik atau slip tata bahasa yang mungkin dihasilkan model bahasa.

Anda akan belajar cara:

* Mendefinisikan fungsi post‑processing yang dapat digunakan kembali yang menerima output model.
* Mendaftarkan fungsi tersebut dengan klien AI Anda sehingga setiap respons otomatis dikoreksi.
* Memperluas pendekatan untuk kamus khusus, pengaturan bahasa, atau penanganan bersyarat.

Tidak ada layanan eksternal yang diperlukan selain kemampuan koreksi bawaan dari AI SDK yang sudah Anda gunakan.

## Prasyarat

* Python 3.8+ terpasang di mesin Anda.  
* Sebuah pustaka klien AI yang menyediakan metode `run_postprocessor` dan `set_post_processor` (contoh menggunakan objek `ai` generik).  
* Familiaritas dasar dengan fungsi dan argumen kata kunci di Python.

Jika Anda sudah memiliki instance AI (`ai = SomeAIClient(...)`), Anda dapat langsung melompat ke implementasi.

## Langkah 1: Definisikan post‑processor pemeriksaan ejaan

Inti dari **mengoreksi teks AI yang dihasilkan** adalah fungsi kecil yang menerima string mentah dari model dan mengembalikan versi yang telah dikoreksi. AI SDK sudah menyediakan rutinitas koreksi tingkat rendah (`ai.run_postprocessor`). Membungkusnya memungkinkan Anda menambahkan logika ekstra nanti (misalnya, kamus khusus atau pencatatan).

```python
def spell_check_post_processor(generated_text, settings=None):
    """
    Post‑processor that corrects AI generated text using the SDK's built‑in
    spell‑checking capability.

    Args:
        generated_text (str): The raw output from the language model.
        settings (dict, optional): Additional options for the correction engine.
                                   Pass None to use defaults.

    Returns:
        str: The corrected text with spelling and basic grammar fixes applied.
    """
    # The SDK method automatically handles language detection and
    # common typo patterns. You can pass a settings dict to tweak behavior.
    corrected_text = ai.run_postprocessor(generated_text, **(settings or {}))
    return corrected_text
```

### Mengapa langkah ini penting

* **Enkapsulasi** – Dengan memisahkan logika koreksi, Anda dapat menggunakannya kembali di berbagai panggilan AI tanpa menduplikasi kode.  
* **Ekstensibilitas** – Parameter `settings` memungkinkan Anda nanti **menerapkan pemeriksaan ejaan** dengan aturan khusus (misalnya, daftar terminologi medis).  
* **Transparansi** – Mengembalikan string biasa menjaga pipeline hilir tetap sederhana dan menghindari struktur data yang tidak terduga.

## Langkah 2: Daftarkan post‑processor dengan instance AI Anda

Setelah fungsi siap, Anda perlu memberi tahu klien AI untuk memanggilnya setelah setiap generasi. Sebagian besar SDK menyediakan metode seperti `set_post_processor` untuk tujuan ini.

```python
# Register the custom post‑processor so every call to ai.generate()
# automatically runs spell_check_post_processor on the result.
ai.set_post_processor(spell_check_post_processor, custom_settings={})
```

### Apa yang terjadi di balik layar?

Saat Anda memanggil `ai.generate(prompt)`, SDK kini mengikuti alur berikut:

1. Menghasilkan teks mentah dari LLM.  
2. Mengirim teks mentah ke `spell_check_post_processor`.  
3. Mengembalikan teks yang telah dikoreksi ke aplikasi Anda.

Karena pendaftaran bersifat global, Anda **menerapkan pemeriksaan ejaan** secara konsisten tanpa harus mengingat memanggil fungsi terpisah setiap kali.

## Langkah 3: Gunakan klien AI seperti biasa

Dengan post‑processor terpasang, kode generasi normal Anda tetap tidak berubah.

```python
prompt = "Write a short summary about the benefits of renewable energy."
raw_output = ai.generate(prompt)   # The SDK will automatically correct it.
print("Corrected output:")
print(raw_output)
```

**Output yang diharapkan**

```
Corrected output:
Renewable energy sources, such as solar and wind, reduce greenhouse gas emissions,
lower reliance on fossil fuels, and create sustainable jobs. They also help
stabilize energy prices and improve air quality.
```

Perhatikan bahwa kata yang salah eja (misalnya “energey”) yang mungkin muncul dalam respons LLM mentah sudah diperbaiki sebelum string mencapai pernyataan `print` Anda.

## Langkah 4: Menyesuaikan perilaku pemeriksaan ejaan (opsional)

Jika Anda memerlukan kontrol lebih besar atas proses koreksi, kirimkan kamus opsi melalui argumen `custom_settings` saat mendaftarkan processor.

```python
custom_rules = {
    "ignore_words": ["OpenAI", "GPT‑4"],   # Preserve brand names
    "language": "en-US",                  # Force US English spelling
    "max_corrections": 5                  # Limit the number of changes per response
}

ai.set_post_processor(spell_check_post_processor, custom_settings=custom_rules)
```

### Tips untuk penggunaan lanjutan

* **Kinerja** – Koreksi bawaan ringan, tetapi jika Anda memproses ribuan respons per menit, pertimbangkan batching atau menonaktifkannya untuk prompt pendek.  
* **Pencatatan** – Tambahkan `print` atau logger di dalam `spell_check_post_processor` untuk memantau berapa banyak koreksi yang diterapkan per permintaan.  
* **Fallback** – Jika SDK melempar pengecualian (misalnya gangguan jaringan), tangkap dan kembalikan `generated_text` asli untuk menghindari kerusakan aplikasi Anda.

```python
def spell_check_post_processor(generated_text, settings=None):
    try:
        return ai.run_postprocessor(generated_text, **(settings or {}))
    except Exception as e:
        # Log the error and fall back to the unmodified text
        logger.warning(f"Spell check failed: {e}")
        return generated_text
```

## Langkah 5: Menguji integrasi

Sebuah unit test singkat memastikan bahwa post‑processor Anda terhubung dengan benar dan output memang telah dikoreksi.

```python
import unittest

class TestSpellCheckProcessor(unittest.TestCase):
    def test_correction(self):
        # Simulate a buggy LLM response
        buggy = "Renewable energey reduces carbon emissions."
        corrected = spell_check_post_processor(buggy)
        self.assertIn("energy", corrected)   # Expect "energy" instead of "energey"

if __name__ == "__main__":
    unittest.main()
```

Menjalankan tes harus lulus, mengonfirmasi bahwa **mengoreksi teks AI yang dihasilkan** berfungsi sebagaimana mestinya.

## Pertanyaan umum dan kasus tepi

| Pertanyaan | Jawaban |
|------------|---------|
| *Bagaimana jika AI sudah mengembalikan teks yang sempurna?* | Mesin koreksi bersifat idempotent; ia akan membiarkan string bersih tetap tidak berubah. |
| *Apakah saya dapat menonaktifkan post‑processor untuk satu panggilan saja?* | Ya—sebagian besar SDK menerima flag `post_processor=False` pada metode `generate`. |
| *Apakah ini bekerja dengan bahasa non‑Inggris?* | `run_postprocessor` bawaan mendukung banyak locale; atur `language` di `custom_settings` sesuai kebutuhan. |
| *Bagaimana ini memengaruhi penggunaan token?* | Koreksi dijalankan secara lokal setelah generasi, sehingga tidak mengonsumsi token LLM tambahan. |

## Kesimpulan

Anda kini memiliki pola lengkap yang dapat digunakan kembali untuk **mengoreksi teks AI yang dihasilkan** dengan **menerapkan pemeriksaan ejaan** sebagai post‑processor di Python. Pendekatannya:

1. Bungkus metode koreksi SDK dalam fungsi bersih.  
2. Daftarkan wrapper secara global dengan `ai.set_post_processor`.  
3. Terus gunakan `ai.generate` seperti sebelumnya, yakin bahwa setiap respons sudah dipoles.

Dari sini Anda dapat mengeksplorasi:

* Mengintegrasikan kamus domain‑spesifik untuk dokumentasi teknis.  
* Menambahkan API pemeriksaan tata bahasa (mis., LanguageTool) untuk kualitas bahasa yang lebih mendalam.  
* Membangun komponen UI yang menyoroti perbaikan sebelum/setelah untuk tinjauan pengguna.

Silakan bereksperimen dengan pengaturan opsional, dan bagikan peningkatan Anda kepada komunitas!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Konversi Gambar ke Teks: Ekstrak Teks dari Gambar Menggunakan Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}