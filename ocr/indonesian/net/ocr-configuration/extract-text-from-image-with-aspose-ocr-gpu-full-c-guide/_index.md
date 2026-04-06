---
category: general
date: 2026-04-06
description: Ekstrak teks dari gambar menggunakan Aspose OCR GPU di C#. Pelajari cara
  memuat gambar dari file dan mengatur batas memori GPU dalam panduan langkah demi
  langkah ini.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: id
og_description: Ekstrak teks dari gambar menggunakan Aspose OCR GPU di C#. Pelajari
  cara memuat gambar dari file dan mengatur batas memori GPU dalam panduan langkah
  demi langkah ini.
og_title: Ekstrak Teks dari Gambar dengan Aspose OCR GPU – Panduan Lengkap C#
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Ekstrak Teks dari Gambar dengan Aspose OCR GPU – Panduan Lengkap C#
url: /id/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Aspose OCR GPU – Panduan Lengkap C# 

Pernahkah Anda perlu **mengekstrak teks dari gambar** tetapi terhambat pada titik di mana kinerja menjadi penting? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika OCR menjadi bottleneck. Dalam tutorial ini kami akan menunjukkan secara tepat cara mengekstrak teks dari gambar menggunakan runtime GPU Aspose OCR, memuat gambar dari file, dan bahkan mengatur batas memori GPU untuk kontrol sumber daya yang lebih ketat.

Kami akan membahas contoh C# lengkap yang siap dijalankan, menjelaskan mengapa setiap baris penting, dan menunjukkan jebakan umum yang mungkin Anda temui. Pada akhir tutorial Anda akan memiliki fondasi yang kuat untuk membangun pipeline OCR yang cepat dan skalabel yang berjalan di GPU.

## Apa yang Dibahas dalam Panduan Ini

- **Prasyarat**: .NET 6+ (atau .NET Framework 4.6+), paket NuGet Aspose.OCR, driver GPU yang kompatibel.
- **Kode langkah‑demi‑langkah** yang memuat gambar dari file, mengonfigurasi mesin GPU Aspose OCR, dan mengekstrak teks.
- **Mengapa** Anda mungkin ingin mengatur batas memori GPU dan cara melakukannya dengan aman.
- **Penanganan kasus‑tepi**: gambar beresolusi rendah, GPU yang tidak ada, dan pemecahan masalah skor kepercayaan.
- **Langkah selanjutnya**: pemrosesan batch, integrasi dengan ASP.NET Core, dan beralih kembali ke CPU jika diperlukan.

> **Pro tip:** Jika Anda tidak yakin apakah GPU Anda sedang digunakan, periksa monitor aktivitas GPU (mis., NVIDIA‑SMI) saat OCR berjalan. Anda akan melihat lonjakan penggunaan memori yang sesuai dengan batas yang Anda tetapkan.

---

![Diagram yang menunjukkan alur mengekstrak teks dari gambar menggunakan mesin GPU Aspose OCR](extract-text-from-image-aspose-ocr-gpu.png "ekstrak teks dari gambar menggunakan Aspose OCR GPU")

## Langkah 1: Inisialisasi Mesin Aspose OCR untuk Pemrosesan GPU

Hal pertama yang Anda butuhkan adalah instance `OcrEngine` yang mengetahui bahwa ia harus dijalankan di GPU. Aspose menyediakan objek `OcrEngineSettings` yang bersih dimana Anda dapat menentukan runtime.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Mengapa ini penting:** Secara default Aspose OCR akan kembali ke CPU, yang cukup untuk gambar kecil tetapi dapat sangat lambat untuk foto beresolusi tinggi. Menetapkan secara eksplisit `Runtime = OcrRuntime.Gpu` memindahkan beban kerja berat ke kartu grafis, memberikan peningkatan kecepatan yang terlihat.

## Langkah 2: (Opsional) Atur Batas Memori GPU

Jika Anda menjalankan pada workstation bersama atau kontainer dengan sumber daya GPU terbatas, Anda dapat membatasi jumlah memori yang dikonsumsi oleh mesin OCR. Ini mencegah crash karena kehabisan memori dan membuat proses lain tetap berjalan lancar.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**Kapan menggunakannya:**  
- **Lingkungan multi‑penyewa** dimana beberapa layanan berbagi GPU yang sama.  
- **Pipeline CI/CD** yang mengalokasikan jumlah memori GPU tetap per pekerjaan.  

Jika Anda menghilangkan baris ini, Aspose akan menggunakan sebanyak memori yang dibutuhkan, yang cukup pada workstation yang didedikasikan.

## Langkah 3: Muat Gambar dari File

Sekarang kita perlu membawa gambar ke memori. Aspose OCR bekerja dengan `System.Drawing.Image`, jadi kita akan menggunakan `Image.FromFile`. Pastikan path mengarah ke file yang nyata; jika tidak, akan dilemparkan pengecualian.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Mengapa memuat dari file penting:** Banyak pengembang mencoba memberi array byte secara langsung, yang memang bekerja tetapi menambah langkah konversi yang tidak diperlukan. Menggunakan `Image.FromFile` sederhana, dan pernyataan `using` menjamin handle file dilepaskan dengan cepat.

## Langkah 4: Jalankan OCR dan Dapatkan Hasilnya

Dengan mesin yang dikonfigurasi dan gambar yang dimuat, kita akhirnya dapat mengekstrak teks. Metode `Recognize` mengembalikan `OcrResult` yang berisi teks mentah serta skor kepercayaan.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Memahami output:**  
- `Confidence` adalah nilai antara 0 dan 1. Kepercayaan 0.95 (atau 95 %) biasanya **menandakan** OCR sangat akurat.  
- `Text` berisi pemisah baris sebagaimana muncul di gambar, yang berguna untuk pemrosesan selanjutnya.

## Langkah 5: Verifikasi Output dan Tangani Kasus‑Tepi

### Memeriksa Tingkat Kepercayaan

Jika kepercayaan turun di bawah, misalnya, 80 %, Anda mungkin ingin kembali ke pemrosesan CPU atau menerapkan pra‑pemrosesan gambar (mis., binarisasi).

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### Menangani GPU yang Tidak Ada

Tidak setiap mesin memiliki GPU yang kompatibel. Aspose akan melempar `OcrException` jika tidak dapat menginisialisasi runtime GPU.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### Gambar Resolusi Tinggi

Gambar sangat besar (mis., lebar > 4000 px) dapat mengonsumsi banyak memori GPU. Jika Anda mencapai batas yang ditetapkan sebelumnya, Aspose akan memotong proses. Dalam kasus seperti itu, turunkan skala gambar terlebih dahulu:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru. Program ini mencakup semua langkah, penanganan error, dan logika fallback opsional.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### Output yang Diharapkan

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

Jika kepercayaan turun di bawah ambang batas, Anda akan melihat pesan fallback CPU tambahan.

---

## Kesimpulan

Anda kini tahu **cara mengekstrak teks dari gambar** menggunakan mesin GPU Aspose OCR, cara **memuat gambar dari file**, dan mengapa Anda mungkin ingin **mengatur batas memori GPU** untuk beban kerja produksi. Contoh di atas adalah solusi yang sepenuhnya berfungsi dan layak disitasi yang dapat Anda masukkan ke proyek .NET apa pun.

Apa selanjutnya? Pertimbangkan:

- **Pemrosesan batch**: iterasi folder gambar dan menulis hasil ke CSV.  
- **Integrasi ASP.NET Core**: expose endpoint API yang menerima gambar yang diunggah dan mengembalikan teks OCR.  
- **Penyetelan kinerja**: bereksperimen dengan nilai `GpuMemoryLimit` yang berbeda dan memantau pemanfaatan GPU untuk menemukan titik optimal.

Silakan sesuaikan kode dengan skenario Anda—apakah Anda membangun pipeline digitalisasi dokumen, aplikasi terjemahan waktu nyata, atau layanan pemindaian struk. Dasar-dasarnya tetap sama: inisialisasi mesin GPU, kelola memori dengan bijak, dan selalu verifikasi kepercayaan.

Ada pertanyaan atau mengalami masalah? Tinggalkan komentar di bawah, dan mari kita selesaikan bersama. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}