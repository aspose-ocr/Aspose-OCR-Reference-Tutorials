---
category: general
date: 2026-06-03
description: Lakukan OCR pada gambar dan ekstrak teks dari gambar menggunakan Aspose.OCR.
  Pelajari cara mendeteksi kata yang salah eja dan mendapatkan saran ejaan dalam satu
  demo C#.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: id
og_description: Lakukan OCR pada gambar untuk mengekstrak teks, kemudian deteksi kata
  yang salah eja dan dapatkan saran ejaan menggunakan Aspose.OCR dalam C#.
og_title: Lakukan OCR pada Gambar dan Deteksi Kata yang Salah Eja di C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: Lakukan OCR pada Gambar dan Deteksi Kata yang Salah Eja di C#
url: /id/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar dan Deteksi Kata Salah Eja dalam C#

Pernah bertanya-tanya bagaimana cara **perform OCR on image** tanpa membuat kepala Anda pusing? Anda tidak sendirian. Baik Anda sedang mendigitalkan surat lama, memindai kwitansi, atau membangun alur kerja dokumen cerdas, mengekstrak teks bersih dari gambar adalah rintangan pertama. Kabar baiknya? Dengan Aspose.OCR Anda dapat membuat solusi dalam hitungan menit, dan bonusnya Anda juga dapat **detect misspelled words** dan **get spelling suggestions** dalam satu proses.

Dalam tutorial ini kami akan menuntun Anda melalui aplikasi konsol C# lengkap yang **extracts text from image**, menjalankan pemeriksa ejaan bahasa Inggris, dan mencetak setiap kesalahan beserta saran perbaikannya. Pada akhir tutorial Anda akan tahu persis **how to extract text**, cara menghubungkan spell‑check API, dan seperti apa output konsol yang diharapkan.

## Apa yang Akan Anda Bangun

- Memuat bitmap (atau PNG) yang berisi kesalahan tipografi.  
- Menjalankan Aspose.OCR untuk **perform OCR on image** dan memperoleh data string mentah.  
- Menginisialisasi pemeriksa ejaan bahasa Inggris bawaan.  
- **Detect misspelled words** dan **get spelling suggestions** untuk masing‑masing.  
- Mencetak laporan rapi ke konsol.

Tanpa layanan eksternal, tanpa panggilan HTTP yang rumit—hanya satu paket NuGet dan beberapa baris kode.

## Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode juga berfungsi pada .NET Framework 4.7+).  
- Visual Studio 2022 (atau editor pilihan Anda).  
- Paket NuGet Aspose.OCR untuk .NET (`Aspose.OCR`).  
- Sebuah file gambar (`letter_with_typos.png`) yang ditempatkan di lokasi yang dapat direferensikan dari proyek.

Jika Anda belum pernah menggunakan Aspose sebelumnya, jangan khawatir—menginstal paketnya semudah menjalankan:

```bash
dotnet add package Aspose.OCR
```

Sekarang mari kita selami implementasinya.

## Langkah 1: Siapkan Proyek dan Instal Aspose.OCR

Buat proyek konsol baru dan tarik pustaka OCR:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

Setelah proses restore selesai, buka `Program.cs`. Kami akan mengganti konten default dengan kode demo lengkap nanti, tetapi pertama-tama mari bahas mengapa setiap namespace penting.

- `Aspose.OCR` – Mesin OCR inti dan penanganan gambar.  
- `Aspose.OCR.SpellCheck` – Utilitas pemeriksa ejaan yang disertakan dalam pustaka.  
- `System` – Kelas dasar .NET standar (misalnya, `Console`).

## Langkah 2: Muat Gambar dan Lakukan OCR pada Gambar

Pekerjaan nyata pertama adalah memberi gambar ke mesin OCR. Aspose.OCR membaca banyak format (PNG, JPEG, TIFF). Berikut cuplikan kode yang melakukan pekerjaan berat:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **Mengapa ini penting:** `OcrImage.FromFile` menyembunyikan detail tingkat piksel, sementara `OcrEngine.Recognize` menjalankan model neural terlatih yang menerjemahkan glif visual menjadi karakter Unicode. Properti `ocrResult.Text` kini berisi string mentah—tepat apa yang Anda butuhkan untuk **extract text from image**.

> **Pro tip:** Jika gambar Anda berisi beberapa bahasa, Anda dapat mengatur `ocrEngine.Language = OcrLanguage.Multilingual;` sebelum memanggil `Recognize`.

## Langkah 3: Inisialisasi Pemeriksa Ejaan Bahasa Inggris

Aspose.OCR dilengkapi dengan mesin pemeriksa ejaan bawaan yang memahami bahasa Inggris secara langsung. Inisialisasinya hanya satu baris:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **Mengapa langkah ini krusial:** Output OCR mungkin mencakup karakter yang salah dikenali (misalnya “l” vs “1”) atau typo nyata dari dokumen sumber. Pemeriksa ejaan akan memindai string, menemukan token mencurigakan, dan menyarankan alternatif.

## Langkah 4: Deteksi Kata Salah Eja dan Dapatkan Saran Ejaan

Sekarang kita masukkan teks OCR ke dalam pemeriksa:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` adalah koleksi di mana setiap entri berisi kata yang salah dan array kemungkinan perbaikan.

## Langkah 5: Tampilkan Hasil

Akhirnya, kita iterasi koleksi tersebut dan mencetak laporan yang mudah dibaca:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### Output Konsol yang Diharapkan

Dengan asumsi `letter_with_typos.png` berisi kalimat:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

Menjalankan demo akan menghasilkan sesuatu seperti:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

Perhatikan bagaimana setiap typo dipasangkan dengan beberapa perbaikan yang masuk akal—tepat apa yang Anda butuhkan saat membangun UI koreksi yang ramah pengguna.

## Contoh Kerja Lengkap

Berikut adalah program **lengkap, siap salin‑tempel**. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya ke file gambar Anda.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **Kasus Tepi yang Perlu Dipertimbangkan**  
> - **Gambar Kosong:** Jika mesin OCR mengembalikan string kosong, `spellChecker.Check` hanya akan mengembalikan koleksi kosong—tidak ada crash.  
> - **Teks Non‑Inggris:** Ganti `OcrLanguage.English` dengan `OcrLanguage.French` (atau bahasa lain yang didukung) untuk **detect misspelled words** dalam locale lain.  
> - **Dokumen Besar:** Untuk PDF multi‑halaman, Anda dapat melakukan loop pada tiap halaman, melakukan OCR, lalu menggabungkan hasil sebelum pemeriksaan ejaan.

## Gambaran Visual (Teks Alt Gambar)

![Diagram showing the flow to perform OCR on image, extract text from image, and then detect misspelled words with spelling suggestions](perform-ocr-on-image-flow.png)

*Diagram di atas menggambarkan alur end‑to‑end: gambar → mesin OCR → teks mentah → pemeriksa ejaan → saran.*

## Pertanyaan Umum & Pro Tips

| Pertanyaan | Jawaban |
|------------|---------|
| **Apakah saya memerlukan koneksi internet?** | Tidak. Aspose.OCR berjalan sepenuhnya secara lokal; cocok untuk lingkungan offline atau yang memerlukan keamanan tinggi. |
| **Seberapa akurat pemeriksa ejaan?** | Menggunakan kamus sekitar 150 ribu kata bahasa Inggris dan pencocokan fuzzy, sehingga sebagian besar typo umum terdeteksi. |
| **Bisakah saya menyesuaikan kamus?** | Ya. `SpellChecker.AddUserDictionary("custom.txt")` memungkinkan Anda memuat istilah khusus domain (misalnya nama produk). |
| **Bagaimana jika gambar miring?** | Mesin OCR secara otomatis mendeteksi orientasi, tetapi Anda dapat memanggil secara manual `ocrEngine.ImagePreprocessing.Rotate(angle)` untuk kasus yang sulit. |
| **Apakah ada cara menyorot saran di UI?** | Setelah Anda memiliki koleksi `misspellings`, Anda dapat memetakan setiap `entry.Word` kembali ke posisinya di `ocrResult.Text` dan menggarisbawahi di RichTextBox atau tampilan web. |

## Kesimpulan

Kami baru saja menunjukkan **how to perform OCR on image**, **extract text from image**, dan kemudian **detect misspelled words** sambil **getting spelling suggestions**—semua dengan aplikasi konsol C# yang ringkas. Ide dasarnya sederhana: biarkan Aspose.OCR menangani pengenalan karakter, lalu biarkan pemeriksa ejaan bawaan membersihkan outputnya. Dari sini Anda dapat mengembangkan demo menjadi layanan pemrosesan dokumen lengkap, mengintegrasikannya dengan API web, atau menambahkannya ke editor desktop.

Siap untuk langkah selanjutnya? Coba ganti bahasa ke Spanyol, beri PDF multi‑halaman, atau bangun front‑end WPF kecil yang memungkinkan pengguna mengklik kata untuk menerima saran. Blok‑blok bangunan sudah tersedia—terus bereksperimen.

Jika Anda mengalami kendala atau memiliki ide untuk ekstensi, tinggalkan komentar di bawah. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}