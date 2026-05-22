---
category: general
date: 2026-05-21
description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose OCR dalam C#.
  Konversi gambar ke PDF, atur resolusi PDF, dan sematkan gambar asli.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- set pdf resolution
- pdf with embedded image
language: id
og_description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose OCR di C#.
  Pelajari cara mengonversi gambar ke PDF, mengatur resolusi PDF, dan menyematkan
  gambar asli.
og_title: Buat PDF yang Dapat Dicari dari Gambar dengan OCR di C#
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF from an image using Aspose OCR in C#. Convert
    image to PDF, set PDF resolution, and embed the original image.
  headline: Create Searchable PDF from Image with OCR in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- Aspose
- C#
- PDF
title: Buat PDF yang Dapat Dicari dari Gambar dengan OCR di C# – Panduan Lengkap
url: /id/net/text-recognition/create-searchable-pdf-from-image-with-ocr-in-c-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PDF yang Dapat Dicari dari Gambar dengan OCR di C# – Panduan Lengkap

Pernah perlu **membuat file PDF yang dapat dicari** dari faktur, kwitansi, atau catatan tulisan tangan yang dipindai? Anda tidak sendirian—para pengembang sering menemui tantangan ini saat membangun pipeline manajemen dokumen. Kabar baik? Dengan Aspose.OCR Anda dapat **mengonversi gambar ke PDF**, menyematkan gambar asli, dan bahkan mengatur DPI output, semuanya dalam beberapa baris C#.

Dalam tutorial ini kita akan melangkah melalui seluruh proses mengubah PNG biasa menjadi **PDF yang dapat dicari**. Anda akan melihat cara **OCR gambar ke PDF**, **mengatur resolusi PDF**, dan mempertahankan grafis sumber di dalam file. Pada akhir tutorial Anda akan memiliki potongan kode siap pakai yang dapat disisipkan ke proyek .NET mana pun.

## Prasyarat

- .NET 6.0 atau lebih baru (API ini bekerja dengan .NET Core dan .NET Framework)
- Lisensi Aspose.OCR atau kunci evaluasi gratis
- Contoh gambar (misalnya `invoice.png`) yang ditempatkan di lokasi yang dapat dibaca aplikasi Anda
- Visual Studio, Rider, atau editor pilihan Anda

Tidak diperlukan paket NuGet tambahan selain `Aspose.OCR`—semua hal lain merupakan bagian dari pustaka kelas dasar .NET.

<img src="/images/searchable-pdf-example.png" alt="Create searchable PDF example in C#" />

## Langkah 1: Inisialisasi OCR Engine – Jantung Proses

Pertama-tama, kita memerlukan instance `OcrEngine` dan harus memberi tahu bahasa yang akan dikenali. Bahasa Inggris cocok untuk kebanyakan faktur, tetapi Anda dapat mengganti dengan nilai enum `OcrLanguage` apa pun.

```csharp
using Aspose.OCR;

// Step 1 – create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English   // Change if you need another language
};
```

**Mengapa ini penting:** Engine adalah mesin utama yang membaca data piksel dan mengubahnya menjadi teks yang dapat dicari. Menetapkan bahasa di awal secara signifikan meningkatkan akurasi—terutama untuk skrip non‑Latin.

## Langkah 2: Muat Gambar Sumber – Dari Disk ke Memori

Selanjutnya kita mengarahkan engine ke file gambar yang ingin diproses. Aspose menyediakan helper `ImageStream.FromFile` yang menyederhanakan boilerplate `FileStream` mentah.

```csharp
using Aspose.OCR;

// Step 2 – load the image containing the text
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");
```

**Tip:** Jika gambar Anda berada di bucket cloud atau berasal dari permintaan HTTP, Anda juga dapat memberi `MemoryStream` ke `ImageStream.FromStream`. Engine OCR tidak peduli dari mana byte-byte tersebut berasal.

## Langkah 3: Konfigurasi Opsi Penyimpanan PDF – Sematkan Gambar & Atur Resolusi

Sekarang kita memberi tahu Aspose bagaimana PDF akhir harus terlihat. Dua opsi penting untuk **PDF yang dapat dicari**:

1. `EmbedOriginalImage = true` – mempertahankan gambar hasil pemindaian di dalam PDF sehingga Anda tetap memiliki kesetiaan visual.
2. `OutputResolution = 300` – menentukan DPI lapisan yang dapat dicari; 300 DPI adalah titik optimal untuk kebanyakan tugas OCR.

```csharp
using Aspose.OCR.Pdf;   // PDF‑specific options

// Step 3 – define how the PDF should be saved
var pdfOptions = new PdfSaveOptions
{
    EmbedOriginalImage = true,   // Keeps the original image inside the PDF
    OutputResolution = 300       // DPI of the searchable PDF (set PDF resolution)
};
```

**Mengapa pengaturan ini?** Menyematkan gambar asli (`pdf with embedded image`) memastikan dokumen tampak persis seperti hasil scan, sementara lapisan teks OCR membuatnya dapat dicari. Sesuaikan `OutputResolution` jika Anda memerlukan file yang lebih ringan (150 DPI) atau presisi lebih tinggi (600 DPI).

## Langkah 4: Simpan Hasil – Dari OCR Engine ke PDF yang Dapat Dicari

Akhirnya, kita memanggil `Save` dengan jalur file output dan `PdfSaveOptions` yang baru saja dibuat. Satu baris ini melakukan pekerjaan berat: menjalankan OCR, membuat lapisan teks tersembunyi, dan menulis PDF ke disk.

```csharp
// Step 4 – generate the searchable PDF
ocrEngine.Save("YOUR_DIRECTORY/invoice_searchable.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created.");
```

**Apa yang Anda dapatkan:** Sebuah file bernama `invoice_searchable.pdf` yang tampak seperti `invoice.png` asli tetapi dapat diindeks oleh Windows Search, alat Find di Adobe Reader, atau mesin pencari teks penuh mana pun.

## Langkah 5: Verifikasi Output – Pemeriksaan Cepat yang Bisa Anda Lakukan

Setelah kode dijalankan, buka PDF di Adobe Acrobat (atau penampil apa pun) dan coba cari kata yang Anda tahu ada di faktur, misalnya “Total”. Jika pencarian menemukan istilah tersebut, Anda telah berhasil **ocr image to PDF**.

Anda juga dapat memeriksa ukuran file: karena kita **menyematkan gambar asli**, PDF akan lebih besar dibandingkan PDF yang hanya berisi teks, tetapi kompromi ini sepadan untuk kesetiaan visual.

## Kesalahan Umum & Pro Tips

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **PDF Kosong** | `ocrEngine.Image` tidak diatur atau jalur salah | Periksa kembali jalur file dan pastikan gambar dimuat tanpa pengecualian |
| **Akurasi Pencarian Buruk** | `OutputResolution` rendah atau bahasa salah | Tingkatkan `OutputResolution` menjadi 300‑600 DPI dan atur `OcrLanguage` yang tepat |
| **File Terlalu Besar** | `EmbedOriginalImage = true` pada scan resolusi tinggi | Turunkan resolusi gambar sumber sebelum memberi ke engine, atau set `EmbedOriginalImage = false` jika hanya membutuhkan teks yang dapat dicari |
| **Exception Lisensi** | Menggunakan versi percobaan tanpa kunci | Daftar untuk kunci lisensi sementara dari Aspose dan panggil `License license = new License(); license.SetLicense("Aspose.OCR.lic");` sebelum membuat engine |

## Contoh Lengkap yang Siap Pakai – Salin, Tempel, Jalankan

Berikut adalah aplikasi konsol mandiri yang dapat Anda kompilasi langsung. Ganti `YOUR_DIRECTORY` dengan folder nyata di mesin Anda.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑specific options

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image (convert image to PDF later)
            string inputPath = @"YOUR_DIRECTORY\invoice.png";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Set PDF options – embed image & set PDF resolution
            var pdfOptions = new PdfSaveOptions
            {
                EmbedOriginalImage = true,
                OutputResolution = 300 // DPI – you can change this to set PDF resolution
            };

            // 4️⃣ Save as searchable PDF
            string outputPath = @"YOUR_DIRECTORY\invoice_searchable.pdf";
            ocrEngine.Save(outputPath, pdfOptions);

            Console.WriteLine("Searchable PDF created at:");
            Console.WriteLine(outputPath);
        }
    }
}
```

**Output yang diharapkan** (di konsol):

```
Searchable PDF created at:
C:\Your\Path\YOUR_DIRECTORY\invoice_searchable.pdf
```

Buka PDF yang dihasilkan dan uji fungsi pencarian—voilà, Anda baru saja **membuat PDF yang dapat dicari** dari gambar.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **membuat PDF yang dapat dicari** menggunakan Aspose OCR di C#. Mulai dari memuat gambar, mengonfigurasi opsi **PDF dengan gambar tersemat**, **mengatur resolusi PDF**, hingga **menyimpan hasil OCR**, seluruh pipeline dapat diselesaikan dalam beberapa baris kode.

Langkah selanjutnya? Coba proses batch puluhan faktur, bereksperimen dengan bahasa lain, atau integrasikan kode ke API ASP.NET Core yang memproses unggahan secara real‑time. Anda juga dapat menambahkan watermark atau tanda tangan digital—keduanya didukung oleh Aspose.PDF untuk memperkuat dokumen lebih lanjut.

Punya pertanyaan tentang kasus tepi, lisensi, atau penyetelan performa? Tinggalkan komentar di bawah, dan selamat coding!

## Tutorial Terkait

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}