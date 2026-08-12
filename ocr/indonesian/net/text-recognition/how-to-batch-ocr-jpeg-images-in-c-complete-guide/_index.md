---
category: general
date: 2026-02-22
description: Cara melakukan OCR batch pada gambar JPEG di C# dengan Aspose.OCR. Pelajari
  cara mengekstrak teks dari JPG, mengonversi JPG ke TXT, dan memproses gambar secara
  batch dengan efisien.
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: id
og_description: Cara melakukan OCR batch pada gambar JPEG di C# menggunakan Aspose.OCR.
  Tutorial ini menunjukkan cara mengekstrak teks dari JPG, mengonversi JPG ke TXT,
  dan memproses gambar secara batch dalam hitungan menit.
og_title: Cara Memproses OCR Gambar JPEG Secara Batch di C# – Panduan Lengkap
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cara Batch OCR Gambar JPEG di C# – Panduan Lengkap
url: /id/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR Gambar JPEG di C# – Panduan Lengkap

Pernah bertanya‑tanya **bagaimana cara batch OCR** sebuah folder penuh gambar tanpa menulis program terpisah untuk setiap file? Pada panduan ini kami akan menunjukkan **cara batch OCR** file JPEG menggunakan Aspose.OCR, sehingga Anda dapat **mengekstrak teks dari jpg** dan **mengonversi jpg ke txt** hanya dengan beberapa baris kode.  

Jika Anda pernah menatap direktori berisi faktur yang dipindai dan berpikir, “Harus ada cara yang lebih cepat,” Anda berada di tempat yang tepat. Kami akan membahas setiap langkah, menjelaskan mengapa setiap bagian penting, dan bahkan menambahkan beberapa tip profesional untuk menangani batch besar.

## Apa yang Akan Anda Bangun

Pada akhir tutorial ini Anda akan memiliki aplikasi konsol kecil yang:

* Memindai direktori yang diberikan untuk file `*.jpg`.  
* Mengirim setiap gambar melalui mesin Aspose OCR (dipercepat GPU bila Anda memiliki kartu yang mendukung).  
* Menulis teks yang dikenali ke file `.txt` yang berada di samping gambar asli.  

Tanpa layanan eksternal, tanpa menyalin‑tempel manual—hanya C# murni dan perpustakaan OCR yang handal.

### Prasyarat

* .NET 6.0 atau lebih baru (kode ini juga berfungsi di .NET Framework 4.8).  
* Visual Studio 2022 atau editor apa pun yang mendukung C#.  
* Paket NuGet Aspose.OCR (versi percobaan gratis cukup untuk pengujian).  

Jika Anda belum memiliki salah satu dari itu, berhenti sejenak dan instal dulu; sisanya mengasumsikan semuanya sudah siap.

![Contoh cara batch OCR](/images/how-to-batch-ocr.png "diagram cara batch ocr")

## Langkah 1: Instal Paket NuGet Aspose.OCR

Hal pertama yang harus dilakukan—proyek Anda memerlukan perpustakaan OCR. Buka terminal di folder solusi dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Atau gunakan UI NuGet Package Manager di Visual Studio. Ini akan mengunduh semua yang Anda perlukan, termasuk binary yang diaktifkan GPU bila mesin Anda mendukungnya.

> **Tip pro:** Jika Anda berencana menjalankannya di server tanpa GPU, setel `UseGpu = false` nanti; mesin akan otomatis beralih ke CPU.

## Langkah 2: Konfigurasi Mesin OCR

Membuat dan mengonfigurasi `OcrEngine` adalah tempat keajaiban dimulai. Anda akan memberi tahu mesin bahasa apa yang diharapkan, apakah menggunakan GPU, dan format output yang diinginkan.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**Mengapa ini penting:** Menetapkan `Language` meningkatkan akurasi karena mesin dapat mempersempit set karakter. Mengaktifkan `UseGpu` dapat memotong waktu pemrosesan hingga setengah pada kartu grafis modern, yang sangat menguntungkan saat Anda **memproses batch gambar**.

## Langkah 3: Kenali Semua File JPEG dalam Folder

Sekarang biarkan Aspose melakukan pekerjaan berat. Metode statik `BatchProcessor.RecognizeFolder` menelusuri direktori, menjalankan OCR pada setiap file yang cocok, dan mengembalikan koleksi hasil.

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**Penanganan kasus tepi:** Jika folder berisi sub‑folder, Anda dapat menambahkan overload `SearchOption.AllDirectories` (atau melakukan rekurensi manual) agar tidak ada file yang terlewat.

## Langkah 4: Tulis Setiap Hasil ke File `.txt` yang Sesuai

Objek `OcrResult` berisi jalur file asli dan teks yang dikenali. Loop melalui mereka, ubah ekstensi, dan tulis outputnya.

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

Itu saja—setiap JPEG kini memiliki file teks saudara yang dapat Anda gunakan dalam proses selanjutnya, indeks pencarian, atau sekadar arsip.

## Langkah 5: Jalankan Aplikasi dan Verifikasi Output

Kompilasi dan jalankan program:

```bash
dotnet run
```

Dengan asumsi folder berisi `invoice1.jpg` dan `receipt2.jpg`, Anda akan melihat `invoice1.txt` dan `receipt2.txt` muncul di sampingnya. Buka salah satu file `.txt`; Anda akan menemukan output OCR mentah, misalnya:

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

Jika teks terlihat berantakan, periksa kembali bahwa gambar sumber memiliki kontras tinggi dan properti `Language` cocok dengan bahasa dokumen.

## Langkah 6: Penyesuaian Lanjutan (Opsional)

### a) Menangani Scan Berkualitas Rendah

Kadang JPEG berisik. Anda dapat memproses gambar terlebih dahulu dengan Aspose.Imaging atau perpustakaan lain:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### b) Paralelisasi Batch

Jika Anda memiliki banyak file dan CPU multi‑core, bungkus loop dengan `Parallel.ForEach`:

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

Namun perlu diingat bahwa mesin Aspose OCR sendiri tidak thread‑safe; Anda memerlukan instance `OcrEngine` terpisah per thread atau menggunakan antrian bersamaan.

### c) Logging dan Penanganan Error

Solusi yang kuat mencatat kegagalan agar dapat dicoba lagi nanti:

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke Console App baru:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

Jalankan, perhatikan output di konsol, lalu buka beberapa file `.txt` untuk memastikan langkah **mengekstrak teks dari jpg** berhasil.  

---

## Kesimpulan

Kami baru saja membahas **cara batch OCR** sekumpulan gambar JPEG di C# menggunakan Aspose.OCR, mengubah setiap gambar menjadi file `.txt` yang dapat dicari. Solusinya ringkas, mendukung GPU, dan mudah diperluas untuk penanganan error, pra‑pemrosesan gambar, atau eksekusi paralel.  

Jika Anda siap melangkah lebih jauh, pertimbangkan langkah selanjutnya berikut:

* **Proses batch gambar** format lain (`*.png`, `*.tif`) dengan mengubah `searchPattern`.  
* Gabungkan output dengan mesin pencarian teks penuh seperti Lucene.NET untuk pencarian dokumen instan.  
* Jelajahi fitur konversi PDF Aspose untuk menghasilkan PDF yang dapat dicari langsung dari hasil OCR.  

Silakan bereksperimen—ganti bahasa, matikan GPU, atau alirkan teks ke basis data. Pola dasarnya tetap sama, dan kini Anda memiliki fondasi yang kuat untuk dibangun.

Selamat coding, semoga pipeline OCR Anda selalu cepat dan akurat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}