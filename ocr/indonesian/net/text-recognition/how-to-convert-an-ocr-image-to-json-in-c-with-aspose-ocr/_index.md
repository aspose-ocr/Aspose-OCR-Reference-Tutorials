---
category: general
date: 2026-09-06
description: Konversi gambar OCR ke JSON dalam C# menggunakan Aspose.OCR – panduan
  langkah demi langkah untuk mengekstrak teks dari gambar dan mendapatkan output JSON.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: id
lastmod: 2026-09-06
og_description: ocr gambar ke json dalam C# dengan Aspose.OCR. Pelajari cara memuat
  gambar untuk OCR, mengenali teks dari foto, dan mengonversi hasilnya ke JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Mengonversi gambar OCR ke JSON dalam C# – panduan lengkap Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Cara mengonversi gambar OCR ke JSON dalam C# dengan Aspose.OCR
url: /id/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengonversi gambar OCR ke JSON dalam C# dengan Aspose.OCR

Jika Anda perlu **ocr image to json** dalam aplikasi .NET, panduan ini menunjukkan cara melakukannya dengan Aspose.OCR. Kami akan memandu proses memuat gambar untuk OCR, mengenali teks dari foto, dan mengonversi hasilnya ke JSON sehingga Anda dapat menggunakan data tersebut dalam API atau basis data.

Mengekstrak teks dari file gambar adalah kebutuhan umum untuk pemrosesan faktur, pemindaian kwitansi, dan proyek arsip. Pada akhir tutorial ini Anda akan dapat **convert image to text**, mengambil hasil teks polos, dan menghasilkan payload JSON terstruktur yang mempertahankan informasi tata letak.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

- .NET 6.0 SDK atau yang lebih baru terpasang  
- Visual Studio 2022 (atau editor apa pun yang mendukung .NET)  
- Paket NuGet Aspose.OCR (`Aspose.OCR`) ditambahkan ke proyek Anda  
- Sebuah gambar contoh (`input.jpg`) ditempatkan di folder yang dapat Anda referensikan dari kode  

Anda tidak memerlukan mesin OCR tambahan; Aspose.OCR menangani proses berat secara internal.

## Langkah 1: Instal paket NuGet Aspose.OCR

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Paket tersebut mencakup kelas `Aspose.OCR.OcrEngine`, yang menyediakan metode untuk **load image for ocr**, pemilihan bahasa, dan ekspor hasil.

## Langkah 2: Buat proyek konsol C# baru

Jika Anda belum memiliki proyek, buatlah satu:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Tambahkan direktif `using` yang Anda perlukan:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Langkah 3: Muat gambar dan konfigurasikan mesin OCR

Kode berikut menunjukkan cara **load image for ocr**, mengatur bahasa, dan menyiapkan mesin untuk pemrosesan. Dalam contoh ini kami menggunakan Cyrillic, tetapi Anda dapat beralih ke `OcrLanguage.English`, `OcrLanguage.French`, dll., tergantung pada bahasa sumber.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Mengapa ini penting:** Menetapkan bahasa yang tepat secara dramatis meningkatkan akurasi ketika Anda **recognize text from photo**. Mesin menggunakan kamus dan set karakter yang spesifik untuk bahasa.

## Langkah 4: Jalankan proses OCR dan ambil hasil

Sekarang jalankan mesin OCR. Jika proses berhasil, Anda dapat **extract text from image** sebagai teks polos, HTML, atau JSON. Aspose.OCR menyediakan metode `SaveJson` yang menulis hasil terstruktur ke sebuah file.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Struktur JSON yang Diharapkan

File `output.json` tipikal terlihat seperti ini (diformat untuk kemudahan membaca):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

Payload JSON berisi teks setiap baris, skor kepercayaan, dan persegi panjang yang mengelilingi baris tersebut dalam foto asli. Ini memudahkan pemetaan hasil OCR kembali ke elemen UI atau bidang basis data.

## Langkah 5: Kode sumber lengkap untuk demo

Berikut adalah program lengkap yang siap dijalankan yang melakukan alur kerja **ocr image to json**. Salin ke `Program.cs` dan jalankan `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Menjalankan contoh

1. Tempatkan gambar bernama `input.jpg` di root proyek.  
2. Jalankan `dotnet run`.  
3. Amati output konsol dan buka `output.json` untuk melihat data terstruktur.

## Tips profesional dan jebakan umum

| Situation | Recommendation |
|-----------|----------------|
| **Foto beresolusi rendah** | Tingkatkan DPI sebelum pemrosesan atau gunakan `ocrEngine.Image = ImageStream.FromFile(path, 300)` untuk memaksa 300 DPI. |
| **Bahasa campuran** | Atur `ocrEngine.Language = OcrLanguage.Multilingual` dan secara opsional sediakan daftar bahasa melalui `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Dokumen besar** | Proses satu halaman pada satu waktu untuk menjaga penggunaan memori rendah; mesin mendukung TIFF multi‑halaman. |
| **Karakter tidak tepat** | Pastikan `OcrLanguage` yang tepat dipilih; menggunakan bahasa yang salah mengurangi akurasi ketika Anda **convert image to text**. |
| **JSON kehilangan bidang** | Pastikan Anda menggunakan Aspose.OCR versi 23.6 atau yang lebih baru; rilis lama tidak menampilkan metode `SaveJson`. |

## Pertanyaan yang sering diajukan

**Q: Bisakah saya mendapatkan hasil OCR sebagai array byte alih-alih file?**  
A: Ya. Gunakan `ocrEngine.SaveJson(Stream)` untuk menulis langsung ke `MemoryStream`, lalu panggil `stream.ToArray()`.

**Q: Apakah mesin mendukung input PDF?**  
A: Aspose.OCR dapat menerima halaman PDF yang dikonversi menjadi gambar melalui Aspose.PDF, tetapi mesin OCR itu sendiri bekerja pada gambar raster. Konversi PDF ke gambar terlebih dahulu, lalu **load image for ocr**.

**Q: Bagaimana cara menangani skrip kanan‑ke‑kiri seperti Arab?**  
A: Atur `ocrEngine.Language = OcrLanguage.Arabic`. JSON mencakup arah teks yang benar, yang dapat Anda render dalam kerangka kerja UI yang mendukung RTL.

## Kesimpulan

Anda kini memiliki solusi lengkap untuk **ocr image to json** dalam C#. Dengan memuat gambar, mengkonfigurasi bahasa, menjalankan mesin OCR, dan mengekspor hasil sebagai JSON, Anda dapat **extract text from image**, **convert image to text**, dan **recognize text from photo** dalam satu alur kerja yang terintegrasi.  

Dari sini Anda dapat menjelajahi:

- Mengintegrasikan output JSON dengan Web API (`ASP.NET Core`)  
- Menyimpan hasil ke basis data NoSQL seperti MongoDB  
- Menambahkan pasca‑pemrosesan untuk memperbaiki kesalahan OCR umum  

Silakan bereksperimen dengan berbagai bahasa, format gambar, dan opsi output untuk menyesuaikan kebutuhan proyek Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [mengenali teks dari gambar dalam C# – Panduan Lengkap OCR dan JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Mengonversi Gambar ke Teks dalam C# dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [Cara Mengekstrak Teks dari Gambar Menggunakan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}