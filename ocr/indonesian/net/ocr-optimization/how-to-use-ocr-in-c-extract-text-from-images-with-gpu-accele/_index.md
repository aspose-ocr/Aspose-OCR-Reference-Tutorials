---
category: general
date: 2025-12-29
description: Cara menggunakan OCR di C# untuk mengekstrak teks dari gambar, menampilkan
  jumlah karakter, dan meningkatkan kinerja dengan akselerasi GPU menggunakan Aspose
  OCR.
draft: false
keywords:
- how to use OCR
- extract text image
- display character count
- gpu acceleration ocr
- c# ocr aspose
language: id
og_description: Cara menggunakan OCR di C# untuk mengekstrak teks dari gambar, menampilkan
  jumlah karakter, dan mempercepat pemrosesan dengan GPU menggunakan Aspose OCR.
og_title: Cara Menggunakan OCR di C# – Ekstraksi Teks Cepat dengan GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: Cara Menggunakan OCR di C# – Mengekstrak Teks dari Gambar dengan Akselerasi
  GPU
url: /id/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Panduan Lengkap

Pernah bertanya-tanya **how to use OCR** dalam proyek .NET tanpa menulis ribuan baris kode? Mungkin Anda telah memindai file TIFF besar dan membutuhkan teks dengan cepat, atau Anda hanya ingin menghitung karakter untuk dasbor pelaporan. Bagaimanapun, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan membahas cara mengekstrak teks dari gambar, menampilkan jumlah karakter, dan mempercepat proses dengan **GPU acceleration OCR** – semuanya dengan pustaka **C# Aspose OCR**.

Kami juga akan menyelipkan topik sekunder yang mungkin Anda cari: **extract text image**, **display character count**, dan trik **c# ocr aspose**. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang dapat memproses pemindaian besar dalam sekejap.

---

## Apa yang Akan Anda Pelajari

- Menyiapkan Aspose OCR dalam proyek C# (tanpa misteri NuGet).
- Mengaktifkan **GPU acceleration OCR** untuk file besar.
- Memuat gambar dan **extract text from the image**.
- **Display character count** serta waktu pemrosesan.
- Menangani jebakan umum seperti driver GPU yang hilang atau format gambar yang tidak didukung.

> **Prerequisite:** .NET 6+ (atau .NET Framework 4.7.2) dan GPU yang kompatibel. Jika Anda tidak memiliki GPU, kode akan beralih secara elegan ke mode CPU.

---

![How to use OCR with GPU acceleration in C#](ocr-gpu.png "how to use OCR example showing GPU usage")

*Image alt text: how to use OCR illustration with GPU acceleration*

---

## Langkah 1: Instal Aspose OCR dan Siapkan Proyek

### Mengapa ini penting

Sebelum Anda dapat **use OCR**, pustaka harus direferensikan. Aspose OCR dikirim sebagai paket NuGet tunggal yang menyertakan binary native untuk CPU dan GPU, sehingga Anda tidak perlu mencari DLL secara manual.

```csharp
// In your terminal or Package Manager Console
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menargetkan .NET Framework, gunakan UI NuGet di Visual Studio untuk menghindari konflik versi.

### Kerangka proyek lengkap

Buat aplikasi konsol baru dan tempelkan `Program.cs` berikut. Ini mencakup semua pernyataan `using` yang diperlukan, sehingga Anda tidak perlu menebak apa yang harus diimpor.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing; // optional, for advanced pre‑processing

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Call the helper that does the heavy lifting
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            // Step 2: Create and configure the OCR engine (see next section)
        }
    }
}
```

Simpan file, pulihkan paket, dan Anda siap untuk langkah berikutnya.

---

## Langkah 2: Cara Menggunakan OCR Engine dengan GPU Acceleration

### Mengapa mengaktifkan GPU?

Memproses TIFF multi‑megapiksel pada CPU dapat memakan detik atau bahkan menit. Jalur **GPU acceleration OCR** memindahkan operasi piksel‑wise ke kartu grafis Anda, memotong waktu secara dramatis—seringkali menjadi sebagian kecil dari waktu asal.

```csharp
static void RunOcr(string imagePath)
{
    // Create an OCR engine instance
    var ocrEngine = new OcrEngine();

    // Enable GPU acceleration – if a compatible device is found
    ocrEngine.UseGpu = true;
    ocrEngine.GpuDeviceId = 0; // 0 = first GPU; change if you have multiple

    // Optional sanity check – fall back to CPU if GPU init fails
    try
    {
        // This call forces the engine to initialize GPU resources
        ocrEngine.InitializeGpu();
        Console.WriteLine("✅ GPU acceleration enabled.");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
        ocrEngine.UseGpu = false;
    }

    // Load the image (this also validates format)
    var inputImage = Image.Load(imagePath);
    
    // Perform OCR – the heavy lifting happens here
    var ocrResult = ocrEngine.Recognize(inputImage);

    // Step 3: Display results (character count & processing time)
    DisplayResult(ocrResult);
}
```

> **Why this works:** `UseGpu` toggles the internal pipeline. `InitializeGpu()` forces early validation so you can catch driver issues before the long‑running `Recognize` call.

---

## Langkah 3: Extract Text Image dan Display Character Count

Sekarang mesin sudah berjalan, mari **extract text from the image** dan tunjukkan berapa banyak karakter yang dikenali. Ini adalah bagian yang sering dilewatkan pengembang, tetapi penting untuk validasi dan analitik selanjutnya.

```csharp
static void DisplayResult(OcrResult ocrResult)
{
    // The raw OCR text
    string extractedText = ocrResult.Text;

    // Character count – includes spaces and line breaks
    int charCount = extractedText.Length;

    // Processing time in milliseconds (provided by Aspose)
    long processingMs = ocrResult.ProcessingTime;

    // Output to console – easy to pipe to a file or logger
    Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
    Console.WriteLine("----- Begin OCR Text -----");
    Console.WriteLine(extractedText);
    Console.WriteLine("------ End OCR Text ------");
}
```

**Expected output** (contoh untuk pemindaian 2‑halaman):

```
✅ GPU acceleration enabled.
🖋️ Extracted 12,345 characters in 842 ms
----- Begin OCR Text -----
Lorem ipsum dolor sit amet, consectetur...
... (rest of the page) ...
------ End OCR Text ------
```

Jika GPU tidak tersedia, Anda akan melihat peringatan dan hasil yang sama, hanya lebih lambat.

---

## Langkah 4: Menangani File Besar dan Kasus Edge

### Bagaimana jika gambar sangat besar?

Aspose OCR dapat melakukan streaming halaman, tetapi Anda tetap memerlukan RAM yang cukup. Praktik yang baik adalah menurunkan DPI yang tidak penting sebelum pengenalan:

```csharp
// Optional pre‑processing: downscale to 300 DPI if original > 600 DPI
if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
{
    inputImage = inputImage.Resize(0.5, 0.5); // 50% reduction
    Console.WriteLine("🔎 Image downscaled for faster OCR.");
}
```

### Driver GPU yang hilang?

`try/catch` di sekitar `InitializeGpu()` sudah menangkap sebagian besar masalah, tetapi Anda juga dapat menanyakan perangkat yang tersedia:

```csharp
var gpuInfo = GpuDeviceManager.GetDevices();
if (gpuInfo.Count == 0)
{
    Console.WriteLine("⚡ No GPU detected – defaulting to CPU.");
    ocrEngine.UseGpu = false;
}
```

### Format gambar tidak didukung?

Aspose mendukung TIFF, PNG, JPEG, BMP, dan beberapa format eksotis. Jika Anda mendapatkan `UnsupportedFormatException`, konversi file terlebih dahulu dengan alat seperti ImageMagick atau metode bawaan `Image.Save` ke PNG.

---

## Langkah 5: Wrap‑Up – Contoh Kerja Lengkap

Salin‑tempel seluruh program di bawah ini ke `Program.cs`. Ini adalah demo mandiri yang dapat Anda jalankan langsung (cukup ganti jalur file).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust the path to point at your scanned TIFF or JPEG
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,
                GpuDeviceId = 0
            };

            try
            {
                ocrEngine.InitializeGpu();
                Console.WriteLine("✅ GPU acceleration enabled.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
                ocrEngine.UseGpu = false;
            }

            var inputImage = Image.Load(imagePath);

            // Optional downscale for gigantic files
            if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
            {
                inputImage = inputImage.Resize(0.5, 0.5);
                Console.WriteLine("🔎 Image downscaled for faster OCR.");
            }

            var ocrResult = ocrEngine.Recognize(inputImage);
            DisplayResult(ocrResult);
        }

        static void DisplayResult(OcrResult ocrResult)
        {
            string extractedText = ocrResult.Text;
            int charCount = extractedText.Length;
            long processingMs = ocrResult.ProcessingTime;

            Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
            Console.WriteLine("----- Begin OCR Text -----");
            Console.WriteLine(extractedText);
            Console.WriteLine("------ End OCR Text ------");
        }
    }
}
```

Jalankan dengan `dotnet run` dan saksikan konsol menampilkan **character count** serta teks OCR. Itulah seluruh siklus **how to use OCR** dari awal hingga akhir.

---

## Kesimpulan

Kami baru saja membahas **how to use OCR** di C# untuk **extract text from images**, **display character count**, dan mempercepat seluruh pipeline dengan **GPU acceleration OCR** menggunakan pustaka **c# ocr aspose**. Poin penting yang dapat diambil:

1. Instal Aspose OCR via NuGet dan referensikan namespace yang tepat.  
2. Aktifkan GPU, tetapi selalu siapkan fallback ke CPU.  
3. Muat gambar Anda, opsional turunkan skala, lalu panggil `Recognize`.  
4. Ambil `ocrResult.Text` dan `ocrResult.ProcessingTime` untuk **display character count** serta metrik kinerja.  

Dari sini Anda dapat memperluas—menyimpan teks ke basis data, mengirimnya ke indeks pencarian, atau menjalankan deteksi bahasa pada string yang diekstrak. Jika Anda perlu memproses PDF, cukup ubah tiap halaman menjadi gambar; kode yang sama akan berfungsi.

**Next steps** yang dapat Anda jelajahi:

- Menggunakan **extract text image** dari PDF multi‑halaman dengan `PdfConverter`.  
- Menyesuaikan pengaturan OCR (paket bahasa, pengurangan noise) untuk akurasi lebih baik.  
- Menskalakan solusi di Azure Functions atau AWS Lambda dengan instance yang mendukung GPU.  

Cobalah, pecahkan, lalu tingkatkan. Begitulah proyek OCR dunia nyata dibangun. Selamat coding, semoga pemindaian Anda selalu dapat dibaca!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}