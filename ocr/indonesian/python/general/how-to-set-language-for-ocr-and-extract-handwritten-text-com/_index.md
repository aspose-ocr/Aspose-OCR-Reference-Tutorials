---
category: general
date: 2026-03-26
description: Cara mengatur bahasa pada mesin OCR dan mengekstrak teks tulisan tangan
  dari gambar – tutorial langkah demi langkah untuk mengubah gambar menjadi teks.
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: id
og_description: Cara mengatur bahasa pada mesin OCR dan mengekstrak catatan tulisan
  tangan dari gambar. Pelajari cara mengubah gambar menjadi teks dalam hitungan menit.
og_title: Cara Mengatur Bahasa untuk OCR – Ekstrak Teks Tangan dengan Mudah
tags:
- OCR
- Python
- Image Processing
title: Cara Mengatur Bahasa untuk OCR dan Mengekstrak Teks Tangan – Panduan Lengkap
url: /id/python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengatur Bahasa untuk OCR dan Mengekstrak Teks Tulisan Tangan – Panduan Lengkap

Pernah bertanya‑tanya **bagaimana cara mengatur bahasa** pada mesin OCR Anda sehingga benar‑benar memahami karakter yang Anda butuhkan? Mungkin Anda memiliki foto daftar belanja, catatan rapat, atau diagram yang tampak berantakan dan Anda tidak dapat mengekstrak teksnya. Kabar baiknya? Anda tidak memerlukan PhD dalam computer vision—hanya beberapa baris Python dan flag yang tepat.

Dalam tutorial ini kami akan menelusuri langkah‑langkah tepat untuk **mengekstrak teks tulisan tangan** dari PNG, mengonversi gambar tersebut ke teks biasa, dan menjelaskan “mengapa” di balik setiap pengaturan. Pada akhir tutorial Anda akan dapat mengenali catatan tulisan tangan dalam proyek apa pun, baik itu aplikasi pencatatan atau pipeline pemrosesan batch.

> **Apa yang Anda perlukan**  
> • Python 3.8+ (kode juga berfungsi dengan 3.10)  
> • Library `ocr` (atau pembungkus kompatibel lain yang mengekspos `OcrEngine`)  
> • Contoh gambar seperti `note_handwritten.png` – gambar apa pun dengan karakter Latin yang diperluas akan cocok.

Mari kita mulai.

---

## Cara Mengatur Bahasa dan Mengaktifkan Pengenalan Tulisan Tangan

Hal pertama yang harus Anda lakukan adalah memberi tahu mesin OCR alfabet apa yang harus diharapkan. Jika Anda melewatkan langkah ini, mesin secara default menggunakan set generik yang sering salah mengenali huruf beraksen atau simbol khusus.

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**Mengapa ini penting:**  
- **ExtendedLatin** mencakup karakter seperti “ñ”, “ø”, dan “ç”, yang umum dalam banyak catatan Eropa.  
- Flag `recognize_handwritten` mengalihkan model dasar dari OCR teks cetak ke jaringan saraf yang dilatih pada goresan kursif. Tanpa flag ini, mesin menganggap coretan Anda sebagai noise.

> **Pro tip:** Jika Anda memproses dokumen dalam banyak bahasa, buatlah mesin terpisah per bahasa atau alihkan secara dinamis `ocr_engine.language` sebelum setiap pemanggilan. Ini menghindari beban memuat set karakter yang tidak digunakan.

![Screenshot konfigurasi mesin OCR yang menunjukkan cara mengatur bahasa](/images/ocr-set-language.png "Cara mengatur bahasa pada mesin OCR")

*Teks alt gambar: “Cara mengatur bahasa pada layar konfigurasi mesin OCR.”*

## Mengekstrak Teks Tulisan Tangan dari Gambar PNG

Sekarang mesin sudah tahu apa yang harus dicari, saatnya memberi gambar kepadanya. Metode `recognize_image` mengembalikan objek hasil yang kaya; atribut `text` berisi string biasa yang Anda butuhkan.

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

Saat Anda menjalankan skrip, Anda akan melihat sesuatu seperti:

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

Output tersebut membuktikan bahwa Anda berhasil **mengonversi gambar ke teks** dan mesin menghormati pengaturan bahasa yang Anda berikan.

**Pitfall umum**  
- **Path tidak tepat** – Periksa kembali lokasi file; file yang hilang akan memicu `FileNotFoundError`.  
- **Gambar beresolusi rendah** – OCR tulisan tangan kesulitan di bawah 300 dpi. Perbesar atau pindai ulang jika output terlihat berantakan.  
- **Inversi warna** – Jika latar belakang gelap dan tinta terang, balikkan warnanya terlebih dahulu (`Pillow` dapat membantu).

## Mengonversi Gambar ke Teks Menggunakan Fungsi Pembantu

Jika Anda berencana menjalankan OCR pada puluhan file, bungkus logika dalam fungsi yang dapat dipakai ulang. Ini juga membuat kode lebih mudah diuji dan diintegrasikan dengan pipeline lain.

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

Pembantu ini mengisolasi logika **cara mengekstrak tulisan tangan**, sehingga Anda dapat memanggilnya dari endpoint Flask, alat CLI, atau pekerjaan batch tanpa menulis ulang konfigurasi setiap kali.

## Mengenali Catatan Tulisan Tangan dalam Skenario Dunia Nyata

Berikut beberapa situasi di mana Anda kemungkinan besar perlu **mengenali catatan tulisan tangan** dan bagaimana pengaturan ini beradaptasi:

| Skenario | Mengapa bahasa penting | Penyesuaian yang disarankan |
|----------|------------------------|-----------------------------|
| **Daftar belanja multibahasa** | Item dapat mengandung aksen (misalnya “crème”) | Ganti `ocr_engine.language` per daftar atau gunakan `ocr.Language.AutoDetect` jika didukung |
| **Foto papan tulis kelas** | Kapur dapat menghasilkan goresan tipis | Tingkatkan kontras gambar sebelum memberi ke mesin |
| **Resep medis** | Tulisan tangan terkenal berantakan | Pasangkan OCR dengan kamus koreksi ejaan untuk nama obat |

Dalam setiap kasus, langkah inti—**cara mengatur bahasa**, mengaktifkan mode tulisan tangan, dan memanggil `recognize_image`—tetap identik. Konsistensi inilah yang membuat pendekatan ini kuat dan mudah dipelihara.

## Kasus Tepi & Penyesuaian Lanjutan

1. **Batch processing** – Muat mesin sekali, iterasi file, dan hanya ubah atribut `language` bila diperlukan. Ini mengurangi beban inisialisasi.  
2. **Non‑Latin scripts** – Jika Anda perlu memproses Cyrillic atau Arab, ganti `ExtendedLatin` dengan enum yang sesuai (mis., `ocr.Language.Cyrillic`). Pola yang sama berlaku.  
3. **Partial recognition** – Kadang mesin mengembalikan string kosong untuk goresan sangat pendek. Pemeriksaan cepat (`if not result.text.strip(): …`) memungkinkan Anda beralih ke model sekunder atau meminta pengguna memindai ulang.  
4. **Performance profiling** – Untuk dataset besar, ukur waktu pemanggilan `recognize_image`. Jika menjadi bottleneck, pertimbangkan paralelisasi menggunakan `concurrent.futures.ThreadPoolExecutor`.

## Contoh Lengkap yang Berfungsi

Berikut skrip lengkap yang dapat Anda salin‑tempel ke file bernama `handwritten_ocr.py`. Skrip ini menyertakan parsing argumen sehingga Anda dapat menunjuk ke gambar apa pun dari baris perintah.

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

Jalankan seperti:

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

Anda akan melihat output yang sama seperti potongan kode sebelumnya, mengonfirmasi bahwa Anda berhasil **mengonversi gambar ke teks** dan **mengenali catatan tulisan tangan**.

## Kesimpulan

Kami telah membahas **cara mengatur bahasa** pada mesin OCR, mengaktifkan flag teks tulisan tangan, dan membangun fungsi yang dapat dipakai ulang untuk **mengekstrak teks tulisan tangan** dari gambar apa pun. Dengan mengikuti langkah‑langkah di atas, Anda dapat secara andal **mengonversi gambar ke teks**, baik Anda menangani satu catatan atau arsip besar dokumen yang dipindai.

Selanjutnya, coba bereksperimen dengan paket bahasa yang berbeda, proses batch folder gambar, atau integrasikan logika ini ke layanan web yang mengembalikan hasil JSON. Dasar‑dasarnya tetap sama, dan fleksibilitas library `ocr` memungkinkan Anda menyesuaikan hampir semua kasus penggunaan.

Ada pertanyaan tentang kasus tepi, performa, atau memperluas skrip ke bahasa lain? Tinggalkan komentar atau hubungi saya di GitHub – selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}