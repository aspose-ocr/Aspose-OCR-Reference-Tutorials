---
category: general
date: 2026-04-03
description: Pelajari cara melakukan OCR batch dengan Aspose.OCR di C#. Panduan ini
  menunjukkan cara mengekstrak teks dari gambar PNG dan mengonversi gambar menjadi
  teks secara efisien.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: id
og_description: Temukan cara melakukan OCR batch di C# untuk mengekstrak teks dari
  gambar PNG dan mengonversi gambar menjadi teks menggunakan Aspose.OCR. Kode lengkap
  disertakan.
og_title: Cara Memproses OCR Secara Batch di C# – Panduan Cepat
tags:
- OCR
- C#
- Aspose
title: Cara Batch OCR di C# – Cara Cepat Mengekstrak Teks dari File PNG
url: /id/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di C# – Cara Cepat Mengekstrak Teks dari File PNG

Pernah bertanya-tanya **how to batch OCR** seluruh folder screenshot tanpa menulis loop untuk setiap file? Anda bukan satu-satunya. Dalam banyak proyek—misalnya digitalisasi faktur atau pengarsipan kwitansi yang dipindai—Anda berakhir dengan puluhan, bahkan ratusan, file PNG yang perlu teksnya diekstrak. Kabar baik? Dengan Aspose.OCR Anda dapat **extract text PNG** gambar secara paralel, dan seluruh proses dapat diselesaikan hanya dalam beberapa baris C#.

Di tutorial ini kami akan membahas contoh lengkap yang siap‑jalan yang menunjukkan cara **convert images to text** menggunakan batch processor. Kami akan membahas prasyarat, menjelaskan mengapa setiap baris penting, dan bahkan memberikan beberapa pro‑tips agar Anda tidak mengalami jebakan umum nanti.

## Prasyarat

- **.NET 6.0** (atau lebih baru) terpasang di mesin Anda. Runtime yang lebih lama masih dapat bekerja, tetapi yang terbaru memberikan kinerja lebih baik dan dukungan async.
- **Aspose.OCR for .NET** package. Anda dapat mengunduhnya via NuGet: `dotnet add package Aspose.OCR`.
- Sebuah folder penuh gambar **PNG** yang ingin Anda proses. Kami akan menyebutnya `YOUR_DIRECTORY` sepanjang panduan.
- Jumlah RAM yang cukup—batch OCR dapat mengonsumsi memori banyak jika Anda meningkatkan paralelisme, tetapi menggunakan `Environment.ProcessorCount` membuatnya aman.

> **Pro tip:** Jika Anda berada di pipeline CI/CD, tambahkan file lisensi Aspose sebagai secret untuk menghindari batas 20 halaman pada evaluasi gratis.

Sekarang, mari kita mulai.

## Langkah 1: Siapkan Batch OCR Processor (Primary Keyword in Header)

Hal pertama yang Anda butuhkan adalah sebuah instance dari `BatchOcrProcessor`. Kelas ini mengabstraksikan logika threading dan memungkinkan Anda fokus pada apa yang harus dilakukan dengan setiap gambar.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Mengapa ini penting:**  
- `Engine = new OcrEngine()` memberi Anda engine OCR baru untuk setiap thread, menghindari kontensi.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` secara otomatis menyesuaikan dengan jumlah core, memberikan throughput terbaik tanpa penyesuaian manual.

## Langkah 2: Sambungkan ke Event Progress (Helps Track Extraction)

Melihat progres sangat penting saat memproses ratusan file. Event `ProgressChanged` dipicu setelah setiap file selesai, memungkinkan Anda mencatat status.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Mengapa Anda akan menyukainya:**  
- Umpan balik waktu nyata mencegah Anda bertanya-tanya apakah aplikasi terhenti.  
- Jika Anda perlu menjeda atau membatalkan, Anda sudah memiliki hook untuk memeriksa `e.Current` vs `e.Total`.

## Langkah 3: Tentukan Pemindaian Folder dan Pola File (Extract Text PNG)

Sekarang kami memberi tahu processor di mana harus mencari dan jenis file apa yang harus diambil. Pola `"*.png"` memastikan kami hanya menangani gambar PNG.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Mengapa ini penting:**  
- Menggunakan pola glob membuat kode fleksibel; ubah `*.png` menjadi `*.jpg` jika nanti Anda perlu menangani JPEG.  
- Callback menerima path gambar dan teks yang dikenali, memberi Anda kontrol penuh atas apa yang harus dilakukan selanjutnya.

## Langkah 4: Simpan Teks yang Diakui di Samping Sumber (Convert Images to Text)

Di dalam callback kami akan menulis output OCR ke file `.txt` yang berada tepat di samping PNG asli. Ini adalah cara paling sederhana untuk **convert images to text** untuk pemrosesan selanjutnya.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Mengapa kami memilih file `.txt` berdampingan:**  
- Ini menjaga hubungan jelas—buka PNG, buka TXT, bandingkan.  
- Tidak perlu database atau lapisan penyimpanan tambahan dalam proyek skala kecil.

## Langkah 5: Akhiri dengan Pesan Penyelesaian yang Ramah

Pesan konsol yang rapi memberi tahu Anda ketika semuanya selesai.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

Saat Anda menjalankan program, Anda akan melihat output seperti:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Setiap PNG kini memiliki file `.txt` saudara yang berisi teks yang diekstrak.

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabungkan)

Berikut adalah seluruh program yang dapat Anda salin‑tempel ke proyek konsol baru. Tidak ada bagian yang hilang—cukup ganti `YOUR_DIRECTORY` dengan path absolut ke gambar Anda.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Hasil yang Diharapkan

- Untuk setiap `image.png` di `C:\MyImages`, sebuah `image.txt` muncul di sampingnya.
- Konsol mencetak baris progres, memudahkan pemantauan batch besar.
- Tidak ada looping manual atau manajemen thread—`BatchOcrProcessor` menangani semuanya.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika gambar saya bukan PNG?

Cukup ubah argumen kedua di `ProcessFolder` menjadi `"*.jpg"` atau `"*.*"` untuk menyertakan semua file. Engine OCR bekerja dengan sebagian besar format raster.

### Berapa banyak memori yang dikonsumsi?

`BatchOcrProcessor` memuat satu gambar per thread. Dengan `Environment.ProcessorCount` diatur, misalnya, 8 core, Anda akan memiliki delapan gambar di memori sekaligus. Jika Anda mengalami pengecualian OutOfMemory, kurangi paralelisme:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### Bisakah saya menyesuaikan bahasa OCR?

Tentu saja. Setelah membuat engine, atur properti `Language`-nya:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose mendukung banyak bahasa; cukup tambahkan paket NuGet yang sesuai jika diperlukan.

### Bagaimana dengan penanganan error?

Bungkus callback dalam blok try/catch dan catat kegagalan. Processor akan melanjutkan ke file berikutnya, mencegah satu gambar rusak menghentikan seluruh proses.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Pro Tips untuk Skalabilitas

- **Chunk the folder**: Jika Anda memiliki puluhan ribu file, bagi menjadi subfolder dan jalankan beberapa batch job secara berurutan.
- **Use a cloud VM**: Mesin dengan lebih banyak core (misalnya, 32‑core) akan selesai jauh lebih cepat. Ingatlah untuk menyesuaikan batas lisensi.
- **Post‑process the text**: Setelah ekstraksi, Anda mungkin ingin menjalankan regex untuk mengambil nomor faktur atau tanggal. File `.txt` adalah input yang sempurna untuk pipeline semacam itu.

## Kesimpulan

Anda kini memiliki resep yang solid dan siap produksi untuk **how to batch OCR** sebuah direktori PNG, **extract text PNG** file, dan **convert images to text** menggunakan Aspose.OCR di C#. Contoh ini berdiri sendiri, menjelaskan “mengapa” di balik setiap baris, dan menyertakan tips untuk menangani beban kerja yang lebih besar atau tipe file yang berbeda.

Siap untuk langkah selanjutnya? Coba ganti callback untuk mengirim hasil ke database, atau tambahkan pra‑pemrosesan gambar (mis., deskew) sebelum OCR. Pola ini skalabel dengan baik, sehingga Anda dapat menyesuaikannya dengan skenario batch‑processing apa pun yang Anda temui.

Selamat coding, semoga pipeline OCR Anda cepat dan bebas error!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}