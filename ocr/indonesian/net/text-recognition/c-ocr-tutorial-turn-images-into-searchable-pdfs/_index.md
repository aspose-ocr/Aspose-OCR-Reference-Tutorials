---
category: general
date: 2026-01-12
description: Tutorial OCR C# yang menunjukkan cara mengenali gambar teks, mengekstrak
  gambar teks dengan C#, dan menghasilkan file OCR gambar ke PDF dengan skor kepercayaan.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: id
og_description: Pelajari tutorial lengkap OCR C# untuk mengenali gambar teks, mengekstrak
  teks dari gambar menggunakan C#, dan membuat dokumen OCR gambar ke PDF dengan skor
  kepercayaan.
og_title: tutorial OCR C# – Mengonversi Gambar menjadi PDF yang Dapat Dicari
tags:
- OCR
- C#
- PDF
title: Tutorial OCR c# – Mengubah Gambar menjadi PDF yang Dapat Dicari
url: /id/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Ubah Gambar menjadi PDF yang Dapat Dicari

Pernah bertanya-tanya bagaimana cara **recognize text image** file dalam proyek C# tanpa mencari layanan pihak ketiga? Anda tidak sendirian. Dalam banyak aplikasi dunia nyata—seperti pemindai faktur, pelacak kwitansi, atau arsip dokumen multibahasa—pengembang membutuhkan mesin OCR yang andal, di‑lokasi, yang juga menghasilkan skor kepercayaan.  

Tutorial **c# ocr tutorial** ini akan memandu Anda melalui semua yang Anda butuhkan: mulai dari memuat gambar, memilih model bahasa, mengaktifkan akselerasi GPU, hingga menyimpan hasil sebagai PDF yang dapat dicari. Pada akhir tutorial Anda akan memiliki contoh kode siap‑jalankan yang mengekstrak teks, melaporkan kepercayaan OCR, dan secara opsional membuat file *image to pdf ocr* — semuanya dalam kurang dari satu menit penulisan kode.

## Apa yang Akan Anda Bangun

- Muat gambar multi‑bahasa (`sample_multi_lang.jpg` digunakan sebagai placeholder).  
- Pilih model bahasa Arab, Hindi, dan Rusia (Anda dapat menambahkan lebih banyak).  
- Aktifkan pemrosesan GPU jika mesin Anda mendukungnya.  
- Dapatkan hasil OCR mentah **with confidence scores**.  
- Serialisasi hasil ke JSON yang diformat rapi **or** tulis PDF yang dapat dicari.  

Tidak ada layanan web eksternal, tidak ada sihir tersembunyi—hanya Aspose.OCR untuk .NET, beberapa baris C#, dan penjelasan jelas tentang **mengapa** setiap baris penting.

## Prasyarat

- .NET 6.0 atau lebih baru (kode dapat dikompilasi pada .NET Core dan .NET Framework).  
- Visual Studio 2022 (atau IDE apa pun yang Anda suka).  
- Lisensi Aspose.OCR untuk .NET (versi percobaan gratis dapat digunakan untuk pengujian).  
- Opsional: GPU yang kompatibel dengan CUDA jika Anda ingin mempercepat pengenalan.

> **Pro tip:** Jika Anda tidak memiliki GPU, cukup set `UseGpu = false` dan mesin akan beralih ke CPU tanpa perubahan kode apa pun.

## Langkah 1: Instal Paket NuGet yang Diperlukan

Buka **Package Manager Console** dan jalankan:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Ketiga paket ini memberikan Anda mesin OCR, akselerasi GPU, dan serializer JSON yang bagus untuk output kepercayaan.

## Langkah 2: Siapkan Struktur Proyek

Buat proyek konsol baru (`dotnet new console -n AsposeOcrDemo`) dan ganti `Program.cs` yang dihasilkan dengan kode di bawah ini.  
Semua logika berada di dalam kelas `Program`; satu tipe tambahan hanyalah metode ekstensi kecil yang memformat hasil OCR menjadi JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Mengapa Kode Ini Berfungsi

1. **GPU toggle** – `GpuOcrEngine` memanfaatkan core CUDA; operator ternary membuat perpindahan tanpa kesulitan.  
2. **Automatic language download** – `AutoDownloadResources = true` memastikan model Arab, Hindi, dan Rusia diunduh saat pertama kali Anda menjalankan aplikasi.  
3. **Confidence scores** – `result.Words` berisi `Confidence` untuk setiap kata yang dikenali; metode ekstensi memformatnya menjadi objek JSON yang bersih.  
4. **Searchable PDF** – `result.Pdf` sudah merupakan PDF yang sepenuhnya dapat dicari, jadi kami cukup menulis array byte ke disk. Tidak diperlukan perpustakaan tambahan.

## Langkah 6: Jalankan Contoh

Buka terminal, arahkan ke folder proyek, dan jalankan:

```bash
dotnet run
```

Jika Anda memilih output **JSON**, Anda akan melihat sesuatu seperti:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Jika Anda beralih ke **PDF**, konsol akan mencetak path dan Anda akan menemukan PDF yang dapat dicari tepat di sebelah gambar sumber.

## Pertanyaan Umum & Kasus Tepi

- **Bagaimana jika model bahasa tidak tersedia?**  
  Mesin OCR akan melempar `ResourceNotFoundException` yang jelas. Karena kami mengatur `AutoDownloadResources = true`, model yang hilang akan diunduh secara otomatis pada pertama kali dijalankan, sehingga pengecualian ini jarang muncul di produksi.

- **Bisakah saya memproses batch gambar?**  
  Tentu saja. Bungkus pemanggilan `engine.Recognize` dalam loop `foreach` pada direktori file. `OcrResultExtensions` yang sama bekerja untuk setiap gambar.

- **Apakah saya memerlukan lisensi untuk GPU?**  
  Tidak. Versi percobaan gratis berfungsi untuk CPU maupun GPU. Lisensi penuh menghapus watermark percobaan dan menghilangkan batasan jumlah halaman.

- **Seberapa akurat skor kepercayaan?**  
  Skor berkisar antara 0.0 (tidak ada kepercayaan) hingga 1.0 (kepercayaan sempurna). Dalam praktiknya, apa pun di atas 0.90 dapat diandalkan untuk pemrosesan lanjutan; Anda dapat menyaring kata dengan kepercayaan lebih rendah jika memerlukan validasi yang lebih ketat.

## Langkah 7: Langkah Selanjutnya (Perluas Toolkit OCR Anda)

1. **Tambahkan lebih banyak bahasa** – cukup tambahkan `LanguageModel.French` (atau model lain yang didukung) ke array `Languages`.  
2. **Gabungkan OCR dengan konversi PDF/A** – Aspose.PDF dapat menyematkan lapisan OCR ke dalam dokumen yang mematuhi PDF/A‑2b untuk arsip.  
3. **Integrasikan dengan Azure Functions** – bungkus logika ke dalam endpoint serverless untuk memproses unggahan secara langsung.  
4. **Sesuaikan ambang kepercayaan** – gunakan `result.Words.Where(w => w.Confidence < 0.85)` untuk menandai kata yang tidak pasti untuk peninjauan manual.

### TL;DR

Tutorial **c# ocr tutorial** ini menunjukkan cara:

- Memuat gambar dan memilih beberapa model bahasa.  
- Mengaktifkan akselerasi GPU dengan satu flag boolean.  
- Mengambil hasil OCR **with confidence scores** dan menyerialisasikannya ke JSON.  
- Secara opsional menulis PDF yang dapat dicari (**image to pdf ocr**).  

Semua itu dapat dicapai dengan hanya beberapa baris kode, versi percobaan Aspose.OCR gratis, dan kode di atas. Cobalah, sesuaikan daftar bahasa, dan Anda akan memiliki pipeline OCR siap produksi dalam hitungan menit.

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}