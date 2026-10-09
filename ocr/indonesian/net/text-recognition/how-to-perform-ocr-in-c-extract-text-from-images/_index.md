---
category: general
date: 2026-10-08
description: Pelajari cara melakukan OCR di C# menggunakan Aspose.OCR untuk mengekstrak
  teks dari file gambar. Panduan ini menunjukkan cara mengonversi gambar menjadi teks
  dan mengenali teks dari JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- recognize text from jpeg
- c# ocr example
language: id
lastmod: 2026-10-08
og_description: Cara melakukan OCR di C# dengan Aspose.OCR. Ikuti panduan langkah
  demi langkah ini untuk mengekstrak teks dari file gambar, mengonversi gambar menjadi
  teks, dan mengenali teks dari JPEG.
og_image_alt: Console output displaying Cyrillic text recognized from a JPEG image
  by a C# OCR program
og_title: Cara melakukan OCR di C# – mengekstrak teks dari gambar
schemas:
- author: Aspose
  dateModified: '2026-10-08'
  description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  headline: How to perform OCR in C# – extract text from images
  type: TechArticle
- description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  name: How to perform OCR in C# – extract text from images
  steps:
  - name: Why each line matters
    text: '* **`OcrEngine ocrEngine = new OcrEngine();`** – Instantiates the engine
      that orchestrates the whole OCR pipeline. * **`ocrEngine.Language = Language.Cyrillic;`**
      – Selects the language model. Choosing the correct language dramatically improves
      accuracy when you **extract text from image** files tha'
  - name: 4.1 Recognizing English or multilingual text
    text: 'Replace the language assignment with the appropriate enum:'
  - name: 4.2 Processing images from a stream instead of a file
    text: 'If your image arrives via an HTTP response or a database blob, use a `MemoryStream`:'
  - name: 4.3 Handling large or low‑resolution images
    text: 'Large images increase memory consumption. You can downscale before OCR:'
  - name: 4.4 Error handling
    text: 'Wrap the recognition call in a try‑catch block to catch network or file‑access
      errors:'
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
- Image Processing
title: Cara melakukan OCR di C# – mengekstrak teks dari gambar
url: /id/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR di C# – mengekstrak teks dari gambar

Jika Anda perlu **how to perform OCR** dalam aplikasi .NET, tutorial ini memberi Anda solusi lengkap yang siap dijalankan. Menggunakan Aspose.OCR Anda dapat **extract text from image** file, **convert image to text**, dan **recognize text from JPEG** dengan hanya beberapa baris kode.

Anda akan melihat seluruh alur kerja—dari menginstal pustaka hingga mencetak string yang dikenali—sehingga Anda dapat menyalin contoh ke dalam proyek Anda sendiri dan mulai memproses gambar segera.

## Apa yang akan Anda pelajari

* Cara menyiapkan proyek C# untuk tugas OCR.  
* Cara memuat JPEG (atau gambar lain yang didukung) dan menjalankan pengenalan.  
* Cara mengambil teks hasil dan menggunakannya dalam aplikasi Anda.  

Satu-satunya prasyarat adalah .NET SDK terbaru (≥ .NET 6) dan koneksi internet untuk mengunduh model bahasa pertama.

## Langkah 1: Siapkan proyek dan instal Aspose.OCR

1. Buat proyek konsol baru:

   ```bash
   dotnet new console -n OcrDemo
   cd OcrDemo
   ```

2. Tambahkan paket NuGet Aspose.OCR:

   ```bash
   dotnet add package Aspose.OCR
   ```

   Paket ini berisi mesin OCR, model bahasa, dan utilitas penanganan gambar yang diperlukan untuk **convert image to text**.

> **Pro tip:** Jika Anda berencana menjalankan OCR pada banyak gambar, pertimbangkan menambahkan paket ke pustaka bersama sehingga Anda dapat menggunakan kembali instance mesin yang sama.

## Langkah 2: Tulis contoh OCR C#

Buat atau ganti `Program.cs` dengan kode berikut. Ini menunjukkan **c# ocr example** yang bekerja untuk format gambar apa pun yang didukung oleh Aspose.OCR (JPEG, PNG, BMP, dll.).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // ---------------------------------------------------------
        // Step 2.1: Create an OCR engine instance
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // Step 2.2: Choose the language model.
        // The example uses Cyrillic; replace with Language.English,
        // Language.French, etc., to match your source image.
        // ---------------------------------------------------------
        ocrEngine.Language = Language.Cyrillic; // <-- change as needed

        // ---------------------------------------------------------
        // Step 2.3: Load the image you want to process.
        // ImageStream.FromFile automatically reads JPEG, PNG, BMP…
        // ---------------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile("sample_cyrillic.jpg");

        // ---------------------------------------------------------
        // Step 2.4: Run the recognition process.
        // This call downloads the required language model the first
        // time it is used, then performs the OCR.
        // ---------------------------------------------------------
        ocrEngine.Recognize();

        // ---------------------------------------------------------
        // Step 2.5: Retrieve the recognized text.
        // The Text property holds the result of the OCR engine.
        // ---------------------------------------------------------
        string recognizedText = ocrEngine.Text;

        // ---------------------------------------------------------
        // Step 2.6: Display the output.
        // This is where you can further process the string,
        // e.g., save to a database, feed to a search index, etc.
        // ---------------------------------------------------------
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### Mengapa setiap baris penting

* **`OcrEngine ocrEngine = new OcrEngine();`** – Membuat instance mesin yang mengatur seluruh pipeline OCR.  
* **`ocrEngine.Language = Language.Cyrillic;`** – Memilih model bahasa. Memilih bahasa yang tepat secara dramatis meningkatkan akurasi ketika Anda **extract text from image** file yang berisi karakter non‑Latin.  
* **`ocrEngine.Image = ImageStream.FromFile(...);`** – Memuat JPEG sumber (atau gambar lain yang didukung). Langkah ini penting untuk **recognize text from jpeg**.  
* **`ocrEngine.Recognize();`** – Menjalankan algoritma inti OCR. Metode ini menunggu hingga mesin selesai memproses.  
* **`ocrEngine.Text;`** – Mengembalikan hasil teks biasa, yang kini dapat Anda **convert image to text** untuk logika selanjutnya.

## Langkah 3: Jalankan program dan verifikasi output

Compile and execute:

```bash
dotnet run
```

Jika gambar `sample_cyrillic.jpg` berisi frasa Cyrillic “Привет мир”, konsol akan menampilkan:

```
=== Recognized Text ===
Привет мир
```

Output tersebut membuktikan bahwa Anda telah berhasil mempelajari **how to perform OCR** dan **extract text from image** menggunakan C#.

## Langkah 4: Variasi umum dan kasus tepi

### 4.1 Mengenali teks Bahasa Inggris atau multibahasa

Replace the language assignment with the appropriate enum:

```csharp
ocrEngine.Language = Language.English;           // English only
ocrEngine.Language = Language.Multilingual;      // Detects many languages automatically
```

### 4.2 Memproses gambar dari stream alih-alih file

If your image arrives via an HTTP response or a database blob, use a `MemoryStream`:

```csharp
using (var ms = new MemoryStream(imageBytes))
{
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
}
```

### 4.3 Menangani gambar berukuran besar atau resolusi rendah

Large images increase memory consumption. You can downscale before OCR:

```csharp
ocrEngine.Config.ImagePreprocessOptions.ScaleFactor = 0.5; // Reduce size by 50%
```

### 4.4 Penanganan error

Wrap the recognition call in a try‑catch block to catch network or file‑access errors:

```csharp
try
{
    ocrEngine.Recognize();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

## Langkah 5: Langkah selanjutnya – memperluas alur kerja OCR Anda

* **Batch processing:** Loop melalui file dalam direktori untuk **convert image to text** untuk setiap JPEG.  
* **Post‑processing:** Terapkan ekspresi reguler untuk membersihkan string yang dikenali, berguna ketika Anda perlu **extract text from image** pada formulir atau faktur.  
* **Integration with Azure Cognitive Services:** Bandingkan hasil Aspose.OCR dengan OCR berbasis cloud untuk akurasi lebih tinggi pada tata letak kompleks.  
* **Storing results:** Masukkan teks yang diekstrak ke dalam basis data SQL atau indeks ElasticSearch untuk dokumen yang dapat dicari.

---

## Kesimpulan

Anda sekarang tahu **how to perform OCR** di C# dengan Aspose.OCR, mulai dari menginstal paket hingga menampilkan string yang dikenali. **c# ocr example** lengkap ini memungkinkan Anda **extract text from image**, **convert image to text**, dan **recognize text from JPEG** hanya dengan beberapa baris kode. Bereksperimenlah dengan model bahasa yang berbeda, sumber gambar, dan teknik post‑processing untuk menyesuaikan dengan kebutuhan spesifik Anda.

---

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menggunakan OCR di C# – Mengekstrak Teks dari File Gambar](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-files/)
- [Mengonversi Gambar ke Teks di C# dengan Aspose OCR – Panduan Langkah‑per‑Langkah](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [Cara Melakukan OCR di C# – Mengekstrak Teks dan Menulis JSON](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}