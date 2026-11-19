---
category: general
date: 2026-05-02
description: Tutorial c# OCR yang menunjukkan cara mengekstrak teks dari gambar c#,
  mengenali teks PNG, lalu menulis JSON terindentasi menggunakan JsonSerializer c#.
  Panduan langkah demi langkah untuk pengembang.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: id
og_description: tutorial c# ocr yang menunjukkan cara mengekstrak teks dari gambar
  c# dan mengenali teks png, kemudian menulis json terindentasi dengan JsonSerializer
  c#. contoh lengkap yang dapat dijalankan.
og_title: Tutorial OCR C# – Ekstrak Teks dan Ekspor sebagai JSON Terindentasi
tags:
- OCR
- C#
- Aspose
- JSON
title: c# OCR tutorial – Ekstrak Teks dari Gambar dan Ekspor sebagai JSON Berindentasi
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# ocr – Ekstrak Teks dari Gambar dan Ekspor sebagai JSON Berindentasi

Pernah membutuhkan **c# ocr tutorial** yang mengubah gambar teks langsung menjadi file JSON yang rapi? Anda tidak sendirian. Dalam banyak proyek – misalnya pemindaian faktur, parsing struk, atau bahkan ekstraksi teks meme sederhana – Anda berakhir dengan file PNG dan bertanya-tanya bagaimana cara mengambil kata‑kata tersebut tanpa menulis pengenalan khusus.  

Panduan ini memberi Anda solusi praktis: kami akan **extract text image c#** menggunakan Aspose.OCR, **recognize png text**, dan kemudian **write indented json** dengan `JsonSerializer` di C#. Pada akhir tutorial Anda akan memiliki aplikasi konsol mandiri yang dapat Anda masukkan ke dalam solusi .NET apa pun. Tanpa tautan “lihat dokumentasi” yang samar, hanya contoh lengkap yang siap salin‑tempel.

## Apa yang Anda Butuhkan

- **.NET 6** (atau versi .NET terbaru). Kerangka kerja yang lebih lama juga dapat bekerja, tetapi sintaks yang ditunjukkan menargetkan .NET 6+.
- **Aspose.OCR for .NET** – instal melalui NuGet: `dotnet add package Aspose.OCR`.
- Contoh gambar PNG (`text.png`) yang berisi teks jelas dan dapat dibaca mesin.
- IDE atau editor pilihan Anda – Visual Studio, VS Code, Rider, dll.

> **Pro tip:** Jika Anda berencana memproses banyak gambar, pertimbangkan untuk menggunakan satu instance `OcrEngine` secara berulang alih‑alih membuat yang baru untuk setiap file. Ini mengurangi beban dan meningkatkan throughput.

## Langkah 1: Siapkan Proyek tutorial c# ocr

Pertama, buat proyek konsol. Perintah berikut membuat kerangka kerja dan menambahkan pustaka OCR:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Sekarang buka `Program.cs` yang dihasilkan. Kami akan mengganti isinya dengan contoh lengkap nanti, tetapi untuk saat ini pastikan proyek dapat dibangun:

```bash
dotnet build
```

Jika tidak ada error, Anda siap melanjutkan.

## Langkah 2: Kenali Teks PNG dari Gambar

Inti dari setiap **c# ocr tutorial** adalah mesin OCR itu sendiri. Aspose.OCR menyembunyikan detail tingkat rendah dan memberi Anda kelas `OcrEngine` yang bersih. Di bawah ini kami membuat engine, menunjuk ke file PNG, dan meminta ia mengenali teks.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Mengapa Ini Berfungsi

- **`RecognizeImage`** menerima banyak format (PNG, JPEG, BMP). Kami secara khusus **recognize png text** karena PNG mempertahankan detail lossless, yang ideal untuk OCR.
- `OcrResult` yang dikembalikan berisi tidak hanya teks biasa tetapi juga skor kepercayaan per‑glyph, berguna bila Anda perlu menyaring karakter dengan kepercayaan rendah nanti.

## Langkah 3: Tulis JSON Berindentasi dengan JsonSerializer c#

Setelah kita memiliki `ocrResult`, langkah logis berikutnya dalam **c# ocr tutorial** kami adalah mengubah objek tersebut menjadi JSON yang dapat dibaca manusia. Serializer bawaan `System.Text.Json` melakukan pekerjaan ini, dan kami akan mengonfigurasinya untuk **write indented json** demi kejelasan.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### Menggunakan `JsonSerializer` dengan Benar

- Flag `WriteIndented` adalah cara termudah untuk **write indented json** tanpa harus menambahkan pustaka pihak ketiga.
- Jika Anda pernah membutuhkan nama properti bergaya camel‑case, tambahkan `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` ke opsi.
- String `jsonOutput` dapat disimpan dengan `File.WriteAllText("result.json", jsonOutput);` – penyesuaian praktis untuk alur kerja dunia nyata.

## Langkah 4: Jalankan dan Verifikasi Output

Kompilasi dan jalankan program:

```bash
dotnet run
```

Dengan asumsi `text.png` berisi frasa *“Hello, OCR World!”*, Anda akan melihat sesuatu seperti:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

JSON tersebut **berindentasi**, sehingga mudah dibaca di log atau diteruskan ke layanan downstream.

### Kasus Pinggir & Tips

| Situasi | Apa yang Dilakukan |
|-----------|------------|
| **Gambar blur** | Tingkatkan `ocrEngine.Config.Dpi` (misalnya, `ocrEngine.Config.Dpi = 300`) sebelum memanggil `RecognizeImage`. |
| **Bahasa non‑Inggris** | Setel `ocrEngine.Config.Language = OcrLanguage.German` (atau bahasa lain yang didukung). |
| **Banyak file sekaligus** | Loop melalui direktori, gunakan kembali instance `OcrEngine` yang sama; simpan setiap hasil JSON dengan nama file unik. |
| **Hanya butuh teks berkepercayaan tinggi** | Filter `ocrResult.Lines` dimana `Confidence` ≥ 0.95 sebelum serialisasi. |

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah *seluruh* program, siap ditempatkan di `Program.cs`. Ia mencakup semua langkah, penanganan error, dan komentar yang membuat kode mudah dipahami.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Jalankan kode, periksa konsol atau file `.json` yang dihasilkan, dan Anda akan melihat teks yang diekstrak beserta skor kepercayaan, semuanya rapi **berindentasi**.

## Kesimpulan

Anda kini memiliki **c# ocr tutorial** yang solid yang menunjukkan cara **extract text image c#**, **recognize png text**, dan **write indented json** menggunakan `JsonSerializer`. Contoh ini lengkap, dapat dijalankan, dan mencakup tips praktis untuk skenario dunia nyata.  

Langkah selanjutnya? Coba ganti Aspose.OCR dengan engine lain (misalnya, Tesseract) dan lihat bagaimana bentuk `OcrResult` berubah, atau kirim JSON ke API downstream yang menyimpan data OCR ke basis data. Anda juga dapat bereksperimen dengan opsi **use jsonserializer c#** seperti konverter khusus untuk format tanggal atau penanganan enum.

Selamat coding, semoga pipeline OCR Anda selalu akurat!  

---  

![c# ocr tutorial diagram](image.png "Diagram illustrating OCR flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}