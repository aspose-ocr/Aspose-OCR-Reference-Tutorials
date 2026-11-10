---
category: general
date: 2026-01-15
description: Tutorial c# OCR yang menunjukkan cara mengenali teks dari gambar, mengekstrak
  teks dari faktur, dan mengonversi gambar menjadi teks menggunakan Aspose OCR pada
  GPU.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: id
og_description: tutorial c# ocr yang mengajarkan Anda cara mengenali teks dari gambar,
  mengekstrak teks dari faktur, dan mengonversi gambar menjadi teks dengan Aspose
  OCR di GPU.
og_title: c# tutorial OCR – Pengenalan Teks Cepat Berbasis GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: Tutorial OCR C# – Mengenali Teks dari Gambar dengan Akselerasi GPU
url: /id/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Mengenali Teks dari Gambar dengan Akselerasi GPU

Pernah membutuhkan **c# ocr tutorial** yang benar‑benar menyelesaikan pekerjaan tanpa percobaan‑dan‑kesalahan yang tak berujung? Mungkin Anda sedang menatap faktur resolusi tinggi dan bertanya‑tanya bagaimana cara **extract text from invoice** file dalam hitungan detik. Kabar baiknya, Anda tidak perlu menciptakan kembali roda—Aspose.OCR memberi Anda API bersih yang dipercepat GPU yang melakukan pekerjaan berat untuk Anda.

Dalam panduan ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan cara **recognize text from image** file, **convert image to text**, dan menangani jebakan paling umum. Pada akhirnya Anda akan memiliki program mandiri yang dapat membaca gambar dokumen apa pun, mulai dari kwitansi hingga kontrak yang dipindai, dan menghasilkan teks bersih yang dapat dicari.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan merujuk paket NuGet Aspose.OCR.
- Cara mengonfigurasi mesin OCR agar berjalan di GPU untuk kinerja super cepat.
- Cara yang tepat untuk **load image for ocr** menggunakan `OcrImage.FromFile`.
- Cara memanggil `Recognize` dengan bahasa yang diinginkan dan mengambil hasilnya.
- Tips untuk menangani PDF multi‑halaman, pemindaian kontras rendah, dan penanganan error.

Tidak diperlukan pengalaman sebelumnya dengan Aspose; cukup dengan lingkungan pengembangan .NET yang berfungsi (Visual Studio 2022 atau VS Code) dan GPU yang cukup (bahkan GPU Intel terintegrasi pun cukup).

---

## Langkah 1 – Instal Aspose.OCR dan Siapkan Proyek Anda

Hal pertama yang perlu dilakukan: Anda memerlukan pustaka Aspose.OCR. Cara termudah adalah melalui NuGet.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menargetkan .NET 6 atau yang lebih baru, paket ini secara otomatis akan mengambil binary GPU native untuk Windows, Linux, dan macOS. Tidak ada DLL tambahan yang perlu disalin.

Setelah paket ditambahkan, buka file proyek Anda (`*.csproj`) dan verifikasi referensinya:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

Sekarang Anda memiliki semua yang diperlukan untuk mulai menulis kode.

## Langkah 2 – Buat Mesin OCR yang Didukung GPU (c# ocr tutorial)

Inti dari **c# ocr tutorial** adalah `OcrEngine`. Dengan mengatur `Engine = Engine.Gpu` kami memberi tahu Aspose untuk menggunakan kartu grafis alih‑alih CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Why GPU?** GPU dapat memproses ribuan piksel secara paralel, memotong waktu OCR dari detik menjadi pecahan detik pada gambar ber‑DPI tinggi yang besar.

## Langkah 3 – Muat Gambar untuk OCR (load image for ocr)

Memuat gambar dengan benar lebih penting daripada yang Anda kira. `OcrImage.FromFile` mendukung PNG, JPEG, BMP, TIFF, dan bahkan halaman PDF. Ia juga membaca DPI gambar, yang memengaruhi akurasi.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Catatan:** Jika Anda menangani PDF, Anda dapat mengekstrak setiap halaman sebagai `OcrImage` dan memberikannya satu per satu.

## Langkah 4 – Kenali Teks dari Gambar (recognize text from image)

Sekarang keajaiban terjadi. Kami meminta mesin untuk mengenali teks bahasa Inggris, tetapi Anda dapat memberikan bahasa apa pun yang didukung oleh Aspose (Spanyol, Jerman, Mandarin, dll.).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

Properti `result.Text` berisi string polos. Jika Anda membutuhkan skor kepercayaan untuk setiap kata, Anda dapat memeriksa `result.Regions`.

### Output yang Diharapkan

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

Jika gambar buram, Anda mungkin melihat karakter yang kacau—di sinilah pra‑pemrosesan dari Langkah 3 membantu.

## Langkah 5 – Ekstrak Teks dari Faktur – Contoh Dunia Nyata

Misalkan Anda memiliki folder berisi faktur yang dipindai dan ingin mengambil total jumlahnya. Di bawah ini adalah ekstensi cepat dari kode sebelumnya yang menggunakan ekspresi reguler sederhana.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

Anda akan memanggil `ExtractTotalAmount(result.Text);` tepat setelah mencetak hasil OCR. Ini menunjukkan betapa mudahnya **extract text from invoice** file setelah Anda memiliki string mentah.

## Langkah 6 – Konversi Gambar ke Teks secara Massal (convert image to text)

Memproses satu file saja cukup untuk demo, tetapi kode produksi sering harus menangani puluhan atau ratusan gambar. Berikut ini loop singkat yang memproses seluruh direktori:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

Menjalankan `ProcessFolder(ocrEngine, @"C:\Invoices")` akan **convert image to text** untuk setiap file yang didukung di folder, memanfaatkan GPU untuk kecepatan.

## Kasus Tepi dan Jebakan Umum

| Situation | Why It Happens | Quick Fix |
|-----------|----------------|-----------|
| **Low‑contrast scan** | OCR kesulitan membedakan latar depan dari latar belakang. | Tingkatkan kontras (`ImagePreprocessor.AdjustContrast`) atau terapkan ambang adaptif. |
| **Multi‑page PDF** | `OcrImage.FromFile` hanya membaca halaman pertama. | Gunakan `PdfDocument` untuk mengekstrak setiap halaman sebagai `OcrImage` dan lakukan loop. |
| **Unsupported language** | Bahasa default yang disetel adalah Inggris. | Berikan `Language.Spanish` atau nilai enum lain yang didukung. |
| **GPU not detected** | Biner native hilang atau driver usang. | Pastikan driver GPU terbaru; instal ulang paket NuGet dengan flag `-runtime`. |
| **Out‑of‑memory on huge images** | Memori GPU terbatas. | Ukur ulang gambar (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

## Contoh Kerja Lengkap

Berikut ini program lengkap yang dapat Anda salin‑tempel ke aplikasi konsol baru. Program ini mencakup semua metode bantu yang dibahas di atas.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}