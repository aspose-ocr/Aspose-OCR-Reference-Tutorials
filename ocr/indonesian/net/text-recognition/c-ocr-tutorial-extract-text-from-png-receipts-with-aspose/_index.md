---
category: general
date: 2026-05-25
description: Tutorial OCR C# yang menunjukkan cara memuat file gambar C# dan mengenali
  teks PNG dari struk menggunakan Aspose OCR – panduan langkah demi langkah.
draft: false
keywords:
- c# OCR tutorial
- load image file c#
- recognize png text
- read receipt OCR
- perform OCR image
language: id
og_description: Tutorial OCR C# yang memandu Anda dalam memuat file gambar C# dan
  mengenali teks PNG dari struk menggunakan Aspose OCR.
og_title: c# OCR tutorial – Ekstrak Teks dari Resi PNG
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: c# OCR tutorial that shows how to load image file c# and recognize
    png text from a receipt using Aspose OCR – step‑by‑step guide.
  headline: 'c# OCR tutorial: Extract Text from PNG Receipts with Aspose'
  type: TechArticle
- description: c# OCR tutorial that shows how to load image file c# and recognize
    png text from a receipt using Aspose OCR – step‑by‑step guide.
  name: 'c# OCR tutorial: Extract Text from PNG Receipts with Aspose'
  steps:
  - name: Why Aspose?
    text: Aspose OCR supports over 30 languages, works offline, and returns a rich
      `OcrResult` object—perfect for **perform OCR image** tasks where you need more
      than just plain text.
  - name: Handling Common Edge Cases
    text: '| Situation | What to do | |-----------|------------| | **Image is blurry**
      | Pre‑process with `System.Drawing` to sharpen or increase DPI. | | **Receipt
      contains multiple languages** | Set `ocrEngine.Language = OcrLanguage.English
      | OcrLanguage.Spanish;` | | **Large batch processing** | Reuse a sin'
  - name: What’s Next?
    text: '- Experiment with **load image file c#** using `SkiaSharp` for true cross‑platform
      support. - Dive deeper into `OcrResult.Words` to extract line items, prices,
      and dates—perfect for expense‑tracking apps. - Combine this tutorial with Azure
      Functions or AWS Lambda to build a serverless receipt‑proces'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: 'Tutorial OCR C#: Ekstrak Teks dari Resi PNG dengan Aspose'
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-png-receipts-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# OCR – Ekstrak Teks dari Resi PNG dengan Aspose

Pernah membutuhkan **c# OCR tutorial** yang benar‑benar menyelesaikan pekerjaan tanpa harus terus‑menerus Googling? Anda berada di tempat yang tepat. Dalam panduan ini kami akan **load image file c#**, **recognize png text**, dan **read receipt OCR** results, sambil menunjukkan cara **perform OCR image** processing dengan Aspose OCR.

Kami akan memulai dengan menginstal paket NuGet yang diperlukan, menelusuri setiap baris kode, dan menyelesaikannya dengan dump JSON yang rapi yang dapat Anda alirkan langsung ke pipeline data berikutnya. Tanpa basa‑basi, hanya solusi praktis yang siap dijalankan.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan Aspose OCR dalam proyek .NET 6 (atau lebih baru).  
- Langkah‑langkah tepat untuk **load an image file c#** dan menyerahkannya ke mesin.  
- Cara **recognize png text** dari gambar resi dan menangkap hasilnya.  
- Cara **read receipt OCR** output sebagai JSON yang terformat rapi.  
- Tips untuk operasi **perform OCR image** pada berbagai jenis file dan menangani jebakan umum.

**Prasyarat**  
- Visual Studio 2022 (atau IDE apa pun yang Anda suka).  
- .NET 6 SDK atau yang lebih baru.  
- Sebuah gambar resi PNG yang siap pakai (kami akan menyebutnya `receipt.png`).  

Jika Anda sudah memiliki itu, mari kita mulai.

![tangkapan layar tutorial c# OCR](ocr-demo.png "hasil tutorial c# OCR menampilkan output JSON")

## Tutorial c# OCR – Menyiapkan Mesin Aspose OCR

Pertama-tama, kita membutuhkan pustaka Aspose OCR. Buka terminal Anda di folder solusi dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah tunggal itu mengunduh semua yang diperlukan, termasuk binary native untuk decoding gambar. Setelah terpasang, buat proyek konsol baru atau tambahkan kode ke proyek yang sudah ada.

### Mengapa Aspose?

Aspose OCR mendukung lebih dari 30 bahasa, dapat bekerja secara offline, dan mengembalikan objek `OcrResult` yang kaya—sempurna untuk tugas **perform OCR image** dimana Anda membutuhkan lebih dari sekadar teks biasa.

## Memuat file gambar c# dan Menyiapkan Resi

Sekarang pustaka sudah siap, mari **load image file c#**. Kelas `System.Drawing.Image` melakukan pekerjaan berat, tetapi Anda juga dapat menggunakan `SkiaSharp` jika lebih menyukai alternatif lintas‑platform.

```csharp
using System;
using System.Drawing;               // For Image loading
using Aspose.OCR;                  // OCR engine
using System.Text.Json;            // JSON serialization

// Step 1: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most receipts; change as needed
    Language = OcrLanguage.English
};

// Step 2: Load the image to be processed
// Replace the path with the actual location of your receipt PNG
string imagePath = @"C:\Receipts\receipt.png";
if (!File.Exists(imagePath))
{
    Console.WriteLine($"File not found: {imagePath}");
    return;
}
using Image receiptImage = Image.FromFile(imagePath);
```

> **Pro tip:** Bungkus `Image` dalam pernyataan `using` (seperti yang ditunjukkan) untuk segera membebaskan sumber daya native—terutama penting ketika Anda **perform OCR image** pada banyak file dalam sebuah loop.

## Mengenali teks PNG dengan Aspose

Dengan gambar berada di memori, mesin kini dapat **recognize png text**. Aspose mengembalikan `OcrResult` yang berisi baik string mentah maupun data terperinci tentang setiap kata yang dikenali.

```csharp
// Step 3: Perform OCR and obtain the result object
OcrResult ocrResult = ocrEngine.RecognizeWithResult(receiptImage);

// Quick sanity check – was anything recognized?
if (string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("No text detected. Verify image quality or language settings.");
    return;
}
```

Mengapa memanggil `RecognizeWithResult` alih‑alih `Recognize` yang lebih sederhana? Yang pertama memberi Anda akses ke skor kepercayaan, kotak pembatas, dan pemisahan baris—berguna jika nanti Anda perlu **read receipt OCR** untuk ekstraksi item baris.

## Membaca Hasil OCR Resi sebagai JSON

Sebagian besar sistem hilir menyukai JSON, jadi mari serialisasikan `OcrResult`. Serializer `System.Text.Json` menangani objek kompleks dengan elegan, dan kami akan mengaktifkan indentasi untuk keterbacaan.

```csharp
// Step 4: Convert the OCR result to a readable JSON string (indented)
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

JSON yang dihasilkan terlihat seperti ini (dipangkas untuk singkat):

```json
{
  "Text": "Walmart\n123 Main St\nTotal $12.34",
  "Words": [
    {
      "Text": "Walmart",
      "Confidence": 0.98,
      "Rectangle": { "X": 10, "Y": 20, "Width": 150, "Height": 30 }
    },
    {
      "Text": "Total",
      "Confidence": 0.95,
      "Rectangle": { "X": 10, "Y": 150, "Width": 80, "Height": 25 }
    }
  ]
}
```

Anda sekarang dapat mengalirkan `jsonResult` ke basis data, antrian pesan, atau cukup mencatatnya untuk debugging.

## Melakukan Pemrosesan Gambar OCR dan Menampilkan Output

Akhirnya, keluarkan JSON ke konsol. Dalam aplikasi dunia nyata Anda mungkin akan menulisnya ke file atau mengirimnya lewat HTTP, tetapi konsol memudahkan verifikasi bahwa semuanya berfungsi.

```csharp
// Step 5: Output the JSON to the console
Console.WriteLine("=== OCR Result (JSON) ===");
Console.WriteLine(jsonResult);
```

Jalankan program (`dotnet run`) dan Anda akan melihat JSON yang terformat rapi tercetak. Jika gambar resi jelas, teks akan tepat; jika tidak, pertimbangkan meningkatkan resolusi gambar atau menerapkan filter pra‑pemrosesan (mis., skala abu‑abu, peningkatan kontras) sebelum memberi makan ke mesin.

### Menangani Kasus Pinggiran Umum

| Situasi | Apa yang harus dilakukan |
|-----------|------------|
| **Gambar buram** | Pra‑proses dengan `System.Drawing` untuk menajamkan atau meningkatkan DPI. |
| **Resi berisi banyak bahasa** | Setel `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` |
| **Pemrosesan batch besar** | Gunakan kembali satu instance `OcrEngine`; hanya ubah `Image` setiap iterasi. |
| **Tekanan memori** | Segera dispose objek `Image` dan pertimbangkan `await Task.Run` untuk pipeline async. |

## Kesimpulan

Selamat—Anda baru saja menyelesaikan **c# OCR tutorial** yang memuat gambar, **recognizes png text**, dan **reads receipt OCR** output sebagai JSON bersih. Langkah‑langkah inti (penyiapan mesin, pemuatan gambar, eksekusi OCR, serialisasi, dan tampilan) membentuk fondasi kuat yang dapat Anda kembangkan ke faktur, paspor, atau dokumen ter‑scan lainnya.

### Apa Selanjutnya?

- Bereksperimen dengan **load image file c#** menggunakan `SkiaSharp` untuk dukungan lintas‑platform yang sesungguhnya.  
- Selami lebih dalam `OcrResult.Words` untuk mengekstrak item baris, harga, dan tanggal—sempurna untuk aplikasi pelacakan pengeluaran.  
- Gabungkan tutorial ini dengan Azure Functions atau AWS Lambda untuk membangun API pemrosesan resi tanpa server.  

Silakan ubah kode, tambahkan lebih banyak gambar, atau bahkan beralih ke paket bahasa lain. Dunia OCR penuh kejutan, dan kini Anda memiliki alat untuk menjelajahinya.

Selamat coding, dan semoga resi Anda selalu dapat dibaca!

## Tutorial Terkait

- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)
- [Cara Menggunakan OCR - Mengenali Gambar tanpa Deteksi Area Teks](/ocr/english/net/image-and-drawing-recognition/recognize-image-without-text-area-detection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}