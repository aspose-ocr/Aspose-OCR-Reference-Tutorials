---
category: general
date: 2026-04-01
description: Pelajari cara mengenali teks dari file PNG dengan cepat dengan mengatur
  ID perangkat GPU dan mengaktifkan percepatan GPU di Aspose OCR. Panduan C# langkah
  demi langkah.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: id
og_description: Mengenali teks dari file PNG dengan cepat dengan mengatur ID perangkat
  GPU. Ikuti panduan lengkap C# ini untuk mengaktifkan percepatan GPU dengan Aspose
  OCR.
og_title: Mengenali teks dari PNG – Tutorial OCR Aspose yang Dipercepat GPU
tags:
- C#
- OCR
- GPU
- Aspose
title: Mengenali teks dari PNG dengan Aspose OCR – Demo Batch Berakselerasi GPU
url: /id/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari png – Tutorial Batch C# dengan Akselerasi GPU Lengkap

Pernah perlu **mengenali teks dari png** gambar tetapi menemukan prosesnya sangat lambat? Anda tidak sendirian. Kebanyakan pengembang memulai dengan panggilan OCR sederhana, lalu menatap konsol yang berjalan lambat seperti siput ketika sebuah folder berisi puluhan tangkapan layar.  

Berita baik? Aspose OCR dapat memindahkan beban kerja berat ke kartu grafis Anda, dan dengan hanya beberapa baris Anda dapat **set gpu device id** untuk memilih GPU yang tepat. Dalam panduan ini kami akan membahas contoh lengkap yang dapat dijalankan yang mengambil setiap PNG dari sebuah folder, mengaktifkan akselerasi GPU, memilih GPU pertama, dan mencetak jumlah karakter untuk setiap file.

Pada akhir tutorial Anda akan memiliki program mandiri yang dapat Anda masukkan ke dalam proyek .NET apa pun, dan Anda akan memahami mengapa mengaktifkan GPU penting, cara menangani kasus tepi, dan apa yang perlu disesuaikan untuk kinerja yang lebih baik.

## Apa yang Anda Butuhkan

- **.NET 6.0** atau lebih baru (kode juga dapat dikompilasi dengan .NET Core).  
- Paket NuGet **Aspose.OCR** – instal dengan `dotnet add package Aspose.OCR`.  
- Mesin dengan GPU yang kompatibel CUDA (biasanya NVIDIA) dan driver yang sesuai.  
- Folder penuh dengan gambar **PNG** yang ingin Anda proses.  

Jika ada yang tidak familiar, jangan panik. Langkah-langkah di bawah ini mencakup perintah tepat yang Anda butuhkan, dan kami juga akan membahas apa yang harus dilakukan ketika GPU tidak tersedia.

## Langkah 1: Inisialisasi OCR Engine dan Aktifkan Akselerasi GPU  

Hal pertama yang harus Anda lakukan adalah membuat instance `OcrEngine` dan mengaktifkan dukungan GPU. Flag ini memberi tahu Aspose untuk menggunakan pustaka CUDA native di balik layar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Mengapa ini penting:** Tanpa `UseGpuAcceleration`, setiap gambar diproses di CPU, yang dapat menjadi jauh lebih lambat, terutama untuk PNG beresolusi tinggi. Mengaktifkan flag ini juga menyiapkan engine untuk menerima perangkat GPU tertentu nanti.

## Langkah 2: Atur GPU Device ID (Opsional tetapi Disarankan)  

Jika workstation Anda memiliki lebih dari satu GPU, Anda dapat memutuskan mana yang akan digunakan. ID perangkat dimulai dari **0**, jadi `0` memilih GPU pertama, `1` yang kedua, dan seterusnya.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Tips profesional:** Saat dijalankan di server bersama, secara eksplisit mengatur GPU device ID dapat mencegah pekerjaan Anda mengambil sumber daya dari proses lain. Jika Anda menghilangkan baris ini, Aspose akan memilih perangkat default, yang biasanya cukup untuk setup satu‑GPU.

## Langkah 3: Kumpulkan Semua File PNG dari Folder Batch Anda  

Selanjutnya kita perlu menemukan setiap PNG yang ingin Anda proses dengan OCR. Metode `Directory.GetFiles` melakukan pekerjaan berat tersebut.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Kasus tepi:** Jika folder kosong, `imageFiles` akan menjadi array kosong. Kami akan menangani itu nanti dengan pesan yang ramah.

## Langkah 4: Proses Setiap Gambar dan Tampilkan Jumlah Karakter yang Dikenali  

Sekarang inti perulangan. Untuk setiap PNG kita memanggil `Recognize`, lalu mencetak nama file dan panjang teks yang diekstrak.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Apa yang akan Anda lihat:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Jika sebuah gambar tidak mengandung teks, hitungannya akan `0`. Itu normal untuk tangkapan layar yang sepenuhnya grafis.

## Langkah 5: Jalankan Program dan Verifikasi Penggunaan GPU  

Kompilasi file (`dotnet build`) dan jalankan (`dotnet run`). Saat konsol bergulir, Anda dapat membuka alat pemantauan GPU (seperti NVIDIA Smi) untuk melihat lonjakan penggunaan GPU sesaat untuk setiap gambar. Jika tidak ada aktivitas, periksa kembali bahwa:

1. Driver CUDA terinstal.  
2. `UseGpuAcceleration` diatur ke `true`.  
3. `GpuDeviceId` yang benar cocok dengan GPU fisik.

Jika GPU tidak tersedia, Aspose akan beralih ke CPU secara otomatis, tetapi Anda akan kehilangan keunggulan kecepatan.

## Variasi Umum & Tips  

| Situation | What to Change |
|-----------|----------------|
| **Format gambar berbeda** (mis., JPEG) | Ubah pola pencarian menjadi `*.jpg` atau `*.*` dan Aspose tetap akan mengenali teks. |
| **Ukuran batch sangat besar** (ribuan file) | Proses dalam potongan untuk menghindari tekanan memori: bagi `imageFiles` menjadi array yang lebih kecil. |
| **Butuh teks sebenarnya, bukan hanya panjangnya** | Ganti `ocrResult.Text.Length` dengan `ocrResult.Text` di dalam `WriteLine`. |
| **Menjalankan di server tanpa tampilan** | Pastikan server memiliki driver GPU; jika tidak, set `UseGpuAcceleration = false` untuk menghindari error yang tidak perlu. |
| **Beberapa GPU, ingin menyeimbangkan beban** | Loop dengan `ocrEngine.GpuDeviceId = i % gpuCount` di dalam `foreach` untuk memutar perangkat. |

## Output yang Diharapkan & Verifikasi  

Ketika semuanya berjalan, konsol mencetak setiap nama file diikuti oleh jumlah karakter, seperti yang ditunjukkan sebelumnya. Untuk memeriksa kembali output OCR sebenarnya, Anda dapat sementara menampilkan teks:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Ingatlah untuk menghapus atau mengomentari baris itu untuk batch besar; mencetak ribuan baris dapat membanjiri terminal Anda.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Simpan ini sebagai `GpuBatchDemo.cs`, jalankan `dotnet add package Aspose.OCR`, lalu `dotnet run`. Anda akan melihat jumlah karakter muncul hampir seketika untuk setiap PNG, berkat akselerasi GPU.

## Kesimpulan  

Anda kini tahu cara **mengenali teks dari png** secara efisien dengan mengaktifkan akselerasi GPU dan secara eksplisit **set gpu device id** di Aspose OCR. Program lengkap yang dapat disalin‑tempel ini menangani penemuan folder, pemeriksaan kasus tepi, dan memberi Anda umpan balik langsung tentang kinerja OCR.  

Langkah selanjutnya? Coba ganti panggilan `Recognize` dengan `ocrEngine.RecognizeAsync` jika Anda membutuhkan pemrosesan non‑blocking, atau bereksperimen dengan opsi pra‑pemrosesan gambar yang berbeda (mis., binarisasi) yang disediakan Aspose. Anda juga dapat mengalirkan hasil OCR ke basis data atau indeks pencarian untuk solusi pencarian teks penuh.  

Ada pertanyaan tentang penanganan PDF multi‑halaman, atau ingin membandingkan Aspose OCR dengan Tesseract? Tinggalkan komentar atau jelajahi tutorial lain kami tentang **batch OCR C#**, **tips kinerja OCR**, dan **pemrosesan gambar berbasis GPU**. Selamat coding!  

![Output konsol menampilkan jumlah karakter yang dikenali untuk file PNG – mengenali teks dari png menggunakan akselerasi GPU](image-placeholder.png "contoh output mengenali teks dari png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}