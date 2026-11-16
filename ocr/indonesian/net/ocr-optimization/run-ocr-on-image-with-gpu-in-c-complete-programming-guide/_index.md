---
category: general
date: 2026-03-26
description: Jalankan OCR pada gambar menggunakan dukungan GPU Aspose OCR di C#. Pelajari
  cara memuat gambar untuk OCR, mengatur ID perangkat GPU, dan mengekstrak teks dari
  gambar dengan cepat.
draft: false
keywords:
- run OCR on image
- extract text from image
- load image for OCR
- recognize text from document
- set GPU device ID
language: id
og_description: Jalankan OCR pada gambar menggunakan Aspose OCR GPU di C#. Panduan
  ini menunjukkan cara memuat gambar untuk OCR, mengatur ID perangkat GPU, dan mengekstrak
  teks dari gambar secara efisien.
og_title: Jalankan OCR pada Gambar dengan GPU di C# – Panduan Lengkap
tags:
- C#
- OCR
- GPU
- Aspose
title: Jalankan OCR pada Gambar dengan GPU di C# – Panduan Pemrograman Lengkap
url: /id/net/ocr-optimization/run-ocr-on-image-with-gpu-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar dengan GPU di C# – Panduan Pemrograman Lengkap

Pernahkah Anda perlu **run OCR on image** file tetapi menemukan versi CPU sangat lambat? Anda tidak sendirian. Dalam banyak aplikasi dunia nyata—pikirkan pemindai faktur atau arsip dokumen berskala besar—bottlenecknya adalah mesin OCR itu sendiri.  

Dalam tutorial ini kami akan membahas **complete, runnable example** yang menunjukkan cara **load image for OCR**, secara opsional **set GPU device ID**, dan akhirnya **extract text from image** menggunakan API Aspose OCR yang dipercepat GPU. Pada akhirnya Anda akan dapat **recognize text from document** gambar dalam sebagian kecil waktu dibandingkan pendekatan CPU murni.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mereferensikan paket Aspose.OCR dan Aspose.OCR.Gpu.  
- Langkah‑langkah tepat untuk **run OCR on image** dengan akselerasi GPU.  
- Mengapa memilih **GPU device ID** yang tepat penting pada mesin multi‑GPU.  
- Tips menangani file besar, strategi fallback, dan jebakan umum.  

### Prasyarat

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 atau lebih baru | Fitur bahasa modern dan kinerja yang lebih baik |
| Visual Studio 2022 (atau IDE C# apa saja) | Untuk memudahkan penyiapan proyek |
| NVIDIA GPU dengan dukungan CUDA (opsional) | Hanya diperlukan jika Anda menginginkan akselerasi GPU |
| Paket NuGet Aspose.OCR & Aspose.OCR.Gpu | Menyediakan kelas `GpuOcrEngine` |

Jika Anda tidak memiliki GPU, jangan panik—kode akan secara elegan beralih ke mesin CPU, yang akan kami bahas nanti.

---

## Langkah 1: Instal Paket Aspose OCR

Sebelum Anda dapat **run OCR on image**, Anda memerlukan pustaka-pustaka tersebut. Buka terminal Anda (atau Package Manager Console) dan jalankan:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Kedua paket ini menyertakan mesin OCR inti dan ekstensi khusus GPU. Setelah instalasi, Anda akan melihat referensi berikut di `.csproj` Anda:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
  <PackageReference Include="Aspose.OCR.Gpu" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** Jaga agar versi paket tetap sinkron; versi yang tidak cocok dapat menyebabkan kesalahan runtime.

---

## Langkah 2: Buat Mesin OCR yang Didukung GPU

Sekarang pustaka sudah tersedia, mari **run OCR on image** menggunakan GPU. Kelas `GpuOcrEngine` adalah titik masuk untuk pemrosesan yang dipercepat.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Instantiate the GPU OCR engine
        var gpuEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Choose which GPU to use – 0 = first GPU
        // This is where the "set GPU device ID" keyword comes into play.
        gpuEngine.DeviceId = 0;

        // The rest of the workflow continues in the following steps...
```

**Mengapa GPU?**  
Inti GPU unggul dalam operasi piksel paralel, yang tepat dibutuhkan OCR saat memindai gambar beresolusi tinggi. Dengan mengatur `DeviceId`, Anda memberi tahu pustaka kartu fisik mana yang akan digunakan—praktis pada workstation dengan banyak GPU.

---

## Langkah 3: Muat Gambar untuk OCR

Sebelum pengenalan, Anda harus **load image for OCR**. Aspose menyediakan metode pabrik statis yang nyaman yang mendukung banyak format (JPEG, PNG, TIFF, dll.).

```csharp
        // Step 3: Load the image you want to recognize
        // Replace the path with your actual file location.
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");

        // Quick sanity check – ensure the image was loaded.
        if (ocrImage == null)
        {
            Console.WriteLine("Failed to load image. Check the file path.");
            return;
        }
```

> **Edge case:** Jika gambar lebih besar dari 10 MB, pertimbangkan untuk menurunkan resolusinya terlebih dahulu agar tidak kehabisan memori GPU. Anda dapat melakukannya dengan `ocrImage.Resize(width, height)` sebelum pengenalan.

---

## Langkah 4: Kenali Teks dari Dokumen

Dengan mesin siap dan gambar dimuat, saatnya **recognize text from document**. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi output teks polos dan metadata tambahan.

```csharp
        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);

        // Verify that OCR succeeded
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR failed or returned empty result.");
            return;
        }
```

**Apa yang terjadi di balik layar?**  
Mesin GPU mengalirkan data piksel ke kernel CUDA, yang melakukan binarisasi, segmentasi karakter, dan inferensi jaringan saraf—semua secara paralel. Inilah mengapa Anda dapat **run OCR on image** file yang sebaliknya akan memakan detik pada CPU.

---

## Langkah 5: Ekstrak Teks dari Gambar dan Output

Akhirnya, kami **extract text from image** dan menampilkannya. Anda juga dapat menulis hasilnya ke file, basis data, atau mengirimnya ke pipeline NLP selanjutnya.

```csharp
        // Step 5: Output the recognized plain‑text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // Optional: Save to a .txt file for later processing
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

Jika Anda menjalankan program dan melihat blok serupa, selamat—Anda telah berhasil **run OCR on image** menggunakan akselerasi GPU!

---

## Menangani Situasi Tanpa GPU (Fallback)

Bagaimana jika mesin tempat Anda melakukan deployment tidak memiliki GPU yang kompatibel? Konstruktor `GpuOcrEngine` akan melempar `GpuNotSupportedException`. Bungkus inisialisasi dalam try‑catch dan kembali ke `OcrEngine` (CPU) seperti berikut:

```csharp
        try
        {
            var gpuEngine = new GpuOcrEngine { DeviceId = 0 };
            // Continue with GPU workflow...
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not available – switching to CPU OCR.");
            var cpuEngine = new OcrEngine();
            OcrResult result = cpuEngine.Recognize(ocrImage);
            Console.WriteLine(result.Text);
        }
```

Pola ini memastikan aplikasi Anda tetap berfungsi terlepas dari perangkat keras, pertimbangan penting untuk deployment di cloud.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah **entire program**—tidak ada bagian yang hilang, cukup ganti jalur file dengan milik Anda.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Create a GPU‑enabled OCR engine
        GpuOcrEngine gpuEngine;
        try
        {
            gpuEngine = new GpuOcrEngine { DeviceId = 0 }; // set GPU device ID
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not detected. Falling back to CPU engine.");
            var cpuEngine = new OcrEngine();
            RunCpuOcr(cpuEngine);
            return;
        }

        // 2️⃣ Load image for OCR
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        if (ocrImage == null)
        {
            Console.WriteLine("Unable to load image – check the path.");
            return;
        }

        // 3️⃣ Recognize text from document
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR returned no text.");
            return;
        }

        // 4️⃣ Extract text from image and output
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }

    // Helper for CPU fallback
    static void RunCpuOcr(OcrEngine cpuEngine)
    {
        var img = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        var result = cpuEngine.Recognize(img);
        Console.WriteLine("=== CPU OCR Result ===");
        Console.WriteLine(result.Text);
    }
}
```

> **Catatan:** Kode di atas secara otomatis **extracts text from image** dan menuliskannya ke `ocr_result.txt`. Sesuaikan jalur sesuai kebutuhan.

---

## Pertanyaan yang Sering Diajukan & Tips

| Question | Answer |
|----------|--------|
| *Apakah saya memerlukan driver NVIDIA khusus?* | Ya—CUDA 11.x atau yang lebih baru disarankan. Periksa catatan rilis Aspose untuk kompatibilitas tepatnya. |
| *Bisakah saya memproses banyak gambar secara bersamaan?* | Tentu saja. Bungkus panggilan OCR dalam loop `Parallel.ForEach`, tetapi perhatikan batas memori GPU. |
| *Bagaimana jika hasil OCR berisi karakter yang rusak?* | Coba sesuaikan pra‑pemrosesan gambar: `ocrImage.Binarize()` atau `ocrImage.Deskew()` sebelum pengenalan. |
| *Apakah ada cara membatasi model bahasa?* | Atur `gpuEngine.Language = OcrLanguage.English;` untuk mempercepat pemrosesan jika Anda hanya membutuhkan bahasa Inggris. |

---

## Kesimpulan

Anda sekarang memiliki **complete, end‑to‑end solution** untuk **run OCR on image**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}