---
category: general
date: 2026-05-25
description: Cara menggunakan OCR di C# untuk mengekstrak teks dari file gambar. Pelajari
  cara mengenali karakter Cina dari file JPG menggunakan Aspose.OCR dalam beberapa
  langkah sederhana.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from jpg
- recognize chinese characters
- ocr chinese simplified
language: id
og_description: Cara menggunakan OCR di C# untuk mengekstrak teks dari file gambar.
  Panduan ini menunjukkan cara mengenali karakter Cina dari file JPG menggunakan Aspose.OCR.
og_title: Cara Menggunakan OCR di C# – Mengenali Teks Cina dari JPG
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  headline: How to Use OCR in C# – Recognize Chinese Text from JPG
  type: TechArticle
- description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  name: How to Use OCR in C# – Recognize Chinese Text from JPG
  steps:
  - name: What’s happening under the hood?
    text: '- **`OcrEngine.Language`** tells Aspose which dictionary to use. By picking
      `ChineseSimplified`, we instruct the engine to look for the Simplified Chinese
      language pack. - **First‑time download**: When `Recognize` runs, the SDK reaches
      out to Aspose’s CDN, pulls the ≈6 MB language file, caches it lo'
  - name: 5.1 Dealing with Low‑Quality Images
    text: 'OCR accuracy drops when the source image is blurry, noisy, or has poor
      lighting. A quick fix is to pre‑process the image:'
  - name: 5.2 Running in a Headless Environment
    text: 'If you’re deploying to a Linux container without a GUI, make sure the `libgdiplus`
      library (required for `System.Drawing`) is installed:'
  - name: 5.3 Caching the Language Pack Manually
    text: You can download the language file once and point Aspose to it via the `License`
      API, which eliminates the one‑time network call. This is handy for offline scenarios.
  - name: Expected Output
    text: 'If the JPG contains the phrase “欢迎光临”, the console will print:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cara Menggunakan OCR di C# – Mengenali Teks Cina dari JPG
url: /id/net/text-recognition/how-to-use-ocr-in-c-recognize-chinese-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Mengenali Teks Cina dari JPG

Pernah bertanya-tanya **bagaimana cara menggunakan OCR** untuk mengambil kata‑kata dari foto yang Anda ambil dengan ponsel? Anda tidak sendirian. Dalam banyak proyek dunia nyata—seperti pemindai kwitansi, aplikasi terjemahan, atau entri data otomatis—Anda akan perlu **mengekstrak teks dari gambar** dengan cepat dan dapat diandalkan.

Dalam tutorial ini kita akan melewati contoh lengkap yang dapat dijalankan yang **mengenali teks dari file JPG** dan bahkan menangani kasus rumit **mengenali karakter Cina** menggunakan paket bahasa **OCR Chinese Simplified**. Pada akhir tutorial, Anda akan memiliki aplikasi konsol mandiri yang mencetak string yang terdeteksi ke konsol, tanpa perlu mengunduh apa pun secara manual.

> **Catatan cepat:** Kode ini bekerja dengan Aspose.OCR ≥ 23.7, yang secara otomatis mengunduh sumber daya bahasa pada penggunaan pertama. Jika Anda menggunakan versi yang lebih lama, Anda harus menambahkan bahasa secara manual.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0 SDK atau yang lebih baru (contoh ini menargetkan .NET 6, tetapi .NET 5 juga dapat digunakan)
- Versi terbaru Visual Studio 2022 atau VS Code dengan ekstensi C#
- Koneksi internet untuk pengunduhan bahasa pertama kali
- Gambar JPG yang berisi teks Cina Sederhana (kami akan menyebutnya `chinese_sign.jpg`)

Itu saja—tanpa mesin OCR berat, tanpa harus mengatur DLL native. Hanya beberapa perintah NuGet dan beberapa baris kode.

## Langkah 1: Instal Aspose.OCR via NuGet

Hal pertama yang harus dilakukan: kita memerlukan pustaka OCR. Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Atau, jika Anda lebih suka UI Visual Studio, klik kanan **Dependencies → Manage NuGet Packages**, cari “Aspose.OCR”, dan klik **Install**.

> **Pro tip:** Jaga paket Anda tetap terbaru. Paket bahasa baru dan perbaikan performa dirilis pada setiap rilis minor.

## Langkah 2: Buat Proyek Konsol Baru (Jika Belum)

Jika Anda memulai dari nol, buat aplikasi konsol baru:

```bash
dotnet new console -n OcrChineseDemo
cd OcrChineseDemo
```

Sekarang Anda memiliki file `Program.cs` yang siap untuk kode OCR.

## Langkah 3: Tulis Kode OCR – Mengenali Chinese Simplified dari JPG

Buka `Program.cs` dan ganti isinya dengan yang berikut. Setiap baris diberi anotasi sehingga Anda dapat melihat *mengapa* kami melakukan setiap langkah, bukan hanya *apa* yang kami lakukan.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;   // Required for Image.FromFile

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // --------------------------------------------------------------
            // 1️⃣  Initialise the OCR engine and request the Simplified Chinese
            //     language. This language isn’t bundled in the core package,
            //     so Aspose.OCR will download it the first time you call
            //     Recognize().
            // --------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                // The enum value maps to the language pack name.
                Language = OcrLanguage.ChineseSimplified
            };

            // --------------------------------------------------------------
            // 2️⃣  Load the image you want to process. Replace the path with
            //     the actual location of your JPG file.
            // --------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";
            using var image = Image.FromFile(imagePath);

            // --------------------------------------------------------------
            // 3️⃣  Perform the recognition. The first call may take a few
            //     seconds because the language resources are being fetched.
            // --------------------------------------------------------------
            string recognizedText = ocrEngine.Recognize(image);

            // --------------------------------------------------------------
            // 4️⃣  Output the result to the console.
            // --------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Apa yang terjadi di balik layar?

- **`OcrEngine.Language`** memberi tahu Aspose kamus mana yang akan dipakai. Dengan memilih `ChineseSimplified`, kami memberi tahu engine untuk menggunakan paket bahasa Chinese Simplified.
- **Unduhan pertama kali**: Ketika `Recognize` dijalankan, SDK akan menghubungi CDN Aspose, mengunduh file bahasa ≈6 MB, menyimpannya secara lokal, lalu melanjutkan OCR. Panggilan selanjutnya akan langsung selesai.
- **`Image.FromFile`** bekerja dengan format raster apa pun yang dapat didekode .NET—JPG, PNG, BMP—sehingga Anda dapat **mengekstrak teks dari gambar** dalam banyak tipe, tidak hanya JPG.

## Langkah 4: Jalankan Aplikasi dan Verifikasi Output

Bangun dan jalankan:

```bash
dotnet run
```

Anda seharusnya melihat sesuatu seperti:

```
=== Recognized Text ===
欢迎光临
```

Jika konsol menampilkan karakter acak atau string kosong, periksa kembali bahwa:

1. Gambar memang berisi karakter Cina yang jelas dan kontras tinggi.  
2. Jalur file sudah benar (tidak ada spasi berlebih atau ekstensi yang hilang).  
3. Mesin Anda dapat mengakses `https://download.aspose.com` untuk mengunduh paket bahasa.

## Langkah 5: Menangani Kasus Tepi dan Kesalahan Umum

### 5.1 Menghadapi Gambar Berkualitas Rendah

Akurasi OCR menurun ketika gambar sumber blur, berisik, atau pencahayaannya buruk. Solusi cepat adalah memproses gambar terlebih dahulu:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
var gray = new Bitmap(image.Width, image.Height);
using (var g = Graphics.FromImage(gray))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}
        });
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(image, new Rectangle(0,0,image.Width,image.Height),
                0,0,image.Width,image.Height, GraphicsUnit.Pixel, attributes);
}

// Use the processed bitmap for OCR
string recognizedText = ocrEngine.Recognize(gray);
```

### 5.2 Menjalankan di Lingkungan Tanpa GUI

Jika Anda men-deploy ke kontainer Linux tanpa antarmuka grafis, pastikan pustaka `libgdiplus` (yang diperlukan untuk `System.Drawing`) terpasang:

```bash
apt-get update && apt-get install -y libgdiplus
```

### 5.3 Menyimpan Paket Bahasa Secara Manual

Anda dapat mengunduh file bahasa sekali saja dan mengarahkan Aspose ke sana melalui API `License`, yang menghilangkan panggilan jaringan satu kali. Ini berguna untuk skenario offline.

```csharp
// Assuming you have the .dat file downloaded to /opt/ocr/langs/
ocrEngine.SetLicense("Aspose.OCR.lic"); // optional if you have a paid license
ocrEngine.LoadLanguage(@" /opt/ocr/langs/ChineseSimplified.dat");
```

## Contoh Lengkap yang Berfungsi (Semua dalam Satu)

Berikut adalah program *lengkap* yang dapat Anda salin‑tempel ke `Program.cs`. Tidak ada bagian tersembunyi, tidak ada skrip eksternal.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise OCR engine with Simplified Chinese language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified
            };

            // Path to the JPG image containing Chinese text
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";

            // Load the image (ensure the file exists)
            using var image = Image.FromFile(imagePath);

            // Recognize text – first call may download the language pack
            string recognizedText = ocrEngine.Recognize(image);

            // Display the result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Output yang Diharapkan

Jika JPG berisi frasa “欢迎光临”, konsol akan mencetak:

```
=== Recognized Text ===
欢迎光临
```

Silakan ganti gambar dengan tanda Cina Sederhana lainnya, nama jalan, atau label produk—engine akan melakukan yang terbaik.

## Kesimpulan

Kita baru saja membahas **cara menggunakan OCR** di C# untuk **mengekstrak teks dari gambar**, khususnya mengatasi tantangan **mengenali karakter Cina** dalam sebuah **JPG**. Dengan memanfaatkan unduhan bahasa on‑the‑fly dari Aspose.OCR, Anda dapat menjaga deployment tetap ringan sambil tetap mendukung **OCR Chinese Simplified** secara langsung.

Apa selanjutnya? Coba ide‑ide berikut:

- **Pemrosesan batch**: Loop melalui folder gambar dan tulis setiap hasil ke CSV.  
- **Gabungkan dengan API terjemahan**: Kirim string yang dikenali ke Azure Translator untuk aplikasi multibahasa waktu nyata.  
- **Jelajahi bahasa lain**: Ganti `OcrLanguage.ChineseSimplified` dengan `Japanese` atau `Arabic` dan lihat bagaimana kode yang sama beradaptasi.

Punya pertanyaan tentang optimasi performa, lisensi, atau integrasi OCR ke layanan web? Tinggalkan komentar di bawah—selamat coding! 

---

![Screenshot of console output showing how to use OCR in C# to recognize Chinese text from a JPG image](ocr-chinese-demo.png "how to use OCR console output")


## Tutorial Terkait

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}