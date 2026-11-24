---
category: general
date: 2026-09-10
description: Cara menggunakan OCR di C# untuk mengekstrak teks Cyrillic, memproses
  gambar, dan mengonversinya menjadi file PDF atau HTML dalam satu contoh yang dapat
  dijalankan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: id
lastmod: 2026-09-10
og_description: Cara menggunakan OCR di C# untuk mengekstrak teks Cyrillic, memproses
  gambar, dan mengekspor hasilnya sebagai PDF atau HTML. Ikuti panduan langkah demi
  langkah ini.
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: Cara menggunakan OCR di C# – mengekstrak teks Cyrillic dan mengonversi gambar
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: Cara menggunakan OCR di C# untuk mengekstrak teks Cyrillic
url: /id/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan OCR di C# untuk mengekstrak teks Cyrillic

Jika Anda perlu **cara menggunakan OCR** di C# untuk mengekstrak teks Cyrillic dari dokumen yang dipindai, panduan ini menunjukkan solusi lengkap yang siap dijalankan. Anda juga akan belajar cara **memproses gambar untuk OCR**, dan cara **mengonversi gambar ke PDF** atau **mengonversi gambar ke HTML** setelah teks dikenali.

Proyek digitalisasi dokumen sering menemui dua masalah: pemindaian berkualitas rendah dan kebutuhan menyimpan hasil dalam berbagai format. Tutorial ini menyelesaikan keduanya dengan menggunakan pustaka Aspose.OCR, yang secara otomatis mengunduh paket bahasa yang hilang, menawarkan bantuan pemrosesan gambar bawaan, dan dapat mengekspor hasil OCR ke PDF atau HTML dengan satu panggilan.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* .NET 6.0 SDK atau yang lebih baru (kode juga berfungsi dengan .NET Framework 4.7+).
* Visual Studio 2022 atau editor apa pun yang mendukung proyek C#.
* Paket NuGet **Aspose.OCR**. Instal dengan:

```bash
dotnet add package Aspose.OCR
```

* Sebuah file gambar yang berisi karakter Cyrillic (misalnya `sample_cyrillic.jpg`).  
  Letakkan file tersebut di folder yang dapat Anda referensikan sebagai `YOUR_DIRECTORY`.

Pustaka akan mengunduh paket bahasa Cyrillic pada pertama kali Anda menetapkan `ocrEngine.Language = Language.Cyrillic;`, jadi tidak diperlukan unduhan manual.

## Langkah 1 – Inisialisasi mesin OCR (cara menggunakan OCR)

Membuat instance `OcrEngine` menyiapkan mesin untuk semua operasi selanjutnya.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**Mengapa ini penting:** Mesin menyimpan konfigurasi seperti bahasa, pengaturan pemrosesan gambar, dan opsi output. Menginisialisasinya sekali membuat sisa kode tetap bersih dan aman untuk thread.

## Langkah 2 – Pilih bahasa Cyrillic (ekstrak teks Cyrillic)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**Mengapa ini penting:** Akurasi OCR sangat bergantung pada model bahasa yang tepat. Dengan secara eksplisit memilih `Language.Cyrillic`, mesin menerapkan tabel frekuensi karakter yang cocok untuk bahasa Rusia, Ukraina, Bulgaria, dll.

## Langkah 3 – Praproses gambar untuk OCR

Pemindaian berkualitas rendah mengandung kemiringan, bintik, atau pencahayaan tidak merata. `ImageProcessor` bawaan dapat meningkatkan tingkat pengenalan hanya dengan dua pemanggilan.

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**Mengapa ini penting:** Praproses mengurangi karakter palsu dan meningkatkan skor kepercayaan. Teks yang miring sering menghasilkan output yang kacau; deskewing meluruskannya. Despeckling menghilangkan artefak kecil yang mungkin diinterpretasikan mesin OCR sebagai huruf.

> **Tip pro:** Jika gambar sumber Anda sudah bersih, Anda dapat melewatkan pemanggilan ini. Untuk pemindaian yang sangat rusak, pertimbangkan langkah tambahan seperti `Binarize()` atau `ContrastStretch()`.

## Langkah 4 – Lakukan OCR pada gambar masukan

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**Mengapa ini penting:** `Process` menjalankan pipeline pengenalan pada bitmap yang diberikan. Ia mengembalikan `void`; teks yang dikenali menjadi tersedia melalui properti `Text`.

## Langkah 5 – Ambil teks yang dikenali dan simpan ke file

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**Mengapa ini penting:** Menyimpan teks mentah memungkinkan pemrosesan lanjutan seperti pencarian, pengindeksan, atau memasukkannya ke layanan terjemahan.

## Langkah 6 – Ekspor hasil OCR ke format lain (konversi gambar ke PDF & konversi gambar ke HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**Mengapa ini penting:** Mengonversi hasil OCR ke PDF atau HTML memungkinkan Anda mempertahankan konteks visual gambar asli sekaligus menyediakan teks yang dapat dicari. Ini sangat berharga untuk alur kerja hukum atau arsip.

### Output yang Diharapkan

Menjalankan program dengan pemindaian Cyrillic yang jelas menghasilkan tiga file:

* `result.txt` – teks Unicode biasa, misalnya `Пример текста на кириллице`.
* `result.pdf` – PDF yang berisi gambar dengan lapisan teks tak terlihat untuk pencarian.
* `result.html` – halaman HTML yang menampilkan gambar dan teks yang dapat dipilih.

Buka salah satu file untuk memverifikasi bahwa karakter Cyrillic telah berhasil diekstrak.

## Pertanyaan umum dan kasus tepi

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika paket bahasa gagal diunduh?** | Pastikan mesin memiliki akses internet. Anda juga dapat mengunduh paket terlebih dahulu dari situs Aspose dan menaruhnya di folder `bin`. |
| **Apakah saya dapat mengenali alfabet lain dalam satu proses?** | Ya. Panggil `ocrEngine.Language = Language.English;` (atau enum yang didukung) sebelum `Process`. Anda mungkin perlu menjalankan `Process` secara terpisah untuk setiap bahasa jika gambar mencampur skrip. |
| **Gambar saya adalah TIFF multi‑halaman – apakah ini bekerja?** | `OcrEngine` memproses satu bitmap pada satu waktu. Muat setiap halaman ke dalam `Bitmap` dan panggil `Process` dalam loop, menggabungkan hasilnya. |
| **Bagaimana cara meningkatkan kinerja untuk batch besar?** | Gunakan kembali satu instance `OcrEngine` dan setel `ocrEngine.OptimizeMemory = true;`. Juga, pertimbangkan pemrosesan paralel dengan instance mesin terpisah per thread. |

## Kesimpulan

Anda sekarang tahu **cara menggunakan OCR** di C# untuk **mengekstrak teks Cyrillic**, **memproses gambar untuk OCR**, dan **mengonversi gambar ke PDF** atau **mengonversi gambar ke HTML** dalam beberapa langkah singkat. Contoh lengkap menunjukkan produksi‑

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menggunakan AspOCR: Filter OCR Praproses Gambar untuk .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Cara Mengekstrak Teks OCR di C# – Panduan Langkah‑per‑Langkah Lengkap](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [Cara Menggunakan Aspose OCR untuk Hasil JSON dalam Pengenalan Gambar](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}