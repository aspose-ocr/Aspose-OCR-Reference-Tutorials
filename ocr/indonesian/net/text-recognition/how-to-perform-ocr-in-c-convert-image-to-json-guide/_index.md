---
category: general
date: 2026-02-17
description: Cara melakukan OCR di C# dan mengonversi gambar ke JSON dengan cepat.
  Ikuti tutorial OCR C# ini untuk mengekstrak teks dari gambar dan menyimpan tata
  letak sebagai JSON.
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: id
og_description: Bagaimana melakukan OCR di C#? Panduan ini menunjukkan cara mengonversi
  gambar ke JSON, mengekstrak teks dari gambar di C#, dan memuat file gambar untuk
  OCR.
og_title: Cara Melakukan OCR di C# – Mengonversi Gambar ke JSON
tags:
- OCR
- C#
- Aspose
title: Cara Melakukan OCR di C# – Panduan Mengonversi Gambar ke JSON
url: /id/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Panduan Mengonversi Gambar ke JSON

Pernah bertanya-tanya **bagaimana cara melakukan OCR** pada struk, faktur, atau dokumen yang dipindai menggunakan C#? Anda bukan satu-satunya. Banyak pengembang menemui kesulitan ketika mereka perlu mengekstrak teks *dan* mempertahankan tata letak tanpa menghabiskan berjam-jam menulis parser khusus.  

Dalam tutorial ini kami akan membahas **c# ocr tutorial** lengkap yang menunjukkan secara tepat bagaimana melakukan OCR, **convert image to json**, dan menyimpan hasilnya untuk analisis selanjutnya. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang memuat file gambar di C#, mengekstrak teks, dan menulis file JSON terperinci yang berisi koordinat, skor kepercayaan, serta teks mentah.

## Prasyarat — Apa yang Anda Butuhkan

- .NET 6 SDK atau yang lebih baru (kode ini juga berfungsi di .NET Core)  
- Visual Studio 2022 atau editor apa pun yang Anda sukai  
- Lisensi Aspose OCR (Anda dapat memulai dengan percobaan gratis)  
- Gambar contoh, misalnya `receipt.png`, ditempatkan di folder yang dapat Anda referensikan  

Itu saja—tidak ada paket NuGet tambahan selain `Aspose.OCR`. Jika Anda sudah memiliki semua itu, Anda siap melanjutkan.

## Cara Melakukan OCR dan Mendapatkan Output JSON

Inti dari **how to perform OCR** dengan Aspose sangat sederhana: buat sebuah `OcrEngine`, beri aliran gambar, panggil `Recognize`, lalu serialisasikan `OcrResult` ke JSON. Mari kita uraikan langkah demi langkah.

### Langkah 1: Instal Paket NuGet Aspose  OCR

Open your terminal in the project folder and run:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Gunakan flag `--version` untuk mengunci ke versi stabil terbaru (mis., `23.9.0`). Ini menjaga build Anda dapat direproduksi.

### Langkah 2: Buat Kerangka Proyek Konsol

Jika Anda belum memiliki proyek, buat satu:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

Sekarang Anda memiliki file `Program.cs` yang siap untuk kode yang akan **load image file c#** dan memulai proses OCR.

### Langkah 3: Tulis Kode Lengkap OCR‑to‑JSON

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke dalam `Program.cs`. Setiap baris diberi komentar sehingga Anda dapat melihat *mengapa* setiap bagian penting.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### Apa yang Dilakukan Kode

| Step | Why It Matters |
|------|----------------|
| **Initialize OcrEngine** | Menyiapkan bahasa default (Inggris) dan mempersiapkan model internal. |
| **Load image file** | Menggunakan `ImageStream.FromFile` memastikan gambar dibaca dalam format yang diharapkan Aspose. |
| **Recognize** | Proses utama—analisis piksel, segmentasi karakter, dan pencarian kamus. |
| **ToJson** | Menghasilkan output terstruktur yang mencakup kotak pembatas, kepercayaan, dan teks mentah. |
| **WriteAllText** | Menyimpan JSON sehingga Anda dapat membagikannya dengan layanan lain. |
| **Console.WriteLine** | Memberikan umpan balik langsung—berguna saat dijalankan dari terminal. |

> **Watch out:** Jika gambar Anda besar, pertimbangkan untuk mengubah ukurannya terlebih dahulu guna meningkatkan kecepatan dan penggunaan memori. Aspose menyediakan metode `Resize` yang dapat Anda panggil pada `ImageStream`.

### Langkah 4: Jalankan Aplikasi dan Verifikasi Output

Dari terminal:

```bash
dotnet run
```

Anda akan melihat:

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

Buka `receipt.json` di editor apa pun; Anda akan menemukan sesuatu seperti:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

JSON tersebut menangkap **extract text image c#** beserta metadata tata letak, sempurna untuk pemrosesan selanjutnya.

## Mengonversi Gambar ke JSON – Lebih Dari Dasar

Sekarang Anda tahu **how to perform OCR**, mari jelajahi beberapa variasi yang mungkin Anda perlukan dalam proyek nyata.

### Menangani Banyak Halaman

Jika sumber Anda adalah PDF atau TIFF multi‑halaman, cukup lakukan loop pada setiap halaman:

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### Menyesuaikan Bahasa dan Akurasi

Aspose mendukung lebih dari 40 bahasa. Untuk beralih ke bahasa Spanyol:

```csharp
ocrEngine.Language = Language.Spanish;
```

Anda juga dapat menyesuaikan `ocrEngine.Settings` untuk mengaktifkan **auto‑rotate**, **noise removal**, atau **dictionary‑based correction**—semua ini meningkatkan kualitas JSON yang Anda peroleh.

### Menyimpan JSON dalam Format Pretty‑Printed

Jika Anda lebih suka JSON berindentasi untuk keterbacaan:

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Load Image File C# – Kesalahan Umum dan Tips

Saat Anda **load image file c#**, Anda mungkin menghadapi:

- **File not found** – Pastikan path bersifat absolut atau gunakan `Path.Combine` dengan `Environment.CurrentDirectory`.  
- **Unsupported format** – Aspose menangani PNG, JPEG, BMP, TIFF, dan PDF. Untuk format RAW, konversi terlebih dahulu.  
- **Large file memory pressure** – Gunakan `ImageStream.FromFile(path, maxSizeInKB)` untuk menurunkan skala saat memuat.

Menangani masalah ini lebih awal menyelamatkan Anda dari pengecualian yang membingungkan di kemudian hari dalam pipeline OCR.

## Extract Text Image C# – Memverifikasi Hasil

Setelah Anda memiliki JSON, Anda mungkin hanya menginginkan teks biasa:

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

Potongan kode ini menunjukkan **extract text image c#** tanpa detail tata letak—berguna untuk pencarian cepat atau pencatatan.

---

![Diagram yang menunjukkan alur kerja OCR – cara melakukan OCR, mengonversi gambar ke JSON, dan mengekstrak teks gambar c#](/images/ocr-workflow.png "alur kerja cara melakukan OCR")

*Teks alt gambar: "diagram alur kerja cara melakukan OCR yang menggambarkan mengonversi gambar ke JSON dan mengekstrak teks gambar c#"*  

*(Gambar ini adalah placeholder; ganti dengan diagram sebenarnya saat dipublikasikan.)*

---

## Kesimpulan

Kami telah membahas **how to perform OCR** di C# dari awal hingga akhir, menunjukkan cara **convert image to JSON**, dan menjelaskan nuansa **load image file c#** serta **extract text image c#**. Contoh kode lengkap siap disisipkan ke dalam proyek .NET apa pun, dan output JSON memberikan Anda teks mentah serta data tata letak yang tepat untuk analitik selanjutnya.

Apa selanjutnya? Cobalah memasukkan JSON ke dalam basis data, memvisualisasikan kotak pembatas pada UI, atau menghubungkan beberapa proses OCR untuk pemrosesan batch. Anda juga dapat bereksperimen dengan fitur Aspose lainnya seperti pengenalan tulisan tangan atau deteksi barcode—keduanya cocok secara alami dalam pipeline yang sama.

Jika Anda menemui kendala, tinjau kembali tips pemecahan masalah di bagian “Load Image File C#”, atau jelajahi dokumentasi lengkap Aspose untuk pengaturan lanjutan. Selamat coding, dan nikmati mengubah gambar menjadi data terstruktur!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}