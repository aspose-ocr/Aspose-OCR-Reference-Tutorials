---
category: general
date: 2026-02-19
description: Buat PDF yang dapat dicari dari gambar menggunakan C# dan Aspose OCR.
  Pelajari cara mengekstrak teks dari gambar dan mengubah gambar menjadi PDF yang
  dapat dicari.
draft: false
keywords:
- create searchable pdf
- extract text from image
- image to searchable pdf
- ocr image c#
- searchable pdf from image
language: id
og_description: Buat PDF yang dapat dicari dari gambar di C# dengan Aspose OCR. Tutorial
  ini menunjukkan langkah demi langkah cara mengekstrak teks dari gambar dan menghasilkan
  PDF yang dapat dicari.
og_title: Buat PDF yang Dapat Dicari dari Gambar di C# – Panduan Lengkap
tags:
- C#
- OCR
- PDF
title: Buat PDF yang Dapat Dicari dari Gambar di C# – Panduan Lengkap
url: /id/net/text-recognition/create-searchable-pdf-from-image-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari Gambar di C# – Panduan Lengkap

Pernah perlu **create searchable PDF** dari kontrak yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian; banyak pengembang mengalami hal ini saat pertama kali menangani alur kerja berbasis OCR. Kabar baiknya, dengan beberapa baris C# dan Aspose OCR Anda dapat mengubah bitmap apa pun (TIFF, JPEG, PNG…) menjadi PDF yang dapat dicari dalam hitungan detik.  

Dalam tutorial ini kami akan membahas seluruh proses—dari menginstal pustaka, mengekstrak teks dari gambar, hingga menulis file **image to searchable PDF** akhir. Sepanjang jalan kami juga akan menyentuh cara **extract text from image** untuk skenario lain, dan mengapa “lapisan teks tersembunyi” penting bagi mesin pencari downstream.

> **Catatan cepat:** Semua kode di bawah ini siap dijalankan; Anda tidak perlu mencari potongan kode tambahan atau dokumentasi eksternal.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:

| Prasyarat | Mengapa penting |
|--------------|----------------|
| .NET 6 SDK (atau lebih baru) | Fitur bahasa modern dan kinerja yang lebih baik |
| Visual Studio 2022 (atau VS Code) | IDE dengan IntelliSense memudahkan kerja |
| Paket NuGet Aspose.OCR | Menyediakan mesin OCR dan penulis PDF |
| Gambar contoh (`input.tif`) | Sumber yang akan Anda konversi menjadi PDF yang dapat dicari |

Jika Anda sudah memiliki proyek .NET, Anda dapat melewati langkah “Create a new project” dan langsung ke instalasi NuGet.

## Langkah 1: Instal Paket NuGet Aspose OCR

Hal pertama yang harus dilakukan—tambahkan pustaka yang melakukan pekerjaan berat.

```bash
dotnet add package Aspose.OCR
```

Baris satu itu mengunduh mesin OCR inti, penulis PDF, dan semua dependensi native. Di Visual Studio Anda juga dapat klik kanan proyek → **Manage NuGet Packages** → cari *Aspose.OCR* dan klik **Install**.

> **Tip pro:** Jaga paket tetap terbaru. Hingga saat ini (Feb 2026) versi 23.9 adalah yang terbaru dan mencakup perbaikan kinerja untuk TIFF beresolusi tinggi.

## Langkah 2: Siapkan Kerangka Proyek

Buat aplikasi konsol sederhana jika Anda belum memilikinya:

```bash
dotnet new console -n PdfDemo
cd PdfDemo
```

Buka `Program.cs` (atau `PdfDemo.cs` jika Anda lebih suka kelas bernama) dan hapus kode “Hello World” default. Kami akan menggantinya dengan contoh lengkap yang dapat dijalankan yang **creates searchable PDF** dari sebuah gambar.

## Langkah 3: Inisialisasi Mesin OCR – “Extract Text from Image”

Mesin OCR perlu mengetahui bahasa apa yang Anda pindai. Untuk kebanyakan kontrak berbahasa Inggris, Anda akan mengatur `Language.English`. Jika Anda memiliki dokumen multibahasa, Aspose mendukung paket bahasa yang dapat Anda muat nanti.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;

class PdfDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // 2️⃣ Perform OCR on the input image – this is where we **extract text from image**
        OcrResult ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/input.tif");

        // 3️⃣ Write the OCR result to a searchable PDF (image + hidden text layer)
        PdfResultWriter.Write(ocrResult, @"YOUR_DIRECTORY/contract_searchable.pdf");

        // 4️⃣ Notify that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

### Mengapa kami menginisialisasi mesin dengan cara ini

* **Pemilihan bahasa** memberi tahu pengenalan karakter set apa yang diharapkan, secara dramatis meningkatkan akurasi.  
* **`RecognizeImage`** mengembalikan `OcrResult` yang berisi bitmap asli serta teks Unicode yang diekstrak. Representasi ganda ini memungkinkan konversi **image to searchable PDF** nanti.

## Langkah 4: Tulis Lapisan Teks Tersembunyi – Menghasilkan **Image to Searchable PDF**

`PdfResultWriter` mengambil `OcrResult` dan membuat PDF dimana setiap halaman menampilkan gambar raster asli **ditambah** lapisan teks tak terlihat. Mesin pencari (dan penampil PDF) dapat mengindeks teks tersembunyi itu, menjadikan dokumen dapat dicari.

```csharp
// Inside Main, after OCR succeeds
PdfResultWriter.Write(ocrResult, @"YOUR_DIRECTORY/contract_searchable.pdf");
```

Di balik layar, Aspose menyematkan teks menggunakan atribut *ActualText* PDF. Jika Anda membuka file hasil di Adobe Acrobat dan melakukan pemilihan teks, Anda akan melihat bahwa Anda dapat menyalin kata‑kata yang mendasarinya meskipun mereka dirender sebagai bagian dari gambar.

## Langkah 5: Verifikasi Output

Jalankan program:

```bash
dotnet run
```

Anda harus melihat:

```
Searchable PDF created.
```

Arahkan ke `YOUR_DIRECTORY` dan buka `contract_searchable.pdf`. Coba pilih sebuah kata—jika pemilihan menyorot teks tak terlihat, Anda telah berhasil **create searchable pdf** dari gambar asli Anda.

### Pemeriksaan cepat

*Buka PDF dalam pengekstrak teks (mis., Adobe Reader → Edit → Copy). Jika Anda dapat menempelkan teks yang dapat dibaca, lapisan tersembunyi berfungsi.* Jika Anda mendapatkan karakter yang kacau, periksa kembali bahwa gambar sumber memiliki resolusi yang cukup (300 dpi adalah baseline yang baik).

## Langkah 6: Menangani Kasus Tepi Umum

### Pemindaian Resolusi Rendah

Jika TIFF Anda di bawah 200 dpi, akurasi OCR dapat menurun. Membesarkan gambar sebelum pengenalan (menggunakan `System.Drawing` atau `ImageSharp`) sering menghasilkan hasil yang lebih baik.

```csharp
using System.Drawing;

// Load, upscale, then feed to OCR
Bitmap lowRes = new Bitmap(@"YOUR_DIRECTORY/input.tif");
Bitmap highRes = new Bitmap(lowRes, new Size(lowRes.Width * 2, lowRes.Height * 2));
highRes.Save(@"YOUR_DIRECTORY/upscaled.tif");
```

### Dokumen Multi‑Halaman

Saat menangani TIFF multi‑halaman, lakukan loop melalui setiap frame:

```csharp
using System.Drawing.Imaging;

// Assume input.tif contains multiple frames
using (Image multiPage = Image.FromFile(@"YOUR_DIRECTORY/input.tif"))
{
    int pageCount = multiPage.GetFrameCount(FrameDimension.Page);
    for (int i = 0; i < pageCount; i++)
    {
        multiPage.SelectActiveFrame(FrameDimension.Page, i);
        string tempPath = $@"YOUR_DIRECTORY/page_{i}.tif";
        multiPage.Save(tempPath, ImageFormat.Tiff);

        OcrResult pageResult = ocrEngine.RecognizeImage(tempPath);
        PdfResultWriter.Write(pageResult, $@"YOUR_DIRECTORY/page_{i}_searchable.pdf");
    }
}
```

Anda kemudian dapat menggabungkan PDF individual menggunakan Aspose.PDF atau pustaka PDF lainnya.

## Contoh Kerja Lengkap (Semua Langkah dalam Satu File)

Berikut adalah program lengkap yang berdiri sendiri yang dapat Anda salin‑tempel ke `Program.cs`. Program ini mencakup instalasi, OCR, pembuatan PDF, dan pembungkus penanganan error sederhana.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;

class PdfDemo
{
    static void Main()
    {
        // Path to the source image – adjust to your environment
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        const string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";

        try
        {
            // 👉 Step 1: Initialize OCR engine (English language)
            OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

            // 👉 Step 2: Run OCR – this **extracts text from image**
            Console.WriteLine("Running OCR on image...");
            OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 👉 Step 3: Convert OCR result to a searchable PDF
            Console.WriteLine("Creating searchable PDF...");
            PdfResultWriter.Write(ocrResult, outputPath);

            Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

### Hasil yang Diharapkan

* Sebuah file bernama `contract_searchable.pdf` muncul di direktori Anda.  
* Membukanya di penampil PDF apa pun menampilkan pemindaian asli, tetapi memilih teks menyalin kata‑kata sebenarnya.  
* Mencari dalam dokumen (Ctrl + F) menemukan istilah yang diekstrak secara instan.

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan bahasa lain?**  
J: Tentu saja. Ganti `Language.English` dengan `Language.French`, `Language.German`, dll., atau muat paket bahasa khusus dari Aspose.

**T: Bagaimana jika saya membutuhkan PDF yang hanya berisi teks?**  
J: Setelah OCR Anda dapat melewatkan gambar dan menggunakan `PdfResultWriter.WriteTextOnly(ocrResult, path)` (tersedia di versi Aspose yang lebih baru).

**T: Bisakah saya menyematkan font untuk meningkatkan rendering?**  
J: Ya. Penulis PDF secara otomatis menyematkan set font standar, tetapi Anda dapat menyediakan objek `PdfSaveOptions` khusus jika memerlukan font perusahaan.

## Kesimpulan

Kami baru saja **create searchable pdf** dari sebuah gambar menggunakan C# dan Aspose OCR, mencakup semua hal mulai dari **extract text from image** hingga file **image to searchable pdf** akhir. Potongan kode ini siap produksi, dan Anda kini memiliki fondasi yang kuat untuk menangani batch yang lebih besar, bahasa yang berbeda, atau bahkan mengintegrasikan alur ini ke dalam API web.

### Apa Selanjutnya?

* Coba konversi seluruh folder pemindaian menjadi satu PDF yang dapat dicari yang digabungkan.  
* Bereksperimen dengan fitur enkripsi Aspose PDF untuk

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}