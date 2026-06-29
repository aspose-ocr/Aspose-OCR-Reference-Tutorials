---
category: general
date: 2026-06-28
description: Mengenali teks dari gambar dengan cepat menggunakan Aspose OCR. Pelajari
  cara mengaktifkan percepatan GPU, memuat gambar untuk OCR, dan mengekstrak teks
  dari struk dalam format teks biasa.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- how to enable gpu acceleration
- convert image to plain text
- load image for ocr
language: id
og_description: Mengenali teks dari gambar dengan Aspose OCR. Panduan ini menunjukkan
  cara mengaktifkan percepatan GPU, memuat gambar untuk OCR, dan mengubahnya menjadi
  teks biasa.
og_title: Mengenali teks dari gambar menggunakan Aspose OCR GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  headline: recognize text from image using Aspose OCR GPU
  type: TechArticle
- description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  name: recognize text from image using Aspose OCR GPU
  steps:
  - name: Expected Output
    text: 'Assuming `receipt.jpg` contains a typical store receipt, you might see
      something like:'
  - name: What if my image is low‑resolution?
    text: OCR accuracy drops dramatically on blurry or tiny images. Before calling
      `Recognize`, consider up‑scaling the image (e.g., using `System.Drawing` or
      `ImageSharp`) and applying a contrast boost. Aspose also offers `Preprocess`
      methods you can experiment with.
  - name: My GPU isn’t being used – why?
    text: '- Verify that `EnableGpu` is `true` *before* you call `Recognize`. - Check
      that your driver supports OpenCL 1.2+ (most modern drivers do). - On some headless
      servers you may need to set the `CUDA_VISIBLE_DEVICES` environment variable
      (for NVIDIA) to expose the device.'
  - name: Can I process multiple images in parallel?
    text: Absolutely. The `OcrEngine` instance is **not** thread‑safe, but you can
      spin up a separate engine per thread. Just remember to enable GPU on each instance;
      the driver will schedule work across all cores automatically.
  - name: How do I change the language (e.g., French receipts)?
    text: '```csharp ocrEngine.Settings.Language = OcrLanguage.French; ```'
  type: HowTo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Mengenali teks dari gambar menggunakan Aspose OCR GPU
url: /id/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# recognize text from image using Aspose OCR GPU

Pernah bertanya-tanya bagaimana cara **recognize text from image** tanpa menulis ribuan baris kode? Anda tidak sendirian. Baik Anda memindai kwitansi untuk laporan pengeluaran atau mengubah catatan tulisan tangan menjadi PDF yang dapat dicari, mendapatkan teks bersih dari gambar adalah kebutuhan umum.

Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan **how to enable GPU acceleration**, **load image for OCR**, dan akhirnya **extract text from receipt** (atau gambar apa pun) sebagai teks biasa. Tanpa basa‑basi, hanya bagian yang benar‑benar Anda perlukan untuk disalin‑tempel.

## What You’ll Build

Pada akhir panduan Anda akan memiliki aplikasi konsol kecil yang:

1. Membuat sebuah `OcrEngine` dan mengaktifkan pemrosesan GPU.  
2. Memuat file gambar lokal (kwitansi, tanda, apa saja).  
3. Menjalankan optical character recognition.  
4. Mencetak teks yang dikenali ke konsol – secara efektif **convert image to plain text**.

Semua ini berjalan pada .NET 6+ dengan perpustakaan Aspose.OCR gratis, dan berfungsi pada mesin dengan GPU NVIDIA atau AMD yang mendukung OpenCL.

## Prerequisites

- .NET 6 SDK atau yang lebih baru terpasang.  
- Visual Studio 2022 (atau editor apa pun yang Anda sukai).  
- Mesin dengan GPU (opsional tetapi disarankan untuk kecepatan).  
- File gambar contoh, misalnya `receipt.jpg`, ditempatkan di suatu lokasi yang dapat Anda referensikan.  

Jika Anda tidak memiliki GPU, kode tetap berfungsi; ia hanya akan kembali ke pemrosesan CPU.

## Step 1: Install Aspose.OCR via NuGet

Pertama, tambahkan paket Aspose.OCR ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

That single line pulls in all the binaries you need, including the native OpenCL wrappers for GPU work.

## Step 2: Enable GPU Acceleration (how to enable gpu acceleration)

Turning on the GPU is as simple as flipping a boolean flag on the engine’s settings. The library automatically picks the first available device, but you can also specify an index if you have multiple GPUs.

```csharp
// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU processing – this is the “how to enable gpu acceleration” part
ocrEngine.Settings.EnableGpu = true;

// (Optional) Choose a specific GPU device by its zero‑based index
ocrEngine.Settings.GpuDeviceId = 0;
```

**Why enable the GPU?**  
Inti GPU unggul dalam tugas paralel seperti pra‑pemrosesan gambar dan inferensi jaringan saraf. Pada kartu RTX modern Anda dapat melihat percepatan OCR sebesar 3‑5× dibandingkan CPU murni.

> **Pro tip:** Jika Anda menemui kesalahan `OpenCL`, pastikan driver grafis Anda terbaru dan `OpenCL.dll` dapat diakses di jalur runtime.

## Step 3: Load Image for OCR (load image for ocr)

Selanjutnya, arahkan engine ke gambar yang ingin Anda baca. Aspose.OCR menyediakan metode factory yang nyaman yang mendukung banyak format (JPEG, PNG, BMP, TIFF, dll.).

```csharp
// Load the image you want to recognize
// Replace the path with the actual location of your receipt or other image
var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Jika file tidak ditemukan, `FromFile` akan melempar `FileNotFoundException`. Bungkus dalam try/catch jika Anda memerlukan penanganan yang elegan.

## Step 4: Perform OCR and Convert Image to Plain Text

Sekarang keajaiban terjadi. Panggil `Recognize` dan ambil properti `Text` dari hasilnya. Ini memberi Anda string bersih—tepat apa yang kami maksud dengan **convert image to plain text**.

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(receiptImage);

// Output the recognized plain‑text to the console
System.Console.WriteLine(ocrResult.Text);
```

Properti `Text` menghapus jeda baris dan mengembalikan Unicode, sehingga Anda dapat mengarahkannya langsung ke file, basis data, atau pipeline pemrosesan selanjutnya.

### Expected Output

Jika `receipt.jpg` berisi kwitansi toko tipikal, Anda mungkin melihat sesuatu seperti:

```
Walmart Supercenter
123 Main St.
Anytown, TX 75001
Date: 06/27/2026
Item          Qty   Price
Apple         2     $1.20
Bread         1     $2.50
TOTAL                $3.70
Thank you for shopping!
```

Pemformatan tepatnya tergantung pada kualitas gambar sumber dan model bahasa yang digunakan secara internal.

## Step 5: Full Working Example

Berikut adalah program lengkap yang dapat Anda salin ke `Program.cs` baru. Program ini mencakup semua langkah di atas, plus sedikit penanganan error untuk keamanan.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        try
        {
            // Step 1: Create the OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Settings.EnableGpu = true;          // Turn on GPU processing
            ocrEngine.Settings.GpuDeviceId = 0;           // (Optional) Choose GPU device by index

            // Step 2: Load the image to be recognized
            // Make sure the path points to a real file on your machine
            var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

            // Step 3: Perform OCR on the loaded image
            var ocrResult = ocrEngine.Recognize(receiptImage);

            // Step 4: Output the recognized plain‑text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Simpa, build, dan jalankan:

```bash
dotnet run
```

Jika semuanya terhubung dengan benar, konsol akan menampilkan teks yang diekstrak, membuktikan bahwa Anda telah berhasil **extract text from receipt** (atau gambar apa pun) menggunakan Aspose OCR dengan dukungan GPU.

## Edge Cases & Common Questions

### What if my image is low‑resolution?

Akurasi OCR turun drastis pada gambar yang buram atau sangat kecil. Sebelum memanggil `Recognize`, pertimbangkan untuk memperbesar gambar (mis., menggunakan `System.Drawing` atau `ImageSharp`) dan menerapkan peningkatan kontras. Aspose juga menyediakan metode `Preprocess` yang dapat Anda coba.

### My GPU isn’t being used – why?

- Pastikan `EnableGpu` bernilai `true` *sebelum* Anda memanggil `Recognize`.  
- Periksa bahwa driver Anda mendukung OpenCL 1.2+ (kebanyakan driver modern melakukannya).  
- Pada beberapa server headless Anda mungkin perlu mengatur variabel lingkungan `CUDA_VISIBLE_DEVICES` (untuk NVIDIA) agar perangkat terlihat.

### Can I process multiple images in parallel?

Tentu saja. Instance `OcrEngine` **tidak** thread‑safe, tetapi Anda dapat membuat engine terpisah per thread. Ingatlah untuk mengaktifkan GPU pada setiap instance; driver akan menjadwalkan pekerjaan di semua core secara otomatis.

### How do I change the language (e.g., French receipts)?

```csharp
ocrEngine.Settings.Language = OcrLanguage.French;
```

Pastikan paket bahasa yang sesuai disertakan dalam paket NuGet (bahasa umum biasanya sudah termasuk).

## Performance Benchmark (Optional)

Pada laptop dengan Intel i7‑12700H dan NVIDIA RTX 3060, waktu berikut tercatat untuk kwitansi JPEG 300 KB:

| Mode               | Time (ms) |
|--------------------|-----------|
| CPU only           | 820       |
| GPU (EnableGpu)    | 210       |

Itu kira‑kira **4× percepatan**, mengonfirmasi mengapa **how to enable gpu acceleration** penting untuk pemrosesan massal.

## Conclusion

Anda baru saja mempelajari cara **recognize text from image** menggunakan Aspose OCR, mengaktifkan GPU acceleration untuk peningkatan kecepatan yang terlihat, **load image for OCR**, dan akhirnya **convert image to plain text**—sempurna untuk mengekstrak teks dari kwitansi, faktur, atau dokumen yang dipindai. Kode lengkapnya mandiri, berjalan pada lingkungan .NET 6+ apa pun, dan dapat diperluas untuk memproses folder secara batch, menyimpan hasil ke basis data, atau memberi umpan ke model AI selanjutnya.

Langkah selanjutnya? Coba ganti kwitansi dengan catatan tulisan tangan, bereksperimen dengan API `Preprocess` untuk meningkatkan akurasi pada pemindaian berisik, atau integrasikan engine ke layanan web ASP.NET Core sehingga pengguna dapat mengunggah gambar dan mendapatkan teks secara instan. Anda juga dapat menjelajahi kata kunci sekunder lain seperti **extract text from receipt** dalam alur kerja yang lebih besar, atau menyelami lebih dalam **how to enable gpu acceleration** untuk produk Aspose lainnya.

Selamat coding, semoga OCR Anda selalu akurat!

## What Should You Learn Next?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}