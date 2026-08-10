---
category: general
date: 2026-05-31
description: Pelajari cara mengenali teks dari gambar dalam C# dengan Aspose OCR,
  termasuk cara mengekstrak teks dari file TIFF dan memuat gambar untuk OCR secara
  efisien.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: id
og_description: Panduan langkah demi langkah untuk mengenali teks dari gambar dengan
  Aspose OCR, mencakup ekstraksi dari TIFF dan pemuatan gambar yang tepat untuk OCR.
og_title: Mengenali teks dari gambar di C# menggunakan Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Mengenali teks dari gambar di C# menggunakan Aspose OCR
url: /id/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar di C# menggunakan Aspose OCR

Pernah perlu **mengenali teks dari gambar** tetapi tidak yakin harus mulai dari mana di C#? Anda tidak sendirian—banyak pengembang mengalami kebuntuan saat menangani dokumen yang dipindai atau TIFF multi‑halaman. Dalam panduan ini kami akan memandu Anda melalui contoh lengkap yang siap‑jalan yang **mengenali teks dari gambar** menggunakan pustaka Aspose OCR, dan kami juga akan menunjukkan cara **mengekstrak teks dari tiff** serta cara terbaik **memuat gambar untuk OCR** tanpa membuat Anda stres.

Kami akan membahas semuanya mulai dari menginstal paket NuGet hingga menangani akselerasi GPU dan beralih kembali ke CPU bila diperlukan. Pada akhir tutorial ini Anda akan memiliki aplikasi konsol yang mencetak teks yang dikenali serta waktu pemrosesan—tanpa bagian yang hilang, tanpa referensi yang samar.

## Apa yang Akan Anda Bangun

- Aplikasi konsol .NET sederhana yang memuat gambar (termasuk TIFF multi‑halaman)  
- Mesin OCR yang dikonfigurasi untuk penggunaan GPU, dengan fallback CPU yang elegan  
- Ekstraksi teks polos dari gambar, dicetak ke konsol  
- Informasi waktu sehingga Anda dapat melihat dampak kinerja antara GPU vs. CPU  

**Prasyarat**

- .NET 6 SDK atau lebih baru (kode ini bekerja dengan .NET Core dan .NET Framework)  
- Familiaritas dasar dengan C# dan baris perintah  
- Akses internet untuk mengunduh paket NuGet Aspose.OCR  

Jika Anda sudah memiliki semua itu, mari kita mulai.

![Kode C# untuk mengenali teks dari gambar menggunakan Aspose OCR](image.png "Kode C# untuk mengenali teks dari gambar menggunakan Aspose OCR")

## Langkah 1 – Mengenali teks dari gambar: Siapkan mesin OCR

Hal pertama yang perlu dilakukan, kita membutuhkan instance `OcrEngine`. Aspose OCR memungkinkan Anda memilih perangkat pemrosesan—GPU untuk kecepatan, CPU sebagai jaring pengaman. Mesin juga menerima petunjuk batas memori, yang dapat berguna pada mesin bersama.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Mengapa ini penting:**  
Memilih `OcrDevice.Gpu` dapat memangkas beberapa detik dari waktu pengenalan untuk gambar besar, terutama TIFF multi‑halaman. `GpuMemoryLimit` mencegah aplikasi Anda menghabiskan semua memori GPU pada workstation yang berbagi sumber daya.

## Langkah 2 – Memuat gambar untuk OCR (termasuk dukungan TIFF)

Sekarang kita memberi mesin sebuah gambar. `ImageStream.FromFile` milik Aspose menerima **format apa pun** yang didukung pustaka—TIFF, PNG, JPEG, apa saja. Langkah ini secara langsung memenuhi kebutuhan **memuat gambar untuk OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Tips pro:** Jika Anda bekerja dengan TIFF multi‑halaman, Aspose secara otomatis memperlakukan setiap halaman sebagai frame terpisah, dan mesin akan memprosesnya secara berurutan. Tidak perlu kode tambahan.

## Langkah 3 – Jalankan pengenalan dan **ekstrak teks dari tiff**

Dengan mesin yang sudah siap dan gambar yang sudah dimuat, kita memulai operasi OCR. Metode `Recognize` mengembalikan `OcrResult` yang berisi teks polos, skor kepercayaan, dan detail waktu.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Penanganan kasus tepi:**  
Jika GPU tidak tersedia, `engine.Recognize()` tetap berfungsi karena mesin secara diam-diam beralih ke CPU. Anda dapat memeriksa `engine.Device` setelah pengenalan jika perlu mencatat perangkat mana yang sebenarnya digunakan.

## Langkah 4 – Mengambil teks polos yang dikenali

Mengekstrak teks sangat mudah—cukup baca properti `Text`. Di sinilah kita akhirnya **mengekstrak teks dari tiff** (atau gambar apa pun) dan menampilkannya kepada pengguna.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Anda akan melihat karakter mentah, dengan jeda baris dipertahankan sebagaimana muncul dalam gambar sumber. Untuk output yang lebih terstruktur (seperti JSON atau CSV), Anda dapat menelusuri `result.Regions` dan `result.Lines`, tetapi teks polos biasanya sudah cukup untuk skrip cepat.

## Langkah 5 – Mengukur waktu pemrosesan dan menangani fallback GPU

Kinerja penting, terutama saat Anda memproses puluhan halaman. Properti `ProcessingTime` memberi tahu Anda berapa lama OCR berlangsung, terlepas dari apakah dijalankan di GPU atau CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Mengapa Anda harus peduli:**  
Jika Anda melihat waktu yang membengkak, Anda mungkin ingin menyesuaikan `GpuMemoryLimit` atau beralih ke CPU secara eksplisit (`Device = OcrDevice.Cpu`). Sebaliknya, hasil kurang dari satu detik pada TIFF besar berarti akselerasi GPU Anda bekerja dengan baik.

## Contoh Lengkap yang Siap‑Jalankan

Salin kode di bawah ini ke dalam proyek konsol baru (`dotnet new console -n OcrDemo`) dan jalankan `dotnet add package Aspose.OCR`. Kemudian ganti `YOUR_DIRECTORY/sample_multi_page.tif` dengan jalur ke gambar Anda.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Output yang diharapkan (dipotong untuk singkat):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Jika mesin Anda tidak memiliki GPU yang memadai, waktu yang berlalu mungkin beberapa detik lebih lama, tetapi teks tetap akan diekstrak dengan benar.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

- **Bagaimana jika gambar sangat besar (lebih dari 10 MB)?**  
  Kurangi resolusinya sebelum memberi ke mesin, atau tingkatkan `GpuMemoryLimit` jika Anda memiliki cukup VRAM.  
- **Bisakah saya memproses banyak gambar dalam loop?**  
  Tentu saja. Cukup gunakan kembali instance `OcrEngine` yang sama dan tetapkan `ImageStream` baru setiap iterasi.  
- **Apakah saya perlu membuang (dispose) sesuatu?**  
  `OcrEngine` mengimplementasikan `IDisposable`. Bungkus dalam blok `using` untuk manajemen sumber daya yang bersih, terutama saat bekerja dengan sumber daya GPU.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **Bagaimana dengan bahasa selain Inggris?**  
  Setel `engine.Language = OcrLanguage.Spanish` (atau bahasa lain yang didukung) sebelum memanggil `Recognize()`.  

## Kesimpulan

Anda kini memiliki solusi lengkap, ujung‑ke‑ujung yang **mengenali teks dari gambar** di C# menggunakan Aspose OCR. Tutorial ini mencakup cara **memuat gambar untuk OCR**, cara **mengekstrak teks dari tiff**, dan cara mengukur kinerja sambil menangani fallback GPU dengan elegan.

Dari sini Anda dapat:

- Bereksperimen dengan format gambar lain (BMP, PDF) untuk melihat bagaimana Aspose menanganinya.  
- Menyelami `result.Regions` untuk data kotak pembatas jika Anda memerlukan informasi tata letak‑aware


## Apa yang Harus Anda Pelajari Selanjutnya?

- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}