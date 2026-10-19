---
category: general
date: 2026-09-13
description: Cara melakukan OCR batch dengan Aspose OCR GPU di C# menggunakan .NET.
  Pelajari cara mengenali teks dari gambar, mengekstrak teks dari file TIFF, dan mempercepat
  pemrosesan dengan dukungan GPU.
draft: false
keywords:
- aspose ocr gpu
- process multiple images
- how to batch ocr
- install aspose ocr
lastmod: 2026-09-13
og_description: Cara melakukan OCR batch dengan Aspose OCR GPU di C# menggunakan .NET.
  Panduan ini menunjukkan cara mengenali teks dari gambar, mengekstrak teks dari file
  TIFF, dan memanfaatkan percepatan GPU untuk pemrosesan berperforma tinggi.
og_image_alt: Screenshot of Aspose OCR GPU batch processing console output in C#
og_title: Cara melakukan OCR batch dengan Aspose OCR GPU di C# menggunakan .NET
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: How to batch OCR with Aspose OCR GPU in C# using .NET. Learn to recognize
    text from images, extract text from TIFF files, and accelerate processing with
    GPU support.
  headline: How to batch OCR with Aspose OCR GPU in C# using .NET
  type: TechArticle
- questions:
  - answer: Yes, as long as the server has a CUDA‑compatible GPU and the appropriate
      driver libraries installed; no display is required.
    question: Can I run the GPU version on a headless Linux server?
  - answer: Absolutely. The engine treats each page as a separate image and returns
      concatenated text, preserving page order.
    question: Does Aspose OCR support multi‑page TIFF files out of the box?
  - answer: Benchmarks show Aspose OCR achieves ≥ 96 % character accuracy on clean
      printed documents and ≥ 90 % on low‑contrast scans, matching leading SaaS providers
      while keeping data on‑premises.
    question: How accurate is the OCR output compared with cloud services?
  - answer: The library imposes no hard limit; practical limits are driven by available
      disk space and GPU memory. Processing 10 000 pages on an RTX 3080 typically
      stays under 2 GB of GPU memory.
    question: Is there a limit to the number of files I can process in one run?
  - answer: Yes, set `ocrEngine.Language = OcrLanguage.Spanish` (or any supported
      language) before calling `Recognize`. The engine supports 30+ languages, including
      Arabic, Chinese, and Hindi.
    question: Can I customize the language model for non‑English scripts?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
title: Cara melakukan OCR batch dengan Aspose OCR GPU di C# menggunakan .NET
url: /id/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan batch OCR dengan Aspose OCR GPU di C# menggunakan .NET

Jika Anda perlu **batch OCR** ratusan halaman yang dipindai dengan cepat, mesin Aspose OCR GPU memberikan cara yang cepat dan dapat diandalkan untuk mengenali teks dari gambar dan file TIFF dalam satu kali proses. Dalam panduan ini Anda akan melihat cara menyiapkan proyek .NET, mengaktifkan akselerasi GPU, dan memproses seluruh folder gambar tanpa menulis satu baris kode boiler‑plate sendiri.

## Jawaban Cepat
- **Apa arti “batch OCR”?** Ini adalah pemrosesan otomatis banyak file gambar dalam satu operasi, mengembalikan teks yang diekstrak untuk setiap file.  
- **Bisakah saya menggunakan versi GPU di mesin mana pun?** Ya, selama sistem memiliki GPU yang kompatibel dengan CUDA dan driver yang sesuai terpasang.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi percobaan gratis dapat digunakan untuk pengujian; lisensi komersial diperlukan untuk produksi.  
- **Versi .NET mana yang didukung?** .NET 6.0 dan yang lebih baru didukung sepenuhnya; .NET 5 juga berfungsi dengan penyesuaian kecil.  
- **Apakah mesin ini thread‑safe untuk menjalankan paralel?** Mesin CPU thread‑safe; mesin GPU memerlukan satu instance per thread atau strategi paralel yang terkontrol.

## Apa itu Aspose OCR GPU?
Mesin `Aspose.OCR` GPU adalah perpustakaan OCR berkinerja tinggi yang memindahkan pekerjaan analisis gambar ke kartu grafis yang mendukung CUDA, memberikan throughput hingga 4× lebih cepat dibandingkan pemrosesan CPU murni. Ia mendukung berbagai format gambar, menyediakan model bahasa bawaan, dan dapat diintegrasikan ke dalam aplikasi .NET apa pun dengan perubahan kode minimal.

## Mengapa menggunakan Aspose OCR GPU untuk pemrosesan batch?
Aspose OCR mendukung **lebih dari 30 format gambar** (termasuk PNG, JPEG, BMP, dan TIFF multi‑halaman) dan dapat menangani file hingga **2 GB** masing‑masing tanpa memuat seluruh dokumen ke memori. Ketika Anda mengaktifkan akselerasi GPU, halaman TIFF 300‑dpi biasanya diproses dalam kurang dari 0,2 detik per halaman pada kartu RTX 3080 modern.

## Prasyarat
- SDK .NET 6.0 (atau lebih baru) terpasang pada mesin pengembangan Anda.  
- Paket NuGet Aspose.OCR untuk .NET – pilih paket `Aspose.OCR.Gpu` jika Anda memiliki GPU yang kompatibel, jika tidak instal `Aspose.OCR`.  
- Sebuah folder yang berisi gambar yang ingin Anda proses (TIFF, PNG, JPEG, dll.).  
- Visual Studio 2022, Rider, atau editor apa pun yang dapat membangun aplikasi konsol .NET.

> **Pro tip:** Pastikan CUDA 11+ terpasang dan `nvidia-smi` melaporkan GPU Anda sebagai “compatible”. Perpustakaan secara otomatis akan beralih ke CPU jika tidak menemukan GPU yang cocok.

## Cara menyiapkan proyek dan menginstal Aspose OCR
Buat aplikasi konsol .NET baru, tambahkan paket NuGet Aspose OCR, dan pulihkan dependensi. Ini menyiapkan proyek ringan yang dapat dikompilasi dan dijalankan pada platform apa pun yang mendukung .NET 6 atau lebih baru. Setelah paket terinstal, Anda dapat merujuk kelas OCR secara langsung dalam kode, mengaktifkan pemrosesan batch tanpa konfigurasi tambahan.

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Jika Anda memiliki lisensi yang mendukung GPU, instal paket khusus GPU sebagai gantinya. Versi ini berisi binding CUDA native yang memungkinkan mesin berjalan pada kartu grafis, memberikan peningkatan kinerja seperti yang dijelaskan sebelumnya.

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Proyek Anda kini merujuk ke perpustakaan OCR yang diperlukan untuk **batch OCR**.

## Cara menginisialisasi mesin OCR (CPU atau GPU)
Kelas `OcrEngine` adalah titik masuk utama untuk melakukan operasi OCR. Ia mengabstraksi perangkat keras yang mendasari dan menyediakan API sederhana untuk eksekusi CPU dan GPU. Muat mesin OCR dan beri tahu apakah akan menggunakan GPU:

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

**Mengapa ini penting:** Menetapkan `UseGpu` memungkinkan Aspose memilih jalur eksekusi tercepat. Ketika GPU yang kompatibel hadir, mesin berjalan pada kartu grafis; jika tidak, ia kembali ke CPU tanpa melempar error, memastikan pekerjaan batch Anda tidak pernah crash karena perangkat keras yang hilang.

## Cara mengumpulkan file yang ingin Anda proses
Mengumpulkan gambar target adalah langkah pertama dalam alur kerja batch apa pun. Buat daftar jalur file yang cocok dengan ekstensi yang didukung, lalu berikan daftar tersebut ke loop OCR. Pendekatan ini menjaga kode tetap sederhana dan memudahkan penambahan penyaringan di kemudian hari.

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

**Catatan kasus tepi:** Jika folder Anda berisi format campuran, ganti pola pencarian dengan `"*.*"` dan filter berdasarkan ekstensi di dalam loop. Ini membuat batch fleksibel dan menghindari file yang terlewat.

## Cara memproses setiap gambar dan menampilkan pratinjau
Untuk setiap file, panggil mesin OCR, ambil teks yang dikenali, dan tampilkan cuplikan singkat di konsol. Menampilkan pratinjau membantu memverifikasi bahwa batch berfungsi dengan benar tanpa membuka setiap file output.

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

**Apa yang akan Anda lihat:** Untuk setiap gambar, konsol mencetak 100 karakter pertama dari teks yang dikenali, mengonfirmasi bahwa batch berhasil tanpa membuka setiap file secara manual.

## Cara menyimpan hasil OCR (opsional tetapi berguna)
Menyimpan output OCR lengkap memungkinkan pengindeksan downstream, analisis AI, atau konversi ke PDF yang dapat dicari. Tulis teks ke file `.txt` yang berada di samping gambar sumber, menggunakan nama dasar yang sama untuk korelasi mudah.

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Sekarang setiap gambar memiliki file teks pendamping yang berisi output OCR lengkap, siap untuk mesin pencari, model bahasa, atau pipeline analitik khusus.

## Cara menjalankan demo dan memverifikasi output
Bangun dan jalankan aplikasi konsol untuk melihat proses batch beraksi. Langkah build mengompilasi kode, sementara langkah run memproses setiap gambar di folder target dan menulis baris pratinjau ke konsol. Jika Anda mengaktifkan langkah penyimpanan opsional, Anda juga akan menemukan file `.txt` untuk setiap gambar sumber.

1. Bangun proyek: `dotnet build`.  
2. Jalankan program: `dotnet run --project GpuBatchDemo.csproj`.

Anda harus melihat baris pratinjau di konsol dan, jika Anda menambahkan langkah opsional, serangkaian file `.txt` di sebelah gambar sumber Anda.

## Kesulitan umum & cara memperbaikinya
| Gejala | Penyebab kemungkinan | Solusi |
|---------|----------------------|--------|
| **Empty `ocrResult.Text`** | Gambar terlalu gelap atau DPI rendah | Praproses gambar (tingkatkan kontras, perbesar) atau aktifkan `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | Driver usang | Perbarui driver GPU, atau setel `UseGpu = false` untuk memaksa pemrosesan CPU. |
| **Exception “File not found”** | Pemisah jalur salah pada Linux/macOS | Gunakan `Path.Combine` atau garis miring maju (`/`). |

## Cara meningkatkan skala di atas beberapa file
Saat Anda beralih dari puluhan ke ribuan gambar, pertimbangkan strategi berikut: gunakan pemrosesan paralel dengan instance mesin terpisah per thread, muat gambar dalam batch yang dapat dikelola, dan catat kemajuan ke file untuk pemulihan mudah. Teknik ini menjaga penggunaan memori rendah dan mempertahankan throughput tinggi.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Ingat:** Memori GPU dibagi di seluruh proses. Memulai terlalu banyak pekerjaan GPU paralel dapat memenuhkan memori dan sebenarnya memperlambat batch. Mulailah dengan 2‑4 thread dan pantau pemanfaatan GPU.

## Pertanyaan yang sering diajukan

**Q: Bisakah saya menjalankan versi GPU di server Linux tanpa tampilan (headless)?**  
A: Ya, selama server memiliki GPU yang kompatibel dengan CUDA dan perpustakaan driver yang sesuai terpasang; tidak diperlukan tampilan.

**Q: Apakah Aspose OCR mendukung file TIFF multi‑halaman secara langsung?**  
A: Tentu saja. Mesin memperlakukan setiap halaman sebagai gambar terpisah dan mengembalikan teks yang digabungkan, mempertahankan urutan halaman.

**Q: Seberapa akurat output OCR dibandingkan dengan layanan cloud?**  
A: Benchmark menunjukkan Aspose OCR mencapai ≥ 96 % akurasi karakter pada dokumen cetak bersih dan ≥ 90 % pada pemindaian kontras rendah, menyamai penyedia SaaS terkemuka sambil menjaga data tetap di‑premise.

**Q: Apakah ada batas jumlah file yang dapat diproses dalam satu kali jalan?**  
A: Perpustakaan tidak memberlakukan batas keras; batas praktis ditentukan oleh ruang disk yang tersedia dan memori GPU. Memproses 10 000 halaman pada RTX 3080 biasanya tetap di bawah 2 GB memori GPU.

**Q: Bisakah saya menyesuaikan model bahasa untuk skrip non‑Inggris?**  
A: Ya, setel `ocrEngine.Language = OcrLanguage.Spanish` (atau bahasa lain yang didukung) sebelum memanggil `Recognize`. Mesin mendukung lebih dari 30 bahasa, termasuk Arab, Cina, dan Hindi.

## Kesimpulan
Anda kini memiliki solusi lengkap end‑to‑end untuk **batch OCR dengan Aspose OCR GPU di C#**. Tutorial ini mencakup penyiapan proyek, aktivasi GPU, enumerasi file, pemrosesan per‑gambar, penyimpanan hasil opsional, dan teknik skala untuk beban kerja besar. Dengan fondasi ini Anda dapat memasukkan output OCR ke dalam indeks pencarian, mengirimnya ke model bahasa besar, atau membangun pipeline pemrosesan dokumen khusus.

Siap untuk tantangan berikutnya? Cobalah menggabungkan teks OCR dengan Aspose .PDF untuk menghasilkan PDF yang dapat dicari, atau integrasikan output dengan Azure Cognitive Search untuk pencarian full‑text instan di ribuan dokumen yang dipindai.

---

**Terakhir Diperbarui:** 2026-09-13  
**Diuji Dengan:** Aspose.OCR 24.5 for .NET (CPU & GPU packages)  
**Penulis:** Aspose  

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```
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

## Tutorial Terkait

- [Cara Menggunakan OCR di C untuk Mengekstrak Teks Dari Gambar dengan Akselerasi GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Mengenali Teks Dari Gambar dengan Aspose OCR GPU yang Dipercepat di C](/ocr/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}