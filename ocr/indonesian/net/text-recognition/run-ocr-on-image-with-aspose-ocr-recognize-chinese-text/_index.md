---
category: general
date: 2026-03-04
description: Jalankan OCR pada gambar menggunakan Aspose OCR di C#. Pelajari cara
  mengenali teks bahasa Mandarin, mengekstrak teks dari gambar, dan memuat gambar
  untuk OCR dalam beberapa langkah saja.
draft: false
keywords:
- run OCR on image
- recognize chinese text
- extract text from image
- load image for OCR
- recognize simplified chinese
language: id
og_description: Jalankan OCR pada gambar dengan Aspose OCR di C#. Panduan ini menunjukkan
  cara mengenali teks Cina, mengekstrak teks dari gambar, dan memuat gambar untuk
  OCR secara efisien.
og_title: Jalankan OCR pada Gambar dengan Aspose OCR – Pengenalan Teks Cina Cepat
tags:
- Aspose OCR
- C#
- Chinese OCR
title: Jalankan OCR pada Gambar dengan Aspose OCR – Kenali Teks Cina
url: /id/net/text-recognition/run-ocr-on-image-with-aspose-ocr-recognize-chinese-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar – Panduan Lengkap C# untuk Teks Cina

Pernahkah Anda perlu **run OCR on image** file tetapi tidak yakin pustaka mana yang dapat menangani Bahasa Cina Sederhana tanpa masalah? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mencoba **recognize Chinese text** dan akhirnya frustrasi dengan masalah encoding.  

Dalam tutorial ini kami akan memotong kebisingan dan menunjukkan kepada Anda, langkah demi langkah, cara **run OCR on image** aset menggunakan Aspose OCR, mengunduh model bahasa yang diperlukan hanya sekali, dan akhirnya **extract text from image** file yang berisi karakter Cina Sederhana. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang mencetak teks yang dikenali ke konsol.

> **What you’ll get:** program C# yang lengkap dan dapat dikompilasi, penjelasan tentang *mengapa* setiap baris penting, serta tip untuk menangani jebakan umum seperti sumber daya yang hilang atau format gambar yang salah.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut terpasang di mesin pengembangan Anda:

| Prasyarat | Mengapa penting |
|--------------|----------------|
| .NET 6.0 SDK atau lebih baru | Menyediakan runtime dan kompiler untuk proyek C#. |
| Visual Studio 2022 (atau VS Code dengan ekstensi C#) | Memberikan IntelliSense dan debugging yang mudah. |
| Aspose.OCR NuGet package | Pustaka inti yang menyediakan kemampuan OCR. |
| Sebuah gambar yang berisi karakter Cina Sederhana (mis., `chinese_sample.png`) | Sumber yang akan Anda **load image for OCR**. |

Anda dapat mengambil paket NuGet dengan:

```bash
dotnet add package Aspose.OCR
```

Sekarang dasar‑dasarnya sudah siap, mari kita menghidupkan mesin.

## Langkah 1 – Pilih Model Bahasa (Recognize Simplified Chinese)

Aspose OCR memisahkan data bahasa dari mesin inti, yang berarti Anda harus memberi tahu SDK model mana yang Anda butuhkan. Karena kita berurusan dengan karakter Cina Daratan, kita pilih model **Simplified Chinese**.

```csharp
using Aspose.OCR;
using Aspose.OCR.ResourceManagement;

// Select the Simplified Chinese language model
LanguageModel languageModel = LanguageModel.ChineseSimplified;
```

*Why this matters:* Mesin OCR menggunakan kamus dan bentuk karakter yang spesifik untuk bahasa. Memilih model yang tepat secara dramatis meningkatkan akurasi, terutama untuk skrip padat seperti Cina.

## Langkah 2 – Unduh Model Sekali (Extract Text from Image)

Kali pertama Anda menjalankan kode, Anda perlu mengambil file model dari server Aspose. `ResourceDownloader` menangani ini untuk Anda. Dalam aplikasi produksi Anda mungkin akan membuat ini asynchronous, tetapi untuk kejelasan tutorial kami akan memblok dengan `.Wait()`.

```csharp
// Initialise the downloader and fetch the model (runs once)
ResourceDownloader resourceDownloader = new ResourceDownloader();
resourceDownloader.DownloadModelAsync(languageModel).Wait();
```

> **Pro tip:** Simpan sumber daya yang diunduh dalam folder yang menjadi bagian dari proyek Anda (mis., `OcrResources`). Dengan begitu run berikutnya melewati panggilan jaringan, mempercepat proses.

## Langkah 3 – Arahkan Mesin ke Sumber Daya Lokal Anda (Load Image for OCR)

Sekarang kami membuat mesin OCR dan memberi tahu di mana file model berada. `LocalResourceProvider` membaca file dari disk, menghilangkan lalu lintas jaringan lebih lanjut.

```csharp
// Create the OCR engine and link it to the local resources folder
OcrEngine ocrEngine = new OcrEngine
{
    ResourceProvider = new LocalResourceProvider(@"YOUR_DIRECTORY/OcrResources")
};
```

Ganti `YOUR_DIRECTORY` dengan path absolut atau relatif yang mengarah ke tempat Anda menyimpan file model.  

*Why this matters:* Jika mesin tidak dapat menemukan sumber daya bahasa, ia akan melempar `FileNotFoundException` dan Anda tidak akan dapat **run OCR on image** sama sekali.

## Langkah 4 – Atur Bahasa untuk Pengenalan (Recognize Chinese Text)

Meskipun kami telah mengunduh model Simplified Chinese, kami tetap harus memberi tahu mesin bahasa mana yang akan diterapkan selama pengenalan.

```csharp
// Tell the engine to use Simplified Chinese for this session
ocrEngine.Language = Language.ChineseSimplified;
```

Jika Anda pernah perlu beralih bahasa secara dinamis (mis., dari Cina ke Inggris), Anda cukup mengubah properti ini sebelum memanggil `Recognize`.

## Langkah 5 – Muat Gambar dan Jalankan OCR (Run OCR on Image)

Berikut inti tutorial: memuat file gambar dan mengekstrak konten teksnya. Metode `ImageInfo.Load` membaca file ke dalam format yang dipahami mesin OCR.

```csharp
// Load the image that contains Chinese characters
var imageInfo = ImageInfo.Load(@"YOUR_DIRECTORY/chinese_sample.png");

// Perform OCR – this is where we actually run OCR on image
OcrResult ocrResult = ocrEngine.Recognize(imageInfo);
```

Jika gambar besar atau berisik, pertimbangkan pra‑pemrosesan (mis., binarisasi) sebelum langkah ini. Aspose OCR juga menawarkan filter, tetapi itu di luar cakupan panduan pemula ini.

## Langkah 6 – Keluarkan Teks yang Dikenali (Extract Text from Image)

Akhirnya, kami mencetak string yang diekstrak ke konsol. Dalam skenario dunia nyata Anda mungkin menulisnya ke basis data, file, atau mengirimnya ke layanan lain.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

Menjalankan program seharusnya menampilkan sesuatu seperti:

```
=== Recognized Text ===
你好，世界！这是一个测试。
```

Itu saja—**run OCR on image** pertama Anda yang **recognize Chinese text**.

## Contoh Lengkap, Siap‑Jalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru (`dotnet new console`). Ingat untuk mengganti `YOUR_DIRECTORY` dengan path aktual di mesin Anda.

```csharp
// ------------------------------------------------------------
// Complete C# example: Run OCR on Image and Recognize Simplified Chinese
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.ResourceManagement;

class Program
{
    static void Main()
    {
        // 1️⃣ Choose the language model (Simplified Chinese)
        LanguageModel languageModel = LanguageModel.ChineseSimplified;

        // 2️⃣ Download the model (only the first time)
        var downloader = new ResourceDownloader();
        downloader.DownloadModelAsync(languageModel).Wait();   // Blocking for tutorial simplicity

        // 3️⃣ Initialise OCR engine with local resources folder
        var ocrEngine = new OcrEngine
        {
            ResourceProvider = new LocalResourceProvider(@"YOUR_DIRECTORY/OcrResources")
        };

        // 4️⃣ Set the language for this session
        ocrEngine.Language = Language.ChineseSimplified;

        // 5️⃣ Load the image that contains Chinese text
        var imageInfo = ImageInfo.Load(@"YOUR_DIRECTORY/chinese_sample.png");

        // 6️⃣ Run OCR on the image and capture the result
        OcrResult result = ocrEngine.Recognize(imageInfo);

        // 7️⃣ Output the extracted text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

> **Expected output:** Konsol mencetak karakter Cina yang ditemukan di `chinese_sample.png`. Jika gambar jelas, akurasi sering melebihi 95 %.

## Kesalahan Umum & Cara Menghindarinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| `FileNotFoundException` on startup | Path folder sumber daya salah | Periksa kembali path di `LocalResourceProvider`. Gunakan `Path.Combine` untuk keamanan lintas‑platform. |
| Output kosong (`ocrResult.Text` kosong) | Gambar terlalu berisik atau format tidak didukung | Konversi gambar ke PNG kontras tinggi, atau gunakan `ocrEngine.PreprocessImage(imageInfo)` sebelum `Recognize`. |
| Exception: `Unsupported language` | Model bahasa tidak diunduh | Jalankan kembali langkah pengunduh, atau hapus folder yang rusak dan biarkan diunduh lagi. |
| Lambat pada run pertama | Unduhan model melalui koneksi lambat | Cache model di lokasi jaringan bersama atau bundel sebelumnya dengan installer Anda. |

## Memperluas Solusi (Langkah Selanjutnya)

- **Batch processing:** Loop melalui direktori gambar, memanggil metode `Recognize` yang sama untuk setiap file. Ini memungkinkan Anda **extract text from image** koleksi tanpa usaha manual.  
- **Post‑processing:** Gunakan ekspresi reguler untuk membersihkan artefak OCR (mis., tanda baca yang terselip).  
- **Language detection:** Jika Anda perlu menangani dokumen multibahasa, periksa `ocrResult.DetectedLanguage` (tersedia di rilis Aspose terbaru) dan ubah `ocrEngine.Language` sesuai kebutuhan.  

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **run OCR on image** file menggunakan Aspose OCR di C#. Dari memilih model **recognize simplified Chinese** yang tepat, mengunduh sumber daya, mengonfigurasi mesin, hingga akhirnya **extract text from image**, tutorial ini memberi Anda solusi mandiri yang dapat disalin‑tempel.  

Sekarang Anda dapat dengan percaya diri **recognize Chinese text** dalam PNG atau JPEG apa pun yang Anda beri ke mesin, dan Anda memiliki fondasi kuat untuk memperluas ke pekerjaan batch, dukungan multibahasa, atau integrasi dengan pipeline analitik hilir.

Ada pertanyaan tentang menyesuaikan pengaturan OCR atau menangani skrip lain? Tinggalkan komentar, dan selamat coding! 

![Contoh Jalankan OCR pada Gambar](image.png "Contoh Jalankan OCR pada Gambar")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}