---
category: general
date: 2026-03-21
description: Cara melakukan OCR batch di C# menjadi sederhana—pelajari cara mengekstrak
  teks dari gambar, mengonversi gambar menjadi teks, dan menyimpan OCR sebagai teks
  dengan pengaturan bahasa.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: id
og_description: Cara melakukan OCR batch di C# memungkinkan Anda mengekstrak teks
  dari gambar, mengonversi gambar menjadi teks, dan menyimpan OCR sebagai teks sambil
  mengatur bahasa OCR dengan mudah.
og_title: Cara Batch OCR di C# – Panduan Cepat
tags:
- OCR
- C#
- Aspose
title: Cara Melakukan Batch OCR di C# – Ekstrak Teks dari Gambar Secara Cepat
url: /id/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di C# – Ekstrak Teks dari Gambar dengan Cepat

Pernah bertanya-tanya **bagaimana cara batch OCR** ketika Anda memiliki ratusan gambar yang berada di dalam folder? Anda tidak sendirian—para pengembang terus-menerus menanyakan cara mengekstrak teks dari gambar tanpa menulis loop untuk setiap file. Kabar baiknya, Aspose.OCR memberikan cara yang bersih dan siap paralel untuk **mengonversi gambar menjadi teks** hanya dalam beberapa baris C#.

Pada tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan cara **menyimpan OCR sebagai teks**, memilih bahasa yang tepat, dan meningkatkan pemrosesan paralel untuk kecepatan. Pada akhir tutorial, Anda akan memiliki solusi mandiri yang dapat Anda masukkan ke dalam proyek .NET apa pun.

## Apa yang Anda Butuhkan

- .NET 6 atau lebih baru (API bekerja dengan .NET Core dan .NET Framework)
- Aspose.OCR untuk .NET (paket NuGet `Aspose.OCR`)
- Folder gambar yang ingin Anda proses (PNG, JPEG, TIFF, dll.)
- Sedikit rasa ingin tahu tentang pemrograman paralel (opsional, tetapi membantu)

Tidak ada layanan tambahan, tidak ada kunci cloud—hanya kode C# murni yang berjalan secara lokal.

---

![alur batch OCR](placeholder.png){alt="diagram alur batch OCR"}

## Langkah 1: Siapkan Proyek dan Instal Aspose.OCR

Pertama-tama, buat aplikasi console (atau gunakan yang sudah ada) dan tambahkan paket Aspose.OCR:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Tip Pro:** Jika Anda menggunakan Visual Studio, klik kanan proyek → *Manage NuGet Packages* → cari *Aspose.OCR* dan instal versi stabil terbaru.

Ini memberi Anda akses ke `OcrBatchProcessor`, `OcrEngineSettings`, dan enum `Language`.

## Langkah 2: Tentukan Folder Input dan Output

Batch processor perlu mengetahui di mana gambar sumber berada dan ke mana file teks yang diekstrak harus ditulis. Simpan jalur sebagai absolut atau relatif terhadap root proyek—pastikan folder tersebut ada sebelum Anda menjalankan kode.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Mengapa ini penting:** Jika folder output tidak ada, processor akan melemparkan pengecualian, menghentikan seluruh batch. Membuatnya sebelumnya menjamin proses berjalan lancar.

## Langkah 3: Konfigurasikan Pengaturan OCR (termasuk bahasa)

Di sinilah Anda **mengatur bahasa OCR** untuk seluruh batch. Aspose.OCR mendukung puluhan bahasa; Bahasa Inggris adalah default, tetapi Anda dapat beralih ke Prancis, Spanyol, dll., dengan mengubah nilai enum `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Jika Anda pernah perlu memproses bahasa yang berbeda per gambar, Anda dapat menimpa pengaturan ini per file nanti—lebih lanjut nanti.

## Langkah 4: Bangun Objek `OcrBatchProcessor`

Sekarang kami menggabungkan semuanya. `OcrBatchProcessor` memungkinkan Anda menentukan folder input, folder output, format output, opsi paralel, dan pengaturan bersama yang baru saja kami buat.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Mengapa paralelisme?** Ketika Anda memiliki puluhan atau ratusan gambar, memprosesnya satu per satu dapat sangat lambat. Menetapkan `MaxDegreeOfParallelism` ke 4 memungkinkan runtime menggunakan empat core CPU secara bersamaan, secara dramatis mengurangi total waktu pada workstation tipikal.

## Langkah 5: Jalankan Operasi Batch

Dengan processor yang dikonfigurasi, eksekusi cukup satu pemanggilan metode. Library menangani enumerasi file, OCR, dan penulisan hasil secara otomatis.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Ketika konsol mencetak *“Batch OCR completed.”* Anda akan menemukan file `.txt` di samping setiap gambar asli di dalam `BatchResults`. Setiap file teks berisi karakter mentah yang diekstrak dari gambar sumbernya—tepat apa yang Anda butuhkan untuk **mengekstrak teks dari gambar** untuk pemrosesan selanjutnya.

### Output yang Diharapkan

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Buka salah satu file tersebut dan Anda akan melihat representasi teks biasa dari konten gambar.

## Langkah 6: Verifikasi Hasil (Opsional)

Biasanya baik untuk memeriksa kembali beberapa file untuk memastikan OCR berjalan seperti yang diharapkan. Cara cepatnya adalah membaca baris pertama setiap file yang dihasilkan dan mencetaknya ke konsol:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Jika Anda melihat karakter yang rusak, pertimbangkan untuk mengubah pengaturan `Language` atau menyesuaikan kualitas gambar (mis., meningkatkan DPI, mengonversi ke skala abu-abu).

## Variasi Lanjutan & Kasus Tepi

### 1. Override Bahasa per File
Terkadang batch berisi dokumen multibahasa. Anda dapat memeriksa nama setiap gambar dan menetapkan bahasa secara langsung:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Format Output Berbeda
Jika Anda membutuhkan PDF yang dapat dicari alih-alih teks biasa, ubah `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

Itu akan **mengonversi gambar menjadi teks** di dalam kontainer PDF, mempertahankan tata letak asli.

### 3. Menangani Gambar Besar
Gambar dengan resolusi sangat tinggi dapat menghabiskan memori. Untuk menjaga proses tetap ringan, aktifkan down‑sampling gambar:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Pencatatan Kesalahan
Processor melemparkan pengecualian untuk file yang tidak dapat dibaca. Bungkus `Execute` dalam try/catch dan catat nama file yang bermasalah:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap disalin‑tempel:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Simpan ini sebagai `Program.cs`, bangun proyek, dan jalankan `dotnet run`. Anda akan melihat output konsol yang mengonfirmasi selesai, diikuti dengan pratinjau singkat teks yang diekstrak.

---

## Kesimpulan

Kami baru saja membahas **cara batch OCR** di C# menggunakan Aspose.OCR, menunjukkan cara **mengekstrak teks dari gambar**, **mengonversi gambar menjadi teks**, dan **menyimpan OCR sebagai teks** sambil **mengatur bahasa OCR** agar sesuai dengan konten Anda. Contoh ini sepenuhnya berfungsi, mencakup pemrosesan paralel untuk kecepatan, dan menyediakan kait untuk skenario lanjutan seperti override bahasa per file atau output PDF.

Siap untuk langkah selanjutnya? Coba ganti `OcrOutputFormat.PlainText` dengan `SearchablePdf` dan lihat betapa mudahnya menghasilkan PDF yang dapat dicari. Atau bereksperimen dengan nilai `MaxDegreeOfParallelism` yang berbeda untuk memaksimalkan setiap milidetik pada mesin multi‑core.

Jika Anda mengalami masalah, periksa kembali jalur folder, pastikan gambar dapat dibaca, dan verifikasi enum bahasa cocok dengan teks dalam gambar Anda. Selamat coding, semoga batch OCR Anda cepat dan akurat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}