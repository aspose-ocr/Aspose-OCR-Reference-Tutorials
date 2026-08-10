---
category: general
date: 2026-04-08
description: Buat PDF yang dapat dicari dengan cepat dan pelajari cara mengompres
  gambar PDF, menyematkan font PDF, serta mengenali teks pada gambar dalam C# menggunakan
  Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: id
og_description: Buat PDF yang dapat dicari dengan cepat menggunakan Aspose.OCR. Pelajari
  cara mengompres gambar PDF, menyematkan font PDF, dan mengenali teks pada gambar
  dalam satu tutorial.
og_title: Buat PDF yang Dapat Dicari – Panduan Lengkap C#
tags:
- Aspose.OCR
- C#
- PDF Generation
title: Buat PDF yang Dapat Dicari – Panduan Lengkap C# untuk Mengubah Gambar ke PDF
url: /id/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari – Panduan Lengkap C#

Perlu **membuat searchable pdf** dari gambar yang dipindai? Anda bukan satu‑satunya yang menatap PNG raksasa dan bertanya‑tanya bagaimana mengubahnya menjadi dokumen ringan yang dapat dicari teksnya. Kabar baiknya, dengan Aspose.OCR Anda dapat melakukannya dalam beberapa baris kode, dan Anda juga akan belajar cara **compress PDF images**, **embed fonts PDF**, dan **recognize text image** tanpa kesulitan.

Dalam tutorial ini kami akan membahas seluruh proses: mulai dari memuat gambar, menjalankan OCR, menyesuaikan opsi penyimpanan PDF, hingga akhirnya menulis PDF yang dapat dicari ke disk. Pada akhir tutorial Anda akan memiliki metode siap pakai yang dapat Anda sisipkan ke proyek .NET apa pun, plus beberapa tip profesional untuk kasus tepi yang mungkin Anda temui nanti.

## Apa yang Anda Butuhkan

- **.NET 6+** (kode ini juga berfungsi di .NET Framework 4.7, namun kami akan menargetkan .NET 6 untuk sintaks modern).  
- **Aspose.OCR for .NET** – instal via NuGet: `Install-Package Aspose.OCR`.  
- Sebuah file gambar (PNG, JPEG, TIFF) yang berisi teks yang ingin Anda jadikan dapat dicari.  
- Sedikit rasa ingin tahu – sisanya dijelaskan di bawah.

> **Pro tip:** Jika Anda berencana memproses puluhan halaman, pertimbangkan untuk menggunakan kembali satu instance `OcrEngine` agar tidak terus‑menerus memuat data bahasa.

## Langkah 1: Siapkan Mesin OCR – Recognize Text Image

Hal pertama yang kita butuhkan adalah mesin OCR yang dapat membaca karakter dari bitmap sumber. Aspose.OCR memungkinkan Anda menentukan bahasa (English, French, dll.) dan mengembalikan objek `OcrResult` yang berisi teks mentah serta data gambar.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**Mengapa ini penting:**  
- Menetapkan bahasa meningkatkan akurasi secara dramatis; mesin memuat kamus khusus bahasa di belakang layar.  
- `OcrResult` tidak hanya menyimpan string yang diekstrak tetapi juga bitmap yang mendasarinya, yang nanti akan kami sematkan ke dalam PDF sehingga dokumen tetap visualnya identik dengan hasil scan asli.

## Langkah 2: Konfigurasikan Opsi Penyimpanan PDF – Compress PDF Images & Embed Fonts

PDF yang dapat dicari pada dasarnya adalah PDF biasa dengan lapisan teks tak terlihat di atas gambar yang dipindai. Jika Anda mengabaikan kompresi, file akhir bisa sangat besar. Kelas `PdfSaveOptions` memberi Anda kontrol detail atas kualitas gambar, penyematan font, dan apakah font harus disubset.

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**Mengapa Anda harus embed fonts PDF:**  
Ketika PDF dibuka di sistem yang tidak memiliki font tepat yang digunakan pada lapisan OCR, teks dapat muncul berantakan. Menyematkan font menjamin kesetiaan visual di semua platform, yang sangat penting untuk dokumen hukum atau arsip.

## Langkah 3: Simpan Hasil sebagai PDF yang Dapat Dicari – Image to Searchable PDF

Sekarang kita menggabungkan semuanya: ambil `OcrResult`, terapkan `PdfSaveOptions` kita, dan tulis file tersebut. Metode `SaveAsSearchablePdf` melakukan pekerjaan berat—membuat overlay teks tersembunyi yang mencerminkan output OCR sambil mempertahankan gambar asli.

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### Contoh Lengkap yang Berfungsi

Di bawah ini adalah program konsol mandiri yang dapat Anda salin‑tempel ke proyek konsol .NET baru. Program ini mengasumsikan gambar berada di folder bernama `YOUR_DIRECTORY` relatif terhadap executable.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

Menjalankan program akan menghasilkan `output.pdf` yang dapat Anda buka di Adobe Reader, Foxit, atau penampil PDF apa pun dan langsung mencari kata‑kata yang sebelumnya hanya ada di gambar.

## Langkah 4: Verifikasi Output – Apakah Pencarian Berfungsi?

Setelah file dihasilkan, buka dan coba pencarian bawaan (Ctrl + F). Jika Anda dapat menemukan kata seperti “invoice”, “date”, atau “total”, maka Anda berhasil membuat **searchable PDF**.  

Jika pencarian tidak menemukan apa‑apa:

1. **Check OCR accuracy** – mungkin gambar sumber beresolusi rendah. Pertimbangkan meningkatkan DPI sebelum OCR (Aspose memungkinkan Anda mengatur `Resolution` pada engine).  
2. **Confirm font embedding** – buka properti PDF dan lihat bagian *Fonts*; Anda harus melihat font yang disematkan terdaftar.  
3. **Inspect image compression** – `ImageQuality` yang sangat rendah dapat membuat lapisan visual tidak dapat dibaca, yang kadang membingungkan alat‑alat downstream.

## Variasi Umum & Kasus Tepi

| Skenario | Apa yang Harus Disesuaikan | Mengapa |
|----------|----------------------------|---------|
| **Multi‑page TIFF** | Loop over each frame, call `RecognizeImage` per page, then use `PdfSaveOptions` with `AppendMode = true`. | Menjaga setiap halaman scan menjadi halaman yang dapat dicari secara terpisah. |
| **Non‑English language** | Change `Language = "fr"` (or appropriate ISO code) and optionally supply a custom dictionary. | Meningkatkan pengenalan untuk karakter beraksen dan glyph khusus bahasa. |
| **Very large images** | Downscale the bitmap before OCR (`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`). | Mengurangi penggunaan memori dan mempercepat OCR tanpa mengorbankan terlalu banyak akurasi. |
| **Need OCR confidence** | Access `ocrResult.RecognizedWords` and inspect `Confidence` property. | Memungkinkan Anda menandai kata dengan kepercayaan rendah untuk peninjauan manual. |

## Tips Kinerja

- **Reuse the `OcrEngine`** ketika memproses batch file – ia menyimpan cache data bahasa.  
- **Parallelize** langkah pengenalan dengan `Parallel.ForEach` jika Anda berada di mesin multi‑core, tetapi tetap lakukan penulisan PDF secara berurutan untuk menghindari konflik akses file.  
- **Tune `ImageQuality`**: 85‑90 memberikan gambar hampir tanpa kehilangan, sementara 60‑70 biasanya cukup untuk dokumen yang padat teks.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **create searchable pdf** dari gambar menggunakan Aspose.OCR, sekaligus belajar cara **compress pdf images**, **embed fonts pdf**, dan secara efisien **recognize text image**. Contoh kode lengkap siap disisipkan ke proyek C# apa pun, dan tip tambahan akan membantu Anda menyesuaikan solusi untuk beban kerja yang lebih besar atau bahasa yang berbeda.

Siap untuk langkah berikutnya? Coba tambahkan watermark, gabungkan beberapa PDF yang dapat dicari, atau integrasikan rutinitas ini ke dalam web API sehingga pengguna dapat mengunggah scan dan langsung menerima PDF yang dapat dicari. Kemungkinannya tak terbatas, dan dengan dasar yang sudah ada Anda akan mudah memperluas alur kerja.

Selamat coding, semoga PDF Anda tetap kecil, dapat dicari, dan tampil sempurna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}