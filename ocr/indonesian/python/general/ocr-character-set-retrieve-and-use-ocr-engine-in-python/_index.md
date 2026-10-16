---
category: general
date: 2026-06-06
description: 'Panduan set karakter OCR: pelajari cara menggunakan mesin OCR untuk
  menampilkan karakter yang didukung untuk skrip Latin dan Cyrillic dengan contoh
  Python lengkap.'
draft: false
keywords:
- ocr character set
- use OCR engine
- supported OCR characters
- script detection OCR
- OCR library Python
language: id
og_description: 'Panduan set karakter OCR: temukan cara menggunakan mesin OCR di Python
  untuk menampilkan karakter yang didukung untuk berbagai skrip, lengkap dengan kode
  dan tips.'
og_title: Set Karakter OCR – Dapatkan dan Gunakan Mesin OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: 'OCR character set guide: learn how to use OCR engine to list supported
    characters for Latin and Cyrillic scripts with full Python examples.'
  headline: OCR Character Set – Retrieve and Use OCR Engine in Python
  type: TechArticle
tags:
- OCR
- Python
- Character Sets
title: Set Karakter OCR – Mengambil dan Menggunakan Mesin OCR di Python
url: /id/python/general/ocr-character-set-retrieve-and-use-ocr-engine-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set Karakter OCR – Mengambil dan Menggunakan Mesin OCR di Python

Ingin mengetahui **ocr character set** yang didukung oleh perpustakaan Anda? Dalam tutorial ini kami akan menunjukkan cara **use OCR engine** untuk menanyakan karakter yang didukung untuk berbagai skrip, dan mengapa hal itu penting untuk proyek dunia nyata.

Jika Anda pernah menatap layar kosong bertanya-tanya mengapa beberapa huruf tidak pernah muncul setelah pemrosesan OCR, Anda tidak sendirian. Jawabannya sering tersembunyi dalam set karakter yang diketahui mesin. Pada akhir panduan ini Anda akan dapat:

* Daftar semua karakter yang dapat dikenali mesin OCR untuk skrip tertentu.  
* Menangani kasus di mana skrip tidak didukung.  
* Menyisipkan informasi set karakter ke dalam validasi hilir atau logika UI.

Tidak ada trik kotak hitam yang ajaib—hanya Python biasa, beberapa baris kode, dan sedikit penjelasan.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* Python 3.8+ terpasang (kode menggunakan f‑strings).  
* Perpustakaan OCR yang menyediakan `ocr.OcrEngine`—untuk contoh ini kami mengasumsikan paket bernama `ocr` sudah terpasang via `pip install ocr-lib`.  
* Familiaritas dasar dengan sistem impor Python dan pencetakan.

Jika Anda belum memiliki perpustakaan tersebut, jalankan:

```bash
pip install ocr-lib
```

Itu saja—tidak ada binari tambahan atau dependensi native yang diperlukan untuk kueri set karakter dasar yang akan kami lakukan.

## Langkah 1: Inisialisasi Instance Mesin OCR

Membuat objek mesin adalah hal pertama yang Anda lakukan ketika **use OCR engine** fungsionalitas. Anggaplah itu seperti menyalakan pemindai; tanpa itu, Anda tidak dapat mengajukan pertanyaan apa pun.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Kelas `OcrEngine` adalah pembungkus ringan di atas mesin pengenalan yang mendasarinya. Ia tidak memulai pemrosesan berat sampai Anda meminta sesuatu, sehingga biaya startupnya dapat diabaikan.

> **Tip pro:** Jika aplikasi Anda membuat banyak instance mesin, gunakan kembali satu instance saja. Ini menghemat memori dan mengurangi latensi inisialisasi.

## Langkah 2: Menanyakan Set Karakter OCR untuk Skrip Tertentu

Sekarang kita memiliki mesin, kita dapat menanyakannya karakter apa yang diketahui untuk sistem penulisan tertentu. Metode `get_supported_characters(script_name)` mengembalikan `list` Python berisi karakter Unicode.

```python
# Step 2: Get the list of characters the engine can recognize for the Latin script
latin_chars = engine.get_supported_characters("Latin")
print(f"Supported Latin chars ({len(latin_chars)}): {latin_chars}")
```

Menjalankan potongan kode di atas mencetak sesuatu seperti:

```
Supported Latin chars (26): ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
```

Output tepatnya tergantung pada versi perpustakaan OCR, tetapi Anda akan selalu mendapatkan daftar datar karakter. Jika Anda membutuhkan huruf besar dan kecil, cukup minta skrip `"Latin"` lalu terapkan `.lower()` pada setiap elemen, atau tanyakan skrip terpisah `"Latin‑lower"` jika perpustakaan membedakannya.

### Mengapa ini penting?

Ketika Anda memberi gambar yang berisi diakritik tidak biasa (mis., “ñ” atau “ø”), mesin OCR mungkin secara diam-diam menggantinya dengan placeholder atau menghapusnya sepenuhnya. Mengetahui **ocr character set** sebelumnya memungkinkan Anda memvalidasi input terlebih dahulu, memberi peringatan kepada pengguna, atau beralih ke mesin lain.

## Langkah 3: Mengambil Karakter untuk Skrip Lain – Contoh Cyrillic

Metode yang sama bekerja untuk skrip apa pun yang diklaim didukung oleh mesin. Mari lihat apa yang terjadi dengan Cyrillic.

```python
# Step 3: Get the list of characters the engine can recognize for the Cyrillic script
cyrillic_chars = engine.get_supported_characters("Cyrillic")
print(f"Supported Cyrillic chars ({len(cyrillic_chars)}): {cyrillic_chars}")
```

Output tipikal:

```
Supported Cyrillic chars (33): ['А', 'Б', 'В', 'Г', 'Д', 'Е', 'Ё', 'Ж', 'З', 'И', 'Й', 'К', 'Л', 'М', 'Н', 'О', 'П', 'Р', 'С', 'Т', 'У', 'Ф', 'Х', 'Ц', 'Ч', 'Ш', 'Щ', 'Ъ', 'Ы', 'Ь', 'Э', 'Ю', 'Я']
```

Jika mesin **tidak** mendukung skrip yang diminta, biasanya ia mengeluarkan `ValueError` (atau mengembalikan daftar kosong tergantung implementasinya). Mari lindungi dari hal itu.

```python
def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

# Example usage:
safe_get_characters(engine, "Arabic")   # Might trigger the error branch
```

## Langkah 4: Visualisasikan Set Karakter OCR (Opsional)

Terkadang visual cepat membantu, terutama ketika Anda perlu menunjukkan kepada pemangku kepentingan karakter mana yang tercakup. Di bawah ini contoh minimal menggunakan `matplotlib` untuk menampilkan grid karakter.

```python
import matplotlib.pyplot as plt

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14, ha='center', va='center')
    plt.title(title)
    plt.show()

# Visualize Latin characters
plot_character_grid(latin_chars, title="Latin OCR Character Set")
```

> **Teks alt gambar:** ![diagram set karakter OCR](ocr_character_set.png){alt="ikhtisar set karakter OCR"}

Diagram tidak diperlukan untuk solusi inti, tetapi ini menunjukkan bagaimana Anda dapat **use OCR engine** metadata di luar pencetakan biasa.

## Langkah 5: Mengintegrasikan Set Karakter ke dalam Alur Kerja Dunia Nyata

Sekarang kita dapat mengambil **ocr character set**, mari lihat skenario praktis: memvalidasi output OCR sebelum menyimpannya ke dalam basis data.

```python
def validate_ocr_output(text, allowed_chars):
    """Return True if every character in `text` exists in `allowed_chars`."""
    invalid = [c for c in text if c not in allowed_chars]
    if invalid:
        print(f"Invalid characters found: {invalid}")
        return False
    return True

# Suppose we ran OCR on an image and got this result:
ocr_result = "HELLO WORLD!"

# Use the previously fetched Latin set for validation:
if validate_ocr_output(ocr_result, set(latin_chars)):
    print("All characters are supported – safe to store.")
else:
    print("Result contains unsupported symbols – consider manual review.")
```

Pola ini mencegah data sampah masuk ke pipeline hilir, titik masalah umum saat menangani dokumen multibahasa.

## Kesalahan Umum dan Kasus Pinggir

| Kesalahan | Mengapa Terjadi | Cara Menghindari |
|-----------|-----------------|------------------|
| **Typo nama skrip** (mis., `"Cyrillic "` dengan spasi di akhir) | Mesin memperlakukan string secara literal dan tidak dapat menemukan skrip. | Hilangkan spasi: `script.strip()` sebelum memanggil `get_supported_characters`. |
| **Daftar karakter kosong** | Beberapa mesin menampilkan skrip tetapi belum memuat model bahasa. | Panggil `engine.load_language_model(script)` jika perpustakaan menyediakan metode tersebut, atau pastikan file model tersedia. |
| **Masalah normalisasi Unicode** | Karakter seperti “é” dapat muncul sebagai terkomposisi (`\u00E9`) atau terdekomposisi (`e\u0301`). | Normalisasi string dengan `unicodedata.normalize('NFC', text)` sebelum validasi. |
| **Kinerja pada skrip besar** (mis., Chinese) | Mengambil ribuan karakter dapat menjadi lambat. | Cache hasil setelah panggilan pertama; kebanyakan aplikasi hanya membutuhkan daftar sekali. |

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut satu skrip yang dapat Anda salin‑tempel dan jalankan:



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Tutorial Aspose OCR – Pengenalan Karakter Optik](/ocr/english/)
- [Pemrosesan Pasca OCR – Dapatkan Pilihan Karakter](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Cara Mengatur Nilai Ambang pada Pengenalan Gambar OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}