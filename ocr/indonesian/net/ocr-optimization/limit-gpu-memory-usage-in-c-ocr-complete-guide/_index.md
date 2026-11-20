---
category: general
date: 2026-05-02
description: Batasi penggunaan memori GPU saat menjalankan OCR pada gambar di C#.
  Pelajari cara mengaktifkan percepatan GPU, mengekstrak teks dari kwitansi, dan kuasai
  tutorial OCR C#.
draft: false
keywords:
- limit gpu memory usage
- extract text from receipt
- how to enable gpu acceleration
- run OCR on image
- c# ocr tutorial
language: id
og_description: Batasi penggunaan memori GPU saat menjalankan OCR pada gambar di C#.
  Panduan ini menunjukkan cara mengaktifkan percepatan GPU, mengekstrak teks dari
  struk, dan menguasai tutorial OCR C#.
og_title: Batasi Penggunaan Memori GPU dalam OCR C# – Panduan Lengkap
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Batasi Penggunaan Memori GPU dalam OCR C# – Panduan Lengkap
url: /id/net/ocr-optimization/limit-gpu-memory-usage-in-c-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# batasi penggunaan memori GPU dalam C# OCR – Panduan Lengkap

Pernahkah Anda perlu **membatasi penggunaan memori GPU** saat memproses sekumpulan struk? Anda tidak sendirian—para pengembang sering mengalami error out‑of‑memory ketika GPU diminta menangani terlalu banyak gambar sekaligus. Kabar baiknya, Aspose.OCR memungkinkan Anda membatasi jejak memori **dan** mengaktifkan percepatan GPU dalam satu baris kode.  

Dalam tutorial ini kami akan membimbing Anda melalui solusi praktis langkah‑demi‑langkah yang menunjukkan **cara mengaktifkan percepatan GPU**, mengambil teks dari contoh gambar struk, dan menjaga penggunaan RAM GPU tetap di bawah 1 GB yang rapi. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# yang siap dijalankan, plus beberapa tips yang dapat Anda pakai kembali dalam skenario **run OCR on image** apa pun.

## Apa yang Anda Butuhkan

- .NET 6.0 SDK atau yang lebih baru (kode juga dapat dikompilasi dengan .NET 5+)  
- Paket NuGet Aspose.OCR untuk .NET (`Aspose.OCR`) – instal dengan `dotnet add package Aspose.OCR`  
- GPU yang mendukung CUDA atau perangkat Windows yang kompatibel dengan DirectML  
- Contoh gambar struk (`receipt.jpg`) yang ditempatkan di folder yang dapat Anda referensikan  

Itu saja—tanpa pustaka native tambahan, tanpa menyalin DLL yang rumit. Aspose mengabstraksi backend GPU, sehingga Anda dapat fokus pada logika bisnis.

## Langkah 1: Instal Paket NuGet Aspose.OCR

Langkah pertama. Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Ini akan mengunduh versi stabil terbaru (per Mei 2026 versi 23.11). Paket ini menyertakan binary CPU dan GPU, jadi Anda tidak perlu mengunduh runtime CUDA atau DirectML secara manual—Aspose akan mendeteksi apa yang tersedia saat runtime.

> **Pro tip:** Jika Anda menargetkan pipeline CI/CD, kunci versi di file `.csproj` Anda untuk menghindari upgrade tak terduga.

## Langkah 2: Buat OCR Engine dan **batasi penggunaan memori GPU**

Sekarang kita akan menginstansiasi `OcrEngine` dan secara eksplisit memberi tahu agar tidak melebihi 1 GB memori GPU. Inilah inti dari persyaratan **batasi penggunaan memori GPU**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

public class GpuExample
{
    public static void Run()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU mode – Aspose auto‑detects CUDA or DirectML
        ocrEngine.Settings.Engine = EngineMode.Gpu;

        // 👉 Limit GPU memory usage to 1024 MB (1 GB)
        ocrEngine.Settings.GpuMemoryLimitMb = 1024;

        // Load the receipt image and run OCR
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

        // Output the plain‑text result
        Console.WriteLine(result.Text);
    }
}
```

Perhatikan komentar `// 👉 Limit GPU memory usage…`—baris itu adalah jawaban untuk kata kunci utama. Dengan mengatur `GpuMemoryLimitMb` Anda memberi tahu mesin inferensi di bawahnya untuk mengalokasikan paling banyak jumlah yang ditentukan, memungkinkan beberapa pekerjaan bersamaan berjalan tanpa menghabiskan memori GPU.

## Langkah 3: **Cara mengaktifkan percepatan GPU** (dan mengapa itu penting)

Anda mungkin bertanya, “Mengapa tidak hanya memakai CPU?” Jawabannya adalah kecepatan. Pada RTX 3080 modern, struk yang sama diproses dalam kurang dari 200 ms dibandingkan 1,2 detik pada CPU 4‑core.  

Mengaktifkan percepatan GPU semudah mengubah enum `EngineMode`:

```csharp
ocrEngine.Settings.Engine = EngineMode.Gpu;
```

Aspose secara otomatis memilih backend terbaik:

| Backend yang Terdeteksi | Apa yang Dilakukan |
|--------------------------|--------------------|
| CUDA (NVIDIA)            | Menggunakan kernel cuDNN untuk OCR, terbaik untuk Windows/Linux dengan kartu NVIDIA |
| DirectML (Windows)       | Memanfaatkan DirectX 12, bekerja pada GPU AMD/Intel tanpa driver tambahan |
| None (fallback)          | Kembali ke jalur CPU yang dioptimalkan |

Jika tidak ada CUDA maupun DirectML, engine secara diam-diam beralih ke CPU—tidak ada crash, hanya performa yang lebih lambat.

## Langkah 4: **Run OCR on image** dan **ekstrak teks dari struk**

Dengan engine yang sudah dikonfigurasi, memberi gambar menjadi sangat mudah. Metode `RecognizeImage` menerima path file, `Stream`, atau bahkan `Bitmap`. Berikut panggilan minimalnya:

```csharp
var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

Berasumsi struk berisi:

```
Store XYZ
Date: 2026-04-30
Total: $23.45
```

Anda akan melihat output serupa dengan:

```
=== OCR Output ===
Store XYZ
Date: 2026-04-30
Total: $23.45
```

Jika teks terlihat berantakan, pastikan gambar memiliki kontras tinggi dan orientasi yang tepat—OCR menyukai pemindaian bersih.

## Langkah 5: Verifikasi Batas Memori dan Tangani Kasus Edge

Setelah run pertama, Anda dapat menanyakan berapa banyak memori GPU yang sebenarnya dipakai engine:

```csharp
Console.WriteLine($"GPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
```

Jika Anda berencana memproses puluhan struk secara paralel, Anda mungkin ingin menurunkan batas menjadi 512 MB dan menjalankan beberapa instance engine. Ingat bahwa setiap instance menghormati batas global yang sama; pustaka akan menyesuaikan alokasi secara otomatis.

> **Kesalahan umum:** Menetapkan batas terlalu rendah (misalnya, 100 MB) dapat menyebabkan engine beralih ke CPU di tengah‑run, menghasilkan performa yang tidak konsisten. Uji dengan beban kerja realistis sebelum mengunci nilai tersebut.

## Contoh Lengkap yang Siap Pakai

Berikut adalah program konsol lengkap yang dapat Anda salin‑tempel. Ganti `YOUR_DIRECTORY` dengan path aktual ke gambar struk Anda.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step‑by‑step demo
            GpuExample.Run();

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }

    class GpuExample
    {
        public static void Run()
        {
            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable GPU acceleration (auto‑detects CUDA or DirectML)
            ocrEngine.Settings.Engine = EngineMode.Gpu;

            // 3️⃣ Limit GPU memory usage to 1 GB for concurrent jobs
            ocrEngine.Settings.GpuMemoryLimitMb = 1024;

            // 4️⃣ Load the image and run OCR
            var recognitionResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

            // 5️⃣ Output the recognized plain‑text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognitionResult.Text);

            // 6️⃣ Optional: Show how much GPU memory was actually used
            Console.WriteLine($"\nGPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
        }
    }
}
```

Simpan file, jalankan `dotnet run`, dan Anda akan melihat teks struk yang diekstrak tercetak di konsol, bersama laporan kecil penggunaan memori GPU.

## Pemecahan Masalah & FAQ

**T: GPU saya tidak terdeteksi—kenapa?**  
J: Pastikan driver NVIDIA terbaru (untuk CUDA) atau Windows 10 1809+ (untuk DirectML) sudah terpasang. Juga verifikasi bahwa DLL `Aspose.OCR` cocok dengan arsitektur proses Anda (disarankan x64).

**T: Output kosong.**  
J: Periksa kualitas gambar—struk yang blur atau terrotasi sering memerlukan pra‑pemrosesan (deskew, binarisasi). Aspose menyediakan `ImagePreprocessor` yang dapat Anda sambungkan sebelum `RecognizeImage`.

**T: Bisakah saya menjalankannya di Linux?**  
J: Ya, selama Anda memiliki GPU NVIDIA dengan CUDA 11+ terpasang. Kode yang sama berfungsi tanpa perubahan.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **membatasi penggunaan memori GPU** sambil **run OCR on image** menggunakan Aspose.OCR di C#. Dari instalasi paket NuGet hingga konfigurasi engine, mengaktifkan percepatan GPU, dan akhirnya **mengekstrak teks dari struk**, panduan ini memberi Anda solusi siap pakai yang ramah memori dan sangat cepat.

Selanjutnya, Anda dapat menjelajahi topik **c# OCR tutorial** yang lebih maju—seperti pemrosesan batch, paket bahasa khusus, atau mengintegrasikan hasil ke dalam basis data. Bereksperimenlah dengan nilai `GpuMemoryLimitMb` yang berbeda untuk menemukan titik optimal bagi beban kerja Anda, dan pantau diagnostik memori‑used agar tidak ada kejutan.

Selamat coding, semoga GPU Anda tetap dingin sementara OCR Anda tetap tajam!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}