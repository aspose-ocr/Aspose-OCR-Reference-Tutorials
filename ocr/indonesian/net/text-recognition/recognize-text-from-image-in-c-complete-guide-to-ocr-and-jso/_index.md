---
category: general
date: 2026-01-10
description: Pelajari cara mengenali teks dari gambar, mengekstrak koordinat teks,
  dan mengonversi struk menjadi JSON menggunakan Aspose OCR di C#. Tutorial langkah
  demi langkah.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: id
og_description: Mengenali teks dari gambar di C# menggunakan Aspose OCR. Panduan ini
  menunjukkan cara mengekstrak teks, mendapatkan koordinat, dan mengonversi struk
  ke JSON.
og_title: Mengenali teks dari gambar – Tutorial OCR C# Lengkap
tags:
- OCR
- C#
- Aspose
title: Mengenali teks dari gambar di C# – Panduan Lengkap OCR dan JSON
url: /id/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali teks dari gambar – Tutorial C# OCR Lengkap

Pernah membutuhkan untuk mengenali teks dari gambar tetapi tidak yakin pustaka mana yang harus dipilih? Anda tidak sendirian. Dalam banyak aplikasi dunia nyata—pelacak pengeluaran, pemindai struk, atau pengarsip dokumen—mengekstrak teks secara andal adalah rintangan pertama.  

Dalam tutorial ini kami akan menjelaskan **cara mengekstrak teks**, mengambil kotak pembatasnya, dan akhirnya **mengonversi struk ke JSON** menggunakan Aspose.OCR untuk .NET. Pada akhir tutorial Anda akan memiliki proyek C# yang berdiri sendiri yang mengambil foto struk dan menghasilkan file JSON rapi dengan skor kepercayaan dan koordinat.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut di mesin Anda:

- **.NET 6.0 SDK** (atau versi yang lebih baru). Kerangka kerja yang lebih lama juga dapat bekerja, tetapi .NET 6 adalah pilihan tepat untuk pustaka modern.
- **Visual Studio 2022** atau VS Code dengan ekstensi C#.
- Paket NuGet **Aspose.OCR for .NET** (`Aspose.OCR` dan `Aspose.OCR.Output`). Anda dapat menginstalnya melalui Package Manager Console:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Contoh gambar struk (misalnya `receipt.jpg`) yang ditempatkan di folder yang akan Anda referensikan nanti.

Itu saja—tidak ada SDK tambahan, tidak ada binary native, hanya kode terkelola murni.

## Langkah 1: Buat Proyek Konsol Baru

Pertama-tama, buat aplikasi konsol. Ini cara tercepat untuk menguji OCR tanpa beban UI.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Tips pro:** Jaga folder proyek tetap rapi; buat sub‑folder bernama `Resources` dan letakkan `receipt.jpg` di sana. Ini memudahkan penanganan path.

## Langkah 2: Muat Gambar Struk

Sekarang kita benar‑benarnya **mengenali teks dari gambar**. Langkah pertama adalah mengarahkan mesin OCR ke file.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Mengapa kita membungkus pemuatan dengan pemeriksaan keberadaan sederhana? Karena dalam produksi Anda sering berurusan dengan unggahan pengguna yang mungkin hilang atau rusak. Menangkap masalah lebih awal menyelamatkan Anda dari pengecualian yang membingungkan kemudian.

## Langkah 3: Lakukan OCR – **mengenali teks dari gambar**

Dengan gambar berada di memori, kami meminta Aspose untuk **mengenali teks dari gambar**. Operasi ini bersifat sinkron dan mengembalikan set hasil yang kaya.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Di balik layar, Aspose menjalankan jaringan saraf yang dilatih pada jutaan karakter. Mesin mengisi `ocrEngine.Text`, `ocrEngine.RecognitionResult`, dan koleksi objek `OcrRegion` yang menyimpan koordinat. Itulah yang tepat kita butuhkan untuk langkah berikutnya.

## Langkah 4: **Cara mengekstrak teks** – Mendapatkan string mentah

Jika Anda hanya membutuhkan teks polos (mungkin untuk pencarian cepat), Anda dapat mengambilnya langsung dari mesin:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Anda akan melihat pemisah baris di mana OCR mendeteksi batas paragraf. Dalam banyak skenario pemindaian struk, string mentah sudah cukup untuk mengekstrak total, tanggal, atau nama vendor menggunakan regex sederhana.

## Langkah 5: **ekstrak koordinat teks** – Kotak pembatas untuk setiap kata

Seringkali Anda perlu mengetahui *di mana* pada gambar sebuah potongan teks berada—misalnya, untuk menyorot jumlah total di UI. Aspose memberikan itu melalui objek `OcrRegion`.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Perhatikan bahwa kami melakukan loop pada **ekstrak koordinat teks** untuk setiap segmen yang dikenali. Koordinat tersebut relatif terhadap gambar asli, sehingga Anda dapat menimpanya pada kanvas grafis atau elemen HTML `<canvas>`.

## Langkah 6: **konversi struk ke JSON** – Menyimpan hasil detail

Sekarang datang bagian yang mengikat semuanya: kami menginginkan struktur yang dapat dibaca mesin yang mencakup teks, skor kepercayaan, dan kotak pembatas. Aspose menyediakan `JsonSaveOptions` yang mempermudah hal ini.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

File yang dihasilkan terlihat seperti ini (dipangkas untuk singkat):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Anda sekarang memiliki artefak **konversi struk ke JSON** yang dapat diberikan ke layanan hilir—misalnya API laporan pengeluaran, pipeline analitik, atau bahkan UI sederhana yang menggambar persegi panjang di sekitar setiap kata.

## Contoh Kerja Lengkap

Menggabungkan semua bagian, berikut `Program.cs` lengkap yang dapat Anda salin‑tempel ke proyek Anda:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Jalankan program (`dotnet run`) dan perhatikan output konsol. Buka `Resources/receipt.json` untuk memverifikasi struktur.

## Pertanyaan Umum & Kasus Tepi

- **Bagaimana jika gambar buram?**  
  Aspose OCR bekerja paling baik dengan 300 dpi atau lebih tinggi. Jika Anda mendapatkan skor kepercayaan rendah, pertimbangkan untuk menerapkan filter penajaman sebelum memberi gambar ke mesin.

- **Apakah saya dapat mengenali banyak bahasa?**  
  Ya. Atur `ocrEngine.Language = Language.English | Language.Spanish;` sebelum memanggil `Recognize()`.

- **Bagaimana cara membatasi output hanya pada angka (mis., total)?**  
  Setelah Anda memiliki teks polos, jalankan regex seperti `\d+\.\d{2}` pada `ocrEngine.Text`. Karena kami sudah memiliki koordinat, Anda dapat memetakan string yang cocok kembali ke wilayahnya untuk penyorotan visual.

- **Apakah format JSON dapat disesuaikan?**  
  Kelas `JsonSaveOptions` menyediakan beberapa flag. Jika Anda memerlukan skema yang sepenuhnya khusus, Anda dapat mengiterasi `ocrEngine.RecognitionResult.Regions` dan menyerialisasi objek sendiri dengan `System.Text.Json`.

## Kesimpulan

Kami baru saja mendemonstrasikan cara **mengenali teks dari gambar** dalam C# menggunakan Aspose.OCR, **cara mengekstrak teks**, mengambil **ekstrak koordinat teks**, dan akhirnya **mengonversi struk ke JSON**. Seluruh alur berada dalam satu aplikasi konsol yang mudah dijalankan, menjadikannya sempurna untuk prototipe atau sebagai blok bangunan dalam sistem yang lebih besar.

Langkah selanjutnya? Cobalah mengirim JSON ke front‑end yang menggambar kotak pembatas, atau sambungkan output ke layanan laporan pengeluaran. Anda juga dapat bereksperimen dengan format gambar berbeda (PNG, TIFF) atau memproses batch folder berisi struk.

Ada pertanyaan lebih lanjut tentang OCR, Aspose, atau penanganan JSON? Tinggalkan komentar di bawah, dan selamat coding! 

![Contoh gambar struk untuk mengenali teks dari gambar](receipt.jpg "Contoh gambar struk")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}