---
category: general
date: 2026-04-26
description: Ekstrak teks dari file PNG dengan cepat menggunakan C#. Pelajari cara
  mengonversi gambar menjadi teks, membaca file PNG, mengulangi gambar, dan melakukan
  OCR batch pada gambar dalam hitungan menit.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: id
og_description: Ekstrak teks dari file PNG dengan cepat menggunakan C#. Panduan ini
  menunjukkan cara mengonversi gambar menjadi teks, membaca file PNG, mengulang gambar,
  dan melakukan OCR batch pada gambar.
og_title: Ekstrak Teks dari PNG – Tutorial OCR Batch C# Lengkap
tags:
- C#
- OCR
- Aspose
title: Ekstrak Teks dari PNG – Tutorial OCR Batch C# Lengkap
url: /id/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari PNG – Tutorial Lengkap OCR Batch C#

Pernah perlu **mengekstrak teks dari file PNG** tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami kebingungan saat pertama kali mencoba OCR pada folder screenshot. Kabar baiknya, dengan beberapa baris C# dan Aspose OCR Anda dapat mengonversi gambar ke teks, membaca file PNG, melakukan loop pada gambar, dan memproses semuanya secara batch dalam satu langkah.  

Dalam tutorial ini kami akan membimbing Anda melalui aplikasi console yang siap dijalankan dan melakukan semua itu. Pada akhir tutorial Anda akan memiliki solusi mandiri yang mengambil teks dari setiap PNG dalam sebuah direktori dan menempatkan file `.txt` yang cocok di samping masing‑masing gambar. Tanpa skrip tambahan, tanpa menyalin‑tempel manual—hanya kode murni.

## Apa yang Anda Butuhkan

- **.NET 6 SDK** (atau versi .NET yang lebih baru). Gratis, cepat, dan dapat dijalankan di mana saja.  
- **Aspose.OCR for .NET** (paket NuGet). Perpustakaan ini menyertakan akselerasi GPU jika Anda memiliki GPU yang kompatibel, namun juga akan beralih ke CPU secara otomatis.  
- Sebuah folder yang berisi beberapa **gambar PNG** yang ingin Anda proses.  
- Editor teks atau IDE—Visual Studio, VS Code, Rider—sesuai preferensi Anda.

Itu saja. Jika Anda sudah memiliki semua itu, Anda siap memulai.

![extract text from png example](image.png "extract text from png demo screenshot")

*Teks alt gambar: “extract text from png using C# batch OCR”*

## Langkah 1 – Siapkan Proyek dan Instal Aspose.OCR

Pertama, buat proyek console baru dan tambahkan paket Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Mengapa kita menggunakan aplikasi console? Ini adalah host paling sederhana untuk pekerjaan batch, dan Anda dapat menjalankannya dari command line atau menjadwalkannya dengan task runner. Jika nanti Anda memerlukan UI, Anda cukup memindahkan logika inti ke dalam class library.

## Langkah 2 – Inisialisasi OCR Engine yang Dipercepat GPU (atau fallback CPU)

Aspose menyediakan `GpuOcrEngine` yang secara otomatis mendeteksi GPU yang didukung. Jika tidak ada yang ditemukan, ia akan beralih ke engine CPU reguler—tanpa kode tambahan.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Pro tip:** Jika Anda berada di server headless tanpa GPU, Anda dapat mengganti `GpuOcrEngine` dengan `OcrEngine` dan kode akan berperilaku persis sama.

## Langkah 3 – Loop Melalui Gambar di Direktori Target

Kita perlu **loop melalui gambar** dan hanya memilih file PNG. Metode `Directory.GetFiles` melakukan pekerjaan berat, dan kita akan melindungi dari folder kosong.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Perhatikan penggunaan `SearchOption.TopDirectoryOnly`. Jika nanti Anda perlu menelusuri sub‑folder, cukup ubah menjadi `AllDirectories`. Perubahan kecil ini memungkinkan Anda **mengonversi gambar ke teks** dalam seluruh pohon direktori dengan satu baris kode.

## Langkah 4 – Lakukan OCR dan Simpan Hasilnya

Sekarang masuk ke inti alur kerja **batch OCR images**. Kita memuat setiap PNG, menjalankan `Recognize()`, dan menulis string yang diekstrak ke file `.txt` yang memiliki nama dasar yang sama.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Mengapa membungkusnya dalam try/catch?** Batch gambar dunia nyata sering berisi file yang rusak atau PNG dengan profil warna yang tidak umum. Menangkap pengecualian mencegah seluruh proses crash dan memungkinkan Anda melanjutkan pemrosesan file yang tersisa.

## Langkah 5 – Jalankan Aplikasi dan Verifikasi Output

Bangun dan luncurkan aplikasi:

```bash
dotnet run
```

Anda seharusnya melihat log console serupa dengan:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Buka salah satu file `.txt` yang dihasilkan—di situ teks yang diekstrak. Jika sebuah file kosong, periksa kembali kualitas gambar; OCR bekerja paling baik dengan teks yang jelas dan kontras tinggi.

### Skrip Verifikasi Cepat (opsional)

Jika Anda ingin memastikan setiap PNG memiliki file teks yang cocok, jalankan satu baris PowerShell berikut:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Variasi Umum & Kasus Edge

| Situasi | Apa yang Diubah |
|-----------|----------------|
| **Bahasa non‑Latin** (misalnya Cyrillic) | Set `ocrEngine.Language = Language.Cyrillic;` |
| **Set gambar besar (>10 000 file)** | Gunakan `Parallel.ForEach` untuk mempercepat pemrosesan, tetapi perhatikan penggunaan memori GPU. |
| **Perlu mempertahankan urutan gambar asli** | Urutkan `pngFiles` sebelum `foreach` (`Array.Sort(pngFiles);`). |
| **Menjalankan di server CI tanpa GPU** | Ganti `GpuOcrEngine` dengan `OcrEngine` untuk menghindari error inisialisasi GPU. |
| **Hanya ingin memproses file yang mengandung kata kunci tertentu** | Setelah `result.Text` didapatkan, periksa `result.Text.Contains("Invoice")` sebelum menulis file. |

Penyesuaian ini memungkinkan Anda mengadaptasi pipeline **convert images to text** ke hampir semua skenario yang mungkin Anda temui.

## Kode Sumber Lengkap (Siap Salin‑Tempel)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Simpan sebagai `Program.cs`, jalankan `dotnet run`, dan saksikan keajaibannya.

## Kesimpulan

Anda kini memiliki **cara lengkap dan siap produksi untuk mengekstrak teks dari file PNG** menggunakan C#. Tutorial ini mencakup semuanya—dari menyiapkan proyek, menginisialisasi OCR engine yang dipercepat GPU, **loop melalui gambar**, hingga **batch OCR images** dan menyimpan hasilnya sebagai teks biasa.  

Jika Anda penasaran dengan langkah selanjutnya, coba:

- **Convert images to text** untuk format lain (JPG, BMP)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}