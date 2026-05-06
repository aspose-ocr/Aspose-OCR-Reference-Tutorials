---
category: general
date: 2026-05-06
description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose OCR di C#.
  Pelajari cara mengonversi PNG ke PDF, mengekstrak teks dari gambar, dan menghasilkan
  PDF yang dapat dicari.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: id
og_description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose OCR di C#.
  Tutorial langkah demi langkah ini menunjukkan cara mengonversi PNG ke PDF, mengekstrak
  teks dari gambar, dan menghasilkan PDF yang dapat dicari.
og_title: Buat PDF yang dapat dicari dari gambar – Panduan OCR Aspose C#
tags:
- Aspose
- C#
- OCR
- PDF
title: Buat PDF yang dapat dicari dari Gambar – Panduan OCR Aspose C#
url: /id/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang dapat dicari dari Gambar – Panduan C# Aspose OCR

Pernahkah Anda perlu **create searchable PDF** dari gambar yang dipindai tetapi tidak yakin harus mulai dari mana? Mungkin Anda memiliki struk PNG, JPEG dari kontrak, atau bitmap apa pun yang ingin Anda ubah menjadi PDF yang sebenarnya dapat Anda cari. Itu adalah titik sakit yang umum, terutama ketika Anda berurusan dengan pemindaian lama yang menganggur di sebuah folder.

Kabar baiknya, dengan Aspose OCR Anda dapat **convert image to PDF**, mengambil teks tersembunyi, dan menghasilkan dokumen yang sepenuhnya dapat dicari—semua dalam beberapa baris C#. Dalam panduan ini kami juga akan menunjukkan cara **convert png to PDF**, **extract text from image**, dan bahkan membahas kasus tepi penanganan TIFF multi‑halaman. Pada akhir tutorial, Anda akan memiliki solusi mandiri yang dapat Anda sisipkan ke proyek .NET mana pun.

## Apa yang Anda Butuhkan

- **.NET 6+** (kode ini juga berfungsi pada .NET Framework 4.6+)
- **Visual Studio 2022** atau IDE apa pun yang Anda sukai
- Paket NuGet **Aspose.OCR** (paket ini secara otomatis menyertakan Aspose.PDF)
- File gambar (PNG, JPEG, BMP, TIFF) yang ingin Anda ubah menjadi PDF yang dapat dicari

Tidak ada trik lisensi tambahan, tidak ada layanan eksternal—hanya satu referensi NuGet dan beberapa menit coding.

## Langkah 1: Instal Paket NuGet Aspose.OCR

Pertama-tama, tambahkan pustaka ke proyek Anda. Buka Package Manager Console dan jalankan:

```powershell
Install-Package Aspose.OCR
```

Perintah tunggal itu mengunduh baik **Aspose.OCR** maupun assembly **Aspose.Pdf** yang menjadi dependensinya, sehingga Anda siap untuk membaca gambar dan menulis PDF.

> **Pro tip:** Jika Anda menggunakan .NET CLI, setaraannya adalah `dotnet add package Aspose.OCR`.

## Langkah 2: Inisialisasi Mesin OCR

Membuat instance `OcrEngine` adalah gerbang ke semua pekerjaan OCR. Anggaplah itu sebagai otak yang akan melihat gambar Anda dan mulai “membaca” karakter.

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

Anda mungkin bertanya, *mengapa tidak langsung memanggil metode statis?* Pendekatan berorientasi objek memungkinkan Anda menyesuaikan pengaturan nanti (bahasa, resolusi, dll.) tanpa mengubah alur keseluruhan.

## Langkah 3: Muat Gambar yang Ingin Anda Konversi

Di sinilah kami **convert image to PDF** secara konseptual—dengan memberi bitmap ke mesin OCR. Ganti `"YOUR_DIRECTORY/input.png"` dengan jalur sebenarnya ke file Anda.

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

Jika Anda memiliki skenario **convert png to pdf**, cukup arahkan ke PNG tersebut. Untuk TIFF multi‑halaman, Aspose.OCR secara otomatis memperlakukan setiap frame sebagai halaman terpisah.

## Langkah 4: Jalankan OCR dan Opsional Ambil Teks

Menjalankan `Recognize()` melakukan pekerjaan berat: ia menganalisis gambar, mendeteksi karakter, dan mengembalikan hasil terstruktur. Anda dapat menyimpan teks untuk logging, pengindeksan pencarian, atau tampilan.

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **Why extract text?** Meskipun kami akan menyematkannya dalam PDF akhir, memiliki string mentah dapat berguna untuk validasi atau analitik.

## Langkah 5: Konfigurasikan Opsi PDF untuk Dokumen yang Dapat Dicari

Aspose.PDF memberi kami mode khusus `PdfSaveOptions` bernama **CreateSearchablePdf**. Mode ini memberi tahu pustaka untuk menyematkan teks OCR sebagai lapisan tak terlihat di belakang gambar, sehingga PDF menjadi dapat dicari.

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

Jika Anda pernah membutuhkan PDF hanya gambar (tanpa teks tersembunyi), Anda dapat beralih ke `PdfSaveOptions.CreatePdf()` sebagai gantinya. Tetapi untuk tujuan kami—**create searchable PDF**—mode dapat dicari adalah bintangnya.

## Langkah 6: Simpan PDF yang Dapat Dicari ke Disk

Sekarang kami mengikat semuanya bersama. Metode `SavePdf` menulis gambar dan teks tersembunyi ke dalam satu file.

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

Pada titik ini Anda memiliki **searchable PDF** yang dapat Anda buka di Adobe Reader, ketik kata di kotak pencarian, dan langsung melompat ke lokasi yang cocok—meskipun halaman yang terlihat masih hanya gambar asli.

## Contoh Kerja Lengkap

Menggabungkan semua bagian, berikut adalah aplikasi konsol siap‑jalankan. Salin‑tempel ke proyek C# baru, sesuaikan jalur file, dan tekan **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### Output yang Diharapkan

Saat Anda menjalankan program, konsol akan menampilkan sesuatu seperti:

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

Dan di `YOUR_DIRECTORY` Anda akan menemukan `output.pdf`. Buka, tekan **Ctrl F**, ketik “Invoice”, dan Anda akan langsung melompat ke kata tersebut—meskipun halaman tampak seperti pemindaian datar.

## Menangani Variasi Umum

### Mengonversi Beberapa Gambar Sekaligus

Jika Anda memiliki folder penuh PNG dan menginginkan satu PDF yang dapat dicari, lakukan loop pada file‑file tersebut dan tambahkan masing‑masing sebagai halaman terpisah:

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

Anda juga dapat menggunakan `PdfFileEditor` dari Aspose.PDF untuk menggabungkan PDF sementara menjadi satu file akhir.

### Menangani Scan Resolusi Rendah

Akurasi OCR menurun ketika DPI gambar di bawah 150. Sebelum memberi gambar ke OCR, Anda dapat memperbesarnya:

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### Memilih Bahasa Spesifik

Jika dokumen Anda bukan bahasa Inggris, atur bahasa sebelum `Recognize()`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

Penyesuaian ini memastikan bahwa **extract text from image** berfungsi secara andal di berbagai skenario.

## Hasil Visual

![PDF yang dapat dicari dibuat dengan Aspose OCR – buat PDF yang dapat dicari](https://example.com/images/searchable-pdf.png)

*Cuplikan layar di atas menunjukkan PDF di mana gambar terlihat, tetapi lapisan teks dapat dicari.*

## Kesimpulan

Anda kini memiliki resep lengkap dan siap produksi untuk **create searchable PDF** dari gambar apa pun menggunakan Aspose OCR dan C#. Kami telah membahas cara **convert image to PDF**, **extract text from image**, dan bahkan menyentuh kasus tepi **convert png to pdf** serta **ocr image to pdf**. Kode ini sepenuhnya mandiri, berjalan pada runtime .NET apa pun, dan dapat diperluas untuk pemrosesan batch atau dukungan bahasa khusus.

Apa selanjutnya? Cobalah menambahkan watermark, mengenkripsi PDF, atau memasukkan teks yang diekstrak ke indeks pencarian seperti Elasticsearch. Kemungkinannya tak terbatas, dan pola yang sama—load → recognize → save—akan melayani Anda dengan baik untuk alur kerja berbasis OCR apa pun.

Jika Anda mengalami kendala atau memiliki kasus penggunaan menarik untuk dibagikan, tinggalkan komentar di bawah. Selamat coding, dan nikmati mengubah pemindaian keras kepala menjadi emas yang dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}