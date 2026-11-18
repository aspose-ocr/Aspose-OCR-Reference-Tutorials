---
category: general
date: 2026-03-28
description: Pelajari cara melakukan OCR batch di C# dan dengan mudah mengonversi
  TIFF menjadi teks. Panduan langkah demi langkah ini menunjukkan cara mengekstrak
  teks dari file TIFF menggunakan Aspose OCR.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: id
og_description: Bagaimana cara melakukan OCR batch di C#? Ikuti tutorial lengkap ini
  untuk mengonversi file TIFF multi‑halaman menjadi teks yang dapat dicari menggunakan
  Aspose OCR.
og_title: Cara Batch OCR di C# – Mengonversi TIFF Multi‑Halaman ke Teks
tags:
- OCR
- C#
- Aspose
title: Cara Batch OCR di C# – Mengonversi TIFF Multi‑Halaman ke Teks
url: /id/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di C# – Mengonversi Multi‑Page TIFF ke Teks

Pernah bertanya-tanya **bagaimana cara batch OCR** sekumpulan halaman yang dipindai tanpa menulis loop untuk setiap gambar? Anda tidak sendirian. Dalam banyak proyek—misalnya pemrosesan faktur atau digitalisasi arsip—kebutuhan untuk **mengonversi TIFF ke teks** muncul setiap hari, dan melakukannya satu halaman pada satu waktu dengan cepat menjadi mimpi buruk.

Kabar baik? Dengan beberapa baris C# dan Aspose OCR Anda dapat memberi seluruh TIFF multi‑page ke mesin dan mendapatkan kamus nomor halaman yang dipetakan ke string yang diekstrak. Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan **cara batch OCR**, **cara mengekstrak teks dari TIFF**, dan mengapa pendekatan ini lebih baik daripada alternatif manual.

## Apa yang Akan Anda Pelajari

- Menyiapkan pustaka Aspose OCR dalam proyek .NET.  
- Memuat file TIFF multi‑page menggunakan `Image.FromMultiPageFile`.  
- Menjalankan `RecognizeBatch` untuk mendapatkan `Dictionary<int,string>` berisi hasil per halaman.  
- Mencetak output dalam format yang bersih dan mudah dibaca.  

Pada akhir tutorial Anda akan memiliki aplikasi console siap‑jalankan yang mengubah TIFF multi‑page apa pun menjadi teks biasa—tanpa alat tambahan.

### Prasyarat

- .NET 6.0 SDK (atau versi .NET terbaru).  
- Visual Studio 2022 atau VS Code—IDE favorit Anda sudah cukup.  
- Lisensi Aspose OCR yang valid atau kunci evaluasi gratis (API berfungsi tanpa lisensi tetapi menambahkan watermark).  
- Contoh file multi‑page TIFF bernama `multipage.tif` yang ditempatkan di folder yang dapat Anda referensikan.

> **Pro tip:** Jika Anda menggunakan Windows, folder proyek default adalah tempat yang nyaman untuk menaruh TIFF; di Linux/macOS cukup sesuaikan pathnya.

## Langkah 1: Instal Paket NuGet Aspose OCR

Sebelum menulis kode apa pun, kita perlu pustaka OCR. Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah ini mengunduh versi stabil terbaru (per Maret 2026 v23.9) dan menambahkan DLL yang diperlukan ke proyek Anda. Tidak ada konfigurasi tambahan yang diperlukan untuk aplikasi console sederhana.

## Langkah 2: Buat Kerangka Aplikasi Console

Mari buat program minimal yang mereferensikan mesin OCR. Direktif `using` sangat penting—tanpa mereka kompiler akan mengeluh tentang tipe yang tidak ditemukan.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **Mengapa ini penting:** Kelas `Image` berada di sub‑namespace, dan lupa mengimpor `ImageProcessing` akan menghasilkan error “type or namespace not found” yang dapat membuang waktu debugging selama satu jam.

Sekarang tambahkan metode `Main` dan komentar singkat yang menjelaskan tujuan:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## Langkah 3: Inisialisasi Mesin OCR

`OcrEngine` adalah mesin utama. Membuatnya satu kali dan menggunakannya kembali untuk semua halaman bersifat efisien dalam memori dan cepat.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Apa yang terjadi di balik layar?** Mesin memuat model bahasa dan mengonfigurasi pengaturan default (misalnya, Inggris, auto‑rotate). Anda dapat menyesuaikannya nanti, tetapi nilai default sudah cukup baik untuk kebanyakan dokumen.

## Langkah 4: Muat TIFF Multi‑Page

Aspose memudahkan pemuatan gambar multi‑frame. Berikan path lengkap atau relatif dari direktori kerja executable.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

Jika file tidak ditemukan, `FromMultiPageFile` akan melempar `FileNotFoundException`. Bungkus dengan `try/catch` jika Anda memerlukan penanganan error yang lebih halus—sesuatu yang akan kami tunjukkan pada langkah berikutnya.

## Langkah 5: Lakukan Batch OCR

Sekarang saatnya bintang utama: `RecognizeBatch`. Metode ini mengembalikan `Dictionary<int,string>` di mana kunci adalah indeks halaman (dimulai dari 0) dan nilai adalah teks yang dikenali.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **Kasus tepi:** Beberapa TIFF berisi halaman kosong. Aspose mengembalikan string kosong untuk halaman tersebut, yang dapat Anda filter nanti jika tidak ingin output berantakan.

## Langkah 6: Tampilkan Hasil

Akhirnya, iterasi kamus dan cetak teks setiap halaman. Menggunakan string interpolasi membuat kode tetap rapi.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

Menjalankan program seharusnya menghasilkan sesuatu seperti:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

Jika Anda melihat output yang kacau, periksa kembali apakah TIFF sumber tidak rusak dan apakah bahasa teks sesuai dengan bahasa default mesin (Inggris). Anda juga dapat mengatur `ocrEngine.Language = OcrLanguage.Spanish;` untuk dokumen non‑Inggris.

## Contoh Lengkap yang Berfungsi

Menggabungkan semua bagian, berikut program lengkap yang dapat Anda salin‑tempel ke `Program.cs` dan jalankan:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Simpan, build, dan jalankan:

```bash
dotnet run
```

Anda akan melihat konten yang diekstrak dari setiap halaman dicetak ke console. Itulah seluruh **c# ocr tutorial** yang Anda minta.

## Pertanyaan yang Sering Diajukan & Kasus Tepi

### Bagaimana jika TIFF saya berisi puluhan halaman?

`RecognizeBatch` memproses semua frame dalam satu panggilan, tetapi penggunaan memori meningkat secara linear dengan jumlah halaman. Untuk dokumen sangat besar (ratusan halaman) pertimbangkan memprosesnya secara bertahap:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### Bisakah saya menyimpan teks yang diekstrak ke file alih‑alih mencetak?

Tentu saja. Ganti blok `Console.WriteLine` dengan I/O file:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

Sekarang setiap halaman akan memiliki file `.txt`‑nya masing‑masing—sempurna untuk pengindeksan selanjutnya.

### Bagaimana cara mengubah bahasa output atau mengaktifkan auto‑rotation?

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

Pengaturan ini harus diterapkan **sebelum** memanggil `RecognizeBatch`.

## Kesimpulan

Kami telah membahas **cara batch OCR** sebuah TIFF multi‑page menggunakan Aspose OCR di C#. Dengan memuat gambar sekali, memanggil `RecognizeBatch`, dan mengiterasi kamus hasil, Anda dapat **mengonversi TIFF ke teks** dalam hitungan detik. Contoh ini juga menunjukkan cara **mengekstrak teks dari TIFF**, menangani error, dan opsional menulis hasil ke file—semua dalam aplikasi console yang bersih dan mandiri.

Siap untuk langkah selanjutnya? Coba gabungkan pendekatan ini dengan pustaka pembuatan PDF untuk menghasilkan PDF yang dapat dicari, atau hubungkan output ke basis data untuk arsip yang dapat dicari. Anda juga dapat bereksperimen dengan format gambar lain (PNG, JPEG) dengan mengganti `Image.FromMultiPageFile` menjadi `Image.FromFile`.

Ada pertanyaan lebih lanjut tentang OCR, lisensi, atau optimasi performa? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}