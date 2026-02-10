---
category: general
date: 2026-02-09
description: Ekstrak teks dari gambar menggunakan OCR offline C#. Contoh OCR lengkap
  dalam C# menunjukkan cara memuat gambar untuk OCR, mengenali teks Cyrillic, dan
  mengekstrak teks dari paspor.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: id
og_description: Ekstrak teks dari gambar dengan OCR offline C#. Pelajari contoh OCR
  C# langkah demi langkah yang memuat gambar untuk OCR, mengenali teks Cyrillic, dan
  mengekstrak teks dari paspor.
og_title: Ekstrak Teks dari Gambar di C# – Panduan OCR Offline
tags:
- OCR
- C#
- Aspose
title: Ekstrak Teks dari Gambar di C# – Contoh OCR Offline
url: /id/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di C# – Contoh OCR Offline

Pernah perlu **ekstrak teks dari gambar** tetapi terhambat oleh API yang bergantung pada jaringan? Anda tidak sendirian. Banyak pengembang mengalami kendala ketika layanan OCR mencoba mengunduh paket bahasa saat runtime, terutama di lingkungan yang terbatas.

Dalam panduan ini kami akan membahas **c# ocr example** yang berjalan sepenuhnya offline, memuat gambar untuk OCR, dan mengenali teks Cyrillic dari paspor. Pada akhir tutorial Anda akan memiliki program siap‑jalankan yang mencetak isi teks polos dari gambar yang didukung langsung ke konsol.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan Aspose.OCR untuk pemrosesan offline.  
- Kode tepat untuk **load image for OCR** dari disk.  
- Cara mengonfigurasi engine untuk **recognize cyrillic text**.  
- Contoh **c# ocr example** lengkap yang siap disalin‑tempel yang mengekstrak teks dari foto bergaya paspor.  

Tidak diperlukan pengalaman sebelumnya dengan Aspose; cukup .NET 6 (atau lebih baru) SDK dan Visual Studio 2022 (atau VS Code).

---

![Extract text from image using Aspose OCR on a passport photo](/images/ocr-passport.jpg "extract text from image")

## Langkah 1: Siapkan Proyek untuk Ekstrak Teks dari Gambar

Sebelum menulis kode apa pun, pastikan paket NuGet Aspose.OCR telah ditambahkan ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

> **Tip pro:** Gunakan flag `--version` untuk mengunci ke rilis stabil terbaru (mis., `13.9.0`). Ini menjamin kompatibilitas dengan .NET 6.

Membuat aplikasi console baru semudah:

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Sekarang Anda memiliki kanvas bersih di mana kami akan **extract text from image** tanpa pernah menyentuh internet.

## Langkah 2: Muat Gambar untuk OCR – Membaca Foto Paspor

Hal pertama yang dibutuhkan engine OCR adalah bitmap atau stream yang mewakili gambar. Dalam skenario kami kami akan **load image for OCR** dari file lokal bernama `cyrillic_passport.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Mengapa ini penting:** Menyediakan stream alih-alih `Bitmap` mentah memungkinkan Aspose menangani deteksi format secara internal, mengurangi kode boilerplate dan potensi bug.

## Langkah 3: Konfigurasikan Mode Offline dan Pilih Bahasa Cyrillic

Aspose.OCR dapat mengunduh model bahasa secara dinamis, tetapi itu menghilangkan tujuan solusi offline. Matikan panggilan jaringan dan secara eksplisit beri tahu engine bahasa yang akan digunakan.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Kasus tepi:** Jika Anda kemudian perlu mengenali karakter Latin dalam dokumen yang sama, cukup tambahkan `OcrLanguage.English` ke array. Engine akan menangani deteksi multi‑bahasa secara otomatis.

## Langkah 4: Jalankan Engine OCR dan Kenali Teks Cyrillic

Sekarang kita benar‑benarnya **recognize text from passport**‑style images. Metode `Recognize` mengembalikan objek hasil yang kaya berisi teks polos, skor kepercayaan, dan kotak pembatas.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Output Konsol yang Diharapkan

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

Jika hasilnya terlihat berantakan, periksa kembali bahwa gambar sumber jelas dan paket bahasa `OfflineMode` untuk Cyrillic ada di folder instalasi Aspose (biasanya `\Aspose.OCR\resources\languages`).

## Contoh Lengkap C# OCR – Kode Sumber Penuh

Berikut adalah **c# ocr example** secara lengkap. Salin‑tempel ke `Program.cs` dan jalankan `dotnet run`. Semua yang Anda butuhkan untuk **extract text from image** ada di sini.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Menjalankan Contoh

```bash
dotnet run
```

Anda akan melihat konsol mencetak detail paspor dalam Cyrillic. Itu saat Anda tahu pipeline **extract text from image** Anda berfungsi.

## Kesalahan Umum & Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| Empty `PlainText` | Model bahasa salah atau gambar terlalu gelap | Pastikan bahasa `OfflineMode` mencakup `Cyrillic` dan tingkatkan kontras gambar |
| `System.DllNotFoundException` | Biner native Aspose OCR tidak ditemukan | Instal ulang paket NuGet atau salin `Aspose.OCR.Native.dll` ke folder output |
| Performa lambat pada gambar besar | Engine memproses resolusi penuh | Ukur ulang gambar menjadi lebar ≤ 1500 px sebelum memberi ke `ImageStream` |
| Karakter berantakan | Gambar diputar secara tidak tepat | Gunakan `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` sebelum membuat stream |

## Langkah Selanjutnya – Memperluas Alur Kerja OCR Offline

- **Load image for OCR** dari `MemoryStream` saat menangani file yang diunggah di ASP.NET Core.  
- Beralih ke **recognize text from passport** dalam mode batch dengan mengulang folder pemindaian paspor.  
- Gabungkan hasil dengan **regular expressions** untuk mengekstrak bidang seperti nomor paspor atau tanggal lahir.  
- Eksperimen dengan `ocrEngine.Configuration.UseParallelProcessing = true` untuk percepatan multi‑core.

### Kesimpulan

Kami baru saja menunjukkan cara **extract text from image** menggunakan pipeline OCR C# yang sepenuhnya offline. **c# ocr example** singkat dan mandiri memuat gambar, mengonfigurasi engine untuk **recognize cyrillic text**, dan mencetak data paspor yang diekstrak—semua tanpa satu pun permintaan jaringan.

Silakan ubah kode, tambahkan lebih banyak bahasa, atau sambungkan output ke basis data. Tidak ada batasan setelah Anda menguasai dasar‑dasar memuat gambar untuk OCR dan mengenali teks dari foto bergaya paspor.

Ada pertanyaan atau ingin berbagi modifikasi Anda? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}