---
category: general
date: 2026-05-31
description: Cara melakukan OCR batch di C# dengan Aspose OCR. Pelajari cara mengonversi
  gambar menjadi teks, mengekstrak teks dari gambar, dan memproses banyak file secara
  efisien.
draft: false
keywords:
- how to batch OCR
- convert images to text
- extract text from images
- OCR multiple files
- batch OCR processing
language: id
og_description: Cara melakukan OCR batch di C# menggunakan Aspose OCR. Mengonversi
  gambar menjadi teks, mengekstrak teks dari gambar, dan menangani OCR pada banyak
  file dengan mudah.
og_title: Cara Batch OCR di C# – Panduan Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  headline: How to Batch OCR in C# – Complete Programming Guide
  type: TechArticle
- description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  name: How to Batch OCR in C# – Complete Programming Guide
  steps:
  - name: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
    text: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
  - name: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
    text: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
  - name: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
    text: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- batch-processing
title: Cara Melakukan Batch OCR di C# – Panduan Pemrograman Lengkap
url: /id/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di C# – Panduan Pemrograman Lengkap

Pernah bertanya‑tanya **bagaimana cara batch OCR** seluruh folder foto yang dipindai tanpa membuka tiap file secara manual? Anda tidak sendirian. Dalam banyak proyek dunia nyata—misalnya otomatisasi faktur atau pengarsipan foto bersejarah—Anda perlu **mengonversi gambar ke teks** secara massal, dan melakukannya satu‑per‑satu merupakan pemborosan waktu yang besar.

Dalam tutorial ini kami akan membahas sebuah aplikasi konsol C# yang siap dijalankan, yang mengambil setiap PNG, JPG, atau TIFF dalam direktori sumber, menjalankan Aspose OCR pada masing‑masing, dan menaruh file *.txt* yang cocok ke dalam folder output. Pada akhir tutorial Anda akan nyaman **mengekstrak teks dari gambar**, menangani **OCR banyak file**, dan memiliki dasar yang kuat untuk **pemrosesan batch OCR** apa pun yang mungkin Anda perlukan nanti.

## Apa yang Akan Anda Pelajari

- Menyiapkan proyek .NET dengan paket NuGet Aspose OCR.  
- Menentukan folder sumber dan tujuan untuk **batch OCR**.  
- Mengenumerasi tipe gambar yang didukung dan memberi mereka ke mesin OCR.  
- Menulis teks yang dikenali ke file *.txt* terpisah, secara efektif **mengonversi gambar ke teks**.  
- Menangani jebakan umum seperti folder yang hilang, format tidak didukung, dan penyesuaian kinerja.

Tidak diperlukan pengalaman sebelumnya dengan Aspose; cukup pemahaman dasar tentang C# dan Visual Studio sudah cukup.

---

![Diagram showing the flow of batch OCR processing from image folder to text output – how to batch OCR](/images/batch-ocr-flow.png){alt="diagram alur batch OCR"}

## Cara Batch OCR – Menyiapkan Proyek

Sebelum kita masuk ke kode, pastikan Anda memiliki:

1. **.NET 6 SDK** (atau yang lebih baru) terpasang – runtime terbaru memberi Anda kinerja lebih baik dan dukungan native untuk async I/O.  
2. **Visual Studio 2022** (Community Edition sudah cukup) atau editor apa pun yang Anda suka.  
3. Paket **Aspose.OCR** NuGet. Instal melalui Package Manager Console:

   ```powershell
   Install-Package Aspose.OCR
   ```

Itu saja. Sisa tutorial mengasumsikan paket sudah direferensikan dengan benar.

## Langkah 2: Siapkan Folder Sumber dan Tujuan (convert images to text)

Pertama, kita membutuhkan dua folder: satu yang menyimpan gambar mentah dan satu lagi tempat file *.txt* yang dihasilkan akan disimpan. Kode di bawah ini membuat folder tujuan jika belum ada—tidak perlu langkah manual.

```csharp
// Define where the images live and where the text files will go
string sourceFolder = @"C:\OCR\Batch";
string outputFolder = @"C:\OCR\BatchTxt";

// Ensure the output directory exists; CreateDirectory is idempotent
Directory.CreateDirectory(outputFolder);
```

> **Mengapa ini penting:** Jika Anda melewatkan pemanggilan `CreateDirectory`, program akan melempar `DirectoryNotFoundException` saat mencoba menulis file teks pertama. Dengan menanganinya di awal, proses batch OCR menjadi lebih tahan banting.

## Langkah 3: Enumerasi File Gambar untuk OCR Multiple Files

Selanjutnya, kita mengumpulkan setiap file yang cocok dengan format yang kami dukung. Menggunakan LINQ membuat kode singkat namun tetap mudah dibaca.

```csharp
// Grab all PNG, JPG, and TIFF files from the source folder (non‑recursive)
var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
    .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));
```

> **Tip:** Jika nanti Anda perlu menangani PDF atau BMP, cukup tambahkan ke klausa `Where`. Menjaga filter di satu tempat membuat penyesuaian di masa depan menjadi mudah.

## Langkah 4: Jalankan Mesin OCR pada Setiap Gambar (how to batch OCR)

Sekarang inti masalah: memberi setiap gambar ke Aspose OCR dan mengambil teks yang dikenali. Loop di bawah ini membuat instance `OcrEngine` baru untuk setiap file—ini menjamin memori dari gambar sebelumnya dibebaskan sebelum gambar berikutnya diproses.

```csharp
foreach (var imagePath in imageFiles)
{
    // Initialize the OCR engine with the current image
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = ImageStream.FromFile(imagePath)
    };

    // Perform recognition; Recognize() returns an OcrResult object
    OcrResult ocrResult = ocrEngine.Recognize();

    // Build the output .txt file path (same base name, .txt extension)
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    // Persist the extracted text
    File.WriteAllText(textFilePath, ocrResult.Text);

    Console.WriteLine($"Processed {Path.GetFileName(imagePath)} → {Path.GetFileName(textFilePath)}");
}
```

**Apa yang terjadi?**  

- `ImageStream.FromFile` memuat gambar ke dalam stream yang dapat dibaca Aspose.  
- `ocrEngine.Recognize()` menjalankan algoritma OCR sebenarnya, mengembalikan string di `ocrResult.Text`.  
- `File.WriteAllText` menulis string tersebut ke disk, secara efektif **mengekstrak teks dari gambar**.

### Menangani Kasus Tepi

- **Gambar rusak** – bungkus pemanggilan pengenalan dalam `try/catch` dan catat kegagalan, lalu lanjutkan ke file berikutnya.  
- **Batch besar** – pertimbangkan memproses file secara asynchronous dengan `Parallel.ForEach` jika Anda memiliki mesin multi‑core.  
- **Bahasa berbeda** – setel `ocrEngine.Language = Language.English;` atau bahasa lain yang didukung sebelum memanggil `Recognize()`.

## Langkah 5: Simpan Teks yang Diekstrak (extract text from images)

Potongan kode sebelumnya sudah menyimpan output OCR, tetapi mari kita pisahkan logika itu ke dalam metode bantu. Ini membuat loop utama lebih bersih dan mendorong penggunaan kembali.

```csharp
static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
{
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    File.WriteAllText(textFilePath, recognizedText);
}
```

Anda kemudian dapat mengganti pemanggilan inline `File.WriteAllText` dengan:

```csharp
SaveOcrResult(outputFolder, imagePath, ocrResult.Text);
```

> **Mengapa dipisahkan ke metode?** Ini memisahkan kepedulian—pengenalan vs. penyimpanan—dan memberi Anda satu tempat untuk menambahkan pasca‑pemrosesan (seperti memotong spasi atau menambahkan timestamp).

## Contoh Lengkap yang Berfungsi – Pemrosesan Batch OCR di C#

Menggabungkan semua bagian, berikut program mandiri yang dapat Anda salin‑tempel ke proyek Console App baru dan jalankan langsung.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Define source & destination folders
            string sourceFolder = @"C:\OCR\Batch";
            string outputFolder = @"C:\OCR\BatchTxt";

            // 2️⃣ Make sure the output folder exists
            Directory.CreateDirectory(outputFolder);

            // 3️⃣ Get all supported image files (convert images to text)
            var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
                .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));

            // 4️⃣ Process each image (how to batch OCR)
            foreach (var imagePath in imageFiles)
            {
                try
                {
                    // Initialise OCR engine for the current file
                    OcrEngine ocrEngine = new OcrEngine
                    {
                        Image = ImageStream.FromFile(imagePath)
                    };

                    // Run OCR – this extracts text from images
                    OcrResult result = ocrEngine.Recognize();

                    // 5️⃣ Save the result (extract text from images)
                    SaveOcrResult(outputFolder, imagePath, result.Text);

                    Console.WriteLine($"✅ {Path.GetFileName(imagePath)} processed.");
                }
                catch (Exception ex)
                {
                    // Gracefully handle problematic files
                    Console.WriteLine($"⚠️ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }

            Console.WriteLine("🎉 Batch OCR processing complete!");
        }

        // Helper to write the OCR output to a .txt file
        static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
        {
            string textFilePath = Path.Combine(outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, recognizedText);
        }
    }
}
```

### Output yang Diharapkan

Saat Anda menjalankan program, konsol akan menampilkan baris‑baris serupa dengan:

```
✅ invoice001.png processed.
✅ receipt123.jpg processed.
✅ map.tif processed.
🎉 Batch OCR processing complete!
```

Sementara itu, folder `C:\OCR\BatchTxt` akan berisi:

- `invoice001.txt`
- `receipt123.txt`
- `map.txt`

Setiap file berisi representasi teks polos dari gambar sumbernya, siap untuk diindeks, dicari, atau dianalisis lebih lanjut.

## Pro Tips & Common Pitfalls (batch OCR processing)

- **Manajemen memori:** Aspose OCR melepaskan buffer gambar setelah setiap pemanggilan `Recognize()`, tetapi jika Anda memproses ribuan file, pertimbangkan memanggil `GC.Collect()` secara hemat untuk menjaga jejak memori tetap rendah.  
- **Peningkatan kecepatan:** Gunakan `OcrEngine.RecognizeAsync()` di .NET 6+ dan jalankan beberapa tugas dengan `Task

## Apa yang Harus Anda Pelajari Selanjutnya?

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Perform OCR on Archive Images with Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}