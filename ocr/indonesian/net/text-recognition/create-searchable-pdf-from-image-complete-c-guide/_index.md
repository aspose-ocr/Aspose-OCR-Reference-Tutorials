---
category: general
date: 2026-03-23
description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose OCR. Pelajari
  cara mengonversi TIFF ke PDF dengan kompresi tinggi dan mengenali teks gambar dalam
  hitungan menit.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: id
og_description: Buat PDF yang dapat dicari dari gambar dengan Aspose OCR. Tutorial
  ini menunjukkan cara mengonversi TIFF ke PDF, menambahkan lapisan teks yang dapat
  dicari, dan menerapkan kompresi tinggi.
og_title: Buat PDF yang Dapat Dicari dari Gambar – Panduan Lengkap C#
tags:
- Aspose OCR
- C#
- PDF generation
title: Buat PDF yang Dapat Dicari dari Gambar – Panduan Lengkap C#
url: /id/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari Gambar – Panduan Lengkap C#

Pernah membutuhkan untuk **create searchable pdf** dari dokumen yang dipindai tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya—banyak pengembang mengalami hal yang sama saat mengubah pemindaian TIFF menjadi PDF yang dapat dicari. Kabar baik? Dengan Aspose OCR Anda dapat **convert tiff to pdf**, menambahkan lapisan teks tersembunyi di atasnya, dan bahkan memperkecil ukuran file dengan opsi **high compression pdf**, semuanya dalam beberapa baris kode C#.

Dalam tutorial ini kami akan membahas seluruh proses: mulai dari menginstal paket NuGet yang tepat, memuat gambar TIFF, mengenali teksnya, dan akhirnya mengekspor PDF yang dapat dicari. Pada akhir tutorial Anda akan memiliki aplikasi console yang dapat dijalankan yang **recognize image text** dan menghasilkan PDF yang kompak, dapat dicari, siap untuk diindeks. Tanpa alat tambahan, tanpa langkah OCR manual—hanya kode bersih dan sedikit penjelasan.

## Prasyarat & Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework 4.6+). API berfungsi pada keduanya, tetapi .NET 6 memberikan perbaikan runtime terbaru.  
- **Visual Studio 2022** atau IDE apa pun yang Anda sukai.  
- Paket NuGet **Aspose.OCR** dan **Aspose.OCR.Gpu** (paket GPU bersifat opsional tetapi mempercepat pengenalan pada perangkat keras yang didukung).  
- File TIFF contoh (misalnya `invoice.tif`) ditempatkan di folder yang Anda kontrol.  

Jika Anda sudah memiliki semua ini, bagus—lewati saja. Jika belum, langkah instalasi di bawah ini akan mencakup semuanya.

## Langkah 1: Instal Paket Aspose OCR

To start, open your project folder in a terminal and run:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Perintah ini mengunduh baik mesin OCR inti maupun pustaka akselerasi GPU. Yang terakhir tidak wajib; mesin akan kembali ke mode CPU jika tidak menemukan GPU yang kompatibel.  

> **Pro tip:** Saat menargetkan lingkungan produksi, kunci versi paket di `csproj` Anda untuk menghindari perubahan yang merusak secara tak terduga.

## Langkah 2: Siapkan Kerangka Proyek

Create a new console app (if you don’t already have one):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

Ganti `Program.cs` yang dihasilkan secara otomatis dengan kode lengkap yang ditampilkan nanti. Program akan:

1. Menginisialisasi `OcrEngine` dengan dukungan GPU.  
2. Memuat gambar TIFF.  
3. Menjalankan OCR dan menghentikan secara elegan jika gagal.  
4. Mengonfigurasi **PdfExportOptions** untuk lapisan yang dapat dicari dan **high compression**.  
5. Menulis file output.

## Langkah 3: Tulis Kode Lengkap (Contoh Penuh)

Berikut adalah file sumber *seluruhnya*. Salin‑tempel ke dalam `Program.cs`. Komentar menjelaskan “mengapa” di balik setiap baris, bukan hanya “apa”.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Mengapa Ini Berfungsi

- **GPU acceleration** dapat memotong waktu pengenalan dari detik menjadi milidetik pada kartu modern—berguna untuk pemrosesan massal.  
- **IncludeTextLayer** menyematkan teks hasil OCR secara tak terlihat, memungkinkan penampil PDF mencari dokumen tanpa mengubah tampilan visualnya.  
- **High compression** menggunakan kompresi Flate (ZIP) pada aliran gambar, yang lossless tetapi mengurangi ukuran file secara dramatis—ideal untuk mengarsipkan ribuan faktur.

## Langkah 4: Jalankan Aplikasi dan Verifikasi Output

Buka terminal di dalam folder proyek dan jalankan:

```bash
dotnet run
```

Jika semuanya telah dikonfigurasi dengan benar, Anda akan melihat:

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

Buka `invoice.pdf` di pembaca PDF apa pun (Adobe Acrobat, Edge, atau bahkan browser). Coba cari kata yang Anda tahu muncul di TIFF asli—misalnya “Total”. Penampil harus menyorot kata tersebut meskipun itu bagian dari gambar. Itu adalah ciri khas **searchable pdf**.

### Ukuran File yang Diharapkan

Faktur yang dipindai biasanya (≈300 KB TIFF) sering menyusut menjadi **~80 KB** setelah menerapkan `PdfCompression.High`. Ukuran pasti tergantung pada kompleksitas gambar, tetapi Anda akan melihat pengurangan yang jelas.

## Langkah 5: Variasi Umum & Kasus Tepi

| Situasi | Apa yang Diubah | Mengapa |
|-----------|----------------|-----|
| **Tidak ada GPU tersedia** | Ubah `new OcrEngine(GpuMode.Enabled)` menjadi `new OcrEngine(GpuMode.Disabled)` | Mencegah mesin mencoba inisialisasi GPU, yang dapat menyebabkan penundaan singkat. |
| **Beberapa halaman (TIFF multi‑halaman)** | Set `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | Memuat semua frame; Aspose akan memproses setiap halaman dan menghasilkan PDF multi‑halaman. |
| **Butuh bahasa OCR selain Inggris** | `ocrEngine.Language = Language.French;` (atau bahasa lain yang didukung) | Meningkatkan akurasi untuk dokumen non‑Inggris. |
| **Ingin overlay teks terlihat alih-alih lapisan tersembunyi** | `pdfExportOptions.IncludeTextLayer = false;` dan tambahkan objek `TextFragment` secara manual. | Berguna ketika Anda ingin teks OCR muncul sebagai teks yang dapat dipilih di atas gambar. |
| **PDF ultra‑kecil** | Gabungkan `PdfCompression.High` dengan `ImageResolution = 150` DPI sebelum pengenalan. | DPI yang lebih rendah mengurangi data gambar, lebih mengecilkan PDF dengan mengorbankan kualitas visual. |

> **Catatan:** Selalu uji kasus tepi pada sampel kecil sebelum memperluas ke produksi. Akurasi OCR dapat bervariasi tergantung pada kualitas gambar, noise, dan bahasa.

## Langkah 6: Tips untuk Implementasi Siap Produksi

1. **Error Logging** – Ganti `Console.WriteLine` dengan kerangka logging yang tepat (Serilog, NLog) untuk diagnostik yang lebih mudah.  
2. **Batch Processing** – Bungkus logika inti dalam metode yang menerima jalur input/output, lalu iterasi melalui direktori file TIFF.  
3. **Async I/O** – Meskipun Aspose OCR sendiri bersifat sinkron, memuat dan menyimpan file dapat dilakukan secara async untuk menjaga thread UI tetap responsif.  
4. **Security** – Jika Anda mengekspos fungsi ini melalui API web, validasi jalur file dan batasi ukuran file untuk mencegah penyalahgunaan.  
5. **Version Pinning** – Gunakan nomor versi yang tepat (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`) untuk menjamin perilaku konsisten di seluruh build.

## Kesimpulan

Kami baru saja membangun **solusi lengkap, end‑to‑end** yang **create searchable pdf** dari gambar yang dipindai, **convert tiff to pdf**, dan melakukannya dengan pengaturan **high compression pdf** sambil **recognize image text** secara akurat. **searchable pdf from image** yang dihasilkan ringan, dapat dicari, dan siap untuk alur kerja hilir seperti pengindeksan, pengarsipan, atau e‑discovery.

Punya sekumpulan faktur? Sambungkan metode ke dalam loop, arahkan ke folder, dan biarkan Aspose OCR melakukan pekerjaan berat. Ingin bereksperimen dengan tingkat kompresi atau paket bahasa yang berbeda? Kode cukup modular untuk menukar opsi tersebut dalam hitungan detik.

---

*Siap untuk naik level?* Coba tambahkan watermark, sematkan metadata, atau bahkan gabungkan beberapa PDF yang diproses OCR menjadi satu. Suite Aspose menawarkan banyak ekstensi—telusuri dokumentasinya dan pertahankan momentum. Selamat coding!

![Contoh screenshot PDF yang dapat dicari dari gambar](https://example.com/images/create-searchable-pdf.png "contoh pdf yang dapat dicari")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}