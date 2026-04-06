---
category: general
date: 2026-04-06
description: Mengenali teks gambar menggunakan Aspose OCR di C#. Pelajari cara mengekstrak
  teks, memuat file gambar di C#, dan menulis JSON di C# dengan contoh langkah demi
  langkah yang sederhana.
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: id
og_description: Mengenali teks gambar dengan Aspose OCR di C#. Panduan ini menunjukkan
  cara mengekstrak teks, memuat file gambar C#, dan menulis JSON di C# dengan cepat.
og_title: Mengenali Teks Gambar dalam C# – Panduan Lengkap Langkah demi Langkah
tags:
- OCR
- C#
- Aspose
title: Mengenali teks gambar di C# – Panduan Lengkap dengan Ekspor JSON
url: /id/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks gambar dalam C# – Panduan Langkah-demi-Langkah Lengkap

Pernah membutuhkan untuk **recognize image text** dari kwitansi yang dipindai tetapi tidak yakin pustaka mana yang harus dipilih? Anda bukan satu-satunya. Dalam banyak aplikasi dunia nyata—pelacak pengeluaran, pemroses faktur, bahkan alat aksesibilitas—mengambil kata‑kata dari gambar adalah rintangan pertama.  

Dalam tutorial ini kami akan membahas solusi praktis yang **recognize image text** menggunakan pustaka Aspose OCR, menunjukkan **how to extract text**, mendemonstrasikan **load image file c#** dengan benar, dan akhirnya **write json in c#** sehingga Anda dapat menyimpan atau mentransmisikan hasilnya. Pada akhir tutorial Anda akan memiliki aplikasi console siap‑jalankan yang mengubah PNG apa pun menjadi payload JSON yang rapi.

---

## Apa yang Anda Butuhkan

- **.NET 6+** (kode ini juga bekerja dengan .NET Framework 4.8, tetapi .NET 6 adalah pilihan terbaik).
- **Aspose.OCR for .NET** paket NuGet. Instal dengan `dotnet add package Aspose.OCR`.
- Sebuah gambar contoh (`input.png`) ditempatkan di lokasi yang dapat dibaca aplikasi Anda.  
- Visual Studio 2022 atau editor apa pun yang Anda sukai—tidak memerlukan trik IDE yang rumit.

> Tips pro: Simpan file gambar Anda dalam folder bernama `Resources` di dalam proyek; ini membuat jalur tetap rapi dan menghindari masalah “file not found”.

## Langkah 1: recognize image text – Memuat file gambar

Sebelum mesin OCR dapat melakukan keajaibannya, Anda harus **load image file c#** dengan aman. Metode `Image.FromFile` akan melempar pengecualian jika jalur salah atau file tidak dalam format yang didukung, jadi kami akan melindungi dari hal tersebut.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*Mengapa ini penting*: Memuat gambar di dalam blok `using` memastikan sumber daya GDI+ yang tidak dikelola dilepaskan segera, mencegah kebocoran memori pada layanan yang berjalan lama.

## Langkah 2: How to extract text dengan Aspose OCR

Sekarang bitmap berada di memori, kami menyerahkannya ke mesin **recognize image text**. `OcrEngine` milik Aspose sangat sederhana: buat instance, panggil `Recognize`, dan Anda akan mendapatkan objek `OcrResult` yang berisi teks mentah, skor kepercayaan, dan bahkan kotak pembatas.

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*Penjelasan*: Metode `Recognize` menjalankan jaringan saraf bawaan. Ia bekerja paling baik dengan gambar kontras tinggi, 300 DPI. Jika Anda memberikannya foto yang buram, skor kepercayaan menurun—pertimbangkan pra‑pemrosesan (deskew, binarize) untuk kode produksi.

## Langkah 3: Write JSON in C# – Mengekspor hasil OCR

Sebagian besar API mengharapkan JSON, jadi kami akan **write json in c#** menggunakan `JsonExport` milik Aspose. Pustaka ini menyerialisasi seluruh `OcrResult`, mempertahankan informasi baris dan nilai kepercayaan.

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### Output JSON yang Diharapkan

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*Mengapa JSON?* Ini bersifat bahasa‑agnostik, mudah dideseralisasi, dan menyimpan metadata OCR detail yang mungkin Anda perlukan untuk validasi selanjutnya.

## Langkah 4: Program lengkap yang dapat dijalankan

Menggabungkan semua bagian, berikut aplikasi console lengkap. Salin‑tempel, pulihkan paket NuGet, dan tekan **F5**.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

Jalankan program dan buka `Resources/output.json`—Anda akan melihat representasi JSON yang terstruktur rapi dari semua yang dikenali mesin.

## Menangani Kasus Pinggir Umum

| Situasi | Apa yang Harus Dilakukan | Mengapa |
|-----------|------------|-----|
| **Gambar null atau rusak** | Bungkus `Image.FromFile` dalam try/catch dan catat pengecualian. | Mencegah aplikasi crash dan memberi Anda pesan error yang jelas. |
| **Skor kepercayaan rendah** | Periksa `ocrResult.Words[i].Confidence`. Jika di bawah 0.75, pertimbangkan pra‑pemrosesan (tingkatkan DPI, tajamkan). | Meningkatkan keandalan untuk proses hilir seperti ekstraksi jumlah. |
| **File besar (>10 MB)** | Ukur ulang gambar sebelum OCR (`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`). | Mengurangi tekanan memori dan mempercepat pengenalan. |
| **Dokumen multi‑bahasa** | Set `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | Memungkinkan mesin mendeteksi karakter dari kedua bahasa. |

## Bonus: Memvisualisasikan hasil OCR (opsional)

Jika Anda ingin melihat di mana setiap kata berada pada gambar, Anda dapat menggambar kotak pembatas:

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

`annotated.png` yang dihasilkan akan menampilkan persegi merah di sekitar setiap kata yang dikenali—berguna untuk debugging.

## Kesimpulan

Kami baru saja **recognize image text** dalam C# dari awal hingga akhir: memuat file gambar, memanggil Aspose OCR untuk **how to extract text**, dan akhirnya **write json in c#** sehingga data dapat bergerak ke mana saja. Contoh lengkap ini dapat dijalankan langsung, dan tips tambahan membantu Anda menangani kwitansi yang buram, file besar, atau pemindaian multibahasa.

Apa selanjutnya? Coba ganti Aspose dengan mesin lain (Tesseract, Microsoft OCR) dan bandingkan skor kepercayaan, atau masukkan JSON ke dalam basis data untuk pelaporan pengeluaran. Anda juga dapat memperluas aplikasi console menjadi ASP .NET Core Web API yang menerima unggahan gambar dan mengembalikan JSON secara langsung.

Ada pertanyaan tentang skalabilitas, penanganan error, atau integrasi dengan Azure Functions? Tinggalkan komentar atau hubungi saya di GitHub. Selamat coding, semoga OCR Anda selalu tajam! 

![Tangkapan layar output JSON OCR – contoh recognize image text](https://example.com/ocr-example.png "contoh recognize image text")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}