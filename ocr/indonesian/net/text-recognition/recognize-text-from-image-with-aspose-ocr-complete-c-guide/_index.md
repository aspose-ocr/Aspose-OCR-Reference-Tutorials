---
category: general
date: 2026-05-25
description: Mengenali teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  memuat gambar untuk OCR, mengatur bahasa OCR, membuat mesin OCR, dan mengekstrak
  teks dari TIFF.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: id
og_description: Mengenali teks dari gambar menggunakan Aspose OCR di C#. Tutorial
  ini menunjukkan cara membuat mesin OCR, memuat gambar untuk OCR, mengatur bahasa
  OCR, dan mengekstrak teks dari TIFF.
og_title: Mengenali teks dari gambar dengan Aspose OCR – Panduan Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: Mengenali Teks dari Gambar dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar dengan Aspose OCR – Panduan Lengkap C# 

Pernah butuh **mengenali teks dari gambar** tetapi tidak yakin perpustakaan mana yang memberikan kecepatan dan akurasi? Anda tidak sendirian. Dalam banyak proyek pemrosesan faktur atau arsip, titik sakit terbesar adalah mendapatkan teks bersih yang dapat dicari dari file TIFF tanpa menulis parser khusus.

Begini: Aspose OCR untuk .NET membuat seluruh alur kerja menjadi sangat mudah. Dalam panduan ini kami akan membahas semua yang Anda perlukan—menginstal paket, **membuat OCR engine**, memuat TIFF, mengatur bahasa OCR, dan akhirnya **mengekstrak teks dari TIFF**. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap jalankan yang dapat **mengenali teks dari gambar** dalam sekejap.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)
- Visual Studio 2022 (atau IDE apa pun yang Anda sukai)
- Aspose.OCR NuGet package (dukungan GPU memerlukan add‑on `Aspose.OCR.Gpu`)
- GPU dengan dukungan CUDA jika Anda menginginkan kecepatan ekstra (opsional namun disarankan)

> **Tips Pro:** Jika Anda tidak memiliki GPU, cukup hapus baris `GpuDevice` dan engine akan beralih ke CPU secara otomatis.

## Langkah 1: Instal Aspose OCR dan Buat OCR Engine

Pertama, tambahkan paket yang diperlukan melalui NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

Sekarang kita dapat **membuat OCR engine**. Objek ini adalah inti dari proses; ia menyimpan konfigurasi seperti perangkat yang digunakan dan batas memori.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**Mengapa ini penting:** Dengan mengaitkan engine ke GPU, Anda secara signifikan mengurangi waktu yang dibutuhkan untuk **mengenali teks dari gambar**, terutama untuk batch besar TIFF beresolusi tinggi.

## Langkah 2: Muat Gambar untuk OCR

Selanjutnya, kita perlu **memuat gambar untuk OCR**. Aspose.OCR bekerja dengan `System.Drawing.Image`, jadi format apa pun yang didukung GDI+ (termasuk TIFF multi‑halaman) dapat digunakan.

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

Jika Anda menangani TIFF multi‑halaman, Anda dapat melakukan loop melalui halaman menggunakan `image.SelectActiveFrame`, tetapi untuk kebanyakan skenario satu panggilan sudah cukup.

## Langkah 3: Atur Bahasa OCR

Engine tidak secara otomatis mengetahui bahasa yang Anda pindai. **Atur bahasa OCR** sebelum menjalankan recognizer; jika tidak, Anda akan mendapatkan output yang berantakan.

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **Tahukah Anda?** Mengganti bahasa saat runtime tidak memakan biaya—Anda bahkan dapat memproses dokumen campuran bahasa dengan mengubah properti ini antar halaman.

## Langkah 4: Lakukan Pengakuan – Mengenali Teks dari Gambar

Sekarang bagian yang menyenangkan: sebenarnya **mengenali teks dari gambar**. Metode `Recognize` mengembalikan string biasa dengan semua karakter yang terdeteksi.

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

Jika Anda memerlukan skor kepercayaan atau kotak pembatas, Anda dapat menggunakan overload yang mengembalikan objek `OcrResult`, tetapi untuk kebanyakan tugas ekstraksi string biasa sudah cukup.

## Langkah 5: Ekstrak Teks dari TIFF (dan tangani file multi‑halaman)

Ketika sumbernya adalah TIFF yang berisi beberapa halaman, Anda perlu mengulangi langkah 2‑4 untuk setiap frame. Berikut loop cepat yang **mengekstrak teks dari TIFF** halaman demi halaman:

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

Kode di atas mencetak teks yang diekstrak untuk setiap halaman, memudahkan untuk mengalirkan hasil ke basis data atau indeks pencarian.

## Langkah 6: Tampilkan atau Simpan Teks yang Diekstrak

Akhirnya, mari **tampilkan teks yang diekstrak** dan opsional menuliskannya ke file untuk pemrosesan selanjutnya.

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

Menjalankan program harus menampilkan karakter yang dikenali dan membuat `extracted_text.txt` di samping TIFF sumber Anda.

---

## Pertanyaan Umum & Kasus Tepi

- **Bagaimana jika GPU saya tidak terdeteksi?**  
  Hapus baris `GpuDevice`; engine akan otomatis beralih ke mode CPU. Performa akan lebih lambat tetapi hasil tetap akurat.

- **Apakah saya dapat memproses file PNG atau JPEG?**  
  Tentu—`Image.FromFile` bekerja dengan format apa pun yang didukung System.Drawing, jadi Anda dapat **memuat gambar untuk OCR** terlepas dari ekstensi.

- **Bagaimana cara menangani pemindaian beresolusi rendah?**  
  Tingkatkan `ocrEngine.PreprocessOptions.Dpi` sebelum memanggil `Recognize`. DPI yang lebih tinggi memberi engine lebih banyak piksel untuk diproses, meningkatkan akurasi.

- **Apakah ada batas ukuran TIFF?**  
  Properti `GpuMemoryLimit` membatasi penggunaan GPU. Jika batas tercapai, engine akan beralih ke CPU untuk halaman yang tersisa.

## Kesimpulan

Anda sekarang memiliki potongan kode lengkap, siap produksi yang **mengenali teks dari gambar** menggunakan Aspose OCR dalam C#. Tutorial ini mencakup cara **membuat OCR engine**, **memuat gambar untuk OCR**, **mengatur bahasa OCR**, dan **mengekstrak teks dari TIFF**—semua sambil memanfaatkan percepatan GPU untuk kecepatan.  

Dari sini Anda dapat:

- Bereksperimen dengan bahasa berbeda (`OcrLanguage.Spanish`, `OcrLanguage.ChineseSimplified`, dll).
- Mengintegrasikan output ke dalam indeks ElasticSearch yang dapat dicari.
- Menambahkan pasca‑pemrosesan (pemeriksaan ejaan, pembersihan regex) untuk meningkatkan kualitas data.

Cobalah pada batch faktur Anda sendiri, sesuaikan batas memori, dan saksikan kinerja OCR melambung. Selamat coding!

## Tutorial Terkait

- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cara Mengekstrak Teks dari Gambar dengan Menyiapkan Persegi Panjang di OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Ekstrak Teks dari Gambar – Mengenali Garis dengan Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}