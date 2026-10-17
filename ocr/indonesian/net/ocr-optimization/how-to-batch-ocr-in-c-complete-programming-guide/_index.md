---
category: general
date: 2026-03-13
description: Cara melakukan OCR batch dengan cepat dan andal sambil belajar cara mengekstrak
  teks dari file TIFF menggunakan Aspose.OCR. Ikuti tutorial langkah demi langkah
  ini.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: id
og_description: Pelajari cara melakukan OCR batch di C# dan mengekstrak teks dari
  file TIFF dengan Aspose.OCR. Panduan ini mencakup pengaturan, kode, dan tips praktik
  terbaik.
og_title: Cara melakukan batch OCR di C# – Panduan Pemrograman Lengkap
tags:
- OCR
- C#
- Aspose
- Batch processing
title: Cara melakukan OCR batch di C# – Panduan Pemrograman Lengkap
url: /id/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan batch OCR di C# – Panduan Pemrograman Lengkap

Pernah bertanya‑tanya **bagaimana cara batch OCR** tumpukan faktur yang dipindai tanpa menulis skrip terpisah untuk setiap file? Anda tidak sendirian. Dalam banyak proyek dunia nyata, masalahnya bukan akurasi OCR itu sendiri, melainkan volume gambar—seringkali TIFF—yang harus diubah menjadi teks yang dapat dicari.  

Tutorial ini menunjukkan **bagaimana cara batch OCR** menggunakan `BatchProcessor` dari Aspose.OCR sekaligus mengajari Anda **cara mengekstrak teks dari tiff** dalam satu proses yang bersih. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang memproses seluruh folder, memanfaatkan akselerasi GPU opsional, dan menaruh hasil teks biasa di mana pun Anda membutuhkannya.

## Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework 4.7.2 jika Anda lebih suka runtime klasik)  
- **Aspose.OCR for .NET** – Anda dapat mengunduh paket NuGet dengan `dotnet add package Aspose.OCR`.  
- Sebuah folder berisi gambar **TIFF** yang ingin Anda baca (tutorial ini menggunakan `Invoices` sebagai contoh).  
- Opsional: GPU yang mendukung DirectX 11 atau CUDA jika Anda ingin mempercepat proses.  

Tidak ada layanan tambahan, tidak ada kunci cloud—hanya proyek C# lokal dan pustaka Aspose.

## Langkah 1: Siapkan Proyek dan Instal Aspose.OCR

Pertama, buat aplikasi konsol.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan Windows dan berencana memakai akselerasi GPU, pastikan driver grafis terbaru telah terpasang. Jika tidak, flag `UseGpu = true` akan otomatis beralih ke CPU.

## Langkah 2: Buat Konfigurasi BatchProcessor

Sekarang kita akan mengonfigurasi `BatchProcessor`. Inilah inti **bagaimana cara batch OCR**—Anda memberi tahu Aspose bahasa yang diharapkan, filter pra‑pemrosesan yang akan diterapkan, dan apakah akan menggunakan GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**Mengapa pengaturan ini?**  
- `Language = Language.English` memberi tahu mesin untuk menggunakan model bahasa Inggris, yang jauh lebih akurat dibandingkan model generik.  
- `UseGpu` dapat memotong waktu pemrosesan hingga setengahnya pada GPU yang layak, tetapi aman untuk membiarkannya `false` jika Anda menggunakan laptop tanpa GPU.  
- Pipeline filter meniru apa yang dilakukan manusia: meluruskan halaman dan membersihkan bintik‑bintik sebelum memberi ke mesin OCR.

## Langkah 3: Arahkan Processor ke Folder TIFF Anda

Bagian selanjutnya dari **bagaimana cara batch OCR** adalah memberi tahu pustaka di mana file sumber berada. Wildcard didukung, sehingga Anda dapat mengambil semua file `.tif` sekaligus.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Kasus tepi:** Jika gambar Anda memiliki ekstensi campuran (`.tiff`, `.tif`, `.png`), panggil `AddFolder` beberapa kali atau gunakan `*.*` dan filter nanti di dalam kode.

## Langkah 4: Pilih Lokasi Hasil OCR

Anda mungkin bertanya, “Ke mana teks yang diekstrak disimpan?” Itulah pilar ketiga **bagaimana cara batch OCR**—menentukan lokasi dan format output. Kami akan menyimpan file teks biasa berdampingan dengan file asli.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

Jika Anda memerlukan JSON atau XML alih‑alih teks biasa, cukup ganti `OutputFormat.PlainText` dengan `OutputFormat.Json` atau `OutputFormat.Xml`. Pustaka akan menangani konversinya untuk Anda.

## Langkah 5: Jalankan Pekerjaan Batch dan Laporkan Hasil

Akhirnya, jalankan pekerjaan tersebut. Metode `Execute` akan memblokir hingga semua file selesai diproses, kemudian Anda dapat memeriksa `ProcessedCount` untuk memastikan keberhasilan.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### Output yang Diharapkan

Saat Anda menjalankan program, konsol akan menampilkan sesuatu seperti berikut:

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

Di folder `Output` Anda akan menemukan satu file `.txt` per TIFF sumber, masing‑masing bernama sesuai gambar asli (misalnya, `Invoice_001.txt`). Buka file apa saja dan Anda akan melihat teks OCR mentah—sempurna untuk dimasukkan ke indeks pencarian atau pipeline ekstraksi data selanjutnya.

## Menangani Masalah Umum

### 1. GPU Tidak Tersedia

Jika `UseGpu = true` tetapi tidak ada perangkat yang kompatibel, Aspose akan beralih ke CPU secara diam‑diam. Untuk menanganinya secara eksplisit, Anda dapat menangkap `DeviceNotFoundException`:

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. File Non‑TIFF di Folder yang Sama

Ketika Anda memiliki folder campuran, filter secara programatik:

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. File Besar Melebihi Memori

Untuk TIFF multi‑halaman yang sangat besar, aktifkan streaming:

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## Pro Tips untuk Akurasi Lebih Baik Saat Anda **mengekstrak teks dari tiff**

- **Resolusi penting** – Targetkan 300 dpi atau lebih tinggi. Di bawah itu mesin OCR mungkin melewatkan karakter.  
- **Warna vs. Grayscale** – Konversi pemindaian berwarna ke grayscale sebelum OCR; `DeskewFilter` sudah melakukannya di belakang layar, tetapi Anda dapat menambahkan `ColorDepthReductionFilter` untuk kecepatan ekstra.  
- **Pasca‑pemrosesan** – Setelah Anda memiliki teks biasa, jalankan pemeriksaan ejaan atau pembersihan regex untuk memperbaiki keanehan OCR umum (misalnya, “0” vs “O”).

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut seluruh program yang dapat Anda kompilasi dan jalankan. Cukup ganti path placeholder dengan direktori Anda sendiri.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

Kompilasi dan jalankan:

```bash
dotnet run
```

Sekarang Anda seharusnya memiliki sekumpulan file `.txt` yang rapi—setiap file merupakan hasil **mengekstrak teks dari tiff** melalui proses batch yang sepenuhnya otomatis.

## Kesimpulan

Kami telah membahas **bagaimana cara batch OCR** di C# dari awal hingga akhir, mencakup semua yang Anda perlukan untuk **mengekstrak teks dari tiff** secara efisien. Poin penting yang dapat diambil:

1. Gunakan `BatchProcessor` Aspose.OCR untuk menghindari penulisan loop berulang.  
2. Manfaatkan filter pra‑pemrosesan (deskew, despeckle) untuk akurasi lebih tinggi.  
3. Aktifkan akselerasi GPU bila memungkinkan, tetapi selalu siapkan fallback ke CPU.  
4. Simpan hasil di struktur folder yang dapat diprediksi sehingga pekerjaan downstream dapat mengambilnya secara otomatis.

Selanjutnya Anda dapat mengeksplorasi:

- Mengirim teks biasa ke **indeks pencarian** (misalnya, Elasticsearch) agar faktur dapat dicari.  
- Mengonversi output ke **JSON** dan mengirimkannya ke model machine‑learning yang mengekstrak item baris.  
- Menambahkan **penanganan error** untuk TIFF yang korup atau masalah izin.

Coba dulu,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}