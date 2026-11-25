---
category: general
date: 2026-08-12
description: Mengenali teks dari gambar menggunakan Aspose OCR untuk C#. Pelajari
  cara mengekstrak teks dari PNG, mengonversi gambar menjadi teks, dan menangani bahasa
  Sirilik.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from png
- convert image to text
- c# image ocr
- aspose ocr c#
language: id
lastmod: 2026-08-12
og_description: Mengenali teks dari gambar dengan Aspose OCR di C#. Panduan ini menunjukkan
  cara mengekstrak teks dari PNG, mengonversi gambar menjadi teks, dan bekerja dengan
  bahasa Cyrillic.
og_image_alt: Diagram showing the OCR processing flow from image file to recognized
  text output
og_title: Mengenali teks dari gambar di C# – tutorial lengkap Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Aspose OCR for C#. Learn how to extract
    text from PNG, convert image to text, and handle Cyrillic language.
  headline: recognize text from image in C# – step‑by‑step Aspose OCR guide
  type: TechArticle
- description: recognize text from image using Aspose OCR for C#. Learn how to extract
    text from PNG, convert image to text, and handle Cyrillic language.
  name: recognize text from image in C# – step‑by‑step Aspose OCR guide
  steps:
  - name: Expected console output
    text: '``` === Recognized Text === Привет мир! Это пример текста на кириллице.
      ```'
  - name: Recognize text from JPEG or BMP
    text: Replace the PNG file path with a JPEG or BMP file; the same `engine.Image`
      assignment works because Aspose.OCR auto‑detects the format.
  - name: Extract text from multiple pages
    text: 'If you need to **extract text from png** files that represent scanned pages,
      loop over the file list and concatenate the results:'
  - name: Convert image to text in an ASP.NET API
    text: 'Expose the OCR logic through a controller action:'
  type: HowTo
tags:
- Aspose OCR
- C#
- OCR
- Image processing
title: Mengenali teks dari gambar di C# – panduan Aspose OCR langkah demi langkah
url: /id/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar di C# – panduan langkah‑per‑langkah Aspose OCR

Jika Anda perlu **mengenali teks dari gambar** dalam aplikasi .NET, tutorial ini memberikan solusi lengkap yang siap dijalankan. Anda akan melihat cara mengekstrak teks dari file PNG, mengonversi gambar ke teks, dan menangani karakter Cyrillic—semua dengan pustaka Aspose.OCR untuk C#.

Panduan ini mencakup semua yang Anda perlukan untuk mulai menggunakan OCR hari ini: paket NuGet yang diperlukan, konfigurasi bahasa, pemuatan gambar, dan penanganan error. Pada akhir tutorial Anda akan memiliki program konsol yang mencetak string yang dikenali ke konsol, dan Anda akan memahami cara menyesuaikan kode untuk format gambar atau bahasa lain.

## Prasyarat

- .NET 6 SDK atau yang lebih baru (kode ini juga berfungsi dengan .NET Framework 4.7.2)
- Visual Studio 2022 atau editor C# apa pun yang Anda sukai
- Akses internet saat pertama kali menjalankan program (Aspose.OCR mengunduh modul bahasa secara otomatis)
- Gambar PNG yang berisi teks yang dapat dibaca (contoh menggunakan *cyrillic_sample.png*)

> **Pro tip:** Simpan file PNG Anda di bawah 2 MB untuk pemrosesan yang lebih cepat. Gambar yang lebih besar dapat diperkecil sebelum OCR untuk meningkatkan akurasi.

## Langkah 1: Instal paket NuGet Aspose.OCR

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Paket ini mencakup mesin OCR inti dan modul bahasa default. Ketika Anda meminta bahasa yang belum ada secara lokal, Aspose akan mengunduhnya secara otomatis.

## Langkah 2: Buat mesin OCR dan pilih bahasa

Mesin OCR adalah objek pusat yang melakukan konversi dari gambar ke teks. Untuk teks Cyrillic Anda mengatur properti `Language` menjadi `Language.Cyrillic`. Properti yang sama bekerja untuk bahasa lain seperti `Language.English`.

```csharp
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Choose the language module – Cyrillic in this example
        engine.Language = Language.Cyrillic;
```

**Mengapa ini penting:** Memilih bahasa yang tepat meningkatkan pengenalan karakter karena mesin memuat kamus dan font khusus bahasa. Jika Anda melewatkan langkah ini, mesin akan kembali ke bahasa Inggris dan karakter Cyrillic akan menjadi kacau.

## Langkah 3: Muat gambar yang ingin diproses

Aspose.OCR mendukung banyak format gambar, tetapi PNG adalah pilihan lossless yang umum dan mempertahankan tepi teks. Gunakan `ImageStream.FromFile` untuk membaca file ke dalam mesin.

```csharp
        // Step 3: Load the PNG image that contains the text
        engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/cyrillic_sample.png");
```

Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya ke file PNG Anda. Jika Anda perlu **mengekstrak teks dari png** yang berada di folder berbeda, cukup sesuaikan jalurnya.

## Langkah 4: Lakukan operasi OCR

Memanggil `engine.Recognize()` menjalankan pipeline OCR dan mengembalikan string biasa. Inilah inti dari fungsionalitas **convert image to text**.

```csharp
        // Step 4: Run OCR and get the recognized string
        string recognizedText = engine.Recognize();
```

Metode ini melemparkan pengecualian jika gambar tidak dapat dimuat atau modul bahasa gagal diunduh. Bungkus pemanggilan dalam blok try‑catch untuk kode produksi.

## Langkah 5: Tampilkan atau simpan output yang dikenali

Untuk demo cepat Anda dapat menulis hasil ke konsol. Pada aplikasi nyata Anda mungkin menyimpannya ke basis data, file teks, atau mengirimnya ke layanan lain.

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### Output konsol yang diharapkan

```
=== Recognized Text ===
Привет мир! Это пример текста на кириллице.
```

Jika gambar berisi teks bahasa Inggris, outputnya akan menjadi kalimat bahasa Inggris yang bersesuaian. Kode yang sama berfungsi untuk tugas **c# image ocr** dalam berbagai bahasa.

## Kode sumber lengkap – siap disalin

Berikut adalah program lengkap, termasuk direktif `using` dan semua langkah dalam satu file. Salin ke `Program.cs` dan jalankan `dotnet run`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // Create an OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Select the Cyrillic language module (downloaded automatically if missing)
            engine.Language = Language.Cyrillic;

            // Load the image that contains Cyrillic text
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/cyrillic_sample.png");

            // Perform the OCR recognition
            string recognizedText = engine.Recognize();

            // Display the recognized text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"OCR failed: {ex.Message}");
        }
    }
}
```

## Menangani variasi umum

### Mengenali teks dari JPEG atau BMP

Ganti jalur file PNG dengan file JPEG atau BMP; penugasan `engine.Image` yang sama tetap berfungsi karena Aspose.OCR secara otomatis mendeteksi format.

```csharp
engine.Image = ImageStream.FromFile("photo.jpg");
```

### Mengekstrak teks dari beberapa halaman

Jika Anda perlu **mengekstrak teks dari png** yang mewakili halaman yang dipindai, lakukan loop pada daftar file dan gabungkan hasilnya:

```csharp
string[] files = Directory.GetFiles("scans", "*.png");
var allText = new StringBuilder();

foreach (var file in files)
{
    engine.Image = ImageStream.FromFile(file);
    allText.AppendLine(engine.Recognize());
}
Console.WriteLine(allText.ToString());
```

### Mengonversi gambar ke teks dalam API ASP.NET

Ekspose logika OCR melalui aksi controller:

```csharp
[HttpPost("api/ocr")]
public async Task<IActionResult> Ocr(IFormFile image)
{
    using var stream = image.OpenReadStream();
    OcrEngine engine = new OcrEngine { Language = Language.English };
    engine.Image = ImageStream.FromStream(stream);
    string text = engine.Recognize();
    return Ok(new { text });
}
```

Ini mendemonstrasikan **c# image ocr** di dalam layanan web, memungkinkan klien mengunggah gambar raster apa pun dan menerima teks yang diekstrak dalam format JSON.

## Tips kinerja dan kasus tepi

- **Kualitas gambar:** Akurasi OCR menurun drastis ketika gambar blur atau kontras rendah. Gunakan pra‑pemrosesan gambar (mis., penajaman, binarisasi) sebelum memberi ke mesin.
- **File besar:** Untuk gambar lebih besar dari 5 MP, ubah ukurannya menjadi maksimal 2000 px pada sisi terpanjang. Ini mengurangi penggunaan memori tanpa mengorbankan pengenalan.
- **Fallback bahasa:** Jika Anda mengatur bahasa yang tidak didukung, mesin akan kembali ke bahasa Inggris. Selalu verifikasi `engine.Language` setelah inisialisasi jika Anda memuat modul bahasa secara dinamis.
- **Keamanan thread:** Instance `OcrEngine` tidak thread‑safe. Buat mesin baru per permintaan dalam lingkungan multi‑thread (mis., ASP.NET Core).

## Kesimpulan

Anda kini tahu cara **mengenali teks dari gambar** di C# menggunakan Aspose.OCR. Tutorial ini menuntun Anda melalui instalasi paket, konfigurasi bahasa, memuat PNG, melakukan OCR, dan menangani output. Dengan blok‑blok bangunan ini Anda juga dapat **mengekstrak teks dari png**, **convert image to text**, dan membangun solusi **c# image ocr** yang kuat untuk desktop, web, atau cloud.

Selanjutnya, jelajahi modul bahasa lain (mis., `Language.Spanish`) atau integrasikan hasil OCR dengan pustaka pemrosesan bahasa alami. Untuk penyetelan kinerja yang lebih mendalam, baca dokumentasi Aspose.OCR tentang pra‑pemrosesan gambar dan kamus khusus.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang erat dengan teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}