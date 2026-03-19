---
category: general
date: 2026-03-18
description: Cara OCR PDF di C# – pelajari cara mengonversi PDF yang dipindai, membuat
  PDF yang dapat dicari, menambahkan watermark PDF, dan mengekstrak teks dari PDF
  dengan alur kerja OcrEngine yang sederhana.
draft: false
keywords:
- how to ocr pdf
- convert scanned pdf
- create searchable pdf
- add watermark pdf
- extract text from pdf
language: id
og_description: Cara melakukan OCR PDF di C#? Panduan ini menunjukkan cara mengonversi
  PDF yang dipindai, membuat PDF yang dapat dicari, menambahkan watermark pada PDF,
  dan mengekstrak teks dari PDF menggunakan OcrEngine.
og_title: Cara OCR PDF di C# – Panduan Cepat dan Lengkap
tags:
- OCR
- PDF
- C#
- Document Processing
title: Cara OCR PDF di C# – Mengonversi PDF yang Dipindai
url: /id/python-java/general/how-to-ocr-pdf-in-c-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR PDF di C# – Mengonversi PDF yang Dipindai

Pernah membutuhkan **cara OCR PDF** tetapi terhambat oleh file hasil pemindaian yang tidak mau bekerja? Anda bukan satu-satunya. Dalam banyak proyek dunia nyata—misalnya digitalisasi faktur atau pengarsipan laporan bersejarah—Anda berakhir dengan tumpukan gambar yang tersembunyi di dalam PDF, dan satu‑satunya cara agar dapat dicari adalah menjalankan OCR pada mereka.  

Berita baik? Dengan hanya beberapa baris C# Anda dapat **mengonversi PDF yang dipindai** menjadi **PDF yang dapat dicari**, menambahkan watermark halus, dan bahkan mengambil teks mentah untuk pemrosesan lebih lanjut. Di bawah ini Anda akan melihat contoh lengkap yang siap dijalankan dan melakukan hal tersebut.

## Apa yang Dibahas dalam Tutorial Ini

* Cara **cara OCR PDF** menggunakan kelas `OcrEngine`.  
* Mengubah PDF yang dipindai menjadi **PDF yang dapat dicari**.  
* Menambahkan watermark pada halaman pertama (**add watermark pdf**).  
* Mengambil string teks biasa dari hasil (**extract text from pdf**).  
* Kesulitan umum—seperti menangani dokumen multi‑halaman atau mengatasi pemindaian beresolusi rendah.  

Tidak ada tautan dokumentasi eksternal, tidak ada potongan kode setengah jadi. Semua yang Anda butuhkan ada di sini.

## Prasyarat

* .NET 6.0 atau lebih baru (kode ini juga dapat dikompilasi dengan .NET 5).  
* Referensi ke perpustakaan OCR yang menyediakan `OcrEngine` dan `ImageFormats` (misalnya, `Aspose.OCR` atau paket serupa).  
* File PDF input bernama `input.pdf` yang ditempatkan di folder yang Anda kontrol.  
* Familiaritas dasar dengan aplikasi konsol C#.  

Jika Anda sudah memiliki semuanya, bagus—mari kita mulai.

## Langkah 1: Siapkan Proyek dan Impor Dependensi

Buat proyek konsol baru dan tambahkan paket OCR melalui NuGet:

```bash
dotnet new console -n OcrPdfDemo
cd OcrPdfDemo
dotnet add package Aspose.OCR
```

Sekarang buka `Program.cs`. Di bagian atas, impor namespace yang Anda perlukan:

```csharp
using System;
using Aspose.OCR;          // OcrEngine lives here
using Aspose.OCR.Image;   // ImageFormats enum
```

*Mengapa ini penting*: Mengimpor namespace yang tepat memungkinkan compiler menemukan `OcrEngine`. Melewatkan langkah ini akan menghasilkan error `CS0246` dan menghentikan proses build Anda.

## Langkah 2: Inisialisasi Mesin OCR

Mesin adalah inti dari proses ini. Anda membuatnya sekali dan menggunakannya kembali untuk setiap halaman.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

*Tips pro*: Jika Anda berencana memproses banyak PDF secara berurutan, pertimbangkan untuk menggunakan kembali instance `engine` yang sama guna menghindari pemeriksaan lisensi berulang.

## Langkah 3: Muat PDF Sumber

Beritahu mesin file mana yang akan diproses. Metode `SetImageFromFile` menerima sumber gambar atau PDF apa pun.

```csharp
// Step 3: Load the scanned PDF you want to OCR
engine.SetImageFromFile(@"YOUR_DIRECTORY\input.pdf");
```

> **Mengapa langkah ini penting** – Mesin membutuhkan representasi bitmap dari setiap halaman. Ketika Anda memberinya PDF, mesin secara internal meraster setiap halaman berdasarkan DPI default (biasanya 300). Jika PDF sumber sudah berbasis teks, mesin akan melewatinya tanpa perubahan, menghemat waktu Anda.

## Langkah 4: Jalankan Pengakuan OCR

Sekarang pekerjaan berat dilakukan. Metode `Recognize` memindai setiap halaman, mengekstrak glyph, dan membangun lapisan yang dapat dicari.

```csharp
// Step 4: Perform OCR on the loaded document
engine.Recognize();
```

*Pertanyaan umum*: *Bagaimana jika PDF memiliki 50 halaman?*  
`Recognize` memproses seluruh dokumen secara default. Untuk lingkungan dengan memori terbatas, Anda dapat mengatur `engine.PageIndex` dan `engine.PageCount` untuk memproses halaman per halaman.

## Langkah 5: Simpan PDF yang Dapat Dicari (Watermark pada Halaman 1)

Kami akan menyimpan hasilnya sebagai PDF. Halaman pertama secara otomatis akan mendapatkan watermark karena perpustakaan OCR menambahkan overlay “Generated by Aspose.OCR” secara default. Jika Anda memerlukan watermark khusus, Anda dapat memodifikasi properti `engine.Watermark` sebelum menyimpan.

```csharp
// Step 5: Save the OCR‑processed PDF with a watermark on page 1
engine.Save(@"YOUR_DIRECTORY\output.pdf", ImageFormats.Pdf);
```

Setelah pemanggilan ini Anda akan memiliki **PDF yang dapat dicari** di mana Anda dapat memilih, menyalin, dan mencari teks seperti pada PDF asli mana pun.

## Langkah 6: Ekstrak Teks Biasa (Opsional namun Berguna)

Jika Anda juga ingin **mengekstrak teks dari pdf** untuk pengindeksan atau analisis lebih lanjut, mesin memberikan akses ke string mentah.

```csharp
// Step 6: Pull the recognized text into a string
string extractedText = engine.Text;
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(extractedText);
Console.WriteLine("=== Extracted Text End ===");
```

Properti `engine.Text` menggabungkan teks semua halaman, mempertahankan jeda baris. Anda dapat memisahkannya dengan `\f` (form feed) jika memerlukan granularitas per halaman.

## Contoh Program Lengkap

Berikut adalah program lengkap. Salin‑tempel ke `Program.cs`, ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif, dan jalankan `dotnet run`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            OcrEngine engine = new OcrEngine();

            // 2️⃣ Load the source PDF to be processed
            // Make sure the file exists; otherwise you'll get a FileNotFoundException.
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            engine.SetImageFromFile(inputPath);

            // 3️⃣ Perform OCR recognition on the loaded document
            engine.Recognize();

            // 4️⃣ Save the recognized document as a PDF (watermark appears on page 1)
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            engine.Save(outputPath, ImageFormats.Pdf);

            // 5️⃣ (Optional) Extract plain text for further use
            string extractedText = engine.Text;
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(extractedText);
            Console.WriteLine("=== Extracted Text End ===");

            Console.WriteLine($"OCR complete! Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Output yang Diharapkan

Menjalankan program mencetak teks yang diekstrak ke konsol dan membuat `output.pdf`. Buka PDF tersebut di penampil apa pun (Adobe Acrobat, Edge, dll.) dan coba cari kata yang muncul dalam pemindaian asli—Anda akan melihat bahwa kini dapat dicari. Halaman pertama menampilkan watermark default, mengonfirmasi langkah **add watermark pdf** berhasil.

## Pertanyaan yang Sering Diajukan & Kasus Khusus

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika pemindaian beresolusi rendah?** | Tingkatkan DPI sebelum pengenalan: `engine.ImageInfo.DpiX = engine.ImageInfo.DpiY = 600;` Ini memberi mesin OCR detail lebih banyak untuk diproses. |
| **Apakah saya dapat memilih watermark khusus?** | Ya. Atur `engine.Watermark = "Confidential – Processed on " + DateTime.Now.ToShortDateString();` sebelum `Save`. |
| **Bagaimana cara menangani PDF yang dilindungi kata sandi?** | Gunakan `engine.LoadPassword = "yourPassword";` sebelum `SetImageFromFile`. |
| **Apakah ada cara membatasi OCR hanya pada halaman tertentu?** | Atur `engine.PageIndex = 2;` dan `engine.PageCount = 5;` untuk memproses halaman 3‑7 saja. |
| **Bagaimana jika saya perlu menjaga gambar asli tidak berubah?** | Setelah OCR Anda dapat menggabungkan PDF asli dengan lapisan OCR menggunakan perpustakaan PDF (misalnya, `Aspose.PDF`) untuk mempertahankan fidelitas gambar. |

## Tips & Praktik Terbaik

* **Tips pro:** Jalankan OCR pada thread latar belakang jika Anda mengintegrasikannya ke dalam aplikasi UI—jika tidak, UI akan membeku.  
* **Waspadai:** PDF dengan konten raster dan vektor campuran. Mesin hanya akan OCR halaman raster; teks vektor tetap dapat dipilih secara otomatis.  
* **Penyesuaian kinerja:** Cache data bahasa OCR (`engine.Language = OcrLanguage.English;`) untuk menghindari memuat ulang pada setiap dokumen.  

## Kesimpulan

Anda kini memiliki solusi lengkap end‑to‑end untuk **cara OCR PDF** di C#. Dengan menginisialisasi `OcrEngine`, memuat file hasil pemindaian, mengenali teks, menyimpan **PDF yang dapat dicari**, menambahkan watermark, dan secara opsional **mengekstrak teks dari pdf**, Anda dapat mengubah PDF berbasis gambar apa pun menjadi aset yang dapat dicari dan diindeks.  

Langkah selanjutnya? Coba rangkai alur kerja ini dengan sistem manajemen dokumen, atau bereksperimen dengan bahasa lain (`engine.Language = OcrLanguage.French;`). Anda juga dapat menjelajahi pemrosesan batch banyak file dalam sebuah folder—cukup lakukan perulangan langkah-langkah dengan instance `engine` baru setiap kali.  

Selamat coding, semoga PDF Anda selalu dapat dicari! 

![Contoh Cara OCR PDF menampilkan file input dan output](https://example.com/ocr-pdf-demo.png "cara OCR PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}