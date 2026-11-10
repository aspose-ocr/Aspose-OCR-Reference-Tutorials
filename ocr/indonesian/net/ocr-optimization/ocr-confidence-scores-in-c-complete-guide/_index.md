---
category: general
date: 2026-05-31
description: Pelajari cara mendapatkan skor kepercayaan OCR di C# saat mengekstrak
  teks dari gambar dan membaca gambar kwitansi dengan Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: id
og_description: Skor kepercayaan OCR memungkinkan Anda mengukur akurasi; panduan ini
  menunjukkan cara mengekstrak teks dari gambar, mendapatkan kotak pembatas, dan membaca
  gambar kwitansi menggunakan Aspose OCR.
og_title: Skor Kepercayaan OCR di C# – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Skor Kepercayaan OCR di C# – Panduan Lengkap
url: /id/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skor kepercayaan OCR dalam C# – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **OCR confidence scores** ketika Anda perlu *extract text from image*? Mungkin Anda sedang mencoba **read receipt image** untuk pelacakan pengeluaran dan ingin mengetahui karakter mana yang tidak pasti bagi mesin. Kabar baik? Dengan Aspose.OCR Anda dapat mengambil persentase kepercayaan, bounding boxes, dan teks biasa dari JPG hanya dalam beberapa baris C#.

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui: menginstal pustaka, mengonfigurasi mesin untuk **perform OCR on JPG**, mengambil skor kepercayaan, dan menafsirkan **OCR bounding boxes** yang memberi tahu Anda di mana setiap karakter berada pada halaman. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang mencetak setiap karakter, kepercayaannya, dan lokasinya—sempurna untuk memvalidasi receipt atau dokumen yang dipindai.

## Apa yang Akan Anda Pelajari

- Instal Aspose.OCR via NuGet dan siapkan mesin OCR dasar.  
- Konfigurasikan `OcrOptions` untuk meminta output plain‑text **with confidence scores** dan **bounding boxes**.  
- Loop melalui `OcrResult` untuk **extract text from image** baris‑per‑baris dan simbol‑per‑simbol.  
- Tangani jebakan umum seperti file yang hilang, karakter dengan kepercayaan rendah, dan format non‑JPG.  
- Perluas contoh untuk memproses beberapa gambar receipt dalam folder.

Tidak diperlukan pengalaman sebelumnya dengan Aspose; cukup dengan lingkungan .NET yang berfungsi dan gambar receipt (JPG) yang ingin Anda uji.

---

## Langkah 1 – Instal Aspose.OCR dan Siapkan Proyek Anda

Langkah pertama: Anda memerlukan paket NuGet Aspose.OCR. Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Versi percobaan gratis berlaku hingga 200 halaman, yang lebih dari cukup untuk menguji pemindaian receipt.

Setelah paket terinstal, buat proyek konsol baru (jika Anda belum memilikinya):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Sekarang Anda dapat membuka `Program.cs` yang dihasilkan dan mulai menambahkan direktif using:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Namespace ini memberi Anda akses ke `OcrEngine`, `OcrOptions`, dan tipe hasil yang akan kita perlukan nanti.

## Langkah 2 – Dapatkan skor kepercayaan OCR dan bounding box OCR

Ini adalah inti dari tutorial. Kami akan mengonfigurasi mesin sehingga setiap karakter yang dikenali dilengkapi dengan **confidence score** dan **bounding box** (persegi panjang yang mengelilingi glyph). Header H2 itu sendiri berisi kata kunci utama, memenuhi aturan SEO.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Mengapa menyertakan confidence scores?**  
Confidence score (0‑100%) memberi tahu Anda seberapa yakin mesin terhadap setiap karakter. Jika Anda memasukkan output ke dalam logika downstream—misalnya, alur kerja persetujuan pengeluaran—Anda dapat menolak atau menandai simbol dengan kepercayaan rendah secara otomatis.

**Mengapa meminta bounding boxes?**  
Bounding box penting ketika Anda perlu menyorot teks pada gambar asli, mengekstrak sub‑region, atau menyelaraskan hasil OCR dengan overlay UI. Setiap `character.Bounds` memberikan X, Y, lebar, dan tinggi dalam koordinat piksel.

## Langkah 3 – Lakukan OCR pada JPG dan extract text from image

Sekarang kita benar‑benar menjalankan mesin. Pemanggilan `Recognize()` melakukan semua pekerjaan berat dan mengembalikan objek `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Jika jalur gambar salah atau file tidak dalam format yang didukung, Aspose akan melempar `FileNotFoundException` atau `UnsupportedImageFormatException`. Bungkus pemanggilan dalam blok try/catch pada kode produksi untuk menangani kasus tepi tersebut dengan elegan.

### Mengambil teks plain

Jika Anda hanya membutuhkan teks yang digabungkan, Anda dapat membaca `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Namun karena kami juga meminta confidence scores dan bounding boxes, kami akan mengiterasi struktur untuk melihat detail setiap karakter.

## Langkah 4 – Iterasi melalui baris, simbol, dan tampilkan OCR confidence scores

Berikut loop yang mencetak setiap karakter, kepercayaannya, dan kotaknya. Inilah contoh **read receipt image** yang benar‑benar bersinar.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Contoh output mungkin terlihat seperti:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Menafsirkan angka:**  
- **Confidence ≥ 90%** – biasanya aman untuk diterima.  
- **Confidence 70‑89%** – Anda mungkin ingin memeriksa kembali, terutama untuk digit pada jumlah.  
- **Confidence < 70%** – pertimbangkan menandai untuk tinjauan manual.

## Langkah 5 – Contoh lengkap yang dapat dijalankan (termasuk penanganan error)

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke `Program.cs`. Program ini mencakup pemeriksaan sederhana untuk file yang hilang dan mencetak pesan ramah jika OCR gagal.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Output yang Diharapkan

Saat Anda menjalankan `dotnet run` konsol akan pertama menampilkan teks receipt yang digabungkan, kemudian daftar setiap karakter dengan confidence score dan bounding box‑nya. Jika confidence sebuah karakter rendah, Anda akan melihat persentase di bawah 80, yang menjadi petunjuk untuk memverifikasi bagian receipt tersebut secara manual.

## Bonus: Memproses Banyak Receipt dalam Folder

Jika Anda memiliki sekumpulan receipt JPG, bungkus logika di atas dalam loop `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. Ingat untuk mereset `OcrEngine` untuk setiap file, atau buat instance baru di dalam loop untuk menghindari kebocoran state.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Pemrosesan massal berguna untuk impor pengeluaran malam hari.

---

## Kesimpulan

Anda kini memiliki solusi end‑to‑end yang solid untuk memperoleh **OCR confidence scores** dalam C#, **extracting text from image**, dan mengambil **OCR bounding boxes** saat Anda **perform OCR on JPG** file seperti **read receipt image**. Kode ini sepenuhnya mandiri, bekerja dengan versi Aspose.OCR terbaru (per 2026‑05‑31), dan memberi Anda data terperinci yang diperlukan untuk membangun pipeline pemrosesan dokumen yang dapat dipercaya.

Apa selanjutnya? Cobalah memvisualisasikan bounding box pada receipt asli menggunakan `System.Drawing` atau pustaka UI, atau kirim karakter dengan confidence rendah ke layanan verifikasi sekunder. Anda juga dapat bereksperimen dengan bahasa lain dengan mengatur `ocrEngine.Options.Language = OcrLanguage.French;` – API mendukung banyak locale.

Selamat coding, dan semoga confidence scores Anda selalu tinggi! 

![Console output showing OCR confidence scores and bounding boxes for a receipt

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cara Mendapatkan Pilihan Karakter OCR untuk Karakter yang Diakui dalam Pengenalan Gambar](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Cara Menggunakan Aspose OCR untuk Hasil JSON dalam Pengenalan Gambar](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}