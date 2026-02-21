---
category: general
date: 2026-02-20
description: Cara melakukan OCR pada file DjVu di C#. Pelajari cara mengenali teks
  dari gambar dan mengonversi DjVu ke teks dengan cepat menggunakan Aspose OCR.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- how to read djvu
- extract text from image
- convert djvu to text
language: id
og_description: Cara melakukan OCR pada file DjVu di C#. Tutorial ini menunjukkan
  cara mengenali teks dari gambar, membaca DjVu, dan mengonversi DjVu ke teks menggunakan
  Aspose OCR.
og_title: Cara Melakukan OCR pada File DjVu di C# – Panduan Lengkap
tags:
- OCR
- C#
- DjVu
- Aspose
title: Cara Melakukan OCR pada File DjVu di C# – Panduan Langkah demi Langkah
url: /id/net/text-recognition/how-to-perform-ocr-on-djvu-files-in-c-step-by-step-guide/
---

produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR pada File DjVu di C# – Panduan Lengkap

Pernah bertanya‑tanya **bagaimana cara melakukan OCR** pada dokumen DjVu tanpa menggaruk kepala? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika harus **mengenali teks dari gambar** yang berada di dalam kontainer DjVu. Kabar baiknya? Dengan beberapa baris C# dan pustaka Aspose OCR, Anda dapat mengekstrak teks tersembunyi itu dalam sekejap.

Dalam tutorial ini kami akan membahas semua yang Anda perlukan untuk mengubah halaman DjVu menjadi teks biasa. Pada akhir tutorial Anda akan tahu **cara membaca DjVu**, cara **mengekstrak teks dari gambar**, dan bahkan cara **mengonversi DjVu ke teks** untuk pemrosesan lanjutan. Tanpa layanan eksternal, tanpa referensi samar—hanya contoh yang dapat dijalankan secara mandiri.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

- .NET 6.0 SDK atau yang lebih baru (kode ini juga bekerja dengan .NET Framework 4.8).
- Visual Studio 2022 atau editor apa pun yang mendukung C#.
- Lisensi Aspose OCR untuk .NET (versi percobaan gratis dapat digunakan untuk pengujian).
- File DjVu contoh (`sample.djvu`) yang ditempatkan di folder yang dapat Anda referensikan.

Menyiapkan semua ini akan membuat alur kerja berjalan mulus—tidak ada kejutan “referensi hilang” di kemudian hari.

## Cara Melakukan OCR pada Halaman DjVu

Inti idenya sederhana: muat halaman DjVu sebagai gambar, serahkan ke mesin OCR, dan baca string hasilnya. Mari kita uraikan langkah demi langkah.

### Langkah 1: Instal Aspose OCR

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah ini akan mengunduh binari Aspose OCR terbaru beserta dependensinya. Jika Anda lebih suka menggunakan UI NuGet Package Manager, cukup cari **Aspose.OCR** dan klik **Install**.

### Langkah 2: Inisialisasi Mesin OCR

Membuat instance `OcrEngine` adalah hal pertama yang Anda lakukan ketika ingin **melakukan OCR**. Anggap saja ini menyalakan otak pemindai.

```csharp
using Aspose.OCR;

// ...

// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Tips profesional:** Menggunakan satu `OcrEngine` untuk beberapa halaman menghemat memori dan mempercepat proses.

### Langkah 3: Muat Halaman DjVu sebagai Gambar

File DjVu tidak didukung secara langsung oleh kebanyakan API gambar, tetapi Aspose dapat memperlakukan setiap halaman sebagai bitmap. Di sini kita menggunakan `System.Drawing.Image` untuk membaca file.

```csharp
using System.Drawing;

// ...

// Step 3: Load a DjVu page as an image
string djvuPath = @"C:\Path\To\Your\Directory\sample.djvu";
Image djvuPage = Image.FromFile(djvuPath);
```

> **Mengapa ini berhasil:** `Image.FromFile` secara otomatis mendekode aliran DjVu menjadi format raster yang dipahami mesin OCR. Jika Anda perlu memproses halaman tertentu dari DjVu multi‑halaman, gunakan Aspose PDF atau Aspose Imaging untuk mengekstrak halaman tersebut terlebih dahulu.

### Langkah 4: Kenali Teks dari Gambar

Sekarang keajaiban terjadi. Metode `Recognize` memindai bitmap dan mengembalikan string yang berisi karakter‑karakter yang terdeteksi.

```csharp
// Step 4: Perform OCR to extract text from the image
string extractedText = ocrEngine.Recognize(djvuPage);
```

Pada titik ini Anda telah **mengenali teks dari gambar** yang awalnya berada di dalam kontainer DjVu. String tersebut mungkin berisi pemisah baris, tanda baca, dan bahkan karakter Unicode jika bahasa sumber mendukungnya.

### Langkah 5: Tampilkan atau Simpan Hasilnya

Untuk pemeriksaan cepat, cukup cetak teks ke konsol. Pada aplikasi dunia nyata Anda mungkin akan menulisnya ke file atau basis data.

```csharp
// Step 5: Display the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan.

```csharp
// File: DjvuOcrExample.cs
using System;
using System.Drawing;
using Aspose.OCR;

class DjvuExample
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load a DjVu page as an image
        Image djvuPage = Image.FromFile(@"C:\Path\To\Your\Directory\sample.djvu");

        // Perform OCR to extract text from the image
        string extractedText = ocrEngine.Recognize(djvuPage);

        // Display the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur...
```

Jika Anda melihat karakter yang kacau, pastikan file DjVu tidak terenkripsi dan Anda telah mengatur bahasa yang tepat pada `ocrEngine.Language`. Secara default mesin mengasumsikan bahasa Inggris; Anda dapat beralih ke bahasa Prancis, Jerman, dll., dengan menetapkan `ocrEngine.Language = Language.French;`.

## Kenali Teks dari Gambar – Kendala Umum

Meskipun contoh sudah solid, pengembang sering menemui beberapa kasus tepi:

| Masalah | Mengapa Terjadi | Solusi |
|---------|----------------|--------|
| **Output kosong** | Resolusi gambar terlalu rendah (<300 dpi). | Gunakan `ocrEngine.ImageResolution = 300;` sebelum memanggil `Recognize`. |
| **Bahasa salah** | OCR default ke bahasa Inggris. | Tetapkan `ocrEngine.Language = Language.Spanish;` (atau bahasa lain yang didukung). |
| **Memory leak** | Halaman DjVu besar tetap berada di memori setelah diproses. | Panggil `djvuPage.Dispose();` setelah selesai. |
| **DjVu multi‑halaman** | Hanya halaman pertama yang dimuat. | Loop melalui halaman menggunakan kelas `DjvuImage` dari Aspose Imaging. |

Menangani hal‑hal ini sejak awal menghemat banyak jam debugging.

## Cara Membaca File DjVu di C# – Lebih dari Sekadar OCR Sederhana

Jika proyek Anda membutuhkan lebih dari satu halaman, Anda harus mengekstrak setiap halaman sebagai gambar terlebih dahulu. Aspose Imaging membuatnya mudah:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;

// ...

string djvuPath = @"sample.djvu";
using (DjvuImage djvu = (DjvuImage)Image.Load(djvuPath))
{
    for (int i = 0; i < djvu.Frames.Count; i++)
    {
        using (Image page = djvu.Frames[i].ConvertToRaster())
        {
            // Run OCR on each page
            string pageText = ocrEngine.Recognize(page);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
    }
}
```

Pola ini memungkinkan Anda **mengonversi DjVu ke teks** halaman demi halaman, cocok untuk pemrosesan batch arsip besar.

## Ekstrak Teks dari Gambar – Penyempurnaan Akurasi

Pengaturan OCR default sudah cukup baik untuk pemindaian bersih, tetapi Anda dapat meningkatkan akurasi:

```csharp
ocrEngine.ImagePreprocessingOptions = new ImagePreprocessingOptions()
{
    // Binarize the image to improve contrast
    BinarizationMethod = BinarizationMethod.Otsu,
    // Deskew the image if it’s tilted
    Deskew = true,
    // Remove noise
    NoiseRemoval = true
};
```

Penyesuaian ini sangat berguna ketika sumber DjVu berisi catatan tulisan tangan atau grafik dengan kontras rendah.

## Konversi DjVu ke Teks – Contoh End‑to‑End Lengkap

Berikut versi ringkas yang menggabungkan semuanya: memuat DjVu multi‑halaman, pra‑memproses tiap halaman, melakukan OCR, dan menyimpan output ke file `.txt`.

```csharp
using System;
using System.IO;
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;
using Aspose.OCR;
using Aspose.OCR.Models;

class DjvuToTextConverter
{
    static void Main()
    {
        // Prepare OCR engine with preprocessing
        OcrEngine ocr = new OcrEngine
        {
            ImagePreprocessingOptions = new ImagePreprocessingOptions()
            {
                BinarizationMethod = BinarizationMethod.Otsu,
                Deskew = true,
                NoiseRemoval = true
            }
        };

        string inputPath = @"C:\Docs\sample.djvu";
        string outputPath = @"C:\Docs\sample_extracted.txt";

        using (DjvuImage djvu = (DjvuImage)Image.Load(inputPath))
        using (StreamWriter writer = new StreamWriter(outputPath))
        {
            for (int i = 0; i < djvu.Frames.Count; i++)
            {
                using (var page = djvu.Frames[i].ConvertToRaster())
                {
                    string text = ocr.Recognize(page);
                    writer.WriteLine($"--- Page {i + 1} ---");
                    writer.WriteLine(text);
                }
            }
        }

        Console.WriteLine($"Extraction complete. Text saved to {outputPath}");
    }
}
```

Menjalankan skrip ini akan membuat `sample_extracted.txt` dengan konten tiap halaman yang dipisahkan rapi. Ini cara tercepat untuk **mengonversi DjVu ke teks** untuk pengindeksan, pencarian, atau pengarsipan.

## Kesimpulan

Kami telah membahas **cara melakukan OCR** pada file DjVu dari awal hingga akhir, mengeksplorasi cara **mengenali teks dari gambar**, serta teknik **mengonversi DjVu ke teks**. Selamat mencoba!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}