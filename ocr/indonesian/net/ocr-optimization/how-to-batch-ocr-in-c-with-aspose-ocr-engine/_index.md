---
category: general
date: 2026-01-01
description: Cara melakukan OCR batch menggunakan Aspose OCR Engine di C#. Pelajari
  cara mengenali teks dari gambar dan mengekstrak teks dari file TIFF dengan akselerasi
  GPU.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: id
og_description: Cara melakukan OCR batch di C# dengan Aspose OCR Engine. Panduan ini
  menunjukkan cara mengenali teks dari gambar dan mengekstrak teks dari file TIFF
  secara efisien.
og_title: Cara Batch OCR di C# – Panduan Lengkap Aspose
tags:
- OCR
- C#
- Aspose
- GPU
title: Cara Batch OCR di C# dengan Mesin OCR Aspose
url: /id/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di C# dengan Aspose OCR Engine

Pernah bertanya‑tanya **bagaimana cara batch OCR** ketika Anda memiliki puluhan dokumen hasil pemindaian yang berada di dalam folder? Anda tidak sendirian—banyak pengembang mengalami hal yang sama saat beralih dari pengenalan gambar tunggal ke pemrosesan seluruh koleksi. Kabar baiknya, Aspose OCR membuatnya sangat mudah, baik Anda menjalankannya di CPU maupun memanfaatkan akselerasi GPU.

Dalam tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang **mengenali teks dari gambar** dan bahkan **mengekstrak teks dari file TIFF** secara massal. Tidak ada jalan pintas “lihat dokumentasi” yang samar—hanya solusi mandiri yang dapat Anda salin‑tempel dan jalankan hari ini.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* .NET 6.0 atau yang lebih baru terpasang (kode menargetkan .NET 6, tetapi .NET 5 juga berfungsi).
* Paket NuGet Aspose.OCR untuk .NET (versi CPU dan GPU tersedia; instal yang sesuai dengan perangkat keras Anda).
* Sebuah folder dengan beberapa file TIFF atau PNG contoh yang ingin Anda proses.
* Visual Studio 2022 atau IDE lain pilihan Anda.

> **Tips pro:** Jika Anda berencana menggunakan versi GPU, pastikan driver grafis Anda terbaru dan CUDA 11+ terpasang. Mesin akan beralih ke CPU secara otomatis jika tidak menemukan GPU yang kompatibel.

## Langkah 1 – Siapkan Proyek dan Instal Aspose.OCR

### H2: Buat Aplikasi Konsol Baru dan Tambahkan Aspose.OCR

Buka terminal (atau Package Manager Console di Visual Studio) dan jalankan:

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Jika Anda memiliki lisensi yang mendukung GPU, tambahkan paket GPU sebagai gantinya:

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Itu saja—proyek Anda kini merujuk ke pustaka OCR yang akan kita gunakan untuk **batch OCR**.

## Langkah 2 – Inisialisasi Mesin OCR (CPU atau GPU)

### H2: Cara Batch OCR – Inisialisasi Mesin

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Mengapa ini penting:** Dengan mengatur `UseGpu`, Anda membiarkan Aspose menentukan jalur tercepat. Jika GPU tidak tersedia, mesin secara diam‑diam beralih kembali ke CPU, sehingga pekerjaan batch Anda tidak akan crash karena hardware yang hilang.

## Langkah 3 – Kumpulkan File yang Ingin Diproses

### H2: Mengenali Teks dari Gambar – Membuat Daftar File

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Catatan kasus tepi:** Jika Anda memiliki campuran format, ubah pola pencarian menjadi `"*.*"` dan saring berdasarkan ekstensi di dalam loop. Ini membuat batch tetap fleksibel.

## Langkah 4 – Proses Setiap Gambar dan Tampilkan Pratinjau

### H2: Ekstrak Teks dari TIFF – Loop Melalui File

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**Apa yang akan Anda lihat:** Untuk setiap TIFF, konsol mencetak sesuatu seperti:

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

Pratinjau itu mengonfirmasi batch berhasil tanpa harus membuka setiap file secara manual.

## Langkah 5 – Simpan Hasil (Opsional tapi Berguna)

### H3: Simpan Output OCR ke File Teks

Jika Anda memerlukan teks lengkap untuk pemrosesan selanjutnya, tambahkan ini di dalam loop `foreach`:

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Sekarang setiap TIFF mendapatkan file `.txt` pendamping yang berisi output OCR lengkap—sempurna untuk pengindeksan, pencarian, atau memberi makan ke model bahasa.

## Langkah 6 – Jalankan Demo dan Verifikasi

1. Bangun proyek: `dotnet build`.
2. Jalankan: `dotnet run --project GpuBatchDemo.csproj`.

Anda akan melihat baris pratinjau tercetak ke konsol, dan (jika Anda menambahkan langkah opsional) serangkaian file `.txt` di samping gambar sumber Anda.

### H3: Kesalahan Umum & Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| **Kosong `ocrResult.Text`** | Gambar terlalu gelap atau DPI rendah | Pra‑proses gambar (tingkatkan kontras, perbesar) atau setel `ocrEngine.Settings.PreprocessImage = true`. |
| **Kesalahan GPU “Versi driver CUDA tidak cukup”** | Driver usang | Perbarui driver GPU, atau setel `UseGpu = false` untuk memaksa CPU. |
| **Pengecualian “File tidak ditemukan”** | Pemilih path salah pada Linux/macOS | Gunakan `Path.Combine` atau garis miring maju (`/`). |

## Langkah 7 – Skalakan (Lebih dari Beberapa File)

Saat Anda beralih dari beberapa TIFF ke ribuan, pertimbangkan:

* **Pemrosesan paralel:** Bungkus `foreach` dalam `Parallel.ForEach` (pastikan instance mesin thread‑safe; jika tidak, buat satu per thread).
* **I/O berpotongan:** Baca gambar dalam batch untuk menghindari kehabisan RAM.
* **Logging:** Tulis progres ke file log; membantu melanjutkan setelah crash.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Ingat:** Memori GPU bersifat bersama, jadi memunculkan terlalu banyak pekerjaan GPU paralel justru dapat memperlambat Anda. Uji dengan beberapa thread terlebih dahulu.

## Contoh Kerja Penuh (Siap Salin‑Tempel)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

Menjalankan program ini akan **mengenali teks dari gambar**, **mengekstrak teks dari TIFF**, dan mendemonstrasikan **cara batch OCR** secara efisien.

---

## Kesimpulan

Anda kini memiliki contoh lengkap, ujung‑ke‑ujung tentang **cara batch OCR** di C# menggunakan mesin OCR Aspose. Tutorial ini mencakup semua mulai dari menyiapkan proyek, mengaktifkan akselerasi GPU, membangun daftar file, memproses setiap gambar, hingga menyimpan hasil. Baik Anda mengekstrak teks dari file TIFF atau format gambar lainnya, pola yang sama dapat diterapkan—cukup ganti ekstensi file.

Siap untuk langkah selanjutnya? Cobalah mengintegrasikan output OCR dengan indeks pencarian, beri makan teks ke model bahasa besar, atau bereksperimen dengan pemrosesan paralel untuk menghemat menit pada batch besar. Langit adalah batasnya, dan Anda sudah memiliki fondasi untuk membangunnya.

Punya pertanyaan atau ingin berbagi trik batch‑OCR Anda? Tinggalkan komentar di bawah—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}