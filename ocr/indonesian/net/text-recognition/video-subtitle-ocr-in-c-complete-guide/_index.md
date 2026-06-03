---
category: general
date: 2026-06-03
description: Tutorial OCR subtitle video yang menunjukkan cara mengekstrak frame dari
  video dan membaca teks dari file video seperti MP4 menggunakan Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: id
og_description: Pelajari OCR subtitle video dengan Aspose.OCR. Ekstrak frame dari
  video, baca teks dari video, dan ekstrak teks dari MP4 dalam beberapa menit.
og_title: OCR Subtitle Video di C# – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: OCR Subtitle Video di C# – Panduan Lengkap
url: /id/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Subtitle Video dalam C# – Panduan Lengkap

Pernah membutuhkan **video subtitle ocr** tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Baik Anda sedang mendigitalkan rekaman kuliah, mengambil caption dari video pelatihan, atau hanya penasaran tentang membaca teks dari video, tutorial ini menunjukkan secara tepat cara melakukannya dengan C# dan Aspose.OCR.  

Dalam beberapa menit ke depan kita akan mengekstrak frame dari video, menjalankan OCR pada frame tersebut, dan akhirnya menampilkan teks subtitle frame‑per‑frame. Pada akhir tutorial Anda akan dapat **membaca teks dari video** file—termasuk MP4—tanpa mencari alat pihak ketiga.

## Apa yang Akan Anda Bangun

Kami akan membuat aplikasi konsol kecil yang:

1. Mendekode MP4 (atau format lain yang didukung) menjadi frame `Bitmap` individual.  
2. Membatasi wilayah OCR ke pita subtitle sehingga mesin tidak terganggu oleh seluruh gambar.  
3. Memproses setiap frame dengan `VideoOcrProcessor` milik Aspose.  
4. Mencetak teks subtitle yang dikenali ke konsol.

Tidak ada embel‑embel, hanya contoh end‑to‑end yang berfungsi yang dapat Anda masukkan ke dalam proyek nyata.

## Prasyarat

- **.NET 6.0** atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – instal melalui NuGet: `Install-Package Aspose.OCR`.  
- Sebuah file video (MP4 sangat cocok).  
- Sebuah cara untuk mendekode frame video – demo ini menggunakan metode placeholder, tetapi Anda dapat mengganti dengan FFmpeg, OpenCV, atau perpustakaan apa pun yang mengembalikan objek `Bitmap`.  

> Pro tip: Jika Anda menggunakan Windows, paket `System.Drawing.Common` berfungsi baik untuk `Bitmap`. Pada Linux/macOS Anda memerlukan dependensi native `libgdiplus`.

## Langkah 1 – Ekstrak Frame dari Video

The first hurdle is turning a moving picture into still images.  The method `GetVideoFrames` below is deliberately left blank; replace it with your favourite decoder.  Here’s a quick sketch using FFmpeg‑Core (just to illustrate the shape of the data):

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **Mengapa ini penting:** Mengekstrak frame memberikan mesin OCR gambar statis untuk diproses, yang secara dramatis meningkatkan akurasi dibandingkan mencoba membaca langsung dari aliran video.

## Langkah 2 – Siapkan VideoOcrProcessor

Now that we have a sequence of `Bitmap` objects, we can hand them to Aspose.OCR.  The `VideoOcrProcessor` lets us define a **Region of Interest (ROI)** – perfect for subtitles that usually sit at the top or bottom of the frame.

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **Mengapa membatasi ROI?** Dengan mengabaikan bagian gambar lainnya kita mengurangi noise, mempercepat waktu pemrosesan, dan menghindari hasil positif palsu dari grafik latar belakang.

## Langkah 3 – Jalankan OCR pada Urutan Frame

With the processor ready, feeding the frames is a one‑liner.  The `Process` method returns an enumerable of `OcrResult` objects, each containing the recognized text for its corresponding frame.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **Apa yang terjadi di balik layar?** Aspose.OCR secara internal menormalkan setiap bitmap, menjalankan pengenalan berbasis jaringan saraf, dan kemudian memproses hasilnya untuk memperbaiki tanda baca dan pemisahan baris.

## Langkah 4 – Tampilkan Teks yang Diekstrak

Finally, we iterate over the results and print each subtitle line.  You could also write them to a SRT file, a database, or feed them into a translation service.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### Contoh Lengkap yang Berfungsi

Putting everything together yields a self‑contained console program:

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**Output yang diharapkan (contoh)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

Jika OCR kesulitan dengan frame tertentu, Anda akan melihat string kosong – itu menjadi petunjuk untuk menyesuaikan ROI atau meningkatkan laju ekstraksi frame.

## Kesalahan Umum & Cara Memperbaikinya

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Karakter sampah** | Frame beresolusi rendah atau kompresi berat | Ekstrak frame dengan bitrate lebih tinggi, atau tingkatkan ukuran bitmap sebelum OCR (`Bitmap.Clone(new Size(...), ...)`). |
| **Tidak ada teks yang dikembalikan** | ROI tidak benar‑benar mencakup pita subtitle | Verifikasi koordinat persegi panjang (gunakan alat screenshot untuk mengukurnya). |
| **Bottleneck kinerja** | Memproses setiap frame pada 30 fps terlalu berlebihan | Turunkan sampel menjadi 1‑2 fps untuk kebanyakan aliran subtitle; Anda masih dapat menangkap setiap perubahan subtitle. |
| **FFmpeg tidak ditemukan** | `ffmpeg.exe` tidak ada di `PATH` | Berikan path lengkap di `ProcessStartInfo.FileName` atau instal FFmpeg secara global. |

## Memperluas Solusi

- **Export to SRT** – gabungkan timestamp dengan teks OCR dan tulis file SubRip.  
- **Multi‑language support** – set `ocrProcessor.Language = OcrLanguage.Spanish` (atau bahasa lain yang didukung).  
- **Real‑time processing** – alirkan frame langsung dari streaming live alih‑alih membaca dari disk.  

Semua variasi ini masih berpusat pada ide inti **mengekstrak frame dari video**, **membaca teks dari video**, dan **mengekstrak teks dari mp4**.

## Kesimpulan

Kami baru saja melewati alur kerja **video subtitle ocr** lengkap dalam C#. Dengan mengekstrak frame dari video, memfokuskan OCR pada pita subtitle, dan mengiterasi hasilnya, Anda dapat secara andal **membaca teks dari video** file seperti MP4. Kode siap untuk disalin‑tempel, dan desain modular memungkinkan Anda mengganti decoder frame apa pun yang Anda sukai.

Langkah selanjutnya? Cobalah mengekspor hasil ke file SRT, bereksperimen dengan ukuran ROI yang berbeda, atau mengirim subtitle ke API terjemahan untuk caption multibahasa. Langit adalah batasnya setelah Anda menguasai dasar‑dasar mengekstrak teks dari video.

Selamat coding, dan semoga subtitle Anda selalu jernih!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar Menggunakan Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}