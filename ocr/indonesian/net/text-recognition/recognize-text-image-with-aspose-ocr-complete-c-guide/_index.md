---
category: general
date: 2026-06-22
description: Pelajari cara mengenali gambar teks dan mengekstrak gambar teks dari
  faktur OCR resolusi tinggi menggunakan Aspose OCR. Termasuk pengaturan bahasa OCR
  dan akselerasi GPU.
draft: false
keywords:
- recognize text image
- extract text image
- high resolution ocr
- process invoice ocr
- set ocr language
language: id
og_description: Mengenali gambar teks menggunakan Aspose OCR di C#. Tutorial ini menunjukkan
  cara mengekstrak gambar teks dari faktur beresolusi tinggi, mengatur bahasa OCR,
  dan meningkatkan kinerja.
og_title: Mengenali gambar teks dengan Aspose OCR – Panduan Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to recognize text image and extract text image from high
    resolution OCR invoices using Aspose OCR. Includes set OCR language and GPU acceleration.
  headline: recognize text image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Learn how to recognize text image and extract text image from high
    resolution OCR invoices using Aspose OCR. Includes set OCR language and GPU acceleration.
  name: recognize text image with Aspose OCR – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code also works on .NET Framework 4.7+). -
      A valid Aspose.OCR NuGet package (free trial works fine). - A high‑resolution
      image of an invoice (e.g., `high_res_invoice.png`). - Basic familiarity with
      C# and Visual Studio or your favorite IDE.'
  - name: 1. Image Quality Matters
    text: Even the fastest GPU can’t fix a blurry scan. Aim for at least **300 dpi**
      for invoices; lower resolutions cause missed characters. If you can’t control
      the source, consider pre‑processing with a sharpening filter before sending
      the image to Aspose.
  - name: 2. Memory Consumption on Very Large Files
    text: A 5000 × 7000 pixel PNG can consume several hundred megabytes of RAM. If
      you hit `OutOfMemoryException`, split the invoice into pages or downscale slightly
      (e.g., to 250 dpi) before OCR.
  - name: 3. Fallback to CPU When GPU Fails
    text: If the GPU driver crashes, Aspose will silently revert to CPU. To ensure
      you’re always using the GPU, check `ocrEngine.ProcessingMode` after initialization
      and log a warning if it isn’t `ProcessingMode.Gpu`.
  - name: 4. Multi‑Language Documents
    text: 'When an invoice contains both English and Spanish, you can enable **multiple
      languages**:'
  type: HowTo
tags:
- Aspose OCR
- C#
- Image Processing
title: Mengenali gambar teks dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/text-recognition/recognize-text-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali gambar teks dengan Aspose OCR – Panduan Lengkap C#

Pernahkah Anda perlu **recognize text image** tetapi hasilnya terlihat buram atau sangat lambat? Anda bukan satu‑satunya. Baik Anda memindai faktur beresolusi tinggi atau mengambil data dari kontrak yang dipindai, mendapatkan output yang bersih dan dapat diandalkan sangat penting. Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang **recognize text image** dari file beresolusi tinggi, **extract text image**, dan bahkan **set OCR language** untuk akurasi terbaik—semua sambil memanfaatkan percepatan GPU.

Kami juga akan menambahkan beberapa trik tambahan: cara **process invoice OCR** secara efisien, mengapa Anda mungkin ingin **high resolution OCR**, dan apa yang harus dilakukan ketika GPU tidak tersedia. Pada akhir tutorial Anda akan memiliki satu program C# yang mengubah PNG buram menjadi teks yang dapat dicari dalam sekejap.

## Apa yang Akan Anda Pelajari

- Cara membuat instance `OcrEngine` dengan Aspose OCR.  
- Mengaktifkan **GPU acceleration** untuk **high resolution OCR** yang super cepat.  
- Menggunakan **set OCR language** untuk menargetkan bahasa Inggris (atau bahasa lain yang didukung).  
- **Extract text image** dari file faktur beresolusi tinggi.  
- Mengukur waktu pemrosesan sehingga Anda dapat membuktikan peningkatan performa.  
- Menangani skenario fallback ketika GPU tidak tersedia.

### Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode ini juga bekerja pada .NET Framework 4.7+).  
- Paket NuGet Aspose.OCR yang valid (versi trial gratis sudah cukup).  
- Gambar beresolusi tinggi dari sebuah faktur (misalnya `high_res_invoice.png`).  
- Familiaritas dasar dengan C# serta Visual Studio atau IDE favorit Anda.

---

## Langkah 1: Instal Aspose.OCR dan Siapkan Proyek

Hal pertama yang harus dilakukan—tambahkan pustaka Aspose OCR ke proyek Anda. Buka terminal di folder solusi Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jaga paket tetap terbaru; versi yang lebih baru meningkatkan dukungan GPU dan model bahasa.

Buat aplikasi console baru jika belum ada:

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
```

Sekarang Anda memiliki kanvas bersih untuk **recognize text image**.

## Langkah 2: Inisialisasi OCR Engine (Aktifkan GPU)

Inti dari proses ini adalah `OcrEngine`. Secara default ia berjalan di CPU, tetapi untuk **high resolution OCR** pada pemindaian faktur besar GPU dapat memangkas beberapa detik dari waktu eksekusi.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // Enable GPU processing – dramatically speeds up high‑resolution OCR
    ProcessingMode = ProcessingMode.Gpu
};
```

> **Mengapa GPU?** Gambar beresolusi tinggi dapat berisi jutaan piksel. GPU memprosesnya secara paralel, mengubah pekerjaan CPU 5 detik menjadi operasi sub‑detik pada kebanyakan kartu grafis modern.

Jika mesin target tidak memiliki GPU yang kompatibel, Aspose secara otomatis akan beralih ke mode CPU. Anda dapat mendeteksi fallback tersebut seperti ini:

```csharp
if (ocrEngine.ProcessingMode != ProcessingMode.Gpu)
{
    Console.WriteLine("GPU not available – using CPU fallback.");
}
```

## Langkah 3: **set OCR language** – Pilih Kamus yang Tepat

Aspose OCR dilengkapi dengan bahasa inti; bahasa Inggris adalah default, tetapi Anda dapat menetapkannya secara eksplisit. Ini penting karena model bahasa memengaruhi segmentasi karakter dan pencarian kamus.

```csharp
// Step 3: Explicitly set the language to English (core language)
ocrEngine.Language = OcrLanguage.English;
```

> **Kasus khusus:** Jika Anda perlu membaca faktur berbahasa Prancis, cukup ganti `OcrLanguage.English` dengan `OcrLanguage.French`. Pemanggilan **set OCR language** yang sama bekerja untuk bahasa apa pun yang didukung.

## Langkah 4: **recognize text image** – Masukkan Faktur Beresolusi Tinggi

Sekarang kita benar‑benar **recognize text image**. Arahkan engine ke PNG (atau TIFF) beresolusi tinggi yang ingin Anda proses. Path dapat bersifat absolut atau relatif; pastikan file tersebut ada.

```csharp
// Step 4: Recognize the image and capture the result
string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);
```

Objek `OcrResult` berisi teks yang diekstrak serta informasi waktu, yang akan kami tampilkan selanjutnya.

## Langkah 5: **extract text image** – Tampilkan Hasil dan Waktu Pemrosesan

Akhirnya, keluarkan teks OCR dan berapa lama prosesnya. Inilah saatnya Anda dapat memverifikasi bahwa **process invoice OCR** berjalan sesuai harapan.

```csharp
// Step 5: Output processing time and extracted text
Console.WriteLine($"GPU OCR time: {ocrResult.ProcessingTimeMs} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

Menjalankan program seharusnya menghasilkan sesuatu seperti:

```
GPU OCR time: 312 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑04‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

Itu saja—alur kerja **extract text image** Anda selesai.

---

## Bonus: Menangani Kendala Umum

### 1. Kualitas Gambar Penting

Bahkan GPU tercepat tidak dapat memperbaiki pemindaian yang buram. Usahakan setidaknya **300 dpi** untuk faktur; resolusi lebih rendah menyebabkan karakter terlewat. Jika Anda tidak dapat mengontrol sumber, pertimbangkan pra‑pemrosesan dengan filter penajaman sebelum mengirim gambar ke Aspose.

### 2. Konsumsi Memori pada File Sangat Besar

PNG berukuran 5000 × 7000 piksel dapat memakan ratusan megabyte RAM. Jika Anda menemui `OutOfMemoryException`, bagi faktur menjadi beberapa halaman atau turunkan skala sedikit (misalnya ke 250 dpi) sebelum OCR.

### 3. Fallback ke CPU Saat GPU Gagal

Jika driver GPU crash, Aspose akan diam‑diam beralih ke CPU. Untuk memastikan Anda selalu menggunakan GPU, periksa `ocrEngine.ProcessingMode` setelah inisialisasi dan catat peringatan jika bukan `ProcessingMode.Gpu`.

### 4. Dokumen Multi‑Bahasa

Ketika faktur berisi bahasa Inggris dan Spanyol, Anda dapat mengaktifkan **multiple languages**:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Engine akan mencoba mengenali karakter dari kedua set bahasa tersebut.

---

## Contoh Lengkap yang Dapat Dijalankan

Berikut adalah program **lengkap, dapat dijalankan** yang menggabungkan semua langkah yang dibahas. Salin‑tempel ke `Program.cs`, ganti path gambar, dan tekan **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 2: Create an OCR engine instance and enable GPU acceleration
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu // Fast high‑resolution OCR
        };

        // Verify GPU availability (optional but helpful)
        if (ocrEngine.ProcessingMode != ProcessingMode.Gpu)
        {
            Console.WriteLine("GPU not detected – falling back to CPU processing.");
        }

        // Step 3: Set the OCR language (set OCR language for better accuracy)
        ocrEngine.Language = OcrLanguage.English; // Change as needed

        // Step 4: Recognize text from a high‑resolution invoice image
        string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // Step 5: Display processing time and the extracted text
        Console.WriteLine($"GPU OCR time: {ocrResult.ProcessingTimeMs} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");
    }
}
```

**Output yang diharapkan** (waktu akan bervariasi tergantung perangkat keras):

```
GPU OCR time: 287 ms
=== Extracted Text Start ===
Invoice #98765
Date: 2024‑03‑22
Amount Due: $2,340.00
...
=== Extracted Text End ===
```

Jalankan terhadap beberapa faktur berbeda untuk melihat bagaimana waktu pemrosesan tetap di bawah setengah detik pada GPU yang cukup sederhana.

---

## Kesimpulan

Anda baru saja mempelajari cara **recognize text image** menggunakan Aspose OCR, **extract text image** dari faktur beresolusi tinggi, dan **set OCR language** untuk hasil optimal—semua sambil memanfaatkan percepatan GPU untuk **high resolution OCR**. Kode yang ditampilkan siap produksi, mencakup logika fallback, dan dapat diperluas untuk menangani PDF multi‑halaman, bahasa berbeda, atau bahkan aliran kamera waktu nyata.

Langkah selanjutnya? Coba:

- Mengonversi teks yang diekstrak menjadi objek JSON faktur terstruktur.  
- Menambahkan pra‑pemrosesan gambar (deskew, binarisasi) untuk meningkatkan akurasi pada pemindaian berkualitas rendah.  
- Mengintegrasikan panggilan OCR ke dalam API ASP.NET Core sehingga layanan web Anda dapat memproses faktur sesuai permintaan.

Punya pertanyaan tentang **process invoice OCR** atau butuh bantuan menyesuaikan paket bahasa? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}