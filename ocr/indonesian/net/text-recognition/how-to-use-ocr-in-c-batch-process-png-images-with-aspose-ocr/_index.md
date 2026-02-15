---
category: general
date: 2026-02-14
description: Cara menggunakan OCR di C# untuk mengekstrak teks dari file PNG dengan
  cepat. Pelajari OCR batch gambar, proses banyak gambar, dan gunakan Aspose OCR C#
  dalam satu panduan.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: id
og_description: Cara menggunakan OCR di C# dengan Aspose OCR C#. Tutorial ini menunjukkan
  cara mengekstrak teks dari file PNG, melakukan OCR batch pada gambar, dan memproses
  banyak gambar secara efisien.
og_title: Cara Menggunakan OCR di C# – Ekstraksi Teks PNG secara Batch
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cara Menggunakan OCR di C# – Memproses Batch Gambar PNG dengan Aspose OCR
url: /id/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

pressure. → translate.

- **Language support:** By default the engine assumes English. Set `engine.Language = Language.French;` (or any supported language) to improve accuracy on non‑English text. → translate.

- **Error handling:** The `try/catch` inside the parallel loop ensures that a corrupt file doesn’t abort the entire batch. You can also log failures to a file for later review. → translate.

- **Result storage:** Instead of printing, you might write `result.Text` to a `.txt` file using `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`. → translate.

Next "## Conclusion" translate.

Paragraphs translate.

Finally shortcodes closing and backtop button.

Make sure to keep markdown formatting.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Memproses Batch Gambar PNG dengan Aspose OCR

Pernah bertanya-tanya **cara menggunakan OCR** untuk mengambil teks dari sekumpulan file PNG tanpa menulis rutinitas terpisah untuk masing‑masing? Anda tidak sendirian. Banyak pengembang mengalami kesulitan ketika mereka harus **mengekstrak teks PNG** secara massal, terutama ketika gambar berada dalam sebuah folder dan Anda harus menyalakan mesin OCR untuk setiap file.  

Dalam panduan ini kami akan menelusuri solusi lengkap yang siap‑jalan yang **batch OCR gambar**, **memproses banyak gambar** secara paralel, dan memanfaatkan pustaka **Aspose OCR C#** yang kuat. Pada akhir Anda akan memiliki satu executable yang membaca sejumlah PNG, mengekstrak teksnya, dan mencetak hasilnya ke konsol—semua dengan hanya beberapa baris kode.

## Prerequisites

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)  
- Lisensi Aspose.OCR untuk .NET yang valid (atau trial gratis) – Anda dapat mendapatkannya dari situs web Aspose.  
- Sebuah folder yang berisi file PNG yang ingin Anda baca.  
- Visual Studio 2022 (atau IDE apa pun yang kompatibel dengan C#).  

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.OCR`.

## Step 1: How to Use OCR – Initialize the Aspose OCR Engine

Hal pertama yang Anda butuhkan adalah sebuah instance dari kelas `Engine`. Objek ini mengabstraksi teknologi OCR di bawahnya dan dapat berjalan di CPU atau GPU, tergantung pada perangkat keras dan lisensi Anda.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Why this matters:* Menginisialisasi mesin sekali dan menggunakannya kembali di seluruh thread menghemat memori dan menghindari beban berulang memuat model OCR. Ini juga menjamin pengaturan yang konsisten untuk semua gambar.

## Step 2: Extract Text PNG – Gather the Image Paths

Selanjutnya, kita memerlukan kumpulan jalur file. Dalam proyek nyata Anda mungkin membaca direktori secara dinamis, tetapi demi kejelasan kami akan mencantumkan beberapa file contoh.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Tip:* Ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif ke gambar Anda. Jika Anda memiliki puluhan file, Anda dapat mengganti daftar manual dengan `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Step 3: Batch OCR Images – Run Recognition in Parallel

Memproses gambar satu per satu itu sederhana tetapi lambat. Dengan menggunakan `Parallel.ForEach` kita dapat **memproses banyak gambar** secara bersamaan, memanfaatkan CPU multi‑core.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Why parallel?* Setiap panggilan OCR memakan CPU secara intensif tetapi independen, sehingga menjalankannya secara bersamaan dapat memangkas total waktu eksekusi secara dramatis, terutama pada mesin dengan 4‑core atau lebih.

## Step 4: Process Multiple Images – Display the Extracted Text

Sekarang kita memiliki kumpulan objek `OcrResult`, kita dapat mengiterasi mereka dan mencetak teks yang dikenali. Di sinilah biasanya Anda menyimpan output ke basis data atau menulis ke file, tetapi output ke konsol membuat contoh ini tetap singkat.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Output konsol yang diharapkan (contoh):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Jika ada gambar yang gagal dimuat, Aspose akan melemparkan pengecualian; Anda dapat membungkus panggilan `engine.Recognize` dalam blok try/catch untuk mencatat kesalahan tanpa menghentikan seluruh batch.

## Step 5: Full Working Example – All Pieces Together

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol C# baru. Ini mencakup semua mulai dari pernyataan `using` hingga loop output akhir.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Running the Sample

1. Buat proyek **Console App** baru di Visual Studio.  
2. Tambahkan paket NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`).  
3. Ganti `YOUR_DIRECTORY` dengan jalur yang berisi file PNG Anda.  
4. Build dan jalankan – Anda akan melihat teks yang diekstrak tercetak di konsol.

## Pro Tips & Edge Cases

- **GPU acceleration:** Jika Anda memiliki GPU yang kompatibel dan lisensi Aspose OCR, aktifkan melalui `EngineSettings` sebelum membuat engine. Ini dapat mengurangi beberapa detik per gambar.  
- **Large files:** Untuk gambar yang lebih besar dari 10 MB, pertimbangkan untuk menurunkan skala terlebih dahulu guna mengurangi tekanan memori.  
- **Language support:** Secara default engine mengasumsikan bahasa Inggris. Set `engine.Language = Language.French;` (atau bahasa lain yang didukung) untuk meningkatkan akurasi pada teks non‑Inggris.  
- **Error handling:** `try/catch` di dalam loop paralel memastikan bahwa file yang rusak tidak menghentikan seluruh batch. Anda juga dapat mencatat kegagalan ke file untuk ditinjau nanti.  
- **Result storage:** Alih-alih mencetak, Anda dapat menulis `result.Text` ke file `.txt` menggunakan `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Conclusion

Anda kini tahu **cara menggunakan OCR** di C# untuk **mengekstrak teks PNG**, **batch OCR gambar**, dan **memproses banyak gambar** secara efisien dengan Aspose OCR C#. Solusinya sepenuhnya mandiri, berjalan paralel, dan dapat diperluas untuk menangani ratusan atau ribuan file dengan perubahan minimal.

Siap untuk langkah selanjutnya? Coba ganti output konsol dengan laporan CSV, bereksperimen dengan akselerasi GPU, atau alirkan teks OCR ke indeks pencarian. Kemungkinannya tak terbatas, dan pola inti—inisialisasi sekali, jalankan paralel, tangani error dengan elegan—akan melayani Anda dengan baik dalam pipeline pemrosesan gambar apa pun.

Happy coding, and may your OCR jobs be fast and error‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}