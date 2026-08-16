---
category: general
date: 2026-03-13
description: Cara menggunakan OCR di C# untuk mengekstrak teks dari pemindaian. Pelajari
  cara mengonversi TIFF menjadi teks dengan Aspose OCR, akselerasi GPU, dan kode langkah
  demi langkah.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: id
og_description: Cara menggunakan OCR di C# untuk mengekstrak teks dari pemindaian.
  Panduan ini menunjukkan cara mengonversi TIFF menjadi teks dengan Aspose OCR dan
  percepatan GPU.
og_title: Cara Menggunakan OCR di C# – Ekstrak Teks dari Pemindaian dengan Cepat
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cara Menggunakan OCR di C# – Ekstrak Teks dari Pemindaian dengan Cepat
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Ekstrak Teks dari Scan dengan Cepat

Pernah bertanya‑tanya **bagaimana cara menggunakan OCR** untuk mengambil teks yang dapat dibaca dari tumpukan file TIFF yang dipindai? Anda tidak sendirian. Dalam banyak proyek dunia nyata—seperti digitalisasi faktur, pengarsipan dokumen bersejarah, atau sekadar membuat PDF dapat dicari—para pengembang membutuhkan cara yang andal untuk **mengekstrak teks dari hasil pemindaian** tanpa harus susah payah.

Kabar baiknya? Dengan Aspose OCR dan beberapa baris kode C# Anda dapat mengonversi TIFF menjadi teks dalam hitungan detik, bahkan pada workstation yang sederhana. Di bawah ini Anda akan menemukan contoh lengkap yang siap dijalankan, beserta alasan di balik setiap pilihan sehingga Anda dapat menyesuaikannya dengan alur kerja Anda sendiri.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

| Prasyarat | Mengapa penting |
|--------------|----------------|
| .NET 6+ (atau .NET Framework 4.7+) | Paket NuGet Aspose OCR menargetkan runtime .NET modern. |
| Visual Studio 2022 (atau IDE lain yang Anda suka) | Menyediakan IntelliSense dan debugging yang mudah. |
| GPU yang kompatibel dengan CUDA & driver (opsional) | Mengaktifkan `ocrEngine.UseGpu = true` untuk percepatan yang signifikan pada batch besar. |
| Folder berisi gambar TIFF yang ingin diproses | Tutorial ini menggunakan file `*.tif`, tetapi Anda dapat menyesuaikan pola pencariannya. |
| Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Perpustakaan inti yang melakukan pekerjaan berat. |

Jika ada yang belum Anda miliki, segera dapatkan—tidak ada gunanya melanjutkan membaca hanya untuk menemukan ketergantungan yang hilang di kemudian hari.

## Ikhtisar Solusi

Secara garis besar program ini melakukan tiga hal:

1. **Membuat mesin OCR** dan secara opsional mengaktifkan akselerasi GPU.  
2. **Menyusuri setiap file TIFF** dalam sebuah direktori, menjalankan pengenalan, dan menangkap teks hasilnya.  
3. **Menulis teks** ke file `.txt` yang berada di samping gambar asli.

Itu saja. Kode dibuat sengaja sesingkat mungkin, namun tetap menampilkan praktik terbaik seperti pemilihan bahasa yang eksplisit, pembuangan sumber daya yang tepat, dan penanganan error untuk kasus‑kasus tepi yang paling umum.

![Contoh cara menggunakan OCR di C#](/images/how-to-use-ocr-csharp.png "Ilustrasi cara menggunakan OCR di C# untuk mengekstrak teks dari hasil pemindaian")

## Langkah 1: Inisialisasi Mesin OCR (How to Use OCR)

Hal pertama yang Anda perlukan adalah sebuah instance `OcrEngine`. Objek ini adalah gerbang ke semua fungsionalitas Aspose OCR. Secara default ia bekerja pada CPU, tetapi dengan mengatur `UseGpu = true` Anda memberi tahu perpustakaan untuk memindahkan perhitungan matriks berat ke kartu grafis Anda—asalkan driver CUDA‑compatible sudah terpasang.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Mengapa ini penting:**  
- **Akselerasi GPU** dapat memotong waktu pemrosesan hingga 70 % untuk scan beresolusi tinggi.  
- **Pemilihan bahasa secara eksplisit** menghindari mesin menebak‑tebak dan meningkatkan akurasi, terutama untuk skrip non‑Latin.

## Langkah 2: Arahkan Mesin ke Scan Anda (Convert TIFF to Text)

Selanjutnya kita memberi tahu program di mana mencari gambar. Menggunakan `Directory.GetFiles` dengan filter `*.tif` membuat logika tetap sederhana dan menghindari pengambilan file yang tidak relevan seperti `.jpg` atau `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Catatan kasus tepi:** Jika direktori kosong, loop di bawah tidak akan pernah dijalankan, yang sepenuhnya dapat diterima. Anda akan melihat pesan ramah “No files found” nanti.

## Langkah 3: Proses Setiap File TIFF (Extract Text from Scans)

Berikutnya adalah inti program: memuat setiap gambar, menjalankan OCR, dan menyimpan hasilnya. Helper `ImageStream.FromFile` menyalurkan file langsung ke memori, yang lebih efisien daripada memuat `Bitmap` terlebih dahulu.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Mengapa kita membungkus setiap iterasi dalam `try/catch`:**  
Memindai batch dokumen seringkali berantakan; TIFF yang rusak atau kehabisan memori tidak seharusnya menghentikan seluruh proses. Blok `catch` mencatat masalah dan melanjutkan, sehingga pipeline tetap tangguh.

### Output yang Diharapkan

Untuk setiap `example.tif` Anda akan menemukan file `example.txt` yang berisi sesuatu seperti berikut:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Jika mesin OCR tidak dapat membaca sebuah baris, ia akan meninggalkan baris kosong atau karakter yang tidak terbaca—tidak ada yang crash.

## Langkah 4: Pembersihan dan Pembuangan (Best Practice)

`OcrEngine` mengimplementasikan `IDisposable`, jadi sebaiknya Anda membebaskan sumber daya native ketika selesai. Pada aplikasi console singkat Anda bisa mengandalkan GC, tetapi pembuangan eksplisit adalah kebiasaan yang baik untuk dibentuk.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Contoh Lengkap yang Siap Pakai (Copy‑Paste Ready)

Berikut adalah program lengkap yang dapat Anda tempel ke dalam proyek Console App baru. Ia akan terkompilasi apa adanya, asalkan Anda telah menambahkan paket NuGet Aspose.OCR.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Daftar Periksa Cepat

- **Flag GPU** – hapus atau set ke `false` jika Anda tidak memiliki driver CUDA.  
- **Bahasa** – ganti `Language.English` dengan bahasa lain yang didukung.  
- **Pola file** – ubah `"*.tif"` menjadi `"*.png"` atau `"*.*"` jika scan Anda berformat lain.  

## Kesalahan Umum & Tips Pro (c# OCR tutorial)

| Kesalahan | Cara menghindarinya |
|---------|-----------------|
| **Error out‑of‑memory** pada batch besar | Proses file dalam potongan lebih kecil atau panggil `GC.Collect()` setiap 50 file (jarang diperlukan). |
| **GPU tidak terdeteksi** padahal `UseGpu = true` | Mesin secara diam‑diam beralih ke CPU, tetapi Anda dapat memeriksa `ocrEngine.IsGpuAvailable` setelah konstruksi. |
| **Paket bahasa salah** menghasilkan output kacau | Selalu set `ocrEngine.Language` secara eksplisit; defaultnya mungkin `Language.Unknown`. |
| **Path file mengandung karakter Unicode** | Gunakan `Path.GetFullPath` untuk menormalkan, atau beri prefix `@"\\?\"` pada Windows jika path melebihi batas |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}