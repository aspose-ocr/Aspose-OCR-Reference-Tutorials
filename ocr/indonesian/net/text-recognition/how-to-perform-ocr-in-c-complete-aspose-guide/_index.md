---
category: general
date: 2026-02-16
description: Pelajari cara melakukan OCR di C# menggunakan Aspose.OCR – mengenali
  teks dari foto, membaca teks dari pemindaian, dan mengekstrak teks dari struk dengan
  akurasi tinggi.
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: id
og_description: Pelajari cara melakukan OCR di C# dengan Aspose.OCR. Panduan ini menunjukkan
  cara mengenali teks dari foto, membaca teks dari pemindaian, dan mengekstrak teks
  dari struk.
og_title: Cara Melakukan OCR di C# – Panduan Lengkap Aspose
tags:
- C#
- Aspose.OCR
- Image Processing
title: Cara Melakukan OCR di C# – Panduan Lengkap Aspose
url: /id/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Panduan Lengkap Aspose

Pernah bertanya-tanya **bagaimana cara melakukan OCR** pada kwitansi yang buram atau foto acak yang Anda ambil dengan ponsel? Anda bukan satu-satunya. Dalam banyak aplikasi dunia nyata kami perlu **mengenali teks dari foto** file, **membaca teks dari pemindaian** dokumen, atau **mengekstrak teks dari gambar kwitansi** tanpa mengirim data ke layanan cloud.  

Dalam tutorial ini kami akan membahas contoh mandiri yang menunjukkan **bagaimana cara melakukan OCR** dengan Aspose.OCR, dan kami akan menyelipkan tips tentang cara **meningkatkan akurasi OCR** sepanjang jalan. Pada akhir tutorial Anda akan memiliki program konsol C# siap‑jalankan yang mengekstrak teks biasa dari gambar apa pun yang Anda tunjuk.

> **Apa yang Anda perlukan**  
> * .NET 6 SDK (atau versi .NET terbaru apa pun)  
> * Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
> * Gambar contoh – misalnya foto kwitansi bernama `photo_receipt.jpg`  

![how to perform OCR example](image.png){alt="cara melakukan OCR"}

## Cara Melakukan OCR dengan Aspose.OCR di C#

Langkah pertama adalah menyiapkan mesin OCR dan memuat model bahasa Inggris. Ini adalah inti dari **bagaimana cara melakukan OCR** dengan Aspose; tanpa model bahasa mesin tidak akan tahu karakter mana yang harus dicari.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*Mengapa ini penting*: Memuat model bahasa yang tepat secara langsung memengaruhi kecepatan dan akurasi pengenalan. Bahasa Inggris adalah kasus paling umum, tetapi Aspose menyediakan puluhan model lain jika Anda pernah perlu **membaca teks dari pemindaian** dokumen dalam bahasa Prancis, Jerman, dll.

## Mengenali Teks dari Foto

Foto yang diambil dengan ponsel sering mengalami rotasi, noise, atau kontras rendah. Sebelum kita meminta mesin untuk **mengenali teks dari foto**, kita mengonfigurasi beberapa opsi pra‑pemrosesan yang membersihkan gambar.

```csharp
// Configure preprocessing to boost OCR results
PreprocessingOptions preprocessingOptions = new PreprocessingOptions
{
    Deskew = true,                     // Auto‑correct rotation (helps with tilted receipts)
    Denoise = DenoiseLevel.Medium,    // Reduce graininess
    Binarize = BinarizeMethod.Otsu,   // Convert to black‑and‑white for sharper edges
    ContrastEnhancement = true        // Boost contrast for faint characters
};

// Apply the preprocessing configuration
ocrEngine.Preprocessing = preprocessingOptions;
```

*Tip pro*: Jika Anda melihat karakter yang hilang, coba ubah `DenoiseLevel` menjadi `High` atau gunakan `BinarizeMethod.Sauvola`. Penyesuaian ini merupakan bagian dari strategi **meningkatkan akurasi OCR**.

## Membaca Teks dari Pemindaian

Sekarang mesin sudah siap, kami memuat gambar. Baik itu halaman PDF yang dipindai disimpan sebagai JPEG atau foto formulir cetak, kodenya tetap sama.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

Jika Anda memiliki `Stream` alih-alih jalur file, cukup ganti `FromFile` dengan `FromStream`. Fleksibilitas ini berguna ketika Anda **membaca teks dari pemindaian** gambar yang berasal dari unggahan web.

## Mengekstrak Teks dari Kwitansi

Dengan semua sudah diatur, pemanggilan OCR sebenarnya hanya satu baris. Metode ini mengembalikan string teks biasa yang diekstrak, yang kemudian dapat kami tampilkan, simpan, atau masukkan ke sistem lain.

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**Output yang diharapkan** (contoh untuk kwitansi sederhana):

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

Jika output terlihat berantakan, tinjau kembali bagian pra‑pemrosesan – itu adalah tempat paling umum untuk **meningkatkan akurasi OCR**.

## Meningkatkan Akurasi OCR – Penyesuaian Lanjutan

Meskipun pengaturan default bekerja untuk banyak kasus, pipeline produksi sering memerlukan perawatan ekstra:

| Situasi | Penyesuaian | Alasan |
|-----------|------------|--------|
| Latar belakang sangat gelap | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | Meningkatkan pemisahan antara teks dan latar belakang |
| Catatan tulisan tangan | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | Model khusus untuk goresan tulisan sambung |
| Pemindaian multi‑halaman | Loop over each page image and call `Recognize()` per iteration | Menjaga jejak memori tetap rendah |
| Gambar besar (> 2000 px) | Resize before feeding to OCR (`Image.Resize(width, height)`) | Pemrosesan lebih cepat, penggunaan memori lebih sedikit |

Ingat, **bagaimana cara melakukan OCR** bukan resep satu‑ukuran‑untuk‑semua – Anda sering akan bereksperimen dengan pengaturan ini sampai output memenuhi standar kualitas Anda.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap disalin‑tempel. Program ini mencakup semua bagian yang kami bahas, plus bantuan kecil yang memeriksa apakah file ada sebelum mencoba membacanya.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine and load language
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 2️⃣ Set up preprocessing to improve OCR accuracy
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = true,
            Denoise = DenoiseLevel.Medium,
            Binarize = BinarizeMethod.Otsu,
            ContrastEnhancement = true
        };

        // 3️⃣ Path to the image – change this to your own file
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo_receipt.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"⚠️  Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Load the image (recognize text from photo / read text from scan)
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 5️⃣ Perform OCR – this is the core of how to perform OCR
        string extractedText = ocrEngine.Recognize();

        // 6️⃣ Show the result – you can now extract text from receipt, invoice, etc.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

Jalankan program dengan `dotnet run`. Jika semuanya sudah diatur dengan benar, Anda akan melihat teks yang diekstrak tercetak di konsol.

## Pertanyaan Umum & Kasus Tepi

**T: Bagaimana jika gambar berupa PDF?**  
J: Konversi setiap halaman PDF menjadi gambar terlebih dahulu (misalnya, menggunakan `Aspose.Pdf` atau `PdfSharp`) lalu berikan bitmap yang dihasilkan ke `ocrEngine.Image`.

**T: Bisakah saya memproses gambar secara paralel?**  
J: Ya, tetapi buatlah `OcrEngine` terpisah per thread. Mesin tidak thread‑safe, sehingga berbagi satu instance dapat menyebabkan kondisi balapan.

**T: Apakah ini bekerja di Linux?**  
J: Tentu saja. Aspose.OCR bersifat lintas‑platform; pastikan dependensi native terpasang (`libgdiplus` untuk .NET Core di Linux).

**T: Bagaimana cara menangani kwitansi multibahasa?**  
J: Muat beberapa model bahasa sebelum mengenali:  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
Mesin akan mencoba setiap model secara berurutan.

## Kesimpulan

Anda kini memiliki jawaban lengkap, end‑to‑end untuk **bagaimana cara melakukan OCR** di C# dengan Aspose.OCR. Tutorial ini mencakup semua mulai dari inisialisasi mesin, **mengenali teks dari foto**, **membaca teks dari pemindaian**, hingga **mengekstrak teks dari kwitansi**, serta memberi Anda cara praktis untuk **meningkatkan akurasi OCR**.  

Langkah selanjutnya? Coba ganti model bahasa Inggris dengan model tulisan tangan, bereksperimen dengan nilai `BinarizeMethod` yang berbeda, atau integrasikan pemanggilan OCR ke dalam API ASP.NET yang memproses unggahan secara langsung. Kemungkinannya seluas gambar yang Anda beri.  

Masih ada pertanyaan tentang OCR, pra‑pemrosesan gambar, atau pustaka Aspose? Tinggalkan komentar atau jelajahi dokumentasi resmi Aspose.OCR untuk penjelajahan lebih dalam. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}