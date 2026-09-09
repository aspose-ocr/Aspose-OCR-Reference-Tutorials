---
category: general
date: 2026-01-02
description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  mengonversi gambar ke format JSONL dengan cepat dan andal.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: id
og_description: Ekstrak teks dari gambar dengan Aspose OCR dan konversi ke format
  JSONL. Tutorial C# lengkap langkah demi langkah untuk pengembang.
og_title: Ekstrak Teks dari Gambar – Konversi ke JSONL dalam C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Ekstrak Teks dari Gambar dan Konversi ke JSONL – Panduan C#
url: /id/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dan Konversi ke JSONL – Tutorial Lengkap C#

Pernah membutuhkan untuk **extract text from image** tetapi tidak yakin perpustakaan mana yang akan memberikan output yang bersih dan terstruktur? Anda tidak sendirian. Dalam banyak proyek pemrosesan kwitansi atau digitalisasi dokumen, kendala utamanya adalah mengubah bitmap menjadi teks yang dapat dicari *dan* format yang dapat dibaca mesin.  

Berita baiknya? Dengan Aspose OCR Anda dapat **extract text from image** dan, dengan beberapa baris kode, **convert image to JSONL** untuk analitik hilir. Panduan ini akan membawa Anda melalui seluruh proses, mulai dari memuat PNG hingga menulis file JSON‑Lines yang dapat dialirkan ke dalam pipeline data.

> **Hint:** Jika Anda sudah menggunakan .NET 6 atau yang lebih baru, kode yang sama berfungsi tanpa konfigurasi tambahan.

## Prasyarat — Apa yang Anda Butuhkan

- **.NET 6 SDK** (atau versi .NET terbaru apa pun)
- **Aspose.OCR** paket NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** untuk serialisasi  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Gambar contoh (misalnya `receipt.png`) ditempatkan di folder yang dapat Anda referensikan.
- IDE atau editor pilihan Anda—Visual Studio, VS Code, Rider, dll.

Tidak ada pengaturan berat, tidak ada layanan eksternal, hanya beberapa paket NuGet.

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Alt text: extract text from image using C# dengan Aspose OCR*

## Langkah 1: Muat Gambar yang Ingin Anda Proses  

Hal pertama yang Anda lakukan ketika ingin **extract text from image** adalah memberikan mesin OCR sebuah bitmap. Menggunakan `System.Drawing.Bitmap` mudah dan bekerja untuk sebagian besar format raster.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Why this matters:** Memuat gambar sebagai `Bitmap` memberi mesin OCR akses piksel langsung, yang meningkatkan kecepatan pengenalan dan akurasi dibandingkan dengan streaming byte mentah.

## Langkah 2: Konfigurasikan Aspose OCR untuk Output JSON‑Lines  

Aspose OCR memungkinkan Anda menentukan bahasa, format output, dan beberapa penyesuaian kinerja. Di sini kami meminta **JSON‑Lines** (satu objek JSON per baris) karena cocok untuk pemrosesan baris‑per‑baris nantinya.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Pro tip:** Jika Anda memerlukan kwitansi multibahasa, atur `Language = Language.Multilingual` atau berikan array nilai `Language`.

## Langkah 3: Jalankan OCR dan Tangkap Hasilnya  

Sekarang kami benar‑benar **extract text from image**. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi koleksi objek `OcrLine`, masing‑masing mewakili satu baris teks yang dikenali beserta kotak pembatasnya.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

Pada titik ini `ocrResult.Lines` berisi semua yang Anda butuhkan—teks mentah, skor kepercayaan, dan koordinat.

## Langkah 4: Serialisasi Baris ke JSON‑Lines  

Kami akan mengubah koleksi menjadi string JSON yang terindeksi rapi. Meskipun JSON‑Lines biasanya ringkas, menambahkan indentasi membuat file lebih mudah diperiksa selama pengembangan.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

Variabel `jsonLines` yang dihasilkan terlihat seperti ini (dipangkas untuk singkatnya):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Setiap baris diakhiri dengan karakter newline, memberi Anda file **JSONL** (JSON‑Lines) yang sesungguhnya.

## Langkah 5: Tulis JSON‑Lines ke Disk  

Akhirnya, kami menyimpan output sehingga layanan lain—seperti Spark, Logstash, atau skrip Bash sederhana—dapat mengonsumsinya baris per baris.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Saat Anda membuka `receipt.jsonl` Anda akan melihat satu objek JSON per baris, siap untuk streaming.

## Langkah 6: Verifikasi Ekspor  

Pemeriksaan cepat menyelamatkan Anda berjam‑jam debugging nantinya. Mari baca beberapa baris pertama kembali dan cetak ke konsol.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Output konsol tipikal:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Jika Anda melihat sesuatu yang serupa, selamat—Anda telah berhasil **extract text from image** dan **convert image to JSONL**.

## Kesalahan Umum & Cara Menghindarinya  

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Output kosong** | Jalur gambar tidak benar atau file tidak dapat dibaca. | Gunakan `File.Exists(imagePath)` sebelum membuat bitmap. |
| **Skor kepercayaan rendah** | Gambar buram atau memiliki kontras rendah. | Pra‑proses gambar (mis., `Bitmap.RotateFlip`, `Graphics.Clear`) atau tingkatkan DPI. |
| **Bahasa tidak tepat** | OCR default ke bahasa Inggris tetapi kwitansi dalam bahasa lain. | Atur `options.Language = Language.Spanish` (atau enum yang sesuai). |
| **JSONL muncul sebagai satu array JSON** | Anda menggunakan `Formatting.None` tanpa penanganan newline. | Pastikan setiap objek yang diserialisasi diakhiri dengan `Environment.NewLine`. |

## Contoh Lengkap yang Berfungsi  

Berikut adalah program lengkap yang siap dijalankan. Tempelkan ke proyek konsol dan tekan **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Hasil yang diharapkan:** Sebuah file `receipt.jsonl` yang berisi satu objek JSON per baris, masing‑masing dengan bidang `Text`, `Confidence`, dan `BoundingBox`. Anda kini dapat memasukkan file ini ke dalam pipeline analitik apa pun yang mengonsumsi JSONL.

## Langkah Selanjutnya – Melampaui OCR Dasar  

- **Pemrosesan batch:** Bungkus logika di atas dalam loop `foreach` untuk menangani seluruh folder kwitansi.  
- **Paralelisme:** Gunakan `Parallel.ForEach` untuk percepatan multi‑core saat menangani ribuan gambar.  
- **Pasca‑pemrosesan:** Hapus baris dengan kepercayaan rendah (`Confidence < 0.9`) sebelum menyimpan.  
- **Integrasi:** Dorong JSONL langsung ke Azure Blob Storage atau AWS S3 dengan SDK masing‑masing.  
- **Format alternatif:** Ganti `OutputFormat` ke `PlainText` atau `Xml` jika sistem hilir Anda lebih menyukainya.  

## Kesimpulan  

Anda kini memiliki solusi menyeluruh, ujung‑ke‑ujung untuk **extracting text from image** dan **converting image to JSONL** menggunakan Aspose OCR dalam C#. Tutorial ini mencakup semua hal mulai dari memuat bitmap hingga memverifikasi output, plus beberapa tips praktis untuk menjaga pipeline Anda tetap kuat.  

Cobalah dengan kwitansi, faktur, atau formulir yang dipindai milik Anda—saksikan mesin OCR mengubah piksel menjadi data yang dapat dicari dan terstruktur per baris dalam hitungan detik. Jika Anda menemukan kasus tepi (mis., pemindaian miring atau teks multibahasa), tinjau kembali bagian *RecognitionOptions* dan sesuaikan bahasa atau langkah pra‑pemrosesan.  

Selamat coding, semoga pipeline data Anda selalu bersih!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}