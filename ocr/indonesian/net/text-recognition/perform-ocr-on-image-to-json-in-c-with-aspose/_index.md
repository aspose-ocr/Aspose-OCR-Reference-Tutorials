---
category: general
date: 2026-04-08
description: Pelajari cara melakukan OCR pada gambar dan menulis file JSON C# menggunakan
  Aspose OCR. Tutorial Aspose OCR C# ini menunjukkan konversi gambar OCR ke JSON dengan
  nilai kepercayaan.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: id
og_description: Lakukan OCR pada gambar dan ekspor hasilnya ke file JSON dalam C#.
  Tutorial ini mencakup alur kerja lengkap Aspose OCR C#, termasuk skor kepercayaan.
og_title: Lakukan OCR pada Gambar ke JSON dalam C# – Panduan OCR Aspose
tags:
- Aspose
- OCR
- C#
- JSON
title: Lakukan OCR pada Gambar ke JSON di C# dengan Aspose
url: /id/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar ke JSON dalam C# dengan Aspose

Pernah membutuhkan untuk **perform OCR on image** file tetapi tidak yakin bagaimana mendapatkan hasilnya dalam format terstruktur? Anda tidak sendirian—para pengembang sering bertanya, “Bagaimana cara mengubah gambar yang dipindai menjadi data yang dapat digunakan?” Kabar baiknya, Aspose.OCR membuat ini sangat mudah, dan Anda bahkan dapat **write JSON file C#**‑style dengan skor kepercayaan yang disertakan.

Dalam panduan ini kami akan membahas tutorial **aspose OCR C# tutorial** lengkap yang mencakup semua mulai dari memuat gambar hingga mengekspor teks yang dikenali sebagai JSON. Pada akhir tutorial Anda akan memiliki aplikasi konsol yang dapat **perform OCR on image**, mengonversi output ke JSON (termasuk nilai kepercayaan), dan menyimpannya dengan satu baris kode. Tanpa langkah tersembunyi, tanpa skrip eksternal—hanya C# murni.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0 SDK atau yang lebih baru (kode ini bekerja dengan .NET Core dan .NET Framework juga)
- Visual Studio 2022 (atau editor apa pun yang Anda suka)
- Lisensi **Aspose.OCR for .NET** yang valid atau lisensi sementara gratis (versi percobaan gratis dapat digunakan untuk pengujian)
- File gambar (`input.png`) yang ingin Anda proses (format umum apa pun—PNG, JPG, BMP—akan cocok)

Itu saja. Jika Anda belum memiliki salah satu dari ini, dapatkan sekarang; sisa tutorial mengasumsikan semuanya sudah siap.

## Langkah 1: Instal Paket NuGet Aspose.OCR

Hal pertama yang harus dilakukan—tambahkan pustaka ke proyek Anda. Buka terminal di folder proyek dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Ini akan mengunduh versi terbaru (per April 2026 versi 23.12) dan menambahkan DLL yang diperlukan ke folder `bin`. Tidak ada konfigurasi tambahan yang diperlukan.

## Langkah 2: Inisialisasi Mesin OCR (Perform OCR on Image)

Sekarang kita membuat instance `OcrEngine` dan memberi tahu bahasa yang akan digunakan. Bahasa Inggris (`"en"`) adalah yang paling umum, tetapi Anda dapat menggantinya dengan `"fr"`, `"de"` atau bahasa lain yang didukung.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Mengapa kita inisialisasi di sini:** `OcrEngine` menyimpan semua konfigurasi yang dibutuhkan untuk proses pengenalan. Menetapkan bahasa di awal memastikan mesin menggunakan set karakter yang tepat, yang secara dramatis meningkatkan akurasi.

## Langkah 3: Kenali Gambar dan Tangkap Kepercayaan

Dengan mesin siap, kita beri file gambar kepadanya. Metode `RecognizeImage` mengembalikan objek `OcrResult` yang berisi teks yang diekstrak serta skor kepercayaan untuk setiap kata.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Apa yang terjadi di balik layar?** Aspose menjalankan pengenalan berbasis jaringan saraf yang menganalisis setiap blok piksel, mencocokkannya dengan model bahasa, dan menambahkan nilai kepercayaan (0‑100) yang menunjukkan seberapa yakin ia terhadap setiap kata.

## Langkah 4: Konversi Hasil ke JSON (OCR Image to JSON)

Aspose membuat konversi menjadi sangat mudah. Dengan menyertakan `includeConfidence: true` kita mendapatkan payload JSON yang terlihat seperti ini:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Berikut kode yang menghasilkan string JSON:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Mengapa menyertakan kepercayaan?** Jika Anda berencana mengirim data ke proses hilir (misalnya, validasi, penyorotan UI), mengetahui kata mana yang kurang pasti memungkinkan Anda memutuskan apakah harus meminta konfirmasi pengguna.

## Langkah 5: Tulis File JSON Gaya C#

Sekarang kita benar‑benar **write JSON file C#**. Metode `File.WriteAllText` bersifat atomik dan bekerja lintas‑platform, menjadikannya pilihan tepat untuk aplikasi konsol.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Itulah seluruh alur kerja—lima langkah singkat yang **perform OCR on image**, mengubah output menjadi JSON, dan menyimpannya.

## Contoh Kerja Penuh

Berikut program lengkap yang dapat Anda salin‑tempel ke `Program.cs`. Pastikan `input.png` berada di folder yang sama dengan binary yang telah dikompilasi atau sesuaikan jalurnya.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Output yang Diharapkan

Saat Anda menjalankan program (`dotnet run`), Anda akan melihat sesuatu seperti:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

Dan `output.json` akan berisi JSON terstruktur yang ditunjukkan sebelumnya, lengkap dengan persentase kepercayaan untuk setiap kata.

## Tips Pro & Kasus Tepi

- **Missing file handling:** Bungkus pemanggilan `RecognizeImage` dalam `try/catch` untuk `FileNotFoundException` jika Anda mengharapkan jalur dinamis.
- **Different languages:** Atur `ocrEngine.Language = "fr"` untuk bahasa Prancis, atau muat paket bahasa khusus melalui `ocrEngine.LoadLanguage("custom.lang")`.
- **Large documents:** Untuk PDF multi‑halaman, konversi setiap halaman menjadi gambar terlebih dahulu (misalnya, menggunakan `Aspose.PDF`) dan lakukan loop melalui langkah‑langkah OCR.
- **Performance tuning:** Jika Anda hanya membutuhkan hasil cepat, beralihlah ke `RecognitionMode.Fast`—Anda akan kehilangan sedikit akurasi tetapi memperoleh kecepatan.
- **JSON formatting:** Ingin JSON yang diformat rapi? Gunakan `JsonConvert.SerializeObject` dari Newtonsoft dengan `Formatting.Indented` setelah mendeseralisasi string JSON Aspose.

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja dengan .NET Framework?**  
A: Tentu saja. Paket NuGet yang sama menargetkan .NET Standard 2.0, sehingga Anda dapat merujuknya dari .NET Framework 4.6.1 dan yang lebih baru.

**Q: Bagaimana jika saya membutuhkan kepercayaan untuk seluruh dokumen, bukan per kata?**  
A: `OcrResult` juga menyediakan `OverallConfidence`. Anda dapat menambahkannya secara manual ke JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: Bisakah saya mengalirkan JSON langsung ke API web?**  
A: Ya. Ganti `File.WriteAllText` dengan POST `HttpClient` yang mengirim `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}