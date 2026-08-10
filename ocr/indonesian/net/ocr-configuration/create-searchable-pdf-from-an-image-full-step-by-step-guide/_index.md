---
category: general
date: 2026-06-06
description: Pelajari cara membuat PDF yang dapat dicari dan mengonversi gambar ke
  PDF dengan OCR. Termasuk penambahan lapisan, pengaturan kompresi, dan kode C# lengkap.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- how to ocr image
- how to add layer
- how to set compression
language: id
og_description: Buat PDF yang dapat dicari dari gambar menggunakan OCR. Panduan ini
  menunjukkan cara menambahkan lapisan teks tersembunyi, mengatur kompresi, dan mengonversi
  gambar ke PDF.
og_title: Buat PDF yang Dapat Dicari – Tutorial Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  headline: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  name: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - The
      Aspose.OCR and Aspose.Pdf NuGet packages (or any equivalent library that offers
      `OcrEngine` and `PdfSaveOptions`). - A sample image, e.g., `invoice.png`, placed
      in a folder you can reference. - A basic understanding of C# syntax'
  - name: Full Working Example
    text: 'Putting it all together, here’s the complete, ready‑to‑run program:'
  - name: Pro tip
    text: If you need to **convert image to PDF** without OCR (just a plain image
      PDF), set `AddTextLayer = false`. The same `PdfSaveOptions` still lets you control
      compression, which is handy for archiving scanned documents that don’t need
      searchability.
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: Buat PDF yang Dapat Dicari dari Gambar – Panduan Langkah demi Langkah Lengkap
url: /id/net/ocr-configuration/create-searchable-pdf-from-an-image-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari – Tutorial Lengkap C#

Pernah bertanya-tanya bagaimana cara **membuat PDF yang dapat dicari** dari faktur yang dipindai tanpa menghabiskan berjam‑jam dengan alat GUI? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mereka harus mengubah gambar menjadi PDF yang tampak seperti aslinya dan memungkinkan pengguna menyalin atau mencari teks.  

Dalam tutorial ini kami akan memandu Anda melalui langkah‑langkah tepat untuk **convert image to pdf**, menjalankan OCR padanya, menambahkan lapisan teks tersembunyi, dan bahkan menyesuaikan pengaturan kompresi. Pada akhir tutorial Anda akan memiliki potongan kode C# siap pakai yang dapat Anda sisipkan ke proyek .NET mana pun.

## Apa yang Akan Anda Pelajari

- Siapkan mesin OCR dan pahami **how to OCR image** file.
- Gunakan opsi **how to add layer** untuk menyematkan lapisan teks yang dapat dicari.
- Terapkan **how to set compression** untuk PDF yang lebih kecil dan terkompresi zip.
- Ubah gambar biasa menjadi alur kerja **create searchable pdf** yang dapat Anda otomatisasi.
- Jebakan umum dan tip profesional untuk menjaga PDF Anda tetap tajam dan cepat.

### Prasyarat

- .NET 6.0 atau lebih baru (kode juga berfungsi pada .NET Framework 4.7+).
- Paket NuGet Aspose.OCR dan Aspose.Pdf (atau perpustakaan setara yang menyediakan `OcrEngine` dan `PdfSaveOptions`).
- Sebuah gambar contoh, misalnya `invoice.png`, ditempatkan di folder yang dapat Anda referensikan.
- Pemahaman dasar tentang sintaks C#—tidak memerlukan pengetahuan OCR yang mendalam.

> **Pro tip:** Jika Anda menggunakan Visual Studio, instal paket-paket tersebut melalui Package Manager Console:  
> `Install-Package Aspose.OCR`  
> `Install-Package Aspose.Pdf`

---

![Contoh PDF yang dapat dicari menunjukkan gambar faktur yang diubah menjadi PDF dengan lapisan teks tersembunyi](/images/create-searchable-pdf.png)

## Langkah 1: Inisialisasi Mesin OCR – **how to ocr image**

Pertama, kita memerlukan mesin OCR yang dapat membaca teks bahasa Inggris dari gambar kita. Kelas `OcrEngine` adalah titik masuk; Anda cukup mengatur bahasa dan kemudian memberikannya gambar.

```csharp
using Aspose.OCR;
using Aspose.Pdf;

// Create and configure the OCR engine
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

*Mengapa ini penting:* Menginisialisasi mesin dengan bahasa yang tepat secara dramatis meningkatkan akurasi. Jika Anda melewatkannya, Anda mungkin mendapatkan karakter yang kacau.

## Langkah 2: Muat Gambar – **convert image to pdf**

Sekarang kami mengarahkan mesin ke file yang ingin diproses. `ImageStream.FromFile` membaca byte dan menyiapkannya untuk OCR.

```csharp
// Load the image you want to turn into a searchable PDF
engine.Image = ImageStream.FromFile(@"C:\Docs\invoice.png");
```

Anda juga dapat memuat dari `MemoryStream` jika gambar berasal dari permintaan web atau basis data.

## Langkah 3: Jalankan Pengakuan OCR – **how to ocr image**

Dengan gambar dimuat, proses berat terjadi dalam satu panggilan. Metode `Recognize` mengembalikan `OcrResult` yang berisi teks yang diekstrak serta bitmap asli.

```csharp
// Perform OCR on the loaded image
OcrResult ocrResult = engine.Recognize();
```

*Di balik layar:* Mesin menganalisis setiap piksel, mendeteksi karakter, dan membangun string Unicode. Ia juga menyimpan data posisi yang diperlukan untuk lapisan teks tersembunyi nanti.

## Langkah 4: Konfigurasikan Opsi Penyimpanan PDF – **how to add layer** & **how to set compression**

Di sinilah keajaiban PDF yang dapat dicari terjadi. Kami membuat objek `PdfSaveOptions` yang memberi tahu Aspose.Pdf cara menyematkan gambar asli, menambahkan lapisan teks tersembunyi, dan mengompres file akhir.

```csharp
// Set up PDF options for a searchable PDF
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    IncludeImage = true,          // Keep the original image in the PDF
    AddTextLayer = true,          // Add a hidden text layer with OCR results
    Compression = PdfCompression.Zip   // Use ZIP compression for smaller size
};
```

- **IncludeImage** memastikan kesetiaan visual pemindaian asli.
- **AddTextLayer** membuat lapisan tak terlihat yang dapat diindeks oleh peramban dan pembaca PDF untuk pencarian.
- **Compression** mengurangi ukuran file tanpa mengorbankan kualitas; ZIP adalah default yang baik untuk kebanyakan dokumen.

## Langkah 5: Simpan Hasil – **create searchable pdf**

Akhirnya, kami menulis hasil OCR ke disk menggunakan opsi yang baru saja kami definisikan. Metode `Save` menerima jalur target dan instance `PdfSaveOptions`.

```csharp
// Save the OCR result as a searchable PDF
ocrResult.Save(@"C:\Docs\invoice_searchable.pdf", pdfOptions);
```

Saat Anda membuka `invoice_searchable.pdf` di Adobe Reader atau penampil modern lainnya, Anda akan melihat gambar asli, tetapi kini Anda dapat memilih, menyalin, dan mencari teks seolah‑olah itu adalah PDF asli.

### Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan:

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine engine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image
            string imagePath = @"C:\Docs\invoice.png";
            engine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            OcrResult result = engine.Recognize();

            // 4️⃣ Configure PDF options (layer + compression)
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                IncludeImage = true,
                AddTextLayer = true,
                Compression = PdfCompression.Zip
            };

            // 5️⃣ Save as searchable PDF
            string pdfPath = @"C:\Docs\invoice_searchable.pdf";
            result.Save(pdfPath, pdfOptions);

            Console.WriteLine($"Searchable PDF created at: {pdfPath}");
        }
    }
}
```

**Output yang diharapkan** (di konsol):  
`Searchable PDF created at: C:\Docs\invoice_searchable.pdf`

Buka file hasil, tekan **Ctrl F**, ketik kata yang Anda lihat di faktur, dan lihat penampil melompat ke sana secara instan. Itulah inti dari **create searchable pdf** dalam aksi.

## Kesalahan Umum & Cara Menghindarinya

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Text not searchable | `AddTextLayer` left `false` or using an older Aspose version | Ensure `AddTextLayer = true` and update to the latest NuGet package |
| PDF huge (megabytes) | Compression set to `PdfCompression.None` | Switch to `PdfCompression.Zip` or `PdfCompression.Jpeg` for images |
| Garbled characters | Wrong language or low‑resolution image | Set `engine.Language` appropriately and supply at least 300 dpi images |
| Hidden layer invisible in some viewers | PDF generated with a non‑standard PDF version | Use `PdfSaveOptions.PdfVersion = PdfVersion.PDF_1_7` (default) or upgrade viewer |

### Pro tip

Jika Anda perlu **convert image to PDF** tanpa OCR (hanya PDF gambar biasa), setel `AddTextLayer = false`. `PdfSaveOptions` yang sama tetap memungkinkan Anda mengontrol kompresi, yang berguna untuk mengarsipkan dokumen yang dipindai yang tidak memerlukan kemampuan pencarian.

## Memperluas Solusi

- **Multiple pages**: Lakukan perulangan pada daftar file gambar, panggil `engine.Image = ...` setiap kali, dan kumpulkan hasilnya menjadi satu PDF menggunakan agregasi `PdfDocument`.
- **Different languages**: Ubah `engine.Language = OcrLanguage.Spanish` (atau bahasa lain yang didukung) untuk menangani faktur multibahasa.
- **Custom compression**: Untuk gambar berwarna kaya, `PdfCompression.Jpeg` dengan pengaturan kualitas (`pdfOptions.JpegQuality = 80`) dapat memperkecil file lebih lanjut.

## Kesimpulan

Kami baru saja membahas semua yang Anda perlukan untuk **create searchable pdf** dari gambar menggunakan C#. Dari menginisialisasi mesin OCR, memuat gambar, melakukan pengenalan, mengonfigurasi lapisan teks tersembunyi, hingga mengatur kompresi—setiap bagian memainkan peran penting dalam menghasilkan dokumen yang cepat dan dapat dicari.  

Sekarang Anda dapat mengotomatisasi pemrosesan faktur, mengarsipkan kontrak, atau membangun utilitas pemindaian massal yang mengubah tumpukan kertas menjadi PDF yang dapat dicari secara instan.  

Siap untuk tantangan berikutnya? Cobalah menambahkan watermark, menggabungkan beberapa PDF yang dapat dicari, atau mengekspos logika ini melalui Web API sehingga seluruh organisasi Anda dapat mengunggah gambar dan menerima PDF yang dapat dicari secara langsung.

---

*Jika Anda menemukan panduan ini berguna, beri ⭐, bagikan kepada rekan tim, atau tinggalkan komentar dengan penyesuaian Anda sendiri. Selamat coding!*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Konversi Gambar ke PDF C# – Simpan Hasil OCR Multi‑halaman](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Cara OCR Gambar – Lakukan OCR pada Gambar dalam OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}