---
category: general
date: 2026-02-14
description: Pelajari cara melakukan OCR pada file TIFF atau gambar dan mengonversi
  PDF menggunakan OCR untuk membuat PDF yang dapat dicari—panduan C# langkah demi
  langkah.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: id
og_description: Temukan cara melakukan OCR pada gambar, mengonversi PDF menggunakan
  OCR, dan membuat PDF yang dapat dicari dengan Aspose OCR dalam tutorial C# yang
  singkat.
og_title: Cara Melakukan OCR dan Membuat PDF yang Dapat Dicari di C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: Cara Melakukan OCR dan Membuat PDF yang Dapat Dicari di C#
url: /id/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

for lists: we have bullet lists and numbered lists.

Make sure headings have same number of #.

Now produce final output with all content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR dan Membuat PDF yang Dapat Dicari di C#

Pernah membutuhkan **perform OCR** pada dokumen yang dipindai tetapi tidak yakin bagaimana mengubah hasilnya menjadi **searchable PDF**? Anda tidak sendirian—banyak pengembang mengalami kendala tersebut saat menangani arsip TIFF lama atau PDF yang hanya berisi gambar. Kabar baiknya? Dengan beberapa baris C# dan pustaka Aspose.OCR, Anda dapat mengonversi TIFF atau gambar apa pun menjadi PDF yang sepenuhnya dapat dicari dalam hitungan detik.

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui: mulai dari menginstal pustaka, memuat TIFF multi‑halaman, hingga memanggil `RecognizeToPdf` sehingga Anda dapat **convert PDF using OCR** dan **make searchable PDF** yang dapat dicari oleh pengguna Anda. Pada akhir tutorial, Anda akan memiliki aplikasi konsol siap‑jalankan yang menghasilkan **searchable PDF** dari sumber gambar.

## Prasyarat

- **.NET 6.0** atau lebih baru (kode juga berfungsi pada .NET Framework 4.7+).
- Lisensi **Aspose.OCR** yang valid atau kunci evaluasi sementara (versi percobaan gratis sudah cukup untuk pengujian).
- Visual Studio 2022 (atau editor apa pun yang Anda sukai) dengan manajer paket **NuGet**.
- File input bernama `input.tif` ditempatkan di folder yang Anda kontrol—TIFF multi‑halaman langsung dapat digunakan.

> **Pro tip:** Jika Anda menggunakan Windows, salin TIFF ke folder yang sama dengan `.exe` yang telah dikompilasi untuk menghindari masalah terkait jalur.

## Langkah 1: Instal Paket NuGet Aspose.OCR

Buka folder proyek Anda di terminal dan jalankan:

```bash
dotnet add package Aspose.OCR
```

## Langkah 2: Buat Aplikasi Konsol Minimal

Buat proyek konsol baru jika Anda belum memilikinya:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Ganti `Program.cs` yang dihasilkan secara otomatis dengan kode lengkap yang ditampilkan pada **Step 3**. Program akan:

1. Membuat instance mesin OCR.
2. Memuat gambar sumber (atau TIFF multi‑halaman).
3. Menjalankan OCR dan menulis output langsung ke **searchable PDF**.
4. Memberi tahu pengguna bahwa proses berhasil.

## Langkah 3: Kode Lengkap – Dari Gambar ke **Searchable PDF**

Berikut adalah file sumber **seluruh**. Salin‑tempel ke `Program.cs`. Komentar disertakan untuk menjelaskan bagian yang tidak jelas.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**What you’ll see:** Setelah menjalankan program, file bernama `searchable.pdf` muncul di folder target. Buka dengan Adobe Reader atau penampil PDF apa pun dan coba cari kata yang ada di TIFF asli. Teks akan ditemukan secara instan, membuktikan bahwa Anda berhasil **made searchable PDF** dari sebuah gambar.

### Menjalankan Aplikasi

```bash
dotnet run
```

Jika semuanya telah diatur dengan benar, Anda akan mendapatkan:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

Buka PDF, tekan `Ctrl+F`, ketik kata dari sumber, dan lihat sorotan melompat ke lokasi yang tepat.

## Langkah 4: Variasi Umum dan Kasus Tepi

### Mengonversi PDF Biasa (hanya gambar) ke **Searchable PDF**

Jika sumber Anda adalah PDF yang berisi gambar hasil pemindaian bukan teks, Anda masih dapat menggunakan metode yang sama—cukup ubah sumber `ImageStream`:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Hal itu memenuhi skenario **convert pdf using OCR** tanpa kode tambahan.

### Menangani Dokumen Multi‑Halaman Besar

Untuk dokumen yang melebihi beberapa ratus halaman, pertimbangkan:

- **Increasing memory limits** (`Engine.MemoryLimit = 2_000; // MB`).
- **Processing in chunks**: muat subset halaman, tulis PDF menengah, lalu gabungkan menggunakan pustaka PDF (mis., Aspose.PDF).

### Menangani Bahasa Selain Bahasa Inggris

Aspose.OCR mendukung banyak bahasa secara langsung. Atur bahasa sebelum pengenalan:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Jika Anda membutuhkan **tiff to searchable pdf** dalam skrip non‑Latin, pastikan paket bahasa yang sesuai telah diinstal.

### Bagaimana Jika PDF Output Kosong?

- Verifikasi bahwa file input tidak rusak.
- Pastikan mesin OCR memiliki lisensi yang valid—mode evaluasi mungkin memberlakukan batasan halaman.
- Periksa bahwa resolusi gambar setidaknya 300 dpi; resolusi lebih rendah dapat menyebabkan pengenalan yang buruk.

## Langkah 5: Memverifikasi Hasil Secara Programatis (Opsional)

Terkadang Anda ingin memastikan bahwa PDF memang berisi lapisan teks. Anda dapat menggunakan Aspose.PDF untuk mengekstrak teks:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

Jika `extracted` tidak kosong, Anda telah berhasil **made searchable pdf**.

## Kesimpulan

Kami telah membahas **how to perform OCR** pada TIFF (atau gambar apa pun) dan secara mulus **convert PDF using OCR** untuk membuat **searchable PDF** yang berperilaku seperti dokumen asli. Langkah kunci adalah:

1. Instal Aspose.OCR.  
2. Inisialisasi `Engine`.  
3. Muat gambar melalui `ImageStream`.  
4. Panggil `RecognizeToPdf`.  

Dari sana Anda dapat bereksperimen dengan pengaturan bahasa, pemrosesan batch besar, atau menggabungkan output dengan tugas manipulasi PDF lainnya. Pola yang sama berlaku untuk **tiff to searchable pdf**, **searchable pdf from image**, dan bahkan PDF yang dipindai.

Siap untuk tantangan berikutnya? Coba sematkan OCR ke dalam API web sehingga pengguna dapat mengunggah pemindaian dan menerima **searchable PDFs** secara instan, atau jelajahi OCR pada catatan tulisan tangan menggunakan pengaturan lanjutan `OcrEngine`. Kemungkinannya tidak terbatas—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}