---
category: general
date: 2026-03-13
description: Buat PDF yang dapat dicari dari gambar apa pun menggunakan Aspose OCR.
  Pelajari cara mengonversi gambar ke EPUB, menambahkan teks yang dapat dicari, dan
  menghasilkan PDF yang dapat dicari dalam C#.
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: id
og_description: Buat PDF yang dapat dicari dari gambar apa pun menggunakan Aspose
  OCR. Panduan ini menunjukkan cara mengonversi gambar ke EPUB, menambahkan teks yang
  dapat dicari, dan menghasilkan PDF yang dapat dicari dalam C#.
og_title: Buat PDF yang Dapat Dicari – Konversi Gambar ke EPUB & Tambahkan Teks
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: Buat PDF yang Dapat Dicari – Konversi Gambar ke EPUB & Tambahkan Teks
url: /id/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari – Konversi Gambar ke EPUB & Tambahkan Teks

Ingin **membuat PDF yang dapat dicari** dari kwitansi yang dipindai atau gambar apa pun? Dalam tutorial ini kami akan menunjukkan cara membuat PDF yang dapat dicari menggunakan Aspose OCR sekaligus **mengonversi gambar ke EPUB** dan **menambahkan lapisan teks yang dapat dicari**—semua dalam satu proyek C#.

Jika Anda pernah mengalami kesulitan dengan PDF yang tampak bagus tetapi tidak dapat dicari, Anda tidak sendirian. Kabar baiknya, lapisan teks tersembunyi dapat mengubah gambar datar menjadi dokumen yang sepenuhnya dapat dicari, dan Aspose membuatnya hampir tanpa rasa sakit.

## Apa yang Akan Anda Pelajari

* Cara menginisialisasi mesin Aspose OCR dan mengatur bahasa.  
* Langkah‑langkah tepat untuk **mengonversi gambar ke EPUB** untuk distribusi e‑book.  
* Cara mengonfigurasi penulis PDF sehingga outputnya berisi lapisan teks tersembunyi yang dapat dicari.  
* Tips menangani kasus khusus seperti kwitansi multi‑halaman atau bahasa non‑Inggris.  

Yang Anda perlukan sebelumnya hanyalah lingkungan pengembangan .NET (Visual Studio 2022 atau lebih baru) dan paket NuGet Aspose OCR. Tanpa layanan eksternal, tanpa file konfigurasi yang rumit—hanya C# biasa yang dapat Anda salin‑tempel dan jalankan.

## Prerequisites

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| .NET 6.0+   | Aspose OCR menargetkan .NET Standard 2.0+, jadi .NET 6 memberi Anda perbaikan runtime terbaru. |
| Aspose.OCR NuGet package | Menyediakan `OcrEngine`, `EpubWriter`, dan `PdfWriter` classes yang digunakan dalam kode. |
| An image file (e.g., `receipt.jpg`) | Sumber yang akan Anda jalankan OCR. Semua gambar raster (PNG, JPEG, BMP) dapat digunakan. |
| Basic C# knowledge | Anda akan membaca dan menyesuaikan potongan kode, bukan belajar bahasa dari awal. |

Anda dapat menginstal paket dengan perintah berikut:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, UI NuGet Package Manager melakukan pekerjaan yang sama—cukup cari “Aspose.OCR”.

## Step 1 – Buat PDF yang Dapat Dicari dengan Aspose OCR

Hal pertama yang kita butuhkan adalah instance `OcrEngine` yang mengetahui bahasa mana yang harus dikenali. Bahasa Inggris adalah default, tetapi Anda dapat menggantinya dengan bahasa Prancis, Jerman, dll., dengan mengatur `ocrEngine.Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

Mengapa menginisialisasi mesin terlebih dahulu? Mesin menyimpan model pengenalan di memori, jadi membuatnya sekali dan menggunakan kembali pada beberapa gambar menghemat CPU dan RAM. Pada pekerjaan batch yang lebih besar, Anda akan mempertahankan instance yang sama tetap hidup selama seluruh proses.

## Step 2 – Muat Gambar dan Lakukan OCR

Selanjutnya kami mengarahkan mesin ke file yang ingin diproses. `ImageStream.FromFile` membaca gambar ke dalam format yang dipahami mesin OCR.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **Bagaimana jika gambar memiliki banyak halaman?**  
> Aspose OCR dapat menangani TIFF multi‑halaman secara langsung. Cukup berikan path ke file TIFF; mesin akan mengiterasi setiap halaman secara otomatis.

## Step 3 – Konversi Gambar ke EPUB

Jika Anda juga memerlukan versi e‑book dari dokumen yang dipindai, Aspose membuatnya menjadi satu baris kode. `EpubWriter` menggunakan instance `OcrEngine` yang sama, artinya hasil OCR digunakan kembali tanpa pemrosesan tambahan.

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

Mengapa mengekspor ke EPUB? EPUB adalah format yang dapat mengalir ulang—sempurna untuk pembaca seluler. Teks OCR menjadi dapat dipilih, dan gambar asli tetap sebagai latar belakang, mempertahankan tampilan pemindaian asli.

## Step 4 – Tambahkan Lapisan Teks yang Dapat Dicari ke PDF

Sekarang tiba bagian yang sebenarnya **membuat PDF yang dapat dicari**. Dengan mengaktifkan `AddSearchableTextLayer`, penulis PDF menyisipkan lapisan teks tak terlihat yang mencerminkan output OCR. Pengguna dapat mencari, menyalin, atau menyorot teks seperti pada PDF asli.

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **Kesalahan umum:** Lupa mengatur `AddSearchableTextLayer` menghasilkan PDF yang tampak sama tetapi tidak mengandung teks yang dapat dicari. Selalu periksa kembali flag ini ketika Anda membutuhkan dokumen yang dapat dicari.

## Step 5 – Contoh Kerja Lengkap

Menggabungkan semuanya, berikut contoh aplikasi konsol mandiri yang dapat Anda masukkan ke dalam proyek .NET baru dan jalankan segera.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### Expected Output

* `receipt.epub` – file EPUB yang dapat Anda buka di Calibre, Apple Books, atau e‑reader apa pun.  
* `receipt_searchable.pdf` – PDF di mana Anda dapat menekan **Ctrl + F** dan menemukan kata apa pun yang muncul di gambar asli.

Jika Anda membuka PDF di Adobe Acrobat dan melihat **File → Properties → Description**, Anda akan melihat aliran teks tersembunyi di bawah tab **Fonts**, yang mengonfirmasi bahwa lapisan yang dapat dicari ada.

## Common Questions & Edge Cases

**Q: Apakah ini bekerja dengan bahasa non‑Inggris?**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}