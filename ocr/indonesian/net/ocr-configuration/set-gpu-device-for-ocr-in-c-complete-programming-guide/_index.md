---
category: general
date: 2026-03-18
description: Atur perangkat GPU di Aspose OCR untuk mengekstrak teks dari gambar dengan
  cepat. Pelajari cara memuat gambar untuk OCR, mengenali gambar struk, dan mendapatkan
  hasil yang akurat.
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: id
og_description: Atur perangkat GPU di Aspose OCR untuk mengekstrak teks dari gambar
  dengan cepat. Ikuti panduan langkah demi langkah ini untuk memuat gambar untuk OCR
  dan mengenali gambar struk.
og_title: Atur Perangkat GPU untuk OCR di C# – Panduan Pemrograman Lengkap
tags:
- OCR
- C#
- GPU
- Aspose
title: Mengatur Perangkat GPU untuk OCR di C# – Panduan Pemrograman Lengkap
url: /id/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengatur Perangkat GPU untuk OCR di C# – Panduan Pemrograman Lengkap

Perlu **mengatur perangkat GPU** untuk pemrosesan OCR yang lebih cepat? Pada panduan ini kami akan menunjukkan cara mengatur perangkat GPU menggunakan Aspose OCR, kemudian mengekstrak teks dari gambar struk dalam beberapa baris kode.  

Jika Anda pernah mengalami kesulitan **memuat gambar untuk OCR** atau bertanya‑tanya *bagaimana mengekstrak teks* dari pemindaian resolusi tinggi, Anda berada di tempat yang tepat. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan, yang mengenali gambar struk, mencetak teks polos, dan beralih secara mulus jika GPU tidak tersedia.

## Apa yang Dibahas Tutorial Ini

Kami akan membahas semua yang perlu Anda ketahui:

* Menginstal paket NuGet Aspose OCR (satu‑satunya dependensi eksternal).  
* Mengatur perangkat GPU (`set GPU device`) dan secara opsional memilih indeks GPU yang berbeda.  
* Memuat file gambar untuk OCR – ya, termasuk langkah “memuat gambar untuk OCR” yang sering membuat pemula kebingungan.  
* Menjalankan mesin pengenalan untuk **mengenali gambar struk**.  
* Mengekstrak string hasil sehingga Anda dapat **mengekstrak teks dari gambar** dan menggunakannya dalam aplikasi Anda.  

Tidak ada sulap, tidak ada tautan dokumen tersembunyi – hanya solusi lengkap yang dapat Anda salin‑tempel ke Visual Studio dan jalankan hari ini.

## Prasyarat

* .NET 6.0 atau lebih baru (kode ini juga berfungsi pada .NET Core dan .NET Framework).  
* Mesin yang mendukung GPU dengan driver yang sesuai terpasang – jika tidak, pustaka akan otomatis beralih ke mode CPU.  
* Contoh gambar struk (misalnya `receipt_highres.png`) yang ditempatkan di lokasi yang dapat Anda referensikan dengan jalur lengkap.  

Itu saja. Jika Anda belum memiliki paket NuGet, jalankan `dotnet add package Aspose.OCR` di folder proyek Anda.

---

## Langkah 1 – Mengatur Perangkat GPU di Aspose OCR

Hal pertama yang harus Anda lakukan adalah **mengatur perangkat GPU** pada mesin OCR. Ini memberi tahu Aspose untuk memindahkan beban kerja berat ke kartu grafis alih‑alih CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**Mengapa ini penting:**  
Ketika mesin berjalan dalam `ProcessingMode.Gpu`, kernel CUDA yang mendasarinya dapat mempercepat segmentasi karakter dan inferensi jaringan saraf secara dramatis. Pada RTX 3080 modern, waktu OCR akan turun dari hitungan detik menjadi sub‑detik untuk struk resolusi tinggi.

> **Tip profesional:** Jika Anda tidak yakin indeks GPU mana yang harus dipakai, panggil `OcrEngine.GetAvailableGpuDevices()` (tersedia pada versi terbaru) dan pilih yang memiliki memori bebas terbanyak.

---

## Langkah 2 – Memuat Gambar untuk OCR

Setelah mesin dikonfigurasi, kita perlu **memuat gambar untuk OCR**. Aspose menyediakan pembungkus `ImageStream` yang memudahkan I/O file dan mendukung aliran dari memori, jaringan, atau disk.

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**Apa yang bisa salah?**  
Jika jalur file salah atau gambar rusak, `FromFile` akan melempar `FileNotFoundException`. Pemeriksaan cepat `File.Exists(imagePath)` sebelum membuat aliran akan menyelamatkan Anda dari crash yang tidak diinginkan.

---

## Langkah 3 – Mengenali Gambar Struk

Dengan gambar di tangan, kita panggil `Recognize`. Inilah langkah yang benar‑benar **mengenali gambar struk** menggunakan pipeline yang dipercepat GPU yang telah kami siapkan sebelumnya.

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**Di balik layar:**  
Mesin pertama‑tama mengonversi gambar menjadi bitmap grayscale ternormalkan, kemudian menjalankan model deep‑learning yang memprediksi probabilitas karakter. Karena kami berada di GPU, model memproses seluruh bitmap secara paralel, itulah mengapa struk besar selesai dengan cepat.

---

## Langkah 4 – Mengekstrak Teks dari Gambar dan Memverifikasi Output

Akhirnya, kami mengambil hasil teks polos dari `OcrResult` dan menuliskannya ke konsol. Inilah saat Anda **mengekstrak teks dari gambar** dan dapat mengirimkannya ke logika selanjutnya (misalnya, parsing item baris).

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**Output yang diharapkan:**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

Jika teks terlihat berantakan, periksa kembali bahwa gambar beresolusi tinggi dan driver GPU sudah terbaru. Anda juga dapat mengubah `ocrEngine.Settings.PreprocessMode` untuk meningkatkan kontras pada struk yang pencahayaannya buruk.

---

## Langkah 5 – Beralih ke CPU (Penanganan Kasus Edge)

Bagaimana jika mesin target tidak memiliki GPU yang kompatibel? Alih‑alih dari crash, Anda dapat mendeteksi situasi tersebut dan beralih ke pemrosesan CPU.

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**Mengapa menyertakan ini?**  
Pada pipeline CI atau kontainer cloud Anda sering menjalankan pada server tanpa GPU. Penurunan kualitas yang mulus memastikan kode yang sama berfungsi di mana saja.

---

## Kesalahan Umum dan Tips Praktis

| Kesalahan | Cara Menghindarinya |
|-----------|---------------------|
| Lupa mengatur `ProcessingMode` sebelum memuat gambar. | Selalu konfigurasi mesin terlebih dahulu (Langkah 1). |
| Menggunakan indeks GPU yang salah (`GpuDeviceId`). | Query perangkat yang tersedia atau gunakan default `0`. |
| Memuat gambar beresolusi rendah, yang menurunkan akurasi OCR. | Targetkan setidaknya 300 DPI untuk struk. |
| Tidak membuang `ImageStream` – menyebabkan file terkunci. | Bungkus aliran dalam blok `using` atau panggil `Dispose()` secara manual. |
| Mengabaikan flag `IsGpuAvailable` pada mesin tanpa CUDA. | Tambahkan logika fallback dari Langkah 5. |

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut seluruh program, siap untuk dikompilasi. Simpan sebagai `Program.cs`, tambahkan paket NuGet Aspose OCR, dan jalankan.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

Menjalankan program akan mencetak teks struk yang diekstrak ke konsol, persis seperti yang ditunjukkan sebelumnya. Anda kini dapat menyalurkan string tersebut ke parser, basis data, atau logika bisnis lain yang Anda perlukan.

---

## Kesimpulan

Kami telah menunjukkan cara **mengatur perangkat GPU** di Aspose OCR, **memuat gambar untuk OCR**, dan **mengenali gambar struk** sehingga Anda dapat **mengekstrak teks dari gambar** dengan kecepatan tinggi. Contoh lengkap yang dapat dijalankan memperlihatkan baik “bagaimana” maupun “mengapa”, memberikan fondasi yang kuat untuk proyek OCR C# apa pun yang memerlukan akselerasi GPU.

Siap untuk langkah selanjutnya? Cobalah bereksperimen dengan:

* Memproses beberapa gambar secara paralel menggunakan `Parallel.ForEach`.  
* Menyetel `ocrEngine.Settings.PreprocessMode` untuk meningkatkan hasil pada pemindaian kontras rendah.  
* Mengekspor output OCR ke JSON untuk analitik selanjutnya.  

Jangan ragu meninggalkan komentar jika Anda menemukan kendala, dan selamat coding!

![Diagram yang menunjukkan cara mengatur perangkat GPU untuk pemrosesan OCR](set-gpu-device.png "set GPU device")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}