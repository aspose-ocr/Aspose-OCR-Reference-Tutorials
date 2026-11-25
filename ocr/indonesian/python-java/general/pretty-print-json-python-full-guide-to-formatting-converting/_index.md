---
category: general
date: 2026-06-16
description: Cetak cantik JSON Python dengan cepat dan pelajari cara mengonversi JSON
  ke dict atau memuat string JSON Python untuk manipulasi data. Tutorial langkah demi
  langkah.
draft: false
keywords:
- pretty print json python
- convert json to dict
- load json string python
language: id
og_description: Cetak cantik JSON di Python dan lihat langsung cara mengonversi JSON
  menjadi dict atau memuat string JSON di Python. Kuasai penanganan JSON dalam hitungan
  menit.
og_title: Cetak Cantik JSON Python – Panduan Lengkap Pemformatan & Konversi
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Pretty print JSON Python quickly and learn how to convert JSON to dict
    or load JSON string Python for data manipulation. Step‑by‑step tutorial.
  headline: Pretty Print JSON Python – Full Guide to Formatting & Converting
  type: TechArticle
tags:
- python
- json
- data‑processing
title: Cetak Cantik JSON Python – Panduan Lengkap untuk Memformat & Mengonversi
url: /id/python-java/general/pretty-print-json-python-full-guide-to-formatting-converting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pretty Print JSON Python – Panduan Lengkap untuk Memformat & Mengonversi

Pernah membutuhkan **pretty print JSON Python** dan bertanya-tanya mengapa outputnya selalu terlihat seperti satu baris yang tidak dapat dibaca? Anda tidak sendirian. Dalam banyak proyek, string JSON mentah adalah kekacauan yang berbelit, membuat proses debugging terasa seperti mencari jarum dalam tumpukan jerami.  

Berita baiknya? Dengan hanya beberapa fungsi bawaan Anda dapat mengubah blob kacau itu menjadi tampilan yang terindentasi rapi, dan kemudian **convert JSON to dict** untuk pemrosesan lanjutan yang mulus. Dalam tutorial ini kami akan membahas setiap langkah—dari memuat string JSON di Python hingga mengiterasi datanya—sehingga Anda dapat fokus pada logika alih-alih berjuang dengan format.

## Apa yang Dibahas dalam Tutorial Ini

- Cara **pretty print JSON Python** menggunakan `json.dumps` dengan argumen `indent`.  
- Cara tepat untuk **load JSON string Python** ke dalam dictionary native.  
- Mengonversi dictionary yang dihasilkan menjadi objek Python yang berguna, termasuk contoh praktis yang mencetak setiap kata dengan skor kepercayaan.  
- Jebakan umum (seperti menangani karakter non‑ASCII) dan perbaikan cepat.  
- Skrip lengkap yang dapat dijalankan, yang dapat Anda salin‑tempel dan sesuaikan secara instan.

Pada akhir panduan ini Anda akan dapat mengubah payload JSON apa pun menjadi format yang dapat dibaca manusia dan memanipulasinya dengan Python murni—tanpa memerlukan pustaka eksternal.

---

## Prasyarat

- Python 3.8 atau lebih baru (modul `json` merupakan bagian dari pustaka standar).  
- Pemahaman dasar tentang dictionary dan loop.  
- Opsional, mesin OCR atau layanan apa pun yang mengembalikan JSON—contoh kami menggunakan panggilan mock `engine.recognize()`, tetapi Anda dapat menggantinya dengan sumber data Anda sendiri.

---

## Langkah 1: Lakukan OCR (atau Pengakuan yang Menghasilkan JSON)

Hal pertama yang perlu dilakukan, Anda memerlukan hasil yang kompatibel dengan JSON. Dalam banyak alur kerja computer‑vision mesin OCR menghasilkan objek terstruktur yang dapat diserialisasi menjadi JSON. Berikut contoh placeholder minimal:

```python
# Step 1: Simulate an OCR engine that returns a result object
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    # The real engine would have a .to_json() method; we mimic it
    def to_json(self, indent=None):
        import json
        return json.dumps({"words": self.words}, indent=indent)

# Imagine `engine` is your pre‑configured OCR engine
engine = MockResult()
result = engine  # In real code: result = engine.recognize()
```

> **Mengapa langkah ini penting:**  
> Bahkan jika Anda tidak melakukan OCR, Anda sering menerima data dari API, file, atau antrian pesan. Objek tersebut harus dapat diserialisasi ke JSON sebelum kita dapat **pretty print**.

---

## Langkah 2: Pretty Print JSON Python

Sekarang kami mengubah data mentah menjadi string yang terindentasi rapi. Parameter `indent` melakukan pekerjaan berat.

```python
# Step 2: Serialize the result with pretty printing
json_str = result.to_json(indent=2)  # <-- pretty print JSON Python
print("🔍 Pretty‑printed JSON output:")
print(json_str)   # optional: view the raw JSON output
```

Output akan terlihat seperti ini:

```json
{
  "words": [
    {
      "text": "Hello",
      "confidence": 0.98
    },
    {
      "text": "World",
      "confidence": 0.95
    }
  ]
}
```

> **Tips pro:** Gunakan `indent=4` jika Anda lebih suka spasi yang lebih lebar, atau tambahkan `sort_keys=True` untuk mengurutkan kunci secara alfabet.

---

## Langkah 3: Load JSON String Python → Dictionary Native

String yang sudah pretty‑printed bagus untuk manusia, tetapi Python menyukai dictionary untuk pekerjaan sebenarnya. Di sinilah kita **load JSON string Python** ke dalam struktur native.

```python
# Step 3: Convert the JSON string to a Python dict
import json

result_dict = json.loads(json_str)   # <-- load json string python
print("\n✅ Loaded dict type:", type(result_dict))
```

Anda akan melihat:

```
✅ Loaded dict type: <class 'dict'>
```

> **Mengapa kami melakukan ini:**  
> Dictionary memberikan Anda pencarian O(1), data yang dapat diubah, dan integrasi mulus dengan seluruh ekosistem Python. Mencoba bekerja langsung dengan string JSON akan memaksa Anda melakukan parsing string yang merepotkan.

---

## Langkah 4: Iterasi Kata yang Diakui – Kasus Penggunaan Dunia Nyata

Mari kita ekstrak setiap kata dan skor kepercayaannya. Ini menunjukkan baik **convert json to dict** (dictionary yang sudah kita miliki) maupun iterasi praktis.

```python
# Step 4: Display each word with its confidence score
print("\n🗣️ Recognized words and confidence values:")
for word in result_dict["words"]:
    # f‑string gives us a clean, readable line
    print(f'{word["text"]} (conf: {word["confidence"]})')
```

Output yang diharapkan:

```
🗣️ Recognized words and confidence values:
Hello (conf: 0.98)
World (conf: 0.95)
```

> **Tips kasus tepi:** Jika JSON mungkin tidak memiliki kunci `"words"`, lindungi dari `KeyError`:

```python
for word in result_dict.get("words", []):
    # safe iteration even when "words" is absent
    print(f'{word.get("text", "<unknown>")} (conf: {word.get("confidence", 0)})')
```

---

## Langkah 5: Menangani Karakter Non‑ASCII (Dukungan Unicode)

Mesin OCR sering mengembalikan karakter seperti “é” atau “ü”. `json.dumps` default akan meng-escape mereka sebagai `\u00e9`. Untuk menjaga agar dapat dibaca, gunakan `ensure_ascii=False`.

```python
# Example with non‑ASCII text
result.words.append({"text": "café", "confidence": 0.92})
json_str_utf8 = result.to_json(indent=2)
json_str_utf8 = json.dumps(json.loads(json_str_utf8), indent=2, ensure_ascii=False)

print("\n🌍 Pretty‑printed JSON with Unicode:")
print(json_str_utf8)
```

Sekarang output menampilkan **café** alih-alih versi yang di‑escape. Ini penting ketika Anda **convert json to dict** nanti; dictionary akan berisi string Unicode yang tepat.

---

## Langkah 6: Menyimpan dan Memuat Ulang JSON yang Pretty‑Printed (Opsional)

Kadang Anda ingin menyimpan JSON yang diformat ke file untuk inspeksi nanti.

```python
# Step 6: Write pretty JSON to a file
with open("ocr_result_pretty.json", "w", encoding="utf-8") as f:
    f.write(json_str_utf8)

# Later you can read it back and still have a dict
with open("ocr_result_pretty.json", "r", encoding="utf-8") as f:
    loaded_dict = json.load(f)   # <-- load json string python from file
print("\n📂 Loaded back from file, type:", type(loaded_dict))
```

File akan berisi JSON yang terindentasi rapi, dan `json.load` secara otomatis mem-parsenya kembali menjadi dictionary.

---

## Langkah 7: Menggabungkan Semua – Solusi Satu‑File

Berikut adalah skrip mandiri yang menggabungkan setiap langkah yang dibahas. Silakan letakkan ke dalam file bernama `pretty_json_demo.py` dan jalankan.

```python
#!/usr/bin/env python3
"""
Complete example: pretty print JSON Python, convert JSON to dict,
and load JSON string Python for further processing.
"""

import json

# ----------------------------------------------------------------------
# Mock OCR engine – replace with your real engine when ready
# ----------------------------------------------------------------------
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    def to_json(self, indent=None, ensure_ascii=True):
        # Produce a JSON string; indent triggers pretty printing
        return json.dumps({"words": self.words}, indent=indent, ensure_ascii=ensure_ascii)

# ----------------------------------------------------------------------
# Main workflow
# ----------------------------------------------------------------------
def main():
    # Step 1: Get the result object (real code would call engine.recognize())
    result = MockResult()

    # Step 2: Pretty print JSON Python
    json_str = result.to_json(indent=2)          # pretty print JSON Python
    print("🔍 Pretty‑printed JSON:")
    print(json_str)

    # Step 3: Load JSON string Python → dict
    result_dict = json.loads(json_str)          # load json string python
    print("\n✅ Dictionary type:", type(result_dict))

    # Step 4: Iterate over words
    print("\n🗣️ Words with confidence:")
    for word in result_dict.get("words", []):
        print(f'{word.get("text", "<missing>")} (conf: {word.get("confidence", 0)})')

    # Step 5: Demonstrate Unicode handling
    result.words.append({"text": "café", "confidence": 0.92})
    json_utf8 = result.to_json(indent=2, ensure_ascii=False)
    print("\n🌍 Unicode‑friendly pretty JSON:")
    print(json_utf8)

    # Step 6: Save to file and reload
    with open("pretty_output.json", "w", encoding="utf-8") as f:
        f.write(json_utf8)

    with open("pretty_output.json", "r", encoding="utf-8") as f:
        reloaded = json.load(f)                 # load json string python from file
    print("\n📂 Reloaded dict, size:", len(reloaded.get("words", [])))

if __name__ == "__main__":
    main()
```

Jalankan:

```bash
python pretty_json_demo.py
```

Anda akan melihat JSON yang pretty‑printed, tipe dictionary, setiap kata dengan kepercayaannya, dan versi yang ramah Unicode yang disimpan ke `pretty_output.json`.  

**Itulah seluruh cerita**—dari output OCR mentah hingga dictionary Python yang bersih dan dapat dimanipulasi.

---

## Pertanyaan yang Sering Diajukan (FAQs)

| Question | Answer |
|----------|--------|
| **Apakah saya memerlukan pustaka eksternal?** | Tidak. Modul `json` bawaan menangani baik pretty printing maupun loading. |
| **Bagaimana jika JSON saya sangat besar?** | Gunakan `json.dump` dengan handle file untuk menghindari memuat semuanya ke memori; Anda masih dapat mengatur `indent` untuk file yang pretty. |
| **Bisakah saya mengurutkan kunci?** | Ya—tambahkan `sort_keys=True` ke `json.dumps` untuk urutan deterministik, yang membantu dalam pengujian berbasis diff. |
| **Bagaimana cara menangani JSON yang tidak valid?** | Bungkus `json.loads` dalam blok `try/except json.JSONDecodeError` dan catat string yang bermasalah. |
| **Apakah ada alternatif yang lebih cepat?** | Untuk payload yang sangat besar, pustaka seperti `orjson` atau `ujson` lebih cepat, tetapi mereka tidak mendukung `indent` out‑of‑ |

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menggunakan Aspose OCR untuk Hasil JSON dalam Pengenalan Gambar](/ocr/english/net/text-recognition/get-result-as-json/)
- [Cara menggunakan Aspose OCR untuk mendapatkan hasil JSON dalam pengenalan gambar](/ocr/spanish/net/text-recognition/get-result-as-json/)
- [Cara menggunakan Aspose OCR untuk Hasil JSON dalam Pengenalan Gambar](/ocr/german/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}