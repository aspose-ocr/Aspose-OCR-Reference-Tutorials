---
category: general
date: 2026-03-05
description: Konversi TIFF ke teks dalam C# dengan Aspose OCR—dengan cepat mengekstrak
  teks dari file gambar yang dipindai dan pelajari cara memuat file gambar di C# untuk
  pemrosesan OCR.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: id
og_description: Konversi TIFF ke teks dalam C# menggunakan Aspose OCR. Pelajari alur
  kerja lengkap untuk mengekstrak teks dari gambar yang dipindai dan memuat file gambar
  secara efisien.
og_title: Konversi TIFF ke Teks di C# – Ekstrak Teks Gambar yang Dipindai
tags:
- OCR
- C#
- Aspose
title: Konversi TIFF ke Teks dalam C# – Ekstrak Teks Gambar yang Dipindai
url: /id/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konversi TIFF ke Teks dalam C# – Ekstrak Teks Gambar Pindai

Perlu **mengonversi TIFF ke teks dalam C#**? Anda bukan satu-satunya yang berjuang dengan gambar pindai multi‑halaman yang keras kepala menolak menjadi string yang dapat dicari.  
Dalam panduan ini kami akan membahas solusi lengkap yang siap dijalankan, yang mengambil file TIFF, memberikannya ke Aspose OCR, dan menghasilkan teks biasa—tanpa layanan tambahan, tanpa keajaiban tersembunyi.

> **Pro tip:** Jika Anda menangani pemindaian resolusi tinggi, mengaktifkan pemrosesan GPU dapat mengurangi beberapa detik per halaman.

Kami juga akan menunjukkan cara **mengekstrak teks dari file gambar pindai** dan cara terbaik untuk **memuat file gambar C#** ke dalam mesin OCR, sehingga Anda dapat menyematkan logika ini ke dalam proyek .NET apa pun hari ini.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut di mesin Anda:

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Runtime modern, mendukung `Span<T>` dan I/O async |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | Mesin OCR yang akan kami gunakan |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | Tanpa itu Anda akan terkena batas evaluasi |
| A TIFF file (single‑ or multi‑page) to test | Contoh yang digunakan: `scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | Mempercepat pengenalan ketika `EngineMode = Gpu` |

Jika Anda belum memiliki salah satu dari ini, dapatkan paket NuGet sekarang:

```bash
dotnet add package Aspose.OCR
```

---

## Langkah 1: Siapkan Proyek dan Impor Namespace

Buat aplikasi console baru (atau tambahkan kode ke proyek yang sudah ada). Hal pertama yang kami lakukan adalah mengimpor kelas‑kelas yang kami butuhkan.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Mengapa ini penting:** Mengimpor `Aspose.OCR.Image` memberi kami pabrik `ImageStream`, yang dapat membaca file TIFF langsung dari disk atau aliran. Melewatkan langkah ini akan menyebabkan kesalahan waktu kompilasi.

---

## Langkah 2: Inisialisasi Mesin OCR dan Pilih Mode Pemrosesan

Mesin OCR harus dikonfigurasi **sebelum** Anda menetapkan gambar apa pun. Di sinilah kami memutuskan apakah akan dijalankan di CPU atau memanfaatkan GPU.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Jika Anda berada di server tanpa tampilan grafis, ubah `Gpu` menjadi `Cpu` atau `Auto`.*  
Mode mesin memengaruhi alokasi memori dan kecepatan; mode GPU dapat 2‑3× lebih cepat pada TIFF berukuran besar dan resolusi tinggi.

---

## Langkah 3: Terapkan Lisensi Aspose OCR Anda

Menjalankan tanpa lisensi membatasi Anda pada beberapa halaman dan watermark. Muat lisensi Anda lebih awal sehingga setiap operasi selanjutnya tidak terbatas.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Kesalahan umum:** Menempatkan `SetLicense` setelah `Recognize()` akan menyebabkan mesin kembali ke mode percobaan untuk panggilan tersebut.

---

## Langkah 4: Muat File TIFF – Menangani Gambar Tunggal dan Multi‑Halaman

Aspose OCR dapat membaca TIFF multi‑halaman secara langsung, tetapi Anda perlu memberikan aliran yang tepat. Berikut pola yang kuat yang bekerja untuk kedua skenario.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Mengapa menggunakan `ImageStream.FromFile`?

- Ini menyembunyikan `FileStream` yang mendasarinya, menangani enumerasi halaman TIFF secara internal.  
- Ia juga berfungsi dengan `MemoryStream`, sehingga Anda dapat memuat gambar dari basis data atau API web tanpa menyentuh sistem file.

### Kasus khusus: TIFF sangat besar

Jika TIFF Anda melebihi 200 MB, pertimbangkan memuatnya halaman demi halaman untuk menghindari pengecualian kehabisan memori:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Langkah 5: Verifikasi Output

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Jika teks terlihat berantakan, periksa kembali:

1. **Resolution** – OCR bekerja paling baik dengan 300 dpi atau lebih tinggi.  
2. **EngineMode** – Ganti ke `Cpu` jika driver GPU sudah usang.  
3. **License** – Pastikan jalur file lisensi benar dan file dapat dibaca.

---

## Pertanyaan yang Sering Diajukan (FAQ)

### Apakah ini bekerja dengan format gambar lain?

Tentu saja. `ImageStream.FromFile` mendukung JPEG, PNG, BMP, dan bahkan PDF (melalui Aspose.PDF). Cukup ganti ekstensi file.

### Bagaimana jika saya perlu memproses gambar yang disimpan dalam basis data?

Baca BLOB ke dalam `MemoryStream` dan berikan ke `ImageStream.FromStream(memoryStream)`. Mesin OCR memperlakukannya sama seperti aliran berbasis file.

### Apakah saya dapat menjalankannya di Linux?

Ya—Aspose OCR bersifat lintas‑platform. Instal runtime .NET yang sesuai dan pastikan pustaka native yang diperlukan untuk GPU (jika digunakan) tersedia.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah seluruh program, siap untuk dikompilasi. Ganti `YOUR_DIRECTORY` dan jalur file lisensi dengan lokasi Anda yang sebenarnya.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Simpan ini sebagai `Program.cs`, jalankan `dotnet run`, dan saksikan teksnya

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}