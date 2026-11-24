---
category: general
date: 2026-11-23
description: Unduh bahasa OCR dan ekstrak teks dari gambar dengan Aspose.OCR. Pelajari
  cara mengenali teks Cyrillic dari file PNG dalam beberapa langkah mudah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- download OCR language
- extract text from image
- how to recognize cyrillic
- recognize text from PNG
- recognize Cyrillic text
language: id
lastmod: 2026-11-23
og_description: Unduh bahasa OCR dan ekstrak teks dari gambar menggunakan Aspose.OCR.
  Ikuti tutorial langkah demi langkah ini untuk mengenali teks Cyrillic dari file
  PNG.
og_image_alt: Screenshot of Aspose.OCR engine recognizing Cyrillic text from a PNG
  image
og_title: Unduh bahasa OCR dan ekstrak teks dari gambar – Panduan Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-11-23'
  description: download OCR language and extract text from an image with Aspose.OCR.
    Learn how to recognize Cyrillic text from PNG files in a few easy steps.
  headline: How to download OCR language and extract text from an image
  type: TechArticle
- description: download OCR language and extract text from an image with Aspose.OCR.
    Learn how to recognize Cyrillic text from PNG files in a few easy steps.
  name: How to download OCR language and extract text from an image
  steps:
  - name: '**Multiple languages** – you can load several language modules at once,
      e.g., `engine.LoadLanguage("cyrillic,english");`. The engine will attempt to
      recognize characters from any loaded set.'
    text: '**Multiple languages** – you can load several language modules at once,
      e.g., `engine.LoadLanguage("cyrillic,english");`. The engine will attempt to
      recognize characters from any loaded set.'
  - name: '**Large images** – for high‑resolution files, consider down‑sampling before
      OCR to reduce memory usage.'
    text: '**Large images** – for high‑resolution files, consider down‑sampling before
      OCR to reduce memory usage.'
  - name: '**Batch processing** – wrap the recognition logic in a loop that iterates
      over a directory of PNG files. Remember to re‑assign `engine.Image` for each
      file; the engine can be reused.'
    text: '**Batch processing** – wrap the recognition logic in a loop that iterates
      over a directory of PNG files. Remember to re‑assign `engine.Image` for each
      file; the engine can be reused.'
  type: HowTo
- questions:
  - answer: Download the language module manually from the Aspose download portal,
      place the `.zip` file in the folder you specify with `SetLocalResourcesPath`,
      and the engine will load it without contacting the internet.
    question: What if the download fails because of a firewall?
  - answer: Yes. The OCR engine accepts any format that `System.Drawing.Image` can
      load. Simply change the file extension in `ImageStream.FromFile`.
    question: Can I recognize text from other image formats (e.g., JPEG, BMP)?
  - answer: The underlying API is the same; PNG is just one of many supported formats.
      Mentioning “recognize text from PNG” helps surface the tutorial for users searching
      for that exact phrase.
    question: How does this differ from “recognize text from PNG” vs. “recognize text
      from image”?
  - answer: 'Each `OcrEngine` instance is not thread‑safe. Create a separate instance
      per thread or use a pool pattern if you need high‑throughput processing. ##
      Edge cases and variations 1. **Multiple languages** – you can load several language
      modules at once, e.g., `engine.LoadLanguage("cyrillic,english");`. '
    question: Is the OCR engine thread‑safe?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cara mengunduh bahasa OCR dan mengekstrak teks dari gambar
url: /id/net/ocr-configuration/how-to-download-ocr-language-and-extract-text-from-an-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengunduh bahasa OCR dan mengekstrak teks dari gambar

Jika Anda perlu **mengunduh bahasa OCR** sumber daya dan mengekstrak teks dari sebuah gambar, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.OCR. Baik sumbernya berupa PNG yang berisi karakter Cyrillic atau format lain yang didukung, Anda akan mendapatkan solusi lengkap yang dapat dijalankan.

Anda akan belajar cara:

* Memuat modul bahasa secara dinamis (langkah “mengunduh bahasa OCR”)  
* Mengenali teks Cyrillic dari file PNG  
* Secara opsional mengarahkan mesin ke folder lokal untuk sumber daya yang telah diunduh sebelumnya  

Pada akhir tutorial Anda dapat mengintegrasikan OCR ke dalam aplikasi .NET apa pun dan secara andal **mengekstrak teks dari gambar**.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 SDK atau yang lebih baru terpasang  
* Lisensi Aspose.OCR yang valid (versi percobaan gratis dapat digunakan untuk evaluasi)  
* Visual Studio 2022 atau IDE kompatibel C# lainnya  
* File gambar (`sample_cyrillic.png`) yang berisi teks Cyrillic  

Potongan kode menggunakan fitur bahasa C# 10, tetapi Anda dapat menyesuaikannya ke versi sebelumnya bila diperlukan.

## Langkah 1: Instal paket NuGet Aspose.OCR

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah ini mengunduh pustaka Aspose.OCR terbaru, yang mencakup mesin OCR inti serta kemampuan untuk **mengunduh modul bahasa OCR** pada waktu berjalan.

## Langkah 2: Buat proyek konsol dan tambahkan direktif using

Buat aplikasi konsol baru (jika Anda belum memilikinya):

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Buka `Program.cs` dan tambahkan namespace yang diperlukan di bagian atas:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Helpers;   // Provides ImageStream helper methods
```

Namespace `Aspose.OCR.Helpers` memberikan metode yang nyaman untuk memuat gambar dari disk.

## Langkah 3: Inisialisasi mesin OCR dan **mengunduh sumber daya bahasa OCR**

Mesin OCR dilengkapi dengan sekumpulan sumber daya minimal. Untuk mengenali karakter Cyrillic Anda harus memuat modul bahasa yang sesuai. Jika modul tersebut tidak ada secara lokal, Aspose.OCR secara otomatis mengunduhnya.

```csharp
// Step 3: Create the OCR engine with default (basic) resources
var engine = new OcrEngine();

// Load the Cyrillic language module; this triggers a download if missing
engine.LoadLanguage("cyrillic");

// Optional: specify a folder for cached language files
// engine.ResourceManager.SetLocalResourcesPath(@"C:\AsposeOCRResources");
```

**Mengapa langkah ini penting:**  
*`LoadLanguage("cyrillic")`* memberi tahu mesin set karakter mana yang akan digunakan. Tanpa pemanggilan ini mesin akan kembali ke set Latin default dan gagal mengenali glif Cyrillic. Pengunduhan terjadi hanya sekali, setelah itu modul disimpan dalam cache untuk eksekusi selanjutnya.

## Langkah 4: Muat gambar yang berisi teks Cyrillic

Aspose.OCR bekerja dengan format gambar apa pun yang didukung oleh `System.Drawing` .NET. Untuk tutorial ini kami menggunakan file PNG karena mempertahankan kualitas lossless, yang meningkatkan akurasi pengenalan.

```csharp
// Step 4: Load the image containing Cyrillic text
engine.Image = ImageStream.FromFile(@"C:\Images\sample_cyrillic.png");
```

Jika Anda lebih suka jalur relatif, letakkan gambar di dalam folder proyek dan gunakan `Path.Combine(Directory.GetCurrentDirectory(), "sample_cyrillic.png")`.

## Langkah 5: Kenali teks dan tampilkan hasilnya

Sekarang mesin sudah dikonfigurasi dan gambar telah dimuat, panggil `Recognize()` dan baca properti `Text`.

```csharp
// Step 5: Perform OCR and output the recognized text
engine.Recognize();

Console.WriteLine("Recognized text:");
Console.WriteLine(engine.Text);
```

**Output yang diharapkan**

```
Recognized text:
Привет, мир!
```

String yang tepat bergantung pada isi `sample_cyrillic.png`, tetapi Anda seharusnya melihat karakter Cyrillic tercetak di konsol.

## Langkah 6: Program lengkap yang dapat dijalankan

Menggabungkan semua bagian, berikut adalah file sumber lengkap yang dapat Anda salin ke `Program.cs` dan jalankan:

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Helpers;

namespace OcrDemo
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            // Initialize OCR engine
            var engine = new OcrEngine();

            // Load Cyrillic language – downloads if not cached
            engine.LoadLanguage("cyrillic");

            // (Optional) Set a custom folder for language resources
            // engine.ResourceManager.SetLocalResourcesPath(@"C:\AsposeOCRResources");

            // Load the PNG image that contains Cyrillic text
            engine.Image = ImageStream.FromFile(@"C:\Images\sample_cyrillic.png");

            // Run OCR
            engine.Recognize();

            // Output the result
            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```

Jalankan program dengan:

```bash
dotnet run
```

Anda akan melihat frasa Cyrillic tercetak di konsol, mengonfirmasi bahwa operasi **mengenali teks Cyrillic** berhasil.

## Tips pro: tingkatkan akurasi untuk file PNG yang berisik

* **Pra‑proses gambar** – ubah ke skala abu‑abu, tingkatkan kontras, atau terapkan filter median menggunakan `System.Drawing` sebelum mengirimkannya ke mesin OCR.  
* **Atur opsi `engine.Config`** – aktifkan `engine.Config.DetectOrientation = true` bila teks mungkin diputar.  
* **Cache modul bahasa** – dengan memanggil `SetLocalResourcesPath` Anda menghindari latensi jaringan pada eksekusi berikutnya.

## Pertanyaan umum yang dijawab

**Q: Bagaimana jika pengunduhan gagal karena firewall?**  
A: Unduh modul bahasa secara manual dari portal unduhan Aspose, letakkan file `.zip` di folder yang Anda tentukan dengan `SetLocalResourcesPath`, dan mesin akan memuatnya tanpa menghubungi internet.

**Q: Bisakah saya mengenali teks dari format gambar lain (misalnya JPEG, BMP)?**  
A: Ya. Mesin OCR menerima format apa pun yang dapat dimuat oleh `System.Drawing.Image`. Cukup ubah ekstensi file di `ImageStream.FromFile`.

**Q: Apa perbedaan antara “mengenali teks dari PNG” vs. “mengenali teks dari gambar”?**  
A: API dasarnya sama; PNG hanyalah salah satu dari banyak format yang didukung. Menyebutkan “mengenali teks dari PNG” membantu menampilkan tutorial ini bagi pengguna yang mencari frasa tersebut secara tepat.

**Q: Apakah mesin OCR thread‑safe?**  
A: Setiap instance `OcrEngine` tidak thread‑safe. Buat instance terpisah per thread atau gunakan pola pool bila Anda memerlukan pemrosesan berkecepatan tinggi.

## Kasus tepi dan variasi

1. **Beberapa bahasa** – Anda dapat memuat beberapa modul bahasa sekaligus, misalnya `engine.LoadLanguage("cyrillic,english");`. Mesin akan berusaha mengenali karakter dari semua set yang dimuat.  
2. **Gambar besar** – untuk file beresolusi tinggi, pertimbangkan melakukan down‑sampling sebelum OCR untuk mengurangi penggunaan memori.  
3. **Pemrosesan batch** – bungkus logika pengenalan dalam loop yang mengiterasi direktori berisi file PNG. Ingat untuk menetapkan kembali `engine.Image` untuk setiap file; mesin dapat digunakan kembali.

## Kesimpulan

Anda kini tahu cara **mengunduh bahasa OCR** sumber daya, mengonfigurasi Aspose.OCR untuk Cyrillic, dan **mengekstrak teks dari gambar**—khususnya file PNG—menggunakan aplikasi konsol C# yang ringkas. Dasar ini memungkinkan Anda membangun solusi yang lebih canggih seperti pemindai dokumen, pipeline entri data otomatis, atau layanan ekstraksi teks multibahasa.

Langkah selanjutnya yang dapat Anda jelajahi:

* Gabungkan **mengenali teks dari PNG** dengan **cara mengenali Cyrillic** untuk dokumen multibahasa.  
* Integrasikan alur OCR ke dalam API ASP.NET Core untuk menyediakan OCR sebagai layanan web.  
* Bereksperimen dengan modul bahasa lain (misalnya `engine.LoadLanguage("arabic")`) untuk memperluas jangkauan aplikasi Anda.

Selamat coding, dan nikmati kekuatan pengunduhan bahasa OCR secara dinamis!

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang erat dengan teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Melakukan OCR di C# – Mengenali Teks Cyrillic dengan Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [Cara Mengunduh Sumber Daya OCR dan Mengenali Teks dari Gambar di C#](/ocr/english/net/text-recognition/how-to-download-ocr-resources-and-recognize-text-from-image/)
- [Cara Mengunduh Model Aspose.OCR dan Mengekstrak Teks dari PNG di C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}