---
category: general
date: 2026-03-07
description: Pelajari cara meluruskan gambar, meningkatkan kontras, dan mengekstrak
  teks dari pemindaian menggunakan Aspose OCR. Lakukan OCR pada gambar dengan contoh
  lengkap C# dan muat gambar untuk OCR dengan mudah.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: id
og_description: Pelajari cara meluruskan gambar, meningkatkan kontras, dan mengekstrak
  teks dari pemindaian menggunakan Aspose OCR dalam C#. Lakukan OCR pada gambar dengan
  kode langkah demi langkah.
og_title: Cara Mengoreksi Kemiringan Gambar dan Menjalankan OCR di C# – Panduan Lengkap
tags:
- C#
- OCR
- Image Processing
title: Cara Mengoreksi Kemiringan Gambar dan Menjalankan OCR di C# – Panduan Lengkap
url: /id/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengoreksi Kemiringan Gambar dan Menjalankan OCR di C# – Panduan Lengkap

Jika Anda pernah bertanya-tanya **cara mengoreksi kemiringan gambar** sebelum menjalankan OCR, Anda berada di tempat yang tepat. Pada tutorial ini kami akan memandu Anda meningkatkan kontras, memuat gambar untuk OCR, dan akhirnya **mengekstrak teks dari hasil pemindaian** dengan Aspose OCR.  

Apakah Anda sedang mendigitalisasi kwitansi lama, membersihkan kontrak yang dipindai, atau hanya membutuhkan cara andal untuk membaca teks dari foto yang miring, langkah‑langkah di bawah ini mencakup semua yang Anda perlukan. Tanpa basa‑basi—hanya contoh yang dapat langsung Anda salin‑tempel ke Visual Studio.  

## Apa yang Akan Anda Capai

Pada akhir panduan ini Anda akan dapat:

* Mengoreksi kemiringan hingga 30° (itulah bagian **cara mengoreksi kemiringan gambar**).  
* Meningkatkan kontras gambar untuk tepi karakter yang lebih tajam (**cara meningkatkan kontras**).  
* Memuat foto Anda ke dalam mesin OCR (**memuat gambar untuk OCR**).  
* Menjalankan proses pengenalan dan **mengekstrak teks dari hasil pemindaian**.  

Semua ini bekerja dengan paket NuGet Aspose.OCR .NET terbaru (v23.11 pada saat penulisan).  

---

![Contoh cara mengoreksi kemiringan gambar](/images/deskew-example.png "cara mengoreksi kemiringan gambar")

*Gambar di atas menunjukkan dokumen yang dipindai sebelum dan sesudah koreksi kemiringan.*

## Prasyarat

* .NET 6.0 atau yang lebih baru (kode ini juga dapat dijalankan pada .NET Framework 4.7+).  
* Visual Studio 2022 (atau IDE C# apa pun yang Anda suka).  
* Paket NuGet Aspose.OCR – instal melalui `dotnet add package Aspose.OCR`.  

Itu saja. Tanpa layanan eksternal, tanpa kunci API.

---

## Cara Mengoreksi Kemiringan Gambar dengan Aspose OCR

Hal pertama yang kami lakukan adalah membuat **ImageProcessingPipeline** dan menambahkan `DeskewFilter`. Filter ini secara otomatis mendeteksi sudut garis teks dominan dan memutar gambar kembali ke posisi horizontal.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Mengapa ini penting:**  
Pemindaian yang miring membingungkan mesin OCR karena karakter tidak lagi sejajar dengan garis dasar. `DeskewFilter` menganalisis histogram gambar, menemukan sudutnya, dan memutarnya, sehingga akurasi pengenalan meningkat secara dramatis.

> **Tips profesional:** Jika Anda tahu dokumen Anda tidak pernah melebihi kemiringan 15°, atur `MaxAngle = 15` untuk mempercepat proses.

---

## Cara Meningkatkan Kontras untuk Pengakuan yang Lebih Baik

Setelah koreksi kemiringan, langkah selanjutnya adalah membuat teks lebih menonjol. `ContrastBoostFilter` memperluas rentang intensitas piksel, yang sangat membantu untuk cetakan yang pudar.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Mengapa ini membantu:**  
Pemindaian dengan kontras rendah menghasilkan karakter berwarna abu‑abu yang dapat diinterpretasikan binarisator sebagai latar belakang. Meningkatkan kontras membuat piksel gelap menjadi lebih gelap dan piksel terang menjadi lebih terang, memberikan `BinarizationFilter` kanvas yang lebih bersih.

---

## Lakukan OCR pada Gambar – Memuat File

Setelah gambar dipra‑proses, kita perlu **memuat gambar untuk OCR**. Aspose menyediakan helper `ImageStream.FromFile` yang praktis.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Jika gambar Anda berada dalam stream (misalnya, diunggah melalui API web), Anda dapat menggunakan `ImageStream.FromStream(yourStream)` sebagai gantinya. Mesin ini menerima BMP, JPEG, PNG, TIFF, dan banyak format lainnya.

---

## Jalankan Proses Pengenalan dan Ekstrak Teks dari Hasil Pemindaian

Setelah semuanya terhubung, memanggil `Recognize()` melakukan pekerjaan berat. Setelah pemanggilan, teks yang dikenali tersedia melalui `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Output yang diharapkan** (contoh untuk faktur sederhana):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Jika output terlihat berantakan, periksa kembali urutan pipeline—pertama koreksi kemiringan, kemudian denoise, peningkatan kontras, dan terakhir binarisasi. Menukar urutan dapat menurunkan hasil.

---

## Kesalahan Umum dan Kasus Tepi

| Masalah | Mengapa Terjadi | Solusi |
|---------|----------------|--------|
| **Hasil kosong** | Gambar terlalu gelap atau terlalu terang untuk metode binarisasi default. | Tingkatkan `ContrastBoostFilter.Strength` atau beralih ke `BinarizationMethod.Otsu`. |
| **Teks sebagian hilang** | Noise masih tersisa setelah denoising. | Gunakan `DenoiseLevel.Medium` untuk gambar yang lebih ringan, atau tambahkan `DenoiseFilter` kedua. |
| **Arah rotasi salah** | Dokumen memiliki orientasi campuran (misalnya, foto halaman yang diputar). | Atur `DeskewFilter.MaxAngle` lebih rendah dan pra‑putar gambar dengan `ImageProcessor.Rotate`. |
| **Perlambatan kinerja** | Batch besar gambar beresolusi tinggi. | Turunkan resolusi gambar (`ImageProcessor.Resize`) sebelum pipeline, atau proses secara paralel (`Parallel.ForEach`). |

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Simpan sebagai `Program.cs`, jalankan `dotnet run`, dan saksikan konsol menampilkan hasil **ekstrak teks dari hasil pemindaian**.  

---

## Langkah Selanjutnya & Topik Terkait

* **Pemrosesan batch** – Bungkus logika di atas dalam loop untuk menangani puluhan file.  
* **Paket bahasa khusus** – Jika Anda perlu membaca skrip non‑Latin, muat model bahasa melalui `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **Output PDF** – Gabungkan Aspose.PDF dengan OCR untuk menyematkan teks yang dapat dicari langsung ke dalam file PDF.  
* **Optimasi kinerja** – Bereksperimen dengan urutan `ImageProcessingPipeline`; kadang‑kadang denoising sebelum koreksi kemiringan menghasilkan proses lebih cepat pada foto yang berisik.  

Semua ini dibangun di atas konsep inti yang telah kami bahas: **cara mengoreksi kemiringan gambar**, **cara meningkatkan kontras**, **memuat gambar untuk OCR**, **melakukan OCR pada gambar**, dan akhirnya **mengekstrak teks dari hasil pemindaian**.

---

## Penutup

Kami baru saja mendemonstrasikan cara lengkap dan siap produksi untuk **cara mengoreksi kemiringan gambar** dan menjalankan OCR di C#. Dengan menambahkan filter deskew, langkah denoise, peningkatan kontras, dan binarisasi, Anda mendapatkan input bersih yang memungkinkan Aspose OCR secara andal **mengekstrak teks dari hasil pemindaian**.  

Cobalah kode tersebut, sesuaikan parameter filter untuk dokumen Anda sendiri, dan Anda akan melihat seberapa cepat akurasi pengenalan meningkat. Ada pertanyaan? Tinggalkan komentar, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}