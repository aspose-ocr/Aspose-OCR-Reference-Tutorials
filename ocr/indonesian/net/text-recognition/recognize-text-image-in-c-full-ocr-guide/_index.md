---
category: general
date: 2026-06-06
description: mengenali gambar teks menggunakan C# OCR – contoh OCR C# langkah demi
  langkah yang mengekstrak teks dari pemindaian dan mengubah pemindaian menjadi teks
  dalam hitungan menit.
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: id
og_description: Mengenali gambar teks dengan C# OCR. Pelajari contoh praktis OCR C#
  yang mengekstrak teks dari pemindaian, mengubah pemindaian menjadi teks, dan menangani
  gambar dunia nyata.
og_title: Mengenali gambar teks di C# – Tutorial OCR Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Mengenali gambar teks di C# – Panduan OCR Lengkap
url: /id/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali gambar teks dalam C# – Tutorial OCR Lengkap

Pernah bertanya-tanya bagaimana cara **recognize text image** langsung dari foto yang dipindai menggunakan C#? Anda tidak sendirian. Baik Anda mendigitalkan kwitansi lama, mengambil data dari kartu nama, atau sekadar mengubah pemindaian resolusi rendah menjadi teks yang dapat diedit, kemampuan mengekstrak teks dari gambar adalah trik berguna yang harus dimiliki setiap pengembang dalam kotak peralatannya.

Dalam panduan ini kami akan menelusuri **c# ocr example** yang memuat gambar, menjalankan optical character recognition, dan mencetak hasilnya ke konsol. Pada akhir Anda akan dapat **extract text scan** file, **convert scan to text**, dan bahkan menyesuaikan proses untuk gambar berisik. Tidak diperlukan layanan pihak ketiga yang mewah—hanya Windows.Media.Ocr API bawaan (atau OcrEngine yang kompatibel) dan beberapa baris kode.

## Apa yang Akan Anda Pelajari

* Cara menyiapkan proyek C# untuk OCR.
* Kode tepat yang diperlukan untuk file **recognize text image**.
* Tips menangani pemindaian resolusi rendah dan dokumen multi‑halaman.
* Cara memperluas contoh menjadi pustaka yang dapat digunakan kembali untuk aplikasi Anda.

### Prasyarat

* .NET 6.0 atau lebih baru (API juga berfungsi pada .NET 5+).
* Visual Studio 2022 (edisi Community sudah cukup) atau IDE apa pun yang Anda suka.
* Gambar contoh seperti `lowres_scan.jpg` yang ditempatkan di folder yang dapat Anda referensikan.
* Familiaritas dasar dengan async/await—panggilan OCR bersifat asynchronous di Windows API.

> **Pro tip:** Jika Anda berada di platform non‑Windows, ganti namespace `Windows.Media.Ocr` dengan pustaka lintas‑platform seperti TesseractSharp; logika di sekitarnya tetap sama.

---

## Langkah 1: Siapkan untuk **recognize text image** dengan OCR Engine

Pertama, kita memerlukan instance OCR engine. Kelas `OcrEngine` adalah titik masuk untuk operasi **image to text c#** apa pun.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**Mengapa ini penting:** Engine mengabstraksi kerja berat pengenalan pola. Dengan secara eksplisit membuatnya, kita mendapatkan kontrol atas pengaturan bahasa, yang penting ketika Anda kemudian ingin **extract text scan** dokumen dalam bahasa lain.

## Langkah 2: Muat File Gambar – Inti dari **convert scan to text**

Selanjutnya, kami membaca gambar dari disk dan mengubahnya menjadi `SoftwareBitmap`, format yang diharapkan OCR engine.

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**Mengapa kami melakukannya:** Memasukkan aliran file mentah langsung ke OCR sering menghasilkan hasil yang buruk, terutama pada pemindaian resolusi rendah. Mengonversi ke `SoftwareBitmap` memungkinkan kami memanipulasi DPI, kedalaman warna, dan bahkan menerapkan filter sebelum pengenalan.

## Langkah 3: Lakukan Operasi **recognize text image**

Sekarang kami akhirnya memanggil metode `RecognizeAsync` engine. Di sinilah keajaiban terjadi.

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**Apa yang akan Anda lihat:** Jika `lowres_scan.jpg` berisi frasa “Hello World”, konsol akan mencetak:

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

Itulah seluruh **c# ocr example** dalam aksi—hanya empat langkah logis, namun mencakup semua mulai dari pemuatan file hingga output akhir.

## Langkah 4: Menangani Kasus Pinggir – Saat Pemindaian Tidak Sempurna

Gambar dunia nyata tidak selalu tajam. Berikut beberapa penyesuaian yang dapat Anda lakukan tanpa menulis ulang seluruh program:

| Masalah | Solusi Cepat |
|-------|-----------|
| **Very low DPI (≤ 72)** | Tingkatkan ukuran bitmap menggunakan `BitmapTransform` sebelum pengenalan. |
| **Skewed text** | Terapkan transformasi rotasi (`SoftwareBitmap.Rotate`) untuk meluruskan halaman. |
| **Multiple languages** | Buat `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` dan atur `engine.Language` sesuai. |
| **Large files** | Proses gambar dalam ubin (`engine.RecognizeAsync(tileBitmap)`) dan gabungkan hasilnya. |

Penyesuaian ini memastikan rutinitas **extract text scan** Anda tetap andal bahkan ketika berhadapan dengan kwitansi berisik atau foto yang diambil dengan sudut miring.

## Langkah 5: Mengubah Contoh menjadi Helper yang Dapat Digunakan Kembali (Opsional)

Jika Anda berencana **convert scan to text** di beberapa bagian aplikasi, bungkus logika dalam kelas utilitas kecil:

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

Sekarang Anda cukup memanggil:

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**Mengapa Anda akan menyukainya:** Helper memisahkan plumbing OCR, memungkinkan Anda fokus pada logika bisnis—sempurna untuk **c# ocr example** yang akan digunakan kembali di berbagai proyek.

---

![recognize text image example](https://example.com/ocr-demo.png "Screenshot of OCR console output showing recognize text image result")

*Alt text:* **recognize text image** output dari aplikasi konsol OCR C#.

---

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja pada .NET Core di Linux?**  
A: Namespace `Windows.Media.Ocr` hanya untuk Windows. Di Linux atau macOS Anda dapat menggantinya dengan TesseractSharp atau IronOcr—keduanya menyediakan metode `Engine.Recognize` yang serupa, sehingga kode di sekitarnya tetap hampir tidak berubah.

**Q: Seberapa akurat OCR bawaan untuk catatan tulisan tangan?**  
A: Pengenalan tulisan tangan masih bersifat eksperimental. Untuk hasil terbaik, gunakan font cetak atau pertimbangkan layanan cloud seperti Azure Cognitive Services jika Anda memerlukan akurasi tinggi.

**Q: Bisakah saya memproses PDF secara langsung?**  
A: Tidak secara langsung. Konversi setiap halaman PDF menjadi gambar terlebih dahulu (menggunakan `PdfSharp` atau `Ghostscript`) lalu berikan bitmap ke OCR engine.

## Kesimpulan

Anda kini memiliki **c# ocr example** lengkap yang siap produksi yang dapat **recognize text image** file, **extract text scan** konten, dan **convert scan to text** hanya dalam beberapa baris kode. Dengan memahami alur—pembuatan engine, pemuatan gambar, pengenalan asynchronous, dan penanganan hasil—Anda dapat menyesuaikan pola ini untuk proyek C# apa pun yang perlu mengubah gambar menjadi string yang dapat dicari.

Siap untuk langkah selanjutnya? Cobalah menambahkan UI sederhana dengan WinForms atau WPF, bereksperimen dengan bahasa berbeda, atau hubungkan output ke basis data untuk arsip yang dapat dicari. Langit adalah batasnya ketika Anda menguasai teknik **image to text c#**.

Selamat coding, dan semoga pemindaian Anda selalu tajam!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Konversi Gambar ke Teks – Lakukan OCR pada Gambar dari URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Cara Mengekstrak Teks dari Gambar dengan Menyiapkan Persegi Panjang di OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}