---
category: general
date: 2026-01-10
description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  mengonversi teks dokumen yang dipindai dengan pemrosesan batch dan menyimpan hasilnya.
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: id
og_description: Ekstrak teks dari gambar dengan Aspose OCR di C#. Tutorial ini menunjukkan
  cara mengonversi teks dokumen yang dipindai menggunakan pemrosesan batch.
og_title: Ekstrak Teks dari Gambar di C# – Panduan Lengkap Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Ekstrak Teks dari Gambar di C# – Panduan Lengkap Aspose OCR
url: /id/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar – Panduan Lengkap Aspose OCR

Pernah perlu **mengekstrak teks dari gambar** tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian; banyak pengembang mengalami kebingungan saat menangani PDF yang dipindai, TIFF multi‑halaman, atau kwitansi berbasis foto. Kabar baiknya, dengan Aspose OCR Anda dapat **mengonversi teks dokumen yang dipindai** hanya dengan beberapa baris kode C#.

Dalam tutorial ini kita akan membahas skenario dunia nyata: mengambil TIFF multi‑halaman, menjalankan OCR batch pada setiap halaman, dan menulis satu file teks yang berisi konten semua halaman. Pada akhir tutorial Anda akan memiliki aplikasi konsol yang siap dijalankan, memahami mengapa setiap langkah penting, dan tahu cara menyesuaikan alur untuk kasus khusus seperti gambar yang dilindungi kata sandi atau paket bahasa khusus.

## Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)  
- Visual Studio 2022 (atau editor lain pilihan Anda)  
- File lisensi Aspose OCR (atau Anda dapat menggunakan mode evaluasi gratis)  
- File gambar multi‑halaman (misalnya `multipage.tif`) yang ditempatkan di folder yang dapat Anda referensikan  

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.OCR`; kami akan menginstalnya pada langkah pertama.

## Langkah 1 – Instal Aspose OCR dan Siapkan Proyek

Untuk memulai, buat proyek konsol baru dan tambahkan pustaka Aspose OCR.

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **Tips pro:** Jika Anda memiliki file lisensi (`Aspose.OCR.lic`), salin ke root proyek. Pustaka akan otomatis mendeteksinya saat runtime.

Mengapa langkah ini? Menginstal paket memberi Anda akses ke `BatchProcessor`, `OcrEngine`, dan kelas berguna lainnya yang menyederhanakan penanganan gambar tingkat rendah. Ini juga memastikan Anda menggunakan algoritma OCR terbaru yang disediakan Aspose.

## Langkah 2 – Muat Gambar Multi‑Halaman dengan BatchProcessor

`BatchProcessor` dirancang khusus untuk skenario ini: mengiterasi setiap halaman gambar multi‑halaman tanpa harus memisahkan file secara manual.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

`BatchProcessor` membaca semua halaman ke memori, menampilkannya melalui `batchProcessor.Pages`. Setiap objek halaman mengetahui nomor halamannya (`ocrPage.Number`) yang akan kita gunakan nanti untuk judul yang jelas.

## Langkah 3 – Siapkan StringBuilder untuk Mengakumulasi Hasil

Kita menginginkan satu file teks yang berisi output OCR semua halaman, dipisahkan oleh header. `StringBuilder` adalah cara paling efisien untuk menggabungkan string dalam loop.

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

Mengapa `StringBuilder`? Menggabungkan string dengan `+` di dalam loop akan membuat alokasi string baru pada setiap iterasi, yang menurunkan kinerja—terutama pada dokumen besar.

## Langkah 4 – Iterasi Setiap Halaman, Jalankan OCR, dan Tambahkan Hasil

Sekarang inti tutorial: melakukan loop pada setiap halaman, mengenali teks, dan menyimpannya dengan penanda halaman.

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**Mengapa membuat `OcrEngine` baru untuk setiap halaman?** Beberapa pengembang menggunakan satu engine dan mengubah properti `Image`‑nya, tetapi hal itu dapat mempertahankan pengaturan bahasa atau hasil sebelumnya, yang menyebabkan bug halus. Membuat engine baru menjamin kondisi bersih.

### Menangani Kasus Edge Umum

- **Halaman kosong:** Jika sebuah halaman tidak mengandung teks yang dapat dikenali, `ocrEngine.Text` akan menjadi string kosong. Anda mungkin ingin menyisipkan placeholder seperti “(Tidak ada teks terdeteksi)”.
- **Pemilihan bahasa:** Secara default Aspose OCR menggunakan bahasa Inggris. Untuk memproses bahasa Jerman atau Prancis, setel `ocrEngine.Language = Language.German;` sebelum memanggil `Recognize()`.
- **Tips kinerja:** Untuk TIFF yang sangat besar, Anda dapat mengaktifkan `ocrEngine.UseParallelProcessing = true;` untuk memanfaatkan beberapa core.

## Langkah 5 – Tulis Output Gabungan ke File Teks

Akhirnya, simpan string yang telah terakumulasi ke disk.

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

File `multipage_result.txt` yang dihasilkan akan terlihat kira‑kira seperti ini:

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

Sekarang Anda telah **mengekstrak teks dari gambar** dan secara efektif **mengonversi teks dokumen yang dipindai** menjadi format yang dapat dicari dan diedit.

## Bonus – Gambaran Visual (Teks Alt)

Berikut adalah diagram alur sederhana yang menggambarkan proses.  
*Alt text:* “Diagram yang menunjukkan cara mengekstrak teks dari gambar menggunakan pemrosesan batch Aspose OCR di C#”.

![Diagram alur OCR](placeholder-image-url.png)

*(Jika Anda mempublikasikan tutorial ini di situs statis, ganti placeholder dengan SVG atau PNG yang sebenarnya.)*

## Pertanyaan yang Sering Diajukan

**Apakah ini bekerja dengan file PDF?**  
Ya, Aspose OCR dapat membaca halaman PDF sebagai gambar. Anda hanya perlu mengonversi PDF ke gambar terlebih dahulu, atau menggunakan `PdfDocument` dari `Aspose.PDF` dan memberikan setiap gambar rasterisasi halaman ke `OcrEngine`.

**Bagaimana jika TIFF saya dilindungi kata sandi?**  
`BatchProcessor` tidak menangani enkripsi secara langsung. Dekripsi file menggunakan pustaka seperti `Aspose.Imaging` sebelum mengirimkannya ke pipeline OCR.

**Bisakah saya menghasilkan JSON alih-alih teks biasa?**  
Tentu saja. Ganti logika `StringBuilder` dengan serializer JSON (misalnya `System.Text.Json`) dan simpan teks setiap halaman di bawah kunci `pageNumber`.

## Contoh Lengkap yang Berfungsi

Berikut program lengkap yang dapat Anda salin‑tempel ke `Program.cs`. Termasuk semua directive `using`, penanganan error, dan komentar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

Jalankan program dengan:

```bash
dotnet run
```

Anda akan melihat pesan konsol yang mengonfirmasi keberhasilan, dan file output akan berisi hasil OCR yang digabungkan.

## Kesimpulan

Kami baru saja mendemonstrasikan cara praktis **mengekstrak teks dari gambar** menggunakan Aspose OCR, mengubah file hasil pindai multi‑halaman menjadi teks biasa yang dapat dicari. Dengan memanfaatkan `BatchProcessor` dan setup `OcrEngine` per halaman yang bersih, Anda dapat secara andal **mengonversi teks dokumen yang dipindai** sambil menjaga kode tetap sederhana dan mudah dipelihara.

Silakan bereksperimen: coba bahasa yang berbeda, ubah output menjadi JSON, atau integrasikan logika ini ke dalam API web yang memproses unggahan secara real‑time. Pola intinya tetap sama—muat, kenali, akumulasi, dan simpan.

Masih ada pertanyaan tentang OCR, lisensi Aspose, atau menangani batch dokumen besar? Tinggalkan komentar di bawah atau lihat dokumentasi resmi Aspose untuk penjelasan lebih mendalam. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}