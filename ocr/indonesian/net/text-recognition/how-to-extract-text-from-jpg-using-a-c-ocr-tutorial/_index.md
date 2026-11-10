---
category: general
date: 2026-09-13
description: Pelajari cara mengekstrak teks dari file JPG di C# dengan memuat gambar
  untuk OCR, mengatur bahasa OCR, dan menjalankan Aspose OCR – panduan langkah demi
  langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from jpg
- load image for ocr
- set ocr language
- c# ocr tutorial
language: id
lastmod: 2026-09-13
og_description: Ekstrak teks dari file JPG di C# dengan tutorial OCR singkat ini.
  Pelajari cara memuat gambar untuk OCR, mengatur bahasa OCR, dan mendapatkan hasil
  yang akurat.
og_image_alt: Screenshot of C# console output showing extracted Ukrainian text from
  a JPG image
og_title: Ekstrak teks dari JPG di C# – tutorial OCR lengkap
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn to extract text from JPG files in C# by loading an image for
    OCR, setting OCR language, and running Aspose OCR – a step‑by‑step guide.
  headline: How to extract text from JPG using a C# OCR tutorial
  type: TechArticle
- description: Learn to extract text from JPG files in C# by loading an image for
    OCR, setting OCR language, and running Aspose OCR – a step‑by‑step guide.
  name: How to extract text from JPG using a C# OCR tutorial
  steps:
  - name: Install the Aspose.OCR package
    text: 'Open a terminal in your project folder and run:'
  - name: Create a console application skeleton
    text: 'Create a new console project if you don’t already have one:'
  - name: Load an image for OCR
    text: The first operation after instantiating the engine is to provide the image
      you want to process. Aspose.OCR supports JPEG, PNG, BMP, GIF, and TIFF. In this
      tutorial we work with a JPEG file named **sample_ukrainian.jpg**.
  - name: Set OCR language
    text: OCR accuracy heavily depends on the language model. Aspose.OCR ships with
      data files for more than 30 languages. To recognize Ukrainian text, set the
      language code to `"ukr"`.
  - name: Perform OCR and extract text from JPG
    text: Calling `Recognize()` runs the recognition pipeline and returns the detected
      text as a plain string.
  - name: Run the program and verify the output
    text: 'Compile and execute the application:'
  - name: Loading images from memory or a web request
    text: 'Instead of `ImageStream.FromFile`, you can create a stream from a byte
      array:'
  - name: Processing multiple images in a batch
    text: 'Wrap the OCR logic in a method and iterate over a collection of file paths:'
  - name: Handling errors and edge cases
    text: 'OCR can fail if the image is corrupted or the language data cannot be downloaded.
      Catch exceptions to provide a graceful fallback:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Cara mengekstrak teks dari JPG menggunakan tutorial OCR C#
url: /id/net/text-recognition/how-to-extract-text-from-jpg-using-a-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekstrak teks dari JPG menggunakan tutorial OCR C#

Jika Anda perlu mengekstrak teks dari gambar JPG dalam aplikasi .NET, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan memuat gambar untuk OCR, mengatur bahasa OCR, dan mengambil teks yang dikenali dengan Aspose.OCR—semua dalam satu program C# yang berdiri sendiri.

Tutorial ini mencakup semua yang diperlukan untuk menjalankan OCR pada bahasa Ukraina, Inggris, atau bahasa lain yang didukung. Tidak diperlukan alat eksternal selain paket NuGet Aspose.OCR, dan kode mengikuti praktik terbaik untuk manajemen sumber daya serta penanganan kesalahan.

## Apa yang akan Anda capai

* Memuat gambar untuk OCR langsung dari sistem file.  
* Mengatur bahasa OCR agar sesuai dengan dokumen sumber.  
* Mengekstrak teks dari file JPG dan menampilkan hasilnya ke konsol.  
* Memahami cara menyesuaikan contoh untuk format gambar atau bahasa lain.

**Prasyarat**  

* .NET 6.0 SDK atau yang lebih baru terpasang.  
* Visual Studio 2022 (atau IDE C# apa pun).  
* Paket NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  

Tidak diperlukan pengalaman OCR sebelumnya.

## Cara mengekstrak teks dari JPG dengan Aspose OCR di C#

Bagian-bagian berikut memecah proses menjadi langkah-langkah yang jelas. Setiap langkah mencakup cuplikan kode, penjelasan mengapa langkah tersebut penting, dan tip praktis yang dapat Anda terapkan dalam proyek nyata.

### Langkah 1: Instal paket Aspose.OCR

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Paket ini berisi kelas `OcrEngine`, file data bahasa, dan utilitas untuk memuat gambar. Menginstalnya sekali membuat perpustakaan tersedia untuk setiap proyek yang merujuk pada file `.csproj`.

### Langkah 2: Buat kerangka aplikasi konsol

Buat proyek konsol baru jika Anda belum memilikinya:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Ganti `Program.cs` yang dihasilkan secara otomatis dengan kode yang ditunjukkan pada langkah berikut. Menjaga proyek tetap minimal membantu Anda fokus pada alur kerja OCR.

### Langkah 3: Muat gambar untuk OCR

Operasi pertama setelah menginstansiasi engine adalah menyediakan gambar yang ingin Anda proses. Aspose.OCR mendukung JPEG, PNG, BMP, GIF, dan TIFF. Dalam tutorial ini kami bekerja dengan file JPEG bernama **sample_ukrainian.jpg**.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 3: Load the image to be processed
        // ImageStream.FromFile reads the file and creates a stream compatible with OcrEngine.
        var imagePath = "YOUR_DIRECTORY/sample_ukrainian.jpg";
        using (var engine = new OcrEngine())
        {
            engine.Image = ImageStream.FromFile(imagePath);
```

**Mengapa ini penting** – Memuat gambar ke dalam `ImageStream` memastikan engine dapat mengakses data piksel tanpa mengunci file asli. Pendekatan ini juga bekerja untuk gambar yang disimpan dalam memori atau diterima dari API web.

### Langkah 4: Atur bahasa OCR

Akurasi OCR sangat bergantung pada model bahasa. Aspose.OCR dilengkapi dengan file data untuk lebih dari 30 bahasa. Untuk mengenali teks Ukraina, atur kode bahasa menjadi `"ukr"`.

```csharp
            // Step 4: Set the language for recognition (Ukrainian = "ukr")
            engine.Language = "ukr";
```

Jika Anda perlu memproses bahasa Inggris, gunakan `"eng"`; untuk bahasa Spanyol, `"spa"`. Kode bahasa mengikuti standar ISO 639‑2. Ketika Anda menentukan bahasa yang belum diunduh, engine secara otomatis mengambil data yang diperlukan pada pertama kali Anda menjalankan kode.

### Langkah 5: Lakukan OCR dan ekstrak teks dari JPG

Memanggil `Recognize()` menjalankan pipeline pengenalan dan mengembalikan teks yang terdeteksi sebagai string biasa.

```csharp
            // Step 5: Perform OCR – required language data will be downloaded automatically if missing
            string recognizedText = engine.Recognize();

            // Step 6: Output the recognized text
            Console.WriteLine("=== Extracted text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**Penjelasan** – Blok `using` menjamin bahwa instance `OcrEngine` dibuang dengan benar, melepaskan sumber daya tak terkelola seperti buffer memori native. Membuang engine sangat penting dalam layanan yang berjalan lama dan memproses banyak gambar.

### Langkah 6: Jalankan program dan verifikasi output

Kompilasi dan jalankan aplikasi:

```bash
dotnet run
```

Anda akan melihat output serupa dengan:

```
=== Extracted text ===
Привіт, це тестовий текст українською мовою.
```

Jika konsol menampilkan karakter yang kacau, pastikan terminal Anda menggunakan encoding UTF‑8 (`chcp 65001` di Windows) dan bahwa gambar sumber berisi teks yang jelas dengan kontras tinggi.

## Menyesuaikan tutorial OCR C# untuk skenario lain

### Memuat gambar dari memori atau permintaan web

Alih-alih `ImageStream.FromFile`, Anda dapat membuat stream dari array byte:

```csharp
byte[] imageBytes = await httpClient.GetByteArrayAsync(imageUrl);
engine.Image = ImageStream.FromBytes(imageBytes);
```

Teknik ini berguna saat memproses gambar yang diunggah melalui endpoint API.

### Memproses beberapa gambar secara batch

Bungkus logika OCR dalam sebuah metode dan iterasi melalui koleksi jalur file:

```csharp
static string ExtractText(string path, string language = "eng")
{
    using var engine = new OcrEngine();
    engine.Image = ImageStream.FromFile(path);
    engine.Language = language;
    return engine.Recognize();
}
```

Pemrosesan batch mengurangi overhead dengan menggunakan kembali instance `OcrEngine` yang sama jika Anda memindahkan pernyataan `using` ke luar loop.

### Menangani kesalahan dan kasus tepi

OCR dapat gagal jika gambar rusak atau data bahasa tidak dapat diunduh. Tangkap pengecualian untuk memberikan fallback yang elegan:

```csharp
try
{
    string text = ExtractText(imagePath, "ukr");
    Console.WriteLine(text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

Mencatat pengecualian membantu Anda memecahkan masalah jaringan ketika file bahasa perlu diunduh.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin langsung ke `Program.cs`. Program ini mencakup semua direktif `using` yang diperlukan, komentar, dan penanganan kesalahan.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Path to the JPEG image you want to process.
        var imagePath = "YOUR_DIRECTORY/sample_ukrainian.jpg";

        // Ensure the file exists before attempting OCR.
        if (!System.IO.File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        try
        {
            // Create the OCR engine inside a using block to guarantee disposal.
            using var engine = new OcrEngine();

            // Load the image for OCR.
            engine.Image = ImageStream.FromFile(imagePath);

            // Set OCR language (Ukrainian = "ukr").
            engine.Language = "ukr";

            // Perform OCR and retrieve the recognized text.
            string recognizedText = engine.Recognize();

            // Output the extracted text.
            Console.WriteLine("=== Extracted text from JPG ===");
            Console.WriteLine(recognizedText);
        }
        catch (Exception ex)
        {
            // Handle any exceptions that occur during OCR.
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Menjalankan kode ini mengekstrak teks dari file JPG dan mencetaknya ke konsol. Ganti `imagePath` dan `engine.Language` untuk bekerja dengan file dan bahasa lain.

## Kesimpulan

Anda kini tahu cara mengekstrak teks dari gambar JPG dalam C# dengan memuat gambar untuk OCR, mengatur bahasa OCR, dan menjalankan tutorial `c# ocr` yang singkat. Contoh ini menunjukkan praktik terbaik seperti pembuangan yang tepat dari `OcrEngine`, penanganan data bahasa yang hilang, dan penyediaan pesan kesalahan yang jelas.

Dari sini Anda dapat:

* Bereksperimen dengan kode bahasa yang berbeda (`"eng"`, `"spa"`, `"fra"`).  
* Mengintegrasikan logika OCR ke dalam API ASP.NET Core untuk pemrosesan gambar sesuai permintaan.  
* Menggabungkan output OCR dengan perpustakaan pemrosesan bahasa alami untuk menganalisis konten yang diekstrak.

Silakan sesuaikan kode dengan proyek Anda sendiri, dan bagikan hasil Anda di komentar atau media sosial. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image in C# – Offline OCR with Aspose (Step‑by‑Step Guide)](/ocr/english/net/text-recognition/extract-text-from-image-in-c-offline-ocr-with-aspose-step-by/)
- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}