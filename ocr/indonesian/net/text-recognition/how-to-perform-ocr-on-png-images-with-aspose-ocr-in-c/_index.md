---
category: general
date: 2026-11-26
description: Pelajari cara melakukan OCR pada file PNG, mengonversi PNG ke teks, dan
  mengekstrak teks Cyrillic menggunakan Aspose.OCR – panduan langkah demi langkah
  untuk pengembang.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: id
lastmod: 2026-11-26
og_description: Cara melakukan OCR pada file PNG dan mengekstrak teks Cyrillic menggunakan
  Aspose.OCR di C#. Ikuti tutorial lengkap ini untuk mengubah PNG menjadi teks.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Cara melakukan OCR pada gambar PNG dengan Aspose.OCR – Panduan C#
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Cara melakukan OCR pada gambar PNG dengan Aspose.OCR di C#
url: /id/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR pada gambar PNG dengan Aspose.OCR di C#

Jika Anda perlu **how to perform OCR** pada file PNG, panduan ini menunjukkan langkah‑langkah tepat untuk mengonversi PNG ke teks menggunakan Aspose.OCR. Baik Anda mengekstrak teks Cyrillic dari dokumen yang dipindai atau sekadar mengenali teks dari screenshot PNG, solusi ini langsung dapat digunakan dan hanya memerlukan beberapa baris kode C#.

Dalam tutorial ini Anda akan belajar cara:

* **load image for OCR** dari folder lokal,
* mengonfigurasi engine untuk **extract Cyrillic text**,
* **recognize text from PNG** dan memperoleh string bersih,
* menangani masalah umum seperti modul bahasa yang hilang dan gambar berukuran besar.

Tidak diperlukan pengalaman sebelumnya dengan Aspose.OCR—hanya lingkungan pengembangan .NET dan gambar PNG yang ingin Anda proses.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* .NET 6.0 (atau lebih baru) terpasang.
* Salinan berlisensi atau percobaan **Aspose.OCR for .NET**. Anda dapat memperoleh percobaan gratis dari situs web Aspose.
* Visual Studio 2022 (atau IDE apa pun yang mendukung .NET).
* File PNG yang berisi teks yang ingin Anda ekstrak (contoh menggunakan `sample_image.png`).

## Langkah 1: Instal paket NuGet Aspose.OCR

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Paket ini mencakup mesin OCR inti dan semua modul bahasa. Ketika Anda meminta bahasa yang tidak ada secara lokal, Aspose.OCR secara otomatis mengunduh modul yang diperlukan.

## Langkah 2: Buat instance mesin OCR (how to perform OCR)

Langkah tindakan pertama dalam alur kerja OCR apa pun adalah menginstansiasi engine. Objek ini mengelola semua operasi selanjutnya seperti memuat gambar dan melakukan pengenalan.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Mengapa ini penting:** Kelas `OcrEngine` mengenkapsulasi pipeline OCR. Membuat satu instance dan menggunakannya kembali pada beberapa gambar mengurangi beban memori dan meningkatkan kinerja.

## Langkah 3: Muat gambar untuk OCR – tentukan file PNG sumber

Memuat gambar adalah titik di mana Anda **load image for OCR**. Aspose.OCR menerima beberapa jenis input; yang paling sederhana adalah `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Pro tip:** Gunakan path absolut atau `Path.Combine` untuk menghindari kesalahan runtime pada lingkungan yang berbeda.

### Menangani gambar besar

Jika PNG lebih besar dari 2 MB, pertimbangkan untuk menurunkan skala sebelum pengenalan untuk mempercepat pemrosesan:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Langkah 4: Konfigurasikan bahasa – extract Cyrillic text

Secara default, Aspose.OCR mengasumsikan bahasa Inggris. Untuk **extract Cyrillic text**, atur properti `Language` menjadi `Language.Cyrillic`. Modul yang diperlukan akan diunduh secara otomatis pada pertama kali Anda menjalankan kode.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Jika Anda perlu mengenali beberapa bahasa (mis., Inggris dan Cyrillic), Anda dapat menggabungkannya:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Kasus tepi: Modul bahasa yang hilang

Jika unduhan gagal (mis., lingkungan offline), engine akan melempar `OcrException`. Tangkap untuk memberikan fallback yang elegan:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Langkah 5: Lakukan operasi pengenalan (recognize text from PNG)

Sekarang gambar dan bahasa sudah diatur, Anda dapat **recognize text from PNG**. Metode `Recognize` menjalankan pipeline OCR secara sinkron.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Mengapa ini berhasil:** Secara internal, Aspose.OCR menerapkan pra‑pemrosesan (binarisasi, penghilangan noise) sebelum memasukkan gambar ke dalam recognizer berbasis jaringan saraf yang disetel untuk bahasa yang dipilih.

## Langkah 6: Ambil dan tampilkan teks yang dikenali (convert PNG to text)

Setelah pengenalan, string yang diekstrak tersedia melalui properti `Text`. Ini adalah langkah akhir dalam **convert PNG to text**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Output yang diharapkan

Jika `sample_image.png` berisi frasa Cyrillic “Привет мир”, konsol akan menampilkan:

```
=== OCR Result ===
Привет мир
```

Output mungkin menyertakan baris baru dan tanda baca persis seperti yang muncul pada gambar. Anda dapat memproses string tersebut dengan `String.Trim()`, `Regex`, atau utilitas pembersihan teks lainnya jika diperlukan.

## Langkah 7: Opsional – Simpan hasil ke file

Menyimpan hasil OCR memungkinkan pemrosesan lanjutan (mis., pengindeksan, terjemahan). Berikut cara cepat menulis teks ke file UTF‑8:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Kesalahan umum dan cara menghindarinya

| Masalah | Gejala | Solusi |
|-------|----------|-----|
| **Modul bahasa yang hilang** | `OcrException` on `Language = Language.Cyrillic` | Pastikan konektivitas internet pada run pertama atau pra‑unduh modul via paket offline Aspose. |
| **Gambar buram atau kontras rendah** | Poor accuracy, many “?” characters | Pra‑proses gambar: tingkatkan kontras, terapkan penajaman, atau konversi ke grayscale sebelum memberi ke engine. |
| **PNG sangat besar** | Long processing time, possible `OutOfMemoryException` | Turunkan skala seperti pada Langkah 3, atau bagi gambar multi‑halaman menjadi ubin terpisah. |
| **Karakter non‑UTF‑8** | Garbled output | Pastikan konsol atau penulis file menggunakan encoding UTF‑8 (`Encoding.UTF8`). |

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang menggabungkan semua langkah di atas. Salin ke proyek konsol baru dan jalankan setelah menyesuaikan jalur file.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Cara kerjanya

1. **Engine creation** – menyiapkan pipeline OCR.  
2. **Image loading** – mendukung baik PNG mentah maupun versi yang diturunkan skalanya untuk kinerja.  
3. **Language selection** – mendemonstrasikan **extract Cyrillic text** sambil menangani modul yang hilang.  
4. **Recognition** – panggilan inti **recognize text from PNG**.  
5. **Result handling** – menunjukkan **convert PNG to text** dan menulis output ke file.

Jalankan program dengan `dotnet run`. Jika semuanya sudah diatur dengan benar, Anda akan melihat teks yang dikenali dicetak ke konsol dan disimpan ke `ocr_output.txt`.

## Kesimpulan

Dalam tutorial ini Anda belajar **how to perform OCR** pada file PNG menggunakan Aspose.OCR untuk .NET, mencakup semua hal mulai dari **load image for OCR** hingga **extract Cyrillic text** dan **convert PNG to text**. Contoh lengkap yang dapat dijalankan memperlihatkan alur kerja standar, kasus tepi umum, dan tips praktis yang membuat pipeline OCR Anda dapat diandalkan.

**Langkah selanjutnya**

* Jelajahi **recognize text from PNG** dengan bahasa tambahan (Arab, Cina) dengan menggabungkan flag `Language`.  
* Integrasikan hasil OCR dengan Azure Cognitive Search untuk arsip dokumen yang dapat dicari.  
* Bereksperimen dengan pengaturan `OcrEngine` Aspose.OCR seperti `Resolution

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode kerja lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengunduh Model Aspose.OCR dan Mengekstrak Teks dari PNG di C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [Cara Melakukan OCR di C# – Mengenali Teks Cyrillic dengan Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [Cara Batch OCR di C# – Cara Cepat Mengekstrak Teks dari File PNG](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}