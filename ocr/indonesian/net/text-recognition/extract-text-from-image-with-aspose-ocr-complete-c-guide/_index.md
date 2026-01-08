---
category: general
date: 2026-01-07
description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  mengenali teks dari foto, meningkatkan akurasi OCR, memuat gambar untuk OCR, dan
  mengatur bahasa OCR.
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: id
og_description: Ekstrak teks dari gambar menggunakan Aspose OCR. Panduan ini menunjukkan
  cara mengenali teks dari foto, meningkatkan akurasi OCR, memuat gambar untuk OCR,
  dan mengatur bahasa OCR.
og_title: Ekstrak Teks dari Gambar dengan Aspose OCR – Tutorial C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar – Implementasi C# Lengkap dengan Aspose OCR

Pernah perlu **mengekstrak teks dari gambar** tetapi tidak yakin pustaka mana yang memberikan hasil dapat diandalkan? Anda tidak sendirian. Dalam banyak aplikasi dunia nyata—pemindai struk, verifikasi ID, atau sekadar alat pencatatan cepat—kemampuan **mengenali teks dari foto** adalah fitur yang wajib dimiliki.

Dalam tutorial ini kita akan melangkah melalui contoh lengkap yang siap dijalankan yang menunjukkan cara **memuat gambar untuk OCR**, mengonfigurasi mesin untuk **mengatur bahasa OCR**, dan menerapkan beberapa trik pra‑pemrosesan untuk **meningkatkan akurasi OCR**. Pada akhir tutorial Anda akan memiliki satu file C# yang mencetak teks yang diekstrak ke konsol, dan Anda akan memahami mengapa setiap pengaturan penting.

> **Tip:** Kode ini bekerja dengan Aspose.OCR ≥ 23.5, .NET 6+ dan lingkungan Windows, Linux, atau macOS apa pun yang dapat menjalankan .NET Core.

## Prasyarat

- .NET 6 SDK (atau lebih baru) terpasang  
- Visual Studio 2022, VS Code, atau editor apa pun yang Anda sukai  
- Paket NuGet `Aspose.OCR` (pasang via `dotnet add package Aspose.OCR`)  
- Sebuah file gambar (JPEG/PNG) yang berisi teks cetak atau ketik yang jelas  

Jika Anda sudah memiliki semua itu, mari kita mulai.

![contoh ekstrak teks dari gambar](/images/ocr-example.png "ekstrak teks dari gambar – output Aspose OCR")

## Langkah 1: Buat dan Buang Engine OCR – Inti “Ekstrak Teks dari Gambar”

Hal pertama yang Anda perlukan adalah sebuah instance `OcrEngine`. Membungkusnya dalam blok `using` menjamin pembuangan sumber daya native yang tepat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**Mengapa ini penting:** `OcrEngine` menyimpan memori tak terkelola untuk DLL OCR native. Membuangnya secara tepat mencegah kebocoran memori, terutama ketika Anda memproses banyak gambar dalam satu batch.

## Langkah 2: Definisikan Pengaturan Pengenalan – Tingkatkan Akurasi OCR

Selanjutnya kita membuat objek `RecognitionSettings`. Di sinilah kita **mengatur bahasa OCR** dan menambahkan filter pra‑pemrosesan yang sering menjadi perbedaan antara string berantakan dan output bersih.

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**Mengapa filter ini?**  
- **Deskew** memperbaiki masalah umum foto yang diambil dengan ponsel yang sedikit miring.  
- **Denoise** menghilangkan bintik‑bintik yang dapat diinterpretasikan sebagai karakter.  
- **ContrastEnhance** membuat tinta yang pudar lebih menonjol, yang penting untuk **meningkatkan akurasi OCR**.

## Langkah 3: Muat Gambar – Memuat Gambar untuk OCR Secara Efisien

Aspose menyediakan `ImageStream.FromFile` untuk pemuatan cepat. Anda juga dapat memberi aliran `MemoryStream` jika gambar berasal dari permintaan web atau basis data.

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**Jebakan umum:** Menyediakan path dengan garis miring maju pada Windows memang berfungsi, tetapi menggunakan `Path.Combine` lebih aman untuk proyek lintas‑platform.

## Langkah 4: Lakukan Pengenalan – Mengenali Teks dari Foto

Sekarang kita memanggil `Recognize`, memberikan aliran gambar serta pengaturan kita. Metode ini mengembalikan string biasa dengan teks yang diekstrak.

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

Jika gambar berisi beberapa blok teks, Aspose akan menggabungkannya dengan jeda baris, mempertahankan tata letak asli sejauh mungkin.

## Langkah 5: Tampilkan Hasil – Verifikasi Ekstraksi

Akhirnya, tuliskan hasilnya ke konsol. Dalam aplikasi nyata Anda mungkin menyimpannya ke basis data, mengirimnya ke layanan lain, atau menampilkannya di UI.

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### Output Konsol yang Diharapkan

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

Jika Anda melihat karakter yang berantakan, periksa kembali bahwa gambar jelas, bahasa cocok dengan teks, dan filter pra‑pemrosesan sesuai.

## Langkah 6: Penyesuaian Opsional – Menyetel untuk Kasus Tepi

### a. Mengganti Bahasa

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### b. Menambahkan Filter Kustom

Aspose juga menawarkan `PreprocessFilter.Sharpen` atau `PreprocessFilter.Binarize`. Bereksperimenlah dengan mereka ketika trio default tidak cukup.

### c. Menangani Gambar Besar

Untuk foto beresolusi sangat tinggi, turunkan skala terlebih dahulu agar penggunaan memori tetap rendah:

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan catatan tulisan tangan?**  
J: Aspose OCR dioptimalkan untuk teks cetak. Pengenalan tulisan tangan memerlukan mesin yang berbeda (misalnya Aspose.OCR for Handwriting atau model pembelajaran mesin).

**T: Bisakah saya memproses banyak gambar dalam sebuah loop?**  
J: Tentu saja. Pindahkan blok `using (var ocrEngine = new OcrEngine())` ke luar loop dan gunakan kembali engine untuk kinerja yang lebih baik.

**T: Bagaimana jika gambar berupa halaman PDF?**  
J: Konversi halaman PDF ke gambar terlebih dahulu (Aspose.PDF dapat merender halaman sebagai PNG/JPEG), lalu berikan ke engine OCR.

## Ringkasan – Apa yang Telah Kita Capai

- **Mengekstrak teks dari gambar** menggunakan satu program C# yang mandiri.  
- Menunjukkan cara **mengenali teks dari foto** dengan pra‑pemrosesan yang **meningkatkan akurasi OCR**.  
- Memperlihatkan cara yang tepat untuk **memuat gambar untuk OCR** dan **mengatur bahasa OCR** untuk skenario multibahasa.  

## Langkah Selanjutnya & Topik Terkait

- **Pemrosesan batch:** Gabungkan potongan kode ini dengan `Directory.GetFiles` untuk OCR seluruh folder.  
- **Pasca‑pemrosesan:** Gunakan ekspresi reguler untuk membersihkan tanggal, jumlah, atau ID setelah ekstraksi.  
- **Integrasi:** Salurkan teks yang diekstrak ke Azure Cognitive Search atau Elastic untuk dokumen yang dapat dicari.  

Silakan bereksperimen dengan kombinasi filter, bahasa, dan sumber gambar yang berbeda. Pola intinya tetap sama: buat engine, konfigurasikan pengaturan, muat gambar, kenali, dan tampilkan. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}