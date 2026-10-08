---
category: general
date: 2026-01-02
description: Jalankan OCR pada PNG dengan cepat menggunakan Aspose OCR dan dukungan
  GPU. Pelajari cara mengenali teks dari gambar, mengekstrak teks dari gambar, dan
  mengatur batas memori GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: id
og_description: Jalankan OCR pada PNG secara efisien dengan memanfaatkan Aspose OCR
  dan akselerasi GPU. Tutorial ini menunjukkan cara mengenali teks dari gambar, mengekstrak
  teks dari gambar, dan mengontrol penggunaan memori GPU.
og_title: Jalankan OCR pada PNG dengan GPU – Panduan Lengkap C#
tags:
- OCR
- C#
- GPU
title: Jalankan OCR pada PNG dengan GPU – Panduan Lengkap C#
url: /id/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada PNG dengan GPU – Panduan Lengkap C#

Pernah membutuhkan **run OCR on PNG** file tetapi merasa terhambat oleh kinerja? Anda tidak sendirian. Dalam banyak alur kerja dunia nyata, satu PNG beresolusi tinggi dapat memperlambat mesin OCR yang hanya menggunakan CPU, mengubah apa yang seharusnya menjadi pencarian cepat menjadi penantian selama satu menit.  

Kabar baiknya, Aspose OCR dilengkapi dengan ekstensi GPU yang memungkinkan Anda **recognize text from image** dalam sebagian kecil waktu. Dalam tutorial ini kami akan menuntun Anda melalui contoh langsung yang menunjukkan secara tepat cara **run OCR on PNG** menggunakan C#, cara **extract text from image**, dan bahkan cara **set GPU memory limit** sehingga Anda tetap berada dalam batas perangkat keras Anda.

Kami juga akan membahas “bagaimana” dan “mengapa” di balik setiap langkah, sehingga Anda memperoleh model mental yang solid—bukan sekadar cuplikan copy‑paste.

## Apa yang Akan Anda Pelajari

- Prasyarat untuk menggunakan dukungan GPU Aspose OCR.  
- Cara memuat PNG ke dalam `Bitmap` dan memberikannya ke mesin OCR.  
- Cara mengonfigurasi `GpuDevice` dan `GpuMemoryLimitMb` untuk kinerja optimal.  
- Cara **recognize text from image** dan mengambil hasil teks polos.  
- Tips menangani kasus umum seperti GPU dengan memori rendah atau PNG multi‑halaman.  

Pada akhir panduan ini Anda akan dapat **run OCR on PNG** dengan kecepatan GPU dan mengendalikan jejak memori pekerjaan OCR Anda dengan percaya diri.

![Diagram yang menunjukkan menjalankan OCR pada PNG dengan percepatan GPU](run-ocr-on-png-diagram.png "contoh menjalankan OCR pada PNG")

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

1. .NET 6.0 atau yang lebih baru (kode ini juga berfungsi dengan .NET Core dan .NET Framework).  
2. GPU NVIDIA dengan dukungan CUDA (contoh ini memilih indeks perangkat 0).  
3. Paket NuGet Aspose.OCR dan ekstensi GPU‑nya (`Aspose.OCR.Extensions`).  
4. Contoh PNG (`input.png`) yang ditempatkan di folder yang dapat Anda referensikan dari proyek Anda.  

Jika ada yang terdengar tidak familiar, jangan khawatir—kami akan mencatat alternatif bila relevan.

---

## Langkah 1 – Instal Aspose OCR dan Ekstensi GPU

Hal pertama yang harus dilakukan. Tanpa pustaka yang tepat, sisa kode tidak akan dapat dikompilasi.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

Paket `Aspose.OCR.Extensions` menyertakan binary CUDA native yang diperlukan untuk percepatan GPU.  
*Pro tip:* Jika Anda berada di mesin tanpa GPU, Anda masih dapat mengompilasi proyek; cukup set `PreferGpu = false` nanti.

---

## Langkah 2 – Muat PNG yang Ingin Diproses

Sekarang kita benar‑benar **run OCR on PNG** dengan memuatnya ke dalam `Bitmap`. Langkah ini sederhana tetapi patut dicatat: `Bitmap` mengharapkan jalur file, jadi pastikan jalurnya benar relatif terhadap executable Anda.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Jika PNG sangat besar (misalnya, > 5000 px pada satu sisi), Anda mungkin ingin menurunkannya terlebih dahulu agar tidak menghabiskan memori GPU. Di sinilah opsi **set GPU memory limit** menjadi berguna nanti.

---

## Langkah 3 – Buat dan Konfigurasikan Mesin OCR untuk Penggunaan GPU

Berikut inti tutorial: mengonfigurasi mesin OCR untuk **recognize text from image** menggunakan GPU. Dua properti menjadi kunci:

- `GpuDevice` – memilih perangkat CUDA mana yang akan digunakan.  
- `GpuMemoryLimitMb` – membatasi jumlah memori GPU yang dapat dialokasikan mesin.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Mengapa menetapkan batas memori?** Beberapa GPU berbagi memori dengan tampilan atau menjalankan beban kerja berganda secara bersamaan. Dengan membatasi alokasi, Anda mencegah crash karena kehabisan memori, terutama saat memproses banyak PNG secara paralel.

---

## Langkah 4 – Tentukan Opsi Pengakuan (Bahasa & Preferensi GPU)

Objek `RecognitionOptions` memberi tahu mesin bahasa apa yang dicari dan apakah harus **prefer GPU** bahkan untuk gambar kecil. Untuk kebanyakan dokumen berbahasa Inggris ini sudah cukup, tetapi Anda dapat mengganti `Language.English` dengan locale lain yang didukung.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Jika Anda perlu **extract text from image** dalam bahasa selain Inggris, cukup ubah enum `Language`. Perpustakaan ini mendukung puluhan bahasa secara bawaan.

---

## Langkah 5 – Jalankan OCR dan Dapatkan Hasilnya

Dengan semua komponen terhubung, panggilan akhir cukup satu baris yang sebenarnya **run OCR on PNG** dan mengembalikan objek hasil yang kaya.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` tidak hanya berisi teks polos (`ocrResult.Text`) tetapi juga skor kepercayaan, bounding box, dan bahkan gambar asli dengan kata‑kata yang disorot—berguna bila Anda perlu men-debug atau memvisualisasikan ekstraksi.

**Output yang diharapkan** (untuk contoh PNG yang menampilkan “Hello World”):

```
=== OCR Output ===
Hello World
```

Jika teks terlihat kacau, periksa kembali apakah PNG tidak rusak dan apakah batas memori GPU tidak terlalu rendah untuk ukuran gambar tersebut.

---

## Langkah 6 – Menangani Kasus Edge dan Tips Praktik Terbaik

### GPU dengan Memori Rendah

Jika Anda melihat pengecualian seperti `CudaException: out of memory`, turunkan `GpuMemoryLimitMb` atau bagi PNG menjadi ubin sebelum diproses. Tiling dapat dilakukan dengan `Graphics.DrawImage` pada klon `Bitmap`.

### Beberapa PNG dalam Batch

Saat memproses folder berisi PNG, gunakan kembali instance `OcrEngine` yang sama—menginisialisasinya sekali menghemat pergantian konteks GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Fallback ke CPU

Jika GPU tidak tersedia, cukup set `PreferGpu = false`. Mesin akan otomatis beralih ke CPU tanpa perubahan kode apa pun.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Contoh Lengkap yang Berfungsi

Berikut program lengkap yang dapat Anda copy‑paste ke proyek konsol baru. Program ini mencakup semua langkah di atas, plus beberapa pemeriksaan keamanan.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Simpan file sebagai `Program.cs`, jalankan `dotnet run`, dan Anda akan melihat teks yang diekstrak tercetak di konsol.

---

## Kesimpulan

Kami baru saja mendemonstrasikan cara **run OCR on PNG** menggunakan ekstensi GPU Aspose OCR, cara **recognize text from image**, dan cara **extract text from image** sambil mengendalikan **set GPU memory limit**. Dengan mengonfigurasi `GpuDevice` dan `GpuMemoryLimitMb` Anda menjaga aplikasi tetap cepat dan stabil, bahkan pada GPU yang sederhana.

Dari sini Anda dapat:

- Bereksperimen dengan bahasa lain (`Language.French`, `Language.Spanish`).  
- Mengintegrasikan langkah OCR ke dalam pipeline pemrosesan dokumen yang lebih besar.  
- Menambahkan pasca‑pemrosesan seperti pemeriksaan ejaan atau ekstraksi entitas untuk memoles teks mentah.  

Ingat, kuncinya bukan hanya kode tetapi memahami mengapa setiap pengaturan penting. Ketika Anda tahu cara **set GPU memory limit** dan kapan harus beralih ke CPU, Anda akan membangun solusi OCR yang dapat diskalakan dengan elegan.

Ada pertanyaan tentang ukuran PNG tertentu, TIFF multi‑halaman, atau cara mengatasi error GPU? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}