---
category: general
date: 2026-01-02
description: Pelajari cara mengenali teks bahasa Mandarin dan mengekstrak teks dari
  file PNG dengan pengenalan teks offline menggunakan Aspose.OCR. Tidak memerlukan
  internet – lakukan OCR pada gambar dalam beberapa langkah saja.
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: id
og_description: Mengenali teks Cina tanpa internet. Tutorial ini menunjukkan cara
  mengekstrak teks dari PNG menggunakan pengenalan teks offline dan melakukan OCR
  pada gambar di C#.
og_title: Mengenali teks Cina secara offline – Panduan C# Langkah demi Langkah
tags:
- OCR
- C#
- Aspose
title: Mengenali Teks Cina Secara Offline – Tutorial OCR C# Lengkap
url: /id/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks Cina offline – Tutorial Lengkap C# OCR

Pernahkah Anda perlu **mengenali teks Cina** dari PNG yang dipindai tetapi aplikasi Anda berjalan di mesin tanpa internet? Anda tidak sendirian. Dalam banyak skenario perusahaan—bayangkan server yang terisolasi atau perangkat lapangan—mengandalkan layanan cloud bukanlah pilihan.  

Dalam panduan ini kami akan menjelaskan solusi mandiri yang memungkinkan Anda **mengekstrak teks dari png** file, menjalankan **pengenalan teks offline**, dan **melakukan OCR pada aset gambar** menggunakan Aspose.OCR. Pada akhir panduan Anda akan memiliki program konsol C# siap‑jalankan yang mencetak karakter Cina langsung ke konsol.

## Prasyarat

- .NET 6 SDK (atau versi .NET terbaru lainnya) terpasang secara lokal.  
- Visual Studio 2022 atau VS Code – mana pun yang Anda sukai.  
- Sebuah salinan paket NuGet Aspose.OCR untuk .NET (`Aspose.OCR`).  
- File sumber daya bahasa untuk Bahasa Inggris dan Bahasa Cina Sederhana (tutorial menunjukkan cara mengunduhnya secara otomatis).  
- Sebuah gambar bernama `chinese_doc.png` ditempatkan di folder yang dapat Anda referensikan (`placeholder YOUR_DIRECTORY`).

Tidak ada layanan tambahan, tidak ada kunci API—hanya DLL lokal dan beberapa file sumber daya.

---

## Langkah 1 – Unduh sumber daya bahasa yang diperlukan (sekali)

Aspose.OCR menyimpan paket bahasa di disk. Pada pertama kali Anda menjalankan aplikasi, Anda perlu mengunduhnya. Pemanggilan `ResourceManager.DownloadResources` melakukan hal itu, dan karena kami memberikan bahasa Inggris Bahasa Cina Sederhana, mesin dapat beralih di antara keduanya nanti tanpa lalu lintas jaringan tambahan.

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **Tips Pro:** Simpan folder yang diunduh (`Aspose.OCR.Resources`) dalam kontrol sumber jika Anda memerlukan build yang dapat direproduksi di beberapa mesin.

## Langkah 2 – Inisialisasi mesin OCR dalam mode offline

Menetapkan `OfflineMode = true` memberi tahu perpustakaan untuk menghindari panggilan HTTP apa pun. Ini adalah kunci untuk **pengenalan teks offline** yang sesungguhnya.

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **Mengapa ini penting:** Beberapa perpustakaan OCR beralih ke layanan cloud ketika paket bahasa tidak tersedia. Dengan memaksa mode offline kami menjamin kinerja yang deterministik dan kepatuhan terhadap kebijakan privasi data.

## Langkah 3 – Muat PNG yang ingin Anda proses

Kami akan menggunakan `System.Drawing.Bitmap` untuk membaca gambar. Jika proyek Anda menargetkan .NET 6+ pada platform non‑Windows, pertimbangkan `SkiaSharp` sebagai alternatif, tetapi untuk kebanyakan penyebaran yang berfokus pada Windows, `Bitmap` berfungsi dengan baik.

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **Kasus khusus:** Jika PNG sangat besar (lebih dari 5 MP) Anda mungkin ingin memperkecilnya terlebih dahulu untuk mempercepat pengenalan dan mengurangi penggunaan memori:

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## Langkah 4 – Jalankan pengenalan dengan bahasa Cina Sederhana

Di sini kami memberi tahu mesin bahasa mana yang akan digunakan. Objek `RecognitionOptions` juga memungkinkan Anda menyesuaikan hal seperti `DetectOrientation` atau `PreserveFormatting`, tetapi nilai default sudah cukup baik untuk kebanyakan dokumen cetak.

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## Langkah 5 – Tampilkan (atau proses lebih lanjut) teks yang diekstrak)

Properti `OcrResult.Text` menyimpan representasi teks polos. Anda dapat menuliskannya ke konsol, file, atau memasukkannya ke dalam pipeline NLP selanjutnya.

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### Output yang Diharapkan

Jika `chinese_doc.png` berisi frasa “你好，世界！”, konsol akan menampilkan:

```
=== Recognized Chinese Text ===
你好，世界！
```

> **Catatan:** Akurasi OCR bergantung pada kualitas gambar, kejelasan font, dan kontras. Untuk hasil terbaik, gunakan pemindaian beresolusi tinggi (300 dpi atau lebih) dan pastikan teks tidak miring.

---

## Contoh Kerja Lengkap

Berikut adalah program lengkap yang siap disalin‑tempel. Simpan sebagai `Program.cs` dalam proyek konsol baru dan jalankan `dotnet run`. Semua langkah digabungkan, sehingga Anda dapat melihat alur dari pengunduhan sumber daya hingga output akhir.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Tips:** Bungkus pemanggilan `ResourceManager.DownloadResources` dalam blok `try/catch` jika Anda menginginkan penanganan yang halus ketika internet benar‑benar tidak tersedia. Metode tersebut akan melempar `NetworkException` jika tidak.

---

## Pertanyaan yang Sering Diajukan (FAQ)

| Question | Answer |
|----------|--------|
| **Apakah saya dapat mengenali Bahasa Cina Tradisional?** | Ya—ganti `Language.ChineseSimplified` dengan `Language.ChineseTraditional` dan unduh paket yang sesuai. |
| **Bagaimana jika saya perlu mengekstrak teks dari JPEG bukan PNG?** | Kode yang sama berfungsi; cukup ubah ekstensi file. `Bitmap` mendukung sebagian besar format raster umum. |
| **Apakah cara untuk mendapatkan kotak pembatas untuk setiap karakter?** | Setel `RecognitionOptions.DetectRegions = true`. `OcrResult` kemudian akan berisi objek `Region` dengan koordinat. |
| **Bagaimana cara menjalankannya di Linux?** | Gunakan paket `System.Drawing.Common` (versi 1.0+). Pada Linux tanpa tampilan (headless) Anda mungkin memerlukan dependensi native `libgdiplus`. |
| **Bisakah saya memproses batch folder gambar?** | Tentu—bungkus logika pengenalan dalam loop `foreach (var file in Directory.GetFiles(folder, "*.png"))`. |

---

## Langkah Selanjutnya & Topik Terkait

- **Tingkatkan akurasi**: coba `RecognitionOptions.PreprocessImage = true` agar mesin secara otomatis meningkatkan kontras.  
- **Gabungkan bahasa**: Anda dapat mengirimkan array bahasa ke `ResourceManager.DownloadResources` dan biarkan mesin mendeteksi secara otomatis.  
- **Integrasikan dengan UI**: masukkan kode konsol ke dalam aplikasi WinForms atau WPF dan tampilkan hasil OCR di textbox.  
- **Jelajahi pustaka Aspose lainnya**: `Aspose.PDF` untuk pembuatan PDF, `Aspose.Slides` untuk otomatisasi slide, dll.  

Jika Anda tertarik mengekstrak teks dari format gambar lain, pola yang sama dapat diterapkan—cukup ganti jalur file dan opsional sesuaikan opsi pra‑pemrosesan. Selamat coding!

---

![recognize chinese text example](/images/recognize-chinese-text.png "Screenshot showing recognize chinese text output in console")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}