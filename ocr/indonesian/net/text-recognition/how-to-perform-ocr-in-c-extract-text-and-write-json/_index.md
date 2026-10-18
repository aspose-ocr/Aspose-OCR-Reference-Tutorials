---
category: general
date: 2026-02-09
description: Pelajari cara melakukan OCR di C# untuk mengekstrak teks dari gambar,
  mengenali teks dari PNG, dan menulis file JSON C# dengan cepat.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: id
og_description: Bagaimana melakukan OCR di C#? Ikuti panduan langkah demi langkah
  ini untuk mengekstrak teks dari gambar, mengenali teks dari PNG, dan menulis file
  JSON di C# secara efisien.
og_title: Cara Melakukan OCR di C# – Ekstrak Teks dan Tulis JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: Cara Melakukan OCR di C# – Ekstrak Teks dan Tulis JSON
url: /id/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Panduan Lengkap

Cara melakukan OCR di C# adalah tantangan umum ketika Anda perlu **ekstrak teks dari gambar**. Dalam panduan ini kami akan membahas cara mengenali teks dari PNG, mengekspor hasil detail ke string JSON, dan akhirnya **menulis file JSON C#**. Pernah melihat formulir yang dipindai dan bertanya‑tanya bagaimana mengubah goresan‑goresan itu menjadi teks yang dapat dicari? Anda tidak sendirian; banyak pengembang mengalami kendala ini di awal.

Kami akan menggunakan pustaka Aspose.OCR karena memberikan kepercayaan per‑simbol secara langsung dan bekerja dengan baik pada proyek .NET 6+. Pada akhir tutorial ini Anda akan memiliki aplikasi konsol siap‑jalankan yang memuat PNG, mengambil setiap karakter, dan menyimpan file JSON rapi yang dapat Anda masukkan ke basis data atau model AI. Tanpa jalan pintas “lihat dokumentasi” yang misterius—hanya solusi mandiri.

## Apa yang Anda Butuhkan

- **.NET 6 SDK** (atau lebih baru) – versi LTS terbaru pada saat penulisan.
- **Aspose.OCR for .NET** paket NuGet – `Install-Package Aspose.OCR`.
- Sebuah gambar PNG yang ingin Anda pindai (misalnya `form.png`).  
- IDE atau editor – Visual Studio, VS Code, Rider – apa saja yang Anda nyaman gunakan.

Itu saja. Jika Anda sudah memiliki semua itu, Anda siap memulai.

![Ilustrasi cara melakukan OCR](ocr-example.png "Cara melakukan OCR di C#")

*Teks alt gambar: ilustrasi cara melakukan OCR yang menunjukkan aplikasi konsol C# memproses PNG.*

## Langkah 1: Siapkan Proyek dan Tambahkan Dependensi

Pertama, buat proyek konsol baru dan tambahkan pustaka Aspose OCR.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Pro tip:** Gunakan flag `--framework net6.0` jika Anda ingin mengunci kerangka target secara eksplisit.

Mengapa langkah ini penting: paket NuGet berisi kelas `OcrEngine`, `ImageStream`, dan `JsonExporter` yang akan kami gunakan. Tanpanya, kompiler tidak akan mengerti apa arti “OCR”.

## Langkah 2: Tulis Logika OCR Inti

Buka `Program.cs` (atau buat file baru) dan ganti isinya dengan berikut. Setiap bagian diberi komentar agar Anda dapat melihat alasannya.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Mengapa Setiap Bagian Penting

- **OcrEngine**: Anggap sebagai otak operasi. Ia memuat model bahasa dan menyiapkan pipeline inferensi.
- **ImageStream.FromFile**: Menangani PNG, JPEG, BMP, dll. Ia mengabstraksi keanehan I/O file.
- **RecognitionResult**: Menyimpan teks mentah beserta skor kepercayaan. Di sinilah Anda mendapatkan data granular untuk validasi lanjutan.
- **JsonExporter**: Mengubah `RecognitionResult` yang kaya menjadi payload JSON bersih, cocok untuk API.
- **File.WriteAllText**: Cara .NET yang sederhana untuk **menulis file JSON C#** tanpa dependensi tambahan.

## Langkah 3: Jalankan Aplikasi dan Verifikasi Output

Kompilasi dan eksekusi program:

```bash
dotnet run
```

Anda akan melihat pesan konsol serupa dengan:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

Buka `form.json` – Anda akan menemukan sesuatu seperti:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

Langkah **ekstrak teks dari gambar** berhasil, dan kini Anda memiliki representasi JSON yang dapat dibaca mesin untuk setiap karakter.

## Langkah 4: Tangani Kasus Edge Umum

### File Hilang atau Rusak

Jika jalur PNG salah, `ImageStream.FromFile` akan melempar `FileNotFoundException`. Bungkus kode pemuatan dalam blok try‑catch:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Skor Kepercayaan Rendah

Kadang OCR menghasilkan kepercayaan rendah untuk pemindaian berisik. Anda dapat memfilter simbol sebelum mengekspor:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

Ini memastikan JSON hanya berisi karakter yang cukup dapat diandalkan—berguna ketika data dimasukkan ke pipeline validasi downstream.

### File Besar & Memori

Memproses PNG berukuran beberapa megabyte dapat meningkatkan penggunaan memori. Pertimbangkan streaming gambar dalam potongan atau gunakan `OcrEngine.RecognizeAsync` (tersedia pada versi Aspose terbaru) untuk menjaga UI tetap responsif.

## Langkah 5: Perluas Solusi (Opsional)

- **Pemrosesan batch**: Loop melalui direktori PNG dan hasilkan JSON yang cocok untuk tiap file.
- **Penyimpanan basis data**: Masukkan JSON ke kolom SQL `NVARCHAR(MAX)` untuk analitik selanjutnya.
- **Pemilihan bahasa**: Set `ocrEngine.Language = OcrLanguage.Spanish;` jika Anda memerlukan dukungan non‑Inggris.

Semua ekstensi ini mengikuti pola **cara melakukan OCR** yang telah kami tetapkan—inisialisasi, pengenalan, ekspor, dan penyimpanan.

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan JPG atau TIFF?**  
J: Tentu saja. `ImageStream.FromFile` otomatis mendeteksi format, jadi Anda dapat mengganti PNG dengan gambar raster apa pun yang didukung.

**T: Bagaimana jika saya perlu mengekstrak teks dari PDF?**  
J: Konversi tiap halaman PDF menjadi gambar terlebih dahulu (misalnya, menggunakan `Aspose.PDF`) lalu berikan PNG ke alur OCR yang dijelaskan di sini.

**T: Bisakah saya mendapatkan hasil OCR sebagai XML alih‑alih JSON?**  
J: Ya. Aspose.OCR juga menyediakan `XmlExporter`. Ganti `JsonExporter` dengan `XmlExporter` dan sesuaikan ekstensi file.

## Kesimpulan

Kami telah menelusuri **cara melakukan OCR** di C# dari awal hingga akhir, menunjukkan cara **ekstrak teks dari gambar**, **mengenali teks dari PNG**, dan **menulis file JSON C#** tanpa hambatan. Contoh lengkap yang dapat dijalankan ada di cuplikan kode di atas, dan Anda kini memahami alasan di balik setiap langkah—menginisialisasi mesin, menangani kasus edge, dan menyimpan hasil.

Selanjutnya, Anda dapat menjelajahi pipeline OCR batch, mengintegrasikan output JSON dengan Azure Cognitive Search, atau bereksperimen dengan model bahasa khusus. Langit adalah batasnya setelah Anda menguasai dasar‑dasar OCR di C#.

Jika Anda mengalami kendala atau memiliki ide untuk ekstensi lebih lanjut, tinggalkan komentar di bawah. Selamat coding, dan nikmati mengubah pemindaian berpixel menjadi data bersih yang dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}