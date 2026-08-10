---
category: general
date: 2026-05-31
description: cara menggunakan Aspose OCR di C# untuk mengekstrak teks dari gambar
  JPG tanpa akses internet – panduan langkah demi langkah
draft: false
keywords:
- how to use aspose
- extract text from jpg
- load image for ocr
- ocr without internet
language: id
og_description: cara menggunakan Aspose OCR di C# untuk mengekstrak teks dari file
  JPG tanpa koneksi internet. kode lengkap dan penjelasan.
og_title: Cara Menggunakan Aspose OCR – Ekstraksi Teks JPG Offline
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: how to use aspose OCR in C# for extracting text from JPG images without
    internet access – step‑by‑step guide.
  headline: How to Use Aspose OCR to Extract Text from JPG Offline
  type: TechArticle
- description: how to use aspose OCR in C# for extracting text from JPG images without
    internet access – step‑by‑step guide.
  name: How to Use Aspose OCR to Extract Text from JPG Offline
  steps:
  - name: Why Each Piece Matters
    text: '- **`ImageStream.FromFile`** – This is the canonical way to **load image
      for OCR** in Aspose. It abstracts away raw byte handling and works with any
      supported format (JPG, PNG, TIFF). - **`OfflineMode = true`** – Without this
      flag the engine would attempt to contact Aspose cloud services for languag'
  - name: Processing Multiple Images in a Loop
    text: 'If you have a folder full of JPGs, wrap the core logic in a `foreach`:'
  - name: Using a Different Language Pack
    text: Swap `english.ocrsrc` for `spanish.ocrsrc` (or any other) and the engine
      will automatically switch recognition language. No code changes needed—just
      point to a different file.
  - name: Handling Large Files
    text: 'For images larger than 5 MB you might want to downscale before feeding
      them to the engine. Aspose provides `ImageProcessor` utilities, but a quick
      `System.Drawing` resize works just as well:'
  type: HowTo
tags:
- aspose
- ocr
- csharp
- image-processing
title: Cara Menggunakan Aspose OCR untuk Mengekstrak Teks dari JPG Secara Offline
url: /id/net/text-recognition/how-to-use-aspose-ocr-to-extract-text-from-jpg-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Aspose OCR untuk Mengekstrak Teks dari JPG Secara Offline

Pernah bertanya-tanya **how to use aspose** OCR ketika Anda terjebak di kereta dengan Wi‑Fi yang tidak stabil? Anda bukan satu-satunya. Mengambil teks dari JPG tanpa panggilan jaringan adalah masalah umum, terutama untuk pemrosesan batch dokumen yang dipindai dalam lingkungan yang aman.

Dalam tutorial ini kami akan membahas **contoh C# lengkap yang dapat dijalankan** yang menunjukkan secara tepat cara **load image for OCR**, mengubah mesin ke **ocr without internet**, dan akhirnya **extract text from jpg**. Pada akhir tutorial Anda akan memiliki program mandiri yang dapat Anda masukkan ke proyek .NET mana pun—tanpa memerlukan kunci cloud.

## Prasyarat

- .NET 6+ SDK (atau .NET Framework 4.7.2 jika Anda lebih suka runtime klasik)  
- Paket NuGet Aspose.OCR untuk .NET (`Install-Package Aspose.OCR`)  
- Gambar JPG yang ingin Anda baca (kami akan menyebutnya `offline_sample.jpg`)  
- Paket bahasa Inggris (`english.ocrsrc`) – Anda dapat mengunduhnya dari situs Aspose dan menaruhnya di samping gambar.

Itu saja. Tidak ada layanan tambahan, tidak ada kunci API, hanya folder lokal dan beberapa baris kode.

## Langkah 1: Siapkan Proyek dan Instal Aspose.OCR

Buka terminal, buat aplikasi console, dan tambahkan pustaka:

```bash
dotnet new console -n AsposeOcrDemo
cd AsposeOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, **NuGet Package Manager** melakukan pekerjaan yang sama dengan beberapa klik.

## Langkah 2: Tulis Kode Lengkap – Cara Menggunakan Aspose OCR Secara Offline

Di bawah ini adalah *seluruh* `Program.cs`. Ini menunjukkan **how to use aspose**, **load image for OCR**, dan menjalankan dalam mode **ocr without internet**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 1️⃣  Load the JPG you want to process.
            // The ImageStream helper reads the file directly from disk.
            var imagePath = "YOUR_DIRECTORY/offline_sample.jpg";
            var ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };

            // 👉 2️⃣  Switch to offline mode – this tells Aspose not to hit any web services.
            ocrEngine.Options = new OcrOptions
            {
                OfflineMode = true           // <-- key for ocr without internet
            };

            // 👉 3️⃣  Load the language pack from a local file.
            // You can swap this for any .ocrsrc you have (French, German, etc.).
            var languagePath = "YOUR_DIRECTORY/english.ocrsrc";
            ocrEngine.Language = OcrLanguage.LoadFromFile(languagePath);

            // 👉 4️⃣  Run the recognition engine.
            OcrResult result = ocrEngine.Recognize();

            // 👉 5️⃣  Output the recognized text to the console.
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

### Mengapa Setiap Bagian Penting

- **`ImageStream.FromFile`** – Ini adalah cara kanonik untuk **load image for OCR** di Aspose. Ini mengabstraksi penanganan byte mentah dan bekerja dengan format yang didukung apa pun (JPG, PNG, TIFF).  
- **`OfflineMode = true`** – Tanpa flag ini mesin akan mencoba menghubungi layanan cloud Aspose untuk pembaruan model bahasa. Menetapkannya menonaktifkan semua lalu lintas jaringan, memenuhi persyaratan **ocr without internet**.  
- **`OcrLanguage.LoadFromFile`** – Dengan menunjuk ke file `.ocrsrc` lokal Anda menjaga seluruh proses tetap mandiri. Jika Anda perlu **extract text from jpg** dalam bahasa lain, cukup letakkan paket yang sesuai di folder yang sama.  
- **`Recognize()`** – Mengembalikan objek `OcrResult`. Properti `Text` berisi representasi teks polos dari semua yang dapat dibaca mesin dari gambar.

## Langkah 3: Build dan Jalankan

```bash
dotnet run
```

Jika semuanya terhubung dengan benar Anda akan melihat sesuatu seperti:

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

> **Bagaimana jika Anda mendapatkan string kosong?**  
> - Verifikasi bahwa path gambar benar (tidak ada typo di `YOUR_DIRECTORY`).  
> - Pastikan paket bahasa cocok dengan bahasa teks.  
> - Periksa bahwa JPG bukan foto hasil scan dokumen yang buram; kualitas OCR turun drastis pada gambar beresolusi rendah.

## Langkah 4: Variasi Umum & Kasus Tepi

### Memproses Banyak Gambar dalam Loop

Jika Anda memiliki folder berisi banyak JPG, bungkus logika inti dalam `foreach`:

```csharp
string[] files = Directory.GetFiles("YOUR_DIRECTORY", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"[{Path.GetFileName(file)}] → {result.Text}");
}
```

### Menggunakan Paket Bahasa yang Berbeda

Ganti `english.ocrsrc` dengan `spanish.ocrsrc` (atau yang lain) dan mesin akan otomatis beralih ke bahasa pengenalan tersebut. Tidak perlu mengubah kode—cukup arahkan ke file yang berbeda.

### Menangani File Besar

Untuk gambar lebih besar dari 5 MB Anda mungkin ingin memperkecil ukuran sebelum memberi ke mesin. Aspose menyediakan utilitas `ImageProcessor`, tetapi memperkecil cepat dengan `System.Drawing` juga berfungsi dengan baik:

```csharp
using System.Drawing;

// ... inside the loop
using var original = Image.FromFile(file);
using var resized = new Bitmap(original, new Size(2000, 0)); // keep aspect ratio
ocrEngine.Image = ImageStream.FromImage(resized);
```

## Langkah 5: Verifikasi Hasil Secara Programatis

Kadang Anda perlu memastikan bahwa OCR berhasil (misalnya, dalam tes otomatis). Anda dapat memeriksa enum `ResultStatus`:

```csharp
if (result.ResultStatus == OcrResultStatus.Success && !string.IsNullOrWhiteSpace(result.Text))
{
    // Good to go
}
else
{
    Console.Error.WriteLine("OCR failed or returned empty text.");
}
```

## Ringkasan Contoh Kerja Lengkap

Untuk salin‑tempel cepat, berikut *seluruh* solusi dalam satu tempat (termasuk potongan `csproj` untuk kelengkapan):

**AsposeOcrDemo.csproj**

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Aspose.OCR" Version="23.11.0" />
  </ItemGroup>
</Project>
```

**Program.cs** – (sama seperti di atas)

Menjalankan proyek ini di mesin mana pun dengan dua file (`offline_sample.jpg` dan `english.ocrsrc`) di folder yang sama akan **extract text from jpg** tanpa pernah menyentuh internet.

---

## Kesimpulan

Kami telah membahas **how to use aspose** OCR dalam skenario sepenuhnya offline, menunjukkan langkah tepat untuk **load image for OCR**, dan memperlihatkan cara **extract text from jpg** menggunakan hanya sumber daya lokal. Hal utama yang perlu diingat adalah flag `OfflineMode = true`—setelah diaktifkan, mesin berperilaku seperti pustaka murni, cocok untuk lingkungan yang aman atau terisolasi.

Selanjutnya, Anda mungkin ingin:

- Bereksperimen dengan paket bahasa yang berbeda untuk mendukung dokumen multibahasa.  
- Menggabungkan Aspose OCR dengan pembuatan PDF (Aspose.PDF) untuk membuat PDF yang dapat dicari secara langsung.  
- Mengintegrasikan kode ke layanan latar belakang yang memantau folder dan memproses pemindaian baru secara otomatis.

Ada pertanyaan tentang kasus tepi, penyetelan kinerja, atau integrasi dengan produk Aspose lainnya? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Cara Menggunakan Aspose untuk Mengenali Gambar dari Stream dalam OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Cara Menggunakan Aspose OCR untuk Hasil JSON dalam Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}