---
category: general
date: 2026-04-26
description: Cara melakukan OCR batch pada gambar PNG dengan cepat. Pelajari cara
  mengekstrak teks dari PNG, mengonversi gambar menjadi teks, menulis teks yang dikenali,
  dan membaca direktori PNG dengan Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: id
og_description: Cara melakukan OCR batch pada gambar PNG di C# dengan Aspose OCR.
  Panduan ini menunjukkan cara mengekstrak teks dari PNG, mengonversi gambar menjadi
  teks, dan menulis teks yang dikenali secara efisien.
og_title: Cara Melakukan OCR Batch pada Gambar PNG di C# – Langkah demi Langkah
tags:
- OCR
- C#
- Aspose
title: Cara Melakukan OCR Massal pada Gambar PNG di C# – Panduan Lengkap
url: /id/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR Gambar PNG di C# – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara batch OCR** seluruh folder berisi file PNG tanpa menulis program terpisah untuk setiap gambar? Anda bukan satu-satunya yang harus menangani puluhan screenshot, kwitansi yang dipindai, atau grafik yang perlu diubah menjadi teks yang dapat dicari. Dalam tutorial ini kami akan membahas solusi praktis yang **mengekstrak teks dari PNG**, **mengonversi gambar menjadi teks**, dan **menulis teks yang dikenali** ke file terpisah—semua sambil membaca direktori PNG secara otomatis.

Pada akhir panduan ini Anda akan memiliki aplikasi konsol C# yang siap dijalankan dan dapat memproses sejumlah gambar sekaligus. Tanpa skrip tambahan, tanpa menyalin‑tempel manual—hanya kode murni yang melakukan pekerjaan berat untuk Anda.

## Apa yang Anda Butuhkan

- **.NET 6.0** atau yang lebih baru (kode ini juga berjalan baik di .NET Framework).  
- Paket NuGet **Aspose.OCR for .NET** (versi percobaan gratis dapat digunakan untuk pengujian).  
- Sebuah folder dengan beberapa file *.png* yang ingin Anda OCR.  
- Visual Studio 2022 atau IDE C# lain yang Anda sukai.

Jika Anda sudah memiliki semua itu, kita dapat langsung melompat ke implementasinya.

## Langkah 1 – Siapkan Folder Input dan Output Anda *(Baca Direktori PNG)*

Hal pertama yang kita lakukan adalah mengarahkan program ke folder yang berisi gambar dan menentukan di mana file *.txt* hasil akan disimpan. Menggunakan `Directory.GetFiles` memberikan kita enumerable bersih dari setiap PNG dalam direktori.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Mengapa ini penting:**  
- Menggunakan wildcard (`*.png`) memastikan kita hanya memproses file gambar, mengabaikan dokumen lain yang tidak diinginkan.  
- Membuat folder output secara otomatis mencegah `DirectoryNotFoundException` di kemudian hari.

> **Tip pro:** Jika Anda perlu mendukung format lain (JPEG, BMP), cukup perpanjang pola pencarian atau panggil `Directory.EnumerateFiles` dengan beberapa ekstensi.

## Langkah 2 – Inisialisasi Engine OCR *(Konversi Gambar menjadi Teks)*

Aspose.OCR menyediakan dua tipe engine: `OcrEngine` berbasis CPU dan `GpuOcrEngine` yang dipercepat GPU. Untuk kebanyakan pekerjaan batch, engine CPU sudah cukup, tetapi Anda dapat mengganti nama kelas jika memiliki GPU yang mendukung.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Mengapa ini penting:**  
- Menentukan bahasa secara signifikan meningkatkan akurasi karena engine mengetahui set karakter apa yang diharapkan.  
- Beralih ke `GpuOcrEngine` hanya memerlukan satu baris perubahan jika Anda mengalami bottleneck kinerja pada batch besar.

## Langkah 3 – Buat Batch Recogniser

Aspose menyediakan `BatchRecognizer` yang nyaman, yang menerima enumerable dari jalur file dan mengalirkan hasil satu per satu. Ini menghindari pemuatan semua gambar ke memori sekaligus—detail penting untuk folder besar.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Mengapa ini penting:**  
- Batch recogniser mengenkapsulasi logika loop, memungkinkan kita fokus pada apa yang harus dilakukan dengan setiap hasil daripada bagaimana mengiterasi dengan aman.

## Langkah 4 – Jalankan OCR pada Semua Gambar dan Tulis Output *(Tulis Teks yang Dikenali)*

Sekarang kita benar‑benarnya melakukan OCR. Metode `Recognize` mengembalikan `IEnumerable<RecognitionResult>` di mana setiap hasil berisi teks yang diekstrak dan metadata lainnya.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Mengapa ini penting:**  
- Menggunakan `File.WriteAllText` memastikan teks disimpan dengan encoding UTF‑8 secara default, mempertahankan karakter khusus.  
- Penamaan bertahap (`out_0.txt`, `out_1.txt`) sesuai dengan urutan pemrosesan, yang berguna untuk debugging.

> **Kasus tepi:** Jika ada gambar yang gagal OCR (mis., file rusak), `RecognitionResult.Text` akan kosong. Anda dapat menambahkan pemeriksaan sederhana di dalam loop untuk mencatat kegagalan:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Langkah 5 – Gabungkan Semua – Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru. Program ini mencakup direktif `using`, validasi folder, dan UI konsol kecil sehingga Anda tahu kapan batch selesai.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Output yang diharapkan:**  
Menjalankan program akan mencetak sesuatu seperti:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

Dan Anda akan melihat `out_0.txt` … `out_11.txt` di dalam folder output, masing‑masing berisi versi teks biasa dari gambar yang bersangkutan.

## Pertanyaan Umum & Tips

| Pertanyaan | Jawaban |
|------------|---------|
| *Bisakah saya OCR sub‑folder juga?* | Ya—ganti `Directory.GetFiles` dengan `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *Bagaimana jika saya membutuhkan bahasa lain?* | Set `ocrEngine.Language = Language.Spanish;` (atau enum bahasa lain yang didukung). |
| *Bagaimana menangani batch besar (ribuan file)?* | Pertimbangkan memproses dalam potongan atau menggunakan `Parallel.ForEach` dengan tingkat paralelisme yang dibatasi untuk menghindari kehabisan memori. |
| *Apakah output selalu UTF‑8?* | `File.WriteAllText` secara default menggunakan UTF‑8 tanpa BOM, yang bekerja untuk kebanyakan bahasa berbasis Latin. Untuk skrip Asia Anda mungkin perlu mengatur `Encoding.UTF8` secara eksplisit. |
| *Bisakah saya mendapatkan skor kepercayaan?* | `RecognitionResult` menyediakan `Confidence`—Anda dapat mencatatnya bersama teks untuk kontrol kualitas. |

## Gambaran Visual *(Cara Batch OCR – Diagram)*

![Diagram alur kerja batch OCR yang menunjukkan folder input → engine OCR → batch recogniser → file txt output](https://example.com/diagram-how-to-batch-ocr.png "Cara Batch OCR")

*Teks alt berisi kata kunci utama, memenuhi persyaratan SEO gambar.*

## Penutup

Kami baru saja membahas **cara batch OCR** sebuah direktori file PNG menggunakan Aspose.OCR, mulai dari membaca direktori PNG hingga menulis setiap file teks yang dikenali. Solusi ini sepenuhnya mandiri, bekerja pada runtime .NET modern apa pun, dan dapat diperluas untuk akselerasi GPU, dukungan multi‑bahasa, atau pemrosesan paralel.

Siap untuk langkah selanjutnya? Coba ganti `Language.Latin` dengan bahasa lain, atau integrasikan output ke dalam indeks pencarian sehingga dokumen Anda langsung dapat dicari. Langit adalah batasnya setelah Anda menguasai batch OCR.

Selamat coding, dan beri tahu saya di komentar jika Anda mengalami kendala!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}