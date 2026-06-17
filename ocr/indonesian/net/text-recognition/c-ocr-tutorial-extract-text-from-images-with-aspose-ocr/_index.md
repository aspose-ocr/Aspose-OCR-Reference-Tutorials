---
category: general
date: 2026-03-21
description: 'Tutorial OCR c#: Pelajari cara mengekstrak teks dari gambar, memindai
  faktur, dan memuat gambar di C# menggunakan Aspose OCR dengan akselerasi GPU.'
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- ocr invoice scanning
- how to ocr image
- load image in c#
language: id
og_description: 'Tutorial OCR C#: Panduan langkah demi langkah untuk mengekstrak teks
  dari gambar, melakukan pemindaian faktur OCR, dan belajar cara melakukan OCR pada
  gambar di C# dengan akselerasi GPU.'
og_title: Tutorial OCR c# – Ekstrak Teks dari Gambar dengan Aspose OCR
tags:
- OCR
- C#
- Image Processing
title: Tutorial OCR c# – Ekstrak Teks dari Gambar dengan Aspose OCR
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# OCR – Ekstrak Teks dari Gambar dengan Aspose OCR

Pernah bertanya-tanya bagaimana cara **c# OCR tutorial** menangani masalah dunia nyata seperti mengubah faktur yang dipindai menjadi teks yang dapat diedit? Anda tidak sendirian. Banyak pengembang menemui kendala ketika mereka perlu *extract text from image* file dan berakhir menulis parser rapuh yang rusak pada pemindaian pertama yang berisik.

Begini—Aspose.OCR membuat seluruh proses menjadi sangat mudah, terutama ketika Anda mengaktifkan akselerasi GPU. Dalam panduan ini Anda akan melihat secara tepat **how to ocr image** file di C#, memuat gambar di c# dengan benar, dan bahkan menangani keanehan pemindaian faktur yang umum tanpa membuat Anda stres.

Pada akhir tutorial ini Anda akan memiliki aplikasi konsol yang dapat dijalankan yang membaca faktur TIFF, menjalankan OCR pada GPU, dan mencetak output teks polos yang bersih. Tidak ada sulap, hanya kode solid yang dapat Anda salin‑tempel dan sesuaikan.

---

## Apa yang Anda Butuhkan

- **.NET 6.0** (atau lebih baru) – versi LTS saat ini, sehingga Anda siap untuk masa depan.
- **Aspose.OCR for .NET** paket NuGet – versi 23.10 (yang terbaru pada saat penulisan).
- Sebuah mesin **GPU‑enabled** (opsional tetapi disarankan) – kode akan kembali ke CPU jika tidak ada GPU yang kompatibel.
- Contoh gambar, misalnya `large_invoice.tif`. Semua format yang didukung (PNG, JPEG, TIFF, PDF) dapat digunakan.

Jika Anda belum menginstal paket NuGet, jalankan:

```bash
dotnet add package Aspose.OCR
```

Sekarang setelah kami membahas prasyarat, mari kita selami langkah‑langkah sebenarnya.

---

## Langkah 1: Buat Proyek Konsol Baru dan Tambahkan Aspose.OCR

Pertama, buat aplikasi konsol baru agar tutorial ini tetap mandiri.

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Gunakan flag `-n` untuk memberi proyek Anda nama yang bermakna; ini membuat solusi tetap rapi ketika Anda mulai menambahkan modul lain nanti.

File `Program.cs` yang dibuat Visual Studio akan menjadi arena bermain kita. Buka dan hapus baris `Console.WriteLine` default – kami akan menggantinya dengan logika OCR.

## Langkah 2: Memuat Gambar di C# – Cara yang Benar

Memuat gambar mungkin terlihat sederhana, tetapi melakukannya dengan salah dapat menyebabkan kebocoran memori atau mengunci file. Kelas `System.Drawing.Image` berfungsi baik untuk kebanyakan skenario, namun Anda harus membungkusnya dalam blok `using` untuk menjamin pembuangan.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 2: Load the image you want to OCR.
            // Replace the path with the actual location of your invoice file.
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // The using statement ensures the image gets disposed automatically.
            using var inputImage = Image.FromFile(imagePath);
            
            // Continue to the OCR engine setup…
        }
    }
}
```

Perhatikan komentar `// 👉 Step 2:` – ini mencerminkan penomoran langkah dalam tutorial kami dan membantu siapa pun yang menelusuri kode nanti.

## Langkah 3: Inisialisasi Mesin OCR dengan Akselerasi GPU

Aspose.OCR memungkinkan Anda memilih mode pemrosesan saat konstruksi. `OcrEngineMode.Gpu` memberi tahu pustaka untuk menggunakan kartu grafis jika terdeteksi; jika tidak, secara diam-diam kembali ke CPU, sehingga Anda tidak perlu menulis logika fallback tambahan.

```csharp
// 👉 Step 3: Create the OCR engine.
// The constructor argument selects GPU mode; it's the fastest option for large invoices.
var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);
```

> **Mengapa GPU?**  
> OCR pada faktur beresolusi tinggi dapat memakan banyak CPU. Memindahkan ke GPU mengurangi waktu eksekusi dari beberapa detik menjadi sebagian kecil, terutama saat Anda memproses batch.

## Langkah 4: Jalankan OCR dan Ekstrak Teks dari Gambar

Sekarang keajaiban terjadi. Panggil `Recognize` dan ambil teks polos. Aspose mengembalikan objek `OcrResult` yang berisi teks mentah, skor kepercayaan, dan bahkan kotak pembatas per‑karakter jika Anda membutuhkannya nanti.

```csharp
// 👉 Step 4: Perform the OCR operation.
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Display the extracted text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
=== OCR Output ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

Jika output terlihat berantakan, periksa kembali bahwa gambar memiliki kontras tinggi dan bahasa OCR telah diatur dengan benar (English adalah default). Anda juga dapat menyesuaikan `ocrEngine.Settings` untuk akurasi lebih baik, tetapi pengaturan default sudah cukup baik untuk kebanyakan faktur cetak.

## Langkah 5: Menangani Kasus Pinggiran Pemindaian Faktur OCR

Faktur datang dalam berbagai bentuk—beberapa multi‑halaman, yang lain memiliki tabel atau catatan tulisan tangan. Berikut beberapa penyesuaian cepat yang dapat Anda lakukan tanpa menulis ulang seluruh pipeline.

### 5.1 PDF atau TIFF Multi‑Halaman

Jika file sumber Anda berisi beberapa halaman, Anda perlu melakukan loop pada setiap halaman dan menggabungkan hasilnya.

```csharp
using var multiPageImage = Image.FromFile(@"C:\Invoices\multi_page_invoice.tif");

// Aspose can split multi‑page TIFFs into separate images.
for (int i = 0; i < multiPageImage.GetFrameCount(FrameDimension.Page); i++)
{
    multiPageImage.SelectActiveFrame(FrameDimension.Page, i);
    using var page = (Image)multiPageImage.Clone();
    var pageResult = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

### 5.2 Pemindaian Resolusi Rendah

Jika DPI di bawah 150, tingkatkan skala gambar sebelum mengirimnya ke mesin. Ini secara dramatis meningkatkan pengenalan karakter.

```csharp
// Simple nearest‑neighbor scaling – replace with a better algorithm if needed.
var highRes = new Bitmap(inputImage, new Size(inputImage.Width * 2, inputImage.Height * 2));
var highResResult = ocrEngine.Recognize(highRes);
Console.WriteLine(highResResult.Text);
```

### 5.3 Paket Bahasa Kustom

Secara default Aspose menggunakan bahasa Inggris. Untuk bahasa lain, unduh paket bahasa yang sesuai dari situs Aspose dan daftarkan:

```csharp
ocrEngine.Settings.Language = OcrLanguage.Spanish; // example for Spanish invoices
```

Penyesuaian ini membuat solusi **ocr invoice scanning** Anda cukup kuat untuk beban kerja produksi.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap dijalankan yang menggabungkan semua langkah di atas. Salin ke `Program.cs`, sesuaikan jalur file, dan tekan **F5**.

```csharp
// ---------------------------------------------------------------
// Complete c# OCR tutorial – Aspose OCR with GPU acceleration
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialize the OCR engine (GPU mode)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);

            // -----------------------------------------------------------------
            // Step 2: Load the image you want to process
            // -----------------------------------------------------------------
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // Using ensures the image is disposed properly.
            using var inputImage = Image.FromFile(imagePath);

            // -----------------------------------------------------------------
            // Step 3: Run OCR and extract plain text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);

            // -----------------------------------------------------------------
            // Step 4: Output the result
            // -----------------------------------------------------------------
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Optional: Demonstrate handling a multi‑page TIFF (comment out if not needed)
            // -----------------------------------------------------------------
            // HandleMultiPageTiff(@"C:\Invoices\multi_page_invoice.tif", ocrEngine);
        }

        // ---------------------------------------------------------------
        // Helper for multi‑page TIFFs – shows how to iterate pages
        // ---------------------------------------------------------------
        static void HandleMultiPageTiff(string path, OcrEngine engine)
        {
            using var multiPage = Image.FromFile(path);
            int pageCount = multiPage.GetFrameCount(FrameDimension.Page);

            for (int i = 0; i < pageCount; i++)
            {
                multiPage.SelectActiveFrame(FrameDimension.Page, i);
                using var page = (Image)multiPage.Clone();
                var result = engine.Recognize(page);
                Console.WriteLine($"\n--- Page {i + 1} ---");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== OCR Output ===
Invoice #98765
Date: 02/28/2026
Bill To: Acme Corp.
Subtotal: $2,500.00
Tax (8%): $200.00
Total: $2,700.00
...
```

Jalankan program dan pastikan konsol mencetak teks yang Anda lihat pada faktur. Jika Anda mendapatkan string kosong, periksa kembali bahwa jalur gambar benar dan file tidak rusak.

## Pertanyaan yang Sering Diajukan (FAQ)

**Q: Apakah ini bekerja di Linux?**  
A: Ya. Aspose.OCR bersifat lintas‑platform. Cukup instal runtime .NET untuk Linux dan paket NuGet yang sama berfungsi. Akselerasi GPU memerlukan GPU yang kompatibel dengan CUDA dan driver yang sesuai.

**Q: Bagaimana jika saya tidak memiliki GPU?**  
A: Konstruktor `OcrEngineMode.Gpu` secara otomatis kembali ke CPU ketika tidak ada GPU yang kompatibel terdeteksi. Anda tetap akan mendapatkan hasil yang akurat; hanya akan memakan waktu sedikit lebih lama.

**Q: Bisakah saya OCR catatan tulisan tangan?**  
A: Model default Aspose berfokus pada teks cetak. Untuk tulisan tangan Anda memerlukan model khusus atau layanan lain (misalnya, Azure Form Recognizer). Namun, Anda masih dapat mencoba kode yang sama—hanya harapkan skor kepercayaan yang lebih rendah.

## Kesimpulan

Anda baru saja menyelesaikan **c# OCR tutorial** yang menunjukkan cara *extract text from image* file, melakukan **ocr invoice scanning**, dan memahami **how to o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}