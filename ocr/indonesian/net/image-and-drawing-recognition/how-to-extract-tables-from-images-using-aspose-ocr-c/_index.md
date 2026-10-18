---
category: general
date: 2026-03-28
description: Pelajari cara mengekstrak tabel dari gambar dengan Aspose OCR dalam C#.
  Panduan ini mencakup cara mendeteksi tabel dalam gambar, memuat gambar untuk OCR,
  dan mengekstrak tabel dari file PNG.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: id
og_description: Tutorial langkah demi langkah tentang cara mengekstrak tabel dari
  gambar dengan Aspose OCR di C#. Menyertakan kode, penjelasan, dan tips untuk mendeteksi
  tabel dalam file gambar.
og_title: Cara Mengekstrak Tabel dari Gambar dengan Aspose OCR (C#)
tags:
- Aspose OCR
- C#
- Table Extraction
title: Cara Mengekstrak Tabel dari Gambar menggunakan Aspose OCR (C#)
url: /id/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekstrak Tabel dari Gambar menggunakan Aspose OCR (C#)

Pernah bertanya-tanya **bagaimana cara mengekstrak tabel** dari faktur yang dipindai atau tangkapan layar spreadsheet? Anda bukan satu-satunya. Dalam banyak proyek dunia nyata kami perlu mengubah gambar tabel menjadi sesuatu yang dapat kami query—biasanya CSV atau DataTable. Kabar baik? Aspose OCR membuatnya sangat mudah, dan Anda dapat melakukannya hanya dengan beberapa baris C#.

Dalam tutorial ini kami akan membahas seluruh proses: dari **load image for OCR**, ke **detect tables in image**, dan akhirnya **extract table from image** serta menyimpannya sebagai file CSV. Pada akhir tutorial Anda akan memiliki aplikasi console siap‑jalankan yang dapat **extract tables from PNG** files (atau bitmap lain yang didukung) tanpa kesulitan.

## Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode ini juga berfungsi dengan .NET Framework)
- Visual Studio 2022 (atau IDE apa pun yang Anda suka)
- File lisensi Aspose.OCR untuk .NET (Anda dapat memulai dengan trial gratis)
- Gambar contoh yang berisi tabel (misalnya `invoice_table.png`)

Jika ada yang terdengar tidak familiar, jangan khawatir—cukup instal .NET SDK dan dapatkan paket NuGet, dan Anda siap melanjutkan.

## Gambaran Umum Solusi

At a high level the workflow looks like this:

1. **Load the image** yang ingin Anda proses.
2. **Run OCR recognition** agar mesin mengetahui di mana teks berada.
3. **Create a TableExtractor** yang memindai hasil OCR untuk struktur seperti grid.
4. **Extract all detected tables** dan pilih yang Anda butuhkan.
5. **Save the table** sebagai CSV (atau format lain yang Anda suka).

Setiap langkah dijelaskan secara detail di bawah, dengan potongan kode lengkap yang dapat Anda salin‑tempel.

<img src="table_extraction_example.png" alt="how to extract tables from image example" width="600">

*(Gambar di atas menunjukkan contoh tabel faktur yang akan kami ekstrak.)*

## Langkah 1 – Load the Image for OCR

Hal pertama yang harus Anda lakukan adalah memberi tahu Aspose OCR file mana yang akan dibaca. Perpustakaan ini mendukung PNG, JPEG, BMP, TIFF, dan beberapa format lainnya. Berikut kode minimalnya:

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**Mengapa ini penting:**  
`Image.FromFile` melakukan pekerjaan berat dalam mendekode PNG (atau bitmap lain) ke format yang dapat dipahami mesin OCR. Jika Anda melewatkan langkah ini atau memberikan file yang rusak, pemanggilan `Recognize()` berikutnya akan melemparkan pengecualian.

> **Pro tip:** Jika Anda menangani PDF besar, ekstrak setiap halaman menjadi gambar terlebih dahulu—jika tidak mesin OCR akan kehabisan memori.

## Langkah 2 – Recognize the Page (Required Before Table Detection)

Recognition mengubah data piksel mentah menjadi tata letak teks yang dapat dicari. Tanpa langkah ini `TableExtractor` tidak memiliki apa‑apa untuk diproses.

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**Apa yang terjadi di balik layar?**  
Aspose OCR menjalankan detektor teks berbasis jaringan saraf, kemudian membuat hierarki objek `Page`, `Paragraph`, dan `Word`. Detektor tabel kemudian memeriksa hubungan spasial antar kata tersebut.

Jika Anda memproses banyak gambar dalam loop, pertimbangkan untuk menggunakan kembali instance `OcrEngine` yang sama dan hanya mengganti properti `Image`—ini mengurangi beban alokasi.

## Langkah 3 – Create a TableExtractor and Detect Tables in Image

Sekarang data OCR sudah ada, kita dapat meminta Aspose untuk menemukan tabel. Kelas `TableExtractor` melakukan hal itu.

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**Mengapa menggunakan `ExtractAll()`?**  
Sebuah gambar tunggal dapat berisi beberapa tabel (bayangkan laporan multi‑bagian). `ExtractAll()` mengembalikan `List<Table>` sehingga Anda dapat mengiterasi, memilih yang tepat, atau bahkan menggabungkannya nanti.

Jika Anda hanya membutuhkan tabel pertama, Anda dapat dengan aman menggunakan `extractedTables[0]`, tetapi selalu periksa apakah daftar kosong untuk menghindari `IndexOutOfRangeException`.

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## Langkah 4 – Save the Extracted Table as CSV (or Any Other Format)

Aspose membuat proses ekspor menjadi sangat mudah. Kelas `Table` memiliki metode bawaan `SaveCsv`, `SaveXls`, dan `SaveJson`. Berikut cara menulis file CSV:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**Seperti apa CSV-nya?**  
Dengan asumsi gambar sumber berisi grid 4 × 3, CSV mungkin terlihat seperti:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

Anda dapat membuka file ini di Excel, Power BI, atau mengirimkannya langsung ke pipeline data Anda.

## Contoh Lengkap End‑to‑End

Berikut adalah program lengkap yang berdiri sendiri. Salin ke proyek console baru (`dotnet new console`) dan jalankan. Pastikan paket NuGet `Aspose.OCR` telah terpasang (`dotnet add package Aspose.OCR`).

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### Output yang Diharapkan

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

Buka `invoice_table.csv` dan Anda akan menemukan baris serta kolom yang mencerminkan gambar asli.

## Pertanyaan Umum & Kasus Edge

### Bagaimana jika gambar berupa JPEG bukan PNG?

Kode yang sama tetap berfungsi—cukup ubah ekstensi file di `Image.FromFile`. Aspose OCR secara otomatis mendeteksi format, jadi **extract tables from png** bukanlah persyaratan keras; ia bekerja dengan bitmap yang didukung apa pun.

### Tabel saya memiliki sel yang digabung. Apakah akan dipertahankan?

Sel yang digabung diperlakukan sebagai kolom terpisah dalam output CSV karena CSV tidak mendukung spanning. Jika Anda memerlukan format yang lebih kaya (misalnya Excel dengan sel yang digabung), gunakan `SaveXls` sebagai gantinya:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### Deteksi melewatkan kolom. Bagaimana cara meningkatkan akurasi?

- Tingkatkan resolusi gambar (≥300 dpi ideal).
- Pralakukan (pre‑process) gambar: konversi ke grayscale, tingkatkan kontras, atau terapkan filter deskew.
- Sesuaikan pengaturan Aspose OCR seperti `PageSegMode` atau `Language` jika tabel berisi karakter non‑Latin.

### Bisakah saya mengekstrak tabel langsung dari PDF?

Ya. Konversi setiap halaman PDF menjadi gambar terlebih dahulu (menggunakan `Aspose.PDF` atau perpustakaan PDF‑to‑image apa pun), lalu masukkan gambar tersebut ke dalam alur kerja yang sama.

## Tips untuk Implementasi Siap‑Produksi

1. **Wrap OCR in a try/catch** – lingkungan berlisensi jaringan dapat melempar pengecualian lisensi.
2. **Dispose of `Image` objects** – bungkus dalam blok `using` untuk membebaskan sumber daya native.
3. **Log the confidence scores** – `TableExtractor` mengekspos `Table.Confidence` yang dapat Anda simpan untuk pemantauan kualitas.
4. **Batch processing** – Saat menangani ratusan faktur, paralelkan panggilan OCR tetapi patuhi pedoman thread‑safety lisensi.

## Langkah Selanjutnya

Sekarang Anda tahu **how to extract tables** dari gambar, Anda mungkin ingin menjelajahi:

- **Detect tables in image** videos (menggunakan `TableExtractor` Aspose pada setiap frame).
- **Load image for OCR** dari API web, memungkinkan layanan ekstraksi tabel berbasis cloud.
- **Extract tables from PNG** files yang disimpan di Azure Blob Storage, mengintegrasikan dengan Azure Functions untuk pemrosesan serverless.

Silakan bereksperimen dengan format file berbeda, mengubah pengaturan OCR, atau mengalirkan output CSV langsung ke database. Tidak ada batasnya.

---

*Selamat coding! Jika Anda mengalami kendala atau memiliki ide untuk perbaikan, tinggalkan komentar di bawah. Kita akan menyelesaikannya bersama.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}