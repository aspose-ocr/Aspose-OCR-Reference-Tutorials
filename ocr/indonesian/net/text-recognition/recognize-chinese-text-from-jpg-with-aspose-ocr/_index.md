---
category: general
date: 2026-04-08
description: Pelajari cara mengenali teks Cina dari gambar JPG menggunakan Aspose
  OCR. Panduan langkah demi langkah ini juga menunjukkan cara mengekstrak teks dari
  gambar dengan cepat.
draft: false
keywords:
- recognize chinese text
- extract text from image
- recognize text from jpg
- Aspose OCR C#
- offline OCR resources
language: id
og_description: Mengenali teks Cina dari gambar JPG menggunakan Aspose OCR. Ikuti
  panduan lengkap ini untuk mengekstrak teks dari gambar secara offline.
og_title: mengenali teks Cina dari JPG dengan Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Mengenali teks Cina dari JPG dengan Aspose OCR
url: /id/net/text-recognition/recognize-chinese-text-from-jpg-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks Cina dari JPG dengan Aspose OCR

Pernah perlu **mengenali teks Cina** dari file JPG tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami kebuntuan ini saat membangun aplikasi pemindaian multibahasa. Kabar baiknya, Aspose OCR membuatnya sangat mudah, bahkan ketika Anda harus bekerja secara offline.

Dalam tutorial ini kami akan menelusuri seluruh proses mengekstrak teks dari gambar, gaya **extract text from image**, dan menunjukkan secara tepat cara **recognize text from jpg** menggunakan C#. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan yang membaca gambar berbahasa Cina dan mencetak karakter yang dikenali ke konsol.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (versi terbaru apa pun dapat digunakan)
- Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- File sumber daya bahasa Cina (tutorial ini menunjukkan cara memuatnya secara offline)
- File gambar bernama `chinese_sample.jpg` yang ditempatkan di folder yang Anda kontrol

Tidak diperlukan trik IDE khusus—Visual Studio, Rider, atau bahkan VS Code sudah cukup.

## Langkah 1: Siapkan Proyek dan Instal Aspose OCR

Pertama, buat proyek konsol baru dan tambahkan pustaka Aspose OCR.

```bash
dotnet new console -n ChineseOcrDemo
cd ChineseOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda berada di belakang proxy perusahaan, tambahkan flag `--no-cache` untuk memaksa unduhan baru.

## Langkah 2: Nonaktifkan Unduhan Sumber Daya Otomatis

Aspose OCR dapat mengambil paket bahasa secara dinamis, tetapi untuk produksi biasanya Anda ingin menyertakan file‑file tersebut bersama aplikasi. Menonaktifkan unduhan otomatis mencegah panggilan jaringan yang tidak terduga.

```csharp
using Aspose.Ocr;

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Turn off the auto‑download feature
ocrEngine.Options.EnableAutomaticResourceDownload = false;
```

Mengapa kita melakukannya? Menyimpan sumber daya secara lokal menjamin kinerja yang konsisten dan memungkinkan Anda menjalankan aplikasi di mesin tanpa akses internet.

## Langkah 3: Muat Sumber Daya Bahasa Cina Secara Offline

Aspose menyediakan data bahasa sebagai file terpisah. Asumsikan Anda telah menempatkan paket bahasa Cina (`zh`) di folder `Resources` di samping executable Anda, muatlah dengan cara berikut:

```csharp
// Path to the folder that contains the language files
string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");

// Tell the engine where to look for resources
ocrEngine.Options.ResourcesFolder = resourcePath;

// Load the Simplified Chinese resources (offline = true)
ocrEngine.LoadLanguageResources("zh", offline: true);
```

> **Watch out:** Jika jalur salah, Anda akan mendapatkan `FileNotFoundException`. Periksa kembali nama folder dan sensitivitas huruf pada Linux.

## Langkah 4: Atur Bahasa Engine ke Cina

Setelah data dimuat, arahkan engine ke kode bahasa yang tepat.

```csharp
ocrEngine.Language = "zh"; // “zh” = Simplified Chinese
```

Menetapkan bahasa secara eksplisit meningkatkan akurasi karena OCR tidak perlu menebak skrip.

## Langkah 5: Kenali Teks dari Gambar JPG

Berikut inti tutorial—memberikan JPG ke engine dan mengambil teksnya.

```csharp
// Full path to the image you want to process
string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");

// Run the OCR operation
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

// Output the raw result
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

Jika semuanya berjalan lancar, konsol akan menampilkan karakter Cina yang terdapat dalam `chinese_sample.jpg`. Anda juga dapat mengakses `ocrResult.Confidence` untuk metrik kualitas.

## Langkah 6: Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semua bagian memberikan Anda program siap‑jalankan. Simpan ini sebagai `Program.cs` di dalam folder proyek Anda.

```csharp
using System;
using System.IO;
using Aspose.Ocr;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Disable automatic resource download
        // -------------------------------------------------
        ocrEngine.Options.EnableAutomaticResourceDownload = false;

        // -------------------------------------------------
        // 3️⃣ Load Chinese language resources (offline)
        // -------------------------------------------------
        string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");
        ocrEngine.Options.ResourcesFolder = resourcePath;
        ocrEngine.LoadLanguageResources("zh", offline: true);

        // -------------------------------------------------
        // 4️⃣ Set language to Simplified Chinese
        // -------------------------------------------------
        ocrEngine.Language = "zh";

        // -------------------------------------------------
        // 5️⃣ Recognize text from a JPG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // -------------------------------------------------
        // 6️⃣ Show the result
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine($"\nConfidence: {ocrResult.Confidence:P2}");
    }
}
```

### Output yang Diharapkan

```
=== Recognized Chinese Text ===
欢迎使用Aspose OCR示例
Confidence: 96.45%
```

Output Anda akan bervariasi tergantung pada gambar sumber, tetapi Anda seharusnya melihat blok karakter Cina diikuti oleh persentase kepercayaan.

## Langkah 7: Variasi Umum & Kasus Tepi

### Mengenali Teks dari PNG atau BMP

Metode `RecognizeImage` menerima format apa pun yang didukung oleh `System.Drawing` .NET. Cukup ubah ekstensi file:

```csharp
ocrEngine.RecognizeImage("sample.png");
```

### Menangani Banyak Bahasa

Jika Anda perlu **extract text from image** yang mencampur bahasa Inggris dan Cina, muat kedua paket bahasa dan setel `ocrEngine.Language = "zh,en";`. Engine akan otomatis beralih antar skrip.

### Mengatasi Gambar Resolusi Rendah

DPI rendah dapat mengurangi akurasi OCR. Sebelum memanggil `RecognizeImage`, Anda dapat memperbesar gambar:

```csharp
using System.Drawing;

Bitmap bmp = new Bitmap(imagePath);
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
highRes.Save("highres.jpg");
ocrResult = ocrEngine.RecognizeImage("highres.jpg");
```

Ingat, memperbesar tidak akan menambahkan detail secara ajaib, tetapi dapat memberi algoritma lebih banyak piksel untuk diproses.

## Langkah 8: Pengujian & Verifikasi

Pemeriksaan cepat adalah membandingkan output OCR dengan string kebenaran dasar yang sudah diketahui.

```csharp
string expected = "欢迎使用Aspose OCR示例";
bool matches = ocrResult.Text.Trim() == expected;
Console.WriteLine($"Match with expected? {matches}");
```

Jika `matches` bernilai `false`, pertimbangkan untuk menyesuaikan gambar (misalnya, meningkatkan kontras) atau mengaktifkan `ocrEngine.Options.UseAdvancedPreprocessing = true`.

## Kesimpulan

Anda baru saja mempelajari cara **recognize chinese text** dari file JPG menggunakan Aspose OCR, dan kini Anda tahu cara **extract text from image** dalam skenario sepenuhnya offline. Solusi lengkap—inisialisasi, pemuatan sumber daya, pemilihan bahasa, dan pemrosesan gambar—termasuk dalam satu aplikasi konsol yang mudah dijalankan.

Apa selanjutnya? Coba proses sekumpulan gambar dengan engine yang sama, bereksperimen dengan paket bahasa lain, atau integrasikan langkah OCR ke dalam ASP .NET Web API sehingga pengguna dapat mengunggah gambar dan menerima teks terjemahan secara langsung. Langit adalah batasnya ketika Anda menggabungkan OCR yang handal dengan alat .NET modern.

Selamat coding, dan jangan ragu meninggalkan komentar jika Anda mengalami kendala!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}