---
category: general
date: 2026-05-28
description: Mengenali teks dari PNG menggunakan Aspose OCR dalam C#. Pelajari cara
  mengekstrak teks dari halaman yang dipindai dan melakukan OCR pada gambar secara
  efisien.
draft: false
keywords:
- recognize text from png
- extract text from scanned pages
- perform ocr on images
- Aspose OCR C#
- OCR image processing
language: id
og_description: Mengenali teks dari PNG menggunakan Aspose OCR di C#. Kuasai cara
  mengekstrak teks dari halaman yang dipindai dan melakukan OCR pada gambar dalam
  hitungan menit.
og_title: Mengenali teks dari PNG dengan Aspose OCR – Panduan Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: recognize text from png using Aspose OCR in C#. Learn how to extract
    text from scanned pages and perform OCR on images efficiently.
  headline: recognize text from png with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: recognize text from png using Aspose OCR in C#. Learn how to extract
    text from scanned pages and perform OCR on images efficiently.
  name: recognize text from png with Aspose OCR – Complete C# Guide
  steps:
  - name: '**Engine initialization** – The `OcrEngine` class is the entry point; it
      holds all configuration and state.'
    text: '**Engine initialization** – The `OcrEngine` class is the entry point; it
      holds all configuration and state.'
  - name: '**Evaluation‑mode guard** – If you’re using a trial license, Aspose caps
      the number of pages you can process. Setting `MaxPagesInEvaluation` prevents
      the library from throwing a *LicenseException* halfway through.'
    text: '**Evaluation‑mode guard** – If you’re using a trial license, Aspose caps
      the number of pages you can process. Setting `MaxPagesInEvaluation` prevents
      the library from throwing a *LicenseException* halfway through.'
  - name: '**Image loading** – `ImageStream.FromFile` abstracts away the `System.Drawing`
      dependency, letting you feed any supported format (PNG, JPEG, BMP) directly.'
    text: '**Image loading** – `ImageStream.FromFile` abstracts away the `System.Drawing`
      dependency, letting you feed any supported format (PNG, JPEG, BMP) directly.'
  - name: '**Recognition loop** – By iterating, you can **perform OCR on images**
      in bulk, which is exactly what most real‑world scanning pipelines need.'
    text: '**Recognition loop** – By iterating, you can **perform OCR on images**
      in bulk, which is exactly what most real‑world scanning pipelines need.'
  - name: '**Disposal** – The engine holds unmanaged resources; disposing releases
      memory promptly, especially important when processing many high‑resolution PNGs.'
    text: '**Disposal** – The engine holds unmanaged resources; disposing releases
      memory promptly, especially important when processing many high‑resolution PNGs.'
  - name: Install the NuGet package.
    text: Install the NuGet package.
  - name: Initialise `OcrEngine`.
    text: Initialise `OcrEngine`.
  - name: (Optional) Set a page limit for evaluation mode.
    text: (Optional) Set a page limit for evaluation mode.
  - name: Load each PNG with `ImageStream.FromFile`.
    text: Load each PNG with `ImageStream.FromFile`.
  - name: Call `Recognize()` and output the result.
    text: Call `Recognize()` and output the result.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Mengenali Teks dari PNG dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/text-recognition/recognize-text-from-png-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali teks dari png dengan Aspose OCR – Panduan Lengkap C# 

Pernah membutuhkan untuk **recognize text from png** file dalam aplikasi .NET? Dengan Aspose OCR Anda dapat dengan cepat **extract text from scanned pages** dan **perform OCR on images** tanpa berurusan dengan pemrosesan gambar tingkat rendah. Dalam tutorial ini kami akan membahas contoh C# yang siap dijalankan, menjelaskan mengapa setiap baris penting, dan menunjukkan cara menyesuaikannya untuk proyek dunia nyata.

Jika Anda bertanya-tanya apakah ini bekerja pada pemindaian multi‑halaman, apakah Anda dapat membatasi mode evaluasi, atau bagaimana menangani file gambar yang sangat besar—tetap ikuti. Pada akhir tutorial Anda akan memiliki potongan kode yang solid dan siap produksi yang dapat Anda salin‑tempel ke dalam solusi Anda sendiri.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

| Prasyarat | Mengapa penting |
|--------------|----------------|
| **.NET 6.0 atau lebih baru** (atau .NET Framework 4.6+) | Aspose.OCR menargetkan runtime modern dan memberikan peningkatan kinerja terbaru. |
| **Visual Studio 2022** (atau IDE apa pun yang Anda suka) | Editor yang nyaman memudahkan pengujian kode. |
| **Paket NuGet Aspose.OCR** | Ini adalah pustaka yang sebenarnya melakukan pekerjaan berat. |
| Sebuah folder dengan beberapa **gambar PNG** yang ingin Anda baca | Tutorial mengasumsikan file bernama `page1.png`, `page2.png`, … |

Jika ada yang terdengar tidak familiar, cukup instal paket NuGet dan buat proyek konsol sederhana—tidak memerlukan konfigurasi tambahan.

## Langkah 1: Instal Aspose.OCR via NuGet

Buka terminal Anda (atau Package Manager Console) dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Atau, jika Anda lebih suka UI, klik kanan **Dependencies → Manage NuGet Packages**, cari *Aspose.OCR*, dan klik **Install**. Ini akan mengunduh semua yang Anda butuhkan, termasuk kelas pembantu `ImageStream` yang digunakan nanti.

> **Pro tip:** Gunakan versi stabil terbaru (per Mei 2026 versi 23.10). Rilis baru sering berisi perbaikan bug untuk format gambar yang rumit.

## Langkah 2: Buat Aplikasi Konsol Minimal

Buat proyek konsol baru jika belum melakukannya:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Ganti isi `Program.cs` dengan contoh lengkap di bawah ini. Perhatikan bagaimana kami menjaga kode **self‑contained**—tanpa file konfigurasi eksternal, tanpa keajaiban tersembunyi.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine
            // -------------------------------------------------
            var engine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣  Optional: limit pages when running in evaluation mode
            // -------------------------------------------------
            // Evaluation licenses only allow a few pages; set this to avoid runtime errors.
            engine.Configuration.MaxPagesInEvaluation = 5;

            // -------------------------------------------------
            // 3️⃣  Define where your PNG files live
            // -------------------------------------------------
            string basePath = @"YOUR_DIRECTORY"; // <-- change this to your real folder

            // -------------------------------------------------
            // 4️⃣  Loop through the images you want to process
            // -------------------------------------------------
            for (int i = 0; i < 5; i++) // adjust the loop count to match your file count
            {
                // Load the current page image
                engine.Image = ImageStream.FromFile($"{basePath}/page{i + 1}.png");

                // -------------------------------------------------
                // 5️⃣  Perform OCR and display the result
                // -------------------------------------------------
                Console.WriteLine($"--- Page {i + 1} ---");
                string recognizedText = engine.Recognize();

                // Show the extracted text; you could also write it to a file.
                Console.WriteLine(recognizedText);
                Console.WriteLine(); // blank line for readability
            }

            // -------------------------------------------------
            // 6️⃣  Clean up (optional but good practice)
            // -------------------------------------------------
            engine.Dispose();
        }
    }
}
```

### Mengapa Struktur Ini Berfungsi

1. **Engine initialization** – Kelas `OcrEngine` adalah titik masuk; ia menyimpan semua konfigurasi dan status.  
2. **Evaluation‑mode guard** – Jika Anda menggunakan lisensi percobaan, Aspose membatasi jumlah halaman yang dapat diproses. Menetapkan `MaxPagesInEvaluation` mencegah pustaka melempar *LicenseException* di tengah proses.  
3. **Image loading** – `ImageStream.FromFile` mengabstraksi ketergantungan `System.Drawing`, memungkinkan Anda memasukkan format yang didukung (PNG, JPEG, BMP) secara langsung.  
4. **Recognition loop** – Dengan iterasi, Anda dapat **perform OCR on images** secara massal, yang tepatnya dibutuhkan oleh kebanyakan alur pemindaian dunia nyata.  
5. **Disposal** – Engine menyimpan sumber daya tak terkelola; membuangnya (dispose) melepaskan memori dengan cepat, terutama penting saat memproses banyak PNG beresolusi tinggi.

## Langkah 3: Jalankan Aplikasi dan Verifikasi Output

Bangun dan jalankan:

```bash
dotnet run
```

Dengan asumsi Anda menempatkan lima file PNG bernama `page1.png` … `page5.png` di folder yang Anda tentukan, Anda akan melihat sesuatu seperti:

```
--- Page 1 ---
Invoice #12345
Date: 2026-05-01
Total: $1,250.00

--- Page 2 ---
Thank you for your purchase!
...

```

Jika Anda mendapatkan string kosong, periksa kembali bahwa gambar berisi **recognizable text** (kontras jelas, bukan foto tanda yang buram). Aspose OCR bekerja paling baik dengan pemindaian berkualitas tinggi—pikirkan 300 dpi atau lebih.

> **Contoh gambar**  
> ![contoh output mengenali teks dari png](https://example.com/ocr-output.png "mengenali teks dari png – output konsol")

## Langkah 4: Kesulitan Umum Saat **extracting text from scanned pages**

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| Output kosong | Gambar memiliki kontras rendah atau berisik | Pra‑proses dengan Aspose.Imaging (binarisasi, deskew). |
| Karakter kacau | Bahasa tidak diatur (default adalah English) | `engine.Configuration.Language = Language.English;` atau atur ke `Language.French`, dll. |
| Exception *“File not found”* | Path folder salah atau ekstensi file hilang | Gunakan `Path.Combine(basePath, $"page{i+1}.png")` untuk keamanan. |
| Kesalahan lisensi setelah beberapa halaman | Menggunakan lisensi percobaan tanpa `MaxPagesInEvaluation` | Beli lisensi atau pertahankan baris `MaxPagesInEvaluation`. |

Tips ini menjaga alur kerja **extract text from scanned pages** Anda tetap lancar, bahkan ketika materi sumber tidak sempurna.

## Langkah 5: Lanjutan – Meningkatkan ke Ratusan Gambar

Jika Anda perlu **perform OCR on images** yang disimpan di basis data atau bucket cloud, ganti loop `for` dengan `foreach` atas koleksi path file:

```csharp
string[] pngFiles = Directory.GetFiles(basePath, "*.png");
foreach (var file in pngFiles)
{
    engine.Image = ImageStream.FromFile(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(engine.Recognize());
}
```

Anda juga dapat mengaktifkan **multithreading** (Aspose OCR aman untuk thread) untuk mempercepat pemrosesan pada mesin multi‑core:

```csharp
Parallel.ForEach(pngFiles, file =>
{
    var localEngine = new OcrEngine(); // each thread gets its own engine
    localEngine.Image = ImageStream.FromFile(file);
    string text = localEngine.Recognize();
    lock (Console.Out) // avoid garbled console output
    {
        Console.WriteLine($"--- {Path.GetFileName(file)} ---");
        Console.WriteLine(text);
    }
    localEngine.Dispose();
});
```

Ingat untuk membuang (dispose) setiap instance engine; jika tidak, Anda akan mengalami kebocoran memori native.

## Langkah 6: Melampaui PNG – Format Lain dan PDF

Aspose OCR tidak terbatas pada PNG. Anda dapat memberi JPEG, BMP, TIFF, atau bahkan **PDF pages** (dengan mengonversinya menjadi gambar terlebih dahulu). Untuk PDF, gabungkan Aspose.PDF dan Aspose.OCR:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load PDF, render each page to a PNG stream, then OCR
Document pdf = new Document("sample.pdf");
for (int pageNum = 1; pageNum <= pdf.Pages.Count; pageNum++)
{
    using var imgStream = new MemoryStream();
    var rasterizer = new PngDevice();
    rasterizer.Process(pdf.Pages[pageNum], imgStream);
    imgStream.Position = 0;

    engine.Image = ImageStream.FromStream(imgStream);
    Console.WriteLine($"--- PDF Page {pageNum} ---");
    Console.WriteLine(engine.Recognize());
}
```

Potongan kode tersebut menunjukkan cara Anda dapat **extract text from scanned pages** yang datang sebagai PDF—situasi umum dalam alur pemrosesan faktur.

## Ringkasan & Langkah Selanjutnya

Kami telah membahas seluruh siklus hidup **recognize text from png** menggunakan Aspose OCR:

1. Instal paket NuGet.  
2. Inisialisasi `OcrEngine`.  
3. (Opsional) Atur batas halaman untuk mode evaluasi.  
4. Muat setiap PNG dengan `ImageStream.FromFile`.  
5. Panggil `Recognize()` dan keluarkan hasilnya.

## Tutorial Terkait

- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar – Kenali Garis dengan Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}