---
category: general
date: 2026-06-03
description: Contoh Aspose OCR C# yang menunjukkan cara mengatur batas memori GPU,
  memuat gambar untuk OCR, dan mengenali teks dari file TIF dengan kode lengkap serta
  tips.
draft: false
keywords:
- aspose ocr c# example
- set gpu memory limit
- load image for ocr
- recognize text from tif
- gpu acceleration asp ocr
- high‑resolution OCR c#
- asp ocr cuda setup
language: id
og_description: 'Pelajari contoh lengkap Aspose OCR C#: aktifkan GPU, atur batas memori
  GPU, muat gambar untuk OCR, dan kenali teks dari file TIF. Kode lengkap disertakan.'
og_title: Contoh Aspose OCR C# – Akselerasi GPU, Batas Memori & Pemrosesan TIF
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  headline: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  type: TechArticle
- description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  name: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  steps:
  - name: Why set a memory limit?
    text: '- **Stability:** Prevents out‑of‑memory crashes when processing gigantic
      images. - **Co‑existence:** Allows other GPU‑heavy apps (e.g., TensorFlow models)
      to run side‑by‑side. - **Predictability:** Makes performance testing repeatable
      because the GPU won’t start swapping.'
  - name: Handling multi‑page TIFFs
    text: If your TIFF contains several pages, Aspose OCR will only read the first
      one by default. To process all pages, you can loop over `image.Pages` (available
      in newer SDK versions) and feed each page to the engine separately.
  - name: Why this works well with TIF
    text: '- **Lossless compression:** TIFF often stores raw pixel data, giving the
      OCR engine the highest fidelity. - **Multiple color spaces:** Aspose can handle
      grayscale, RGB, or even CMYK TIFFs without extra conversion code.'
  - name: Expected output
    text: 'Running the program on a clear, 300 dpi scan of a printed page typically
      yields something like:'
  - name: Quick checklist
    text: '- ✅ **Aspose OCR C# example** compiled without errors. - ✅ **GPU enabled**
      (`Enable = true`). - ✅ **GPU memory limit** set to 2048 MB. - ✅ **Image loaded**
      from a TIF file. - ✅ **Text recognized** and printed.'
  type: HowTo
tags:
- Aspose
- OCR
- C#
- GPU
title: Contoh Aspose OCR C# – Aktifkan GPU, Atur Batas Memori & Proses Gambar TIF
url: /id/net/ocr-optimization/aspose-ocr-c-example-enable-gpu-set-memory-limit-process-tif/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR C# Example – Aktifkan GPU, Atur Batas Memori & Proses Gambar TIF

Pernahkah Anda bertanya-tanya bagaimana cara memaksimalkan kinerja kode **Aspose OCR C# example** saat menangani pemindaian TIFF yang besar? Anda tidak sendirian. Dalam banyak proyek dunia nyata—bayangkan mendigitalkan arsip atau mengekstrak data dari kwitansi resolusi tinggi—bottleneck bukanlah algoritma OCR itu sendiri, melainkan pemanfaatan perangkat keras.

Begini: Aspose OCR mendukung percepatan GPU, tetapi Anda harus memberi tahu berapa banyak memori yang boleh digunakannya, memuat tipe gambar yang tepat, dan akhirnya mengambil teks yang dikenali dari file .tif. Tutorial ini memandu Anda melalui setiap langkah, mulai dari menginstal SDK hingga menyesuaikan pengaturan GPU, sehingga Anda dapat menjalankan OCR dengan kecepatan tinggi tanpa menghabiskan RAM GPU Anda.

Kami juga akan menambahkan beberapa skenario “bagaimana jika”—seperti menangani TIFF multi‑halaman atau kembali ke CPU ketika GPU tidak tersedia—sehingga Anda mendapatkan solusi yang kuat, bukan hanya potongan kode satu kali.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut di mesin Anda:

| Prerequisite | Why it matters |
|--------------|----------------|
| **.NET 6 SDK** (or later) | Aspose OCR menargetkan .NET Standard 2.0+, jadi semua versi .NET terbaru dapat digunakan. |
| **Aspose.OCR NuGet package** (`Install-Package Aspose.OCR`) | Pustaka inti yang menyediakan `OcrEngine`, `GpuSettings`, dll. |
| **CUDA 11+** (NVIDIA) **or ROCm 5+** (AMD) | Diperlukan untuk percepatan GPU; SDK akan memeriksa driver yang kompatibel pada saat runtime. |
| A **GPU with at least 2 GB VRAM** (we’ll cap it at 2048 MB) | Tanpa memori yang cukup, engine dapat beralih ke CPU secara diam‑diam. |
| A **high‑resolution TIFF** image you want to process | Aspose OCR dapat membaca hampir semua format raster, tetapi TIF umum untuk pemindaian. |
| Visual Studio 2022 (or any editor you like) | Untuk membangun dan men-debug proyek C#. |

Jika ada yang kurang, kode tetap dapat dikompilasi, tetapi Anda tidak akan melihat peningkatan kinerja yang diinginkan.

## Langkah 1: Buat Engine Aspose OCR C# Example

Hal pertama dalam setiap **Aspose OCR C# example** adalah menginstansiasi engine OCR. Anggap `OcrEngine` sebagai sutradara film—ia mengoordinasikan segala hal mulai dari pemuatan gambar hingga ekstraksi teks.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **Pro tip:** Jika Anda berencana memproses banyak gambar secara berurutan, pertahankan satu `OcrEngine` tetap hidup. Membuatnya kembali per gambar menambah overhead yang dapat melampaui waktu OCR.

## Langkah 2: Atur Batas Memori GPU (dan Aktifkan Akselerasi)

Sekarang datang bagian yang sering membuat orang kebingungan: **atur batas memori GPU**. Secara default Aspose OCR akan mencoba menggunakan sebanyak mungkin VRAM, yang pada workstation bersama dapat menghambat aplikasi lain. Objek `GpuSettings` memungkinkan Anda membatasi alokasi.

```csharp
        // Step 2: Enable GPU acceleration (requires CUDA 11+ or ROCm 5+)
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,          // Turn on the GPU path
            DeviceId = 0,           // First GPU in the system (change if you have multiple)
            MemoryLimitMb = 2048    // Optional cap – 2 GB in this example
        };
```

### Mengapa mengatur batas memori?

- **Stability:** Mencegah crash out‑of‑memory saat memproses gambar raksasa.
- **Co‑existence:** Memungkinkan aplikasi berat GPU lain (misalnya model TensorFlow) berjalan berdampingan.
- **Predictability:** Membuat pengujian kinerja dapat diulang karena GPU tidak akan mulai swapping.

Jika Anda menghilangkan `MemoryLimitMb`, Aspose akan mengalokasikan apa pun yang dianggap perlu, yang mungkin baik pada server inferensi khusus tetapi berisiko pada laptop pengembang.

## Langkah 3: Muat Gambar untuk OCR

Memuat format file yang tepat adalah langkah penting berikutnya. Metode `OcrImage.FromFile` secara otomatis mendeteksi tipe gambar, tetapi Anda tetap harus memverifikasi bahwa file ada dan merupakan varian TIFF yang didukung (misalnya LZW‑compressed atau CCITT‑G4).

```csharp
        // Step 3: Load the high‑resolution image to be processed
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);
```

### Menangani TIFF multi‑halaman

Jika TIFF Anda berisi beberapa halaman, Aspose OCR secara default hanya membaca halaman pertama. Untuk memproses semua halaman, Anda dapat melakukan loop pada `image.Pages` (tersedia pada versi SDK terbaru) dan memberi setiap halaman ke engine secara terpisah.

```csharp
        foreach (var page in image.Pages)
        {
            var result = ocrEngine.Recognize(page);
            System.Console.WriteLine($"--- Page {page.Index + 1} ---");
            System.Console.WriteLine(result.Text);
        }
        return; // Skip the single‑image path below
```

Potongan kode di atas menunjukkan pola **load image for OCR** yang bekerja untuk file tunggal maupun multi‑halaman.

## Langkah 4: Kenali Teks dari TIF (atau raster apa pun)

Sekarang gambar berada di memori, kami meminta Aspose melakukan magisnya. Metode `Recognize` mengembalikan `OcrResult` yang berisi teks polos, skor kepercayaan, dan bahkan informasi bounding‑box jika Anda memerlukannya.

```csharp
        // Step 4: Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

### Mengapa ini bekerja baik dengan TIF

- **Lossless compression:** TIFF sering menyimpan data piksel mentah, memberikan engine OCR fidelitas tertinggi.
- **Multiple color spaces:** Aspose dapat menangani TIFF grayscale, RGB, atau bahkan CMYK tanpa kode konversi tambahan.

Jika Anda perlu menyesuaikan paket bahasa (misalnya Prancis atau Jepang), setel `ocrEngine.Settings.Language = "fr"` sebelum memanggil `Recognize`.

## Langkah 5: Tampilkan Teks yang Dikenali

Akhirnya, kami menampilkan teks ke konsol. Dalam aplikasi nyata Anda mungkin menulis ke basis data, file JSON, atau mengirim string ke pipeline NLP berikutnya.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Output yang Diharapkan

Menjalankan program pada pemindaian bersih 300 dpi dari halaman cetak biasanya menghasilkan sesuatu seperti:

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
...
```

Jika gambar buram atau batas memori GPU terlalu rendah, Anda mungkin melihat karakter acak atau hasil terpotong. Menurunkan `MemoryLimitMb` di bawah jejak memori gambar (sering ~1 GB untuk TIFF 6000×8000 piksel) dapat menyebabkan engine beralih ke CPU secara otomatis.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke dalam proyek Console App baru, ganti `YOUR_DIRECTORY/large_photo.tif` dengan path ke TIFF Anda sendiri, dan tekan **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration and set a memory cap
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,
            DeviceId = 0,
            MemoryLimitMb = 2048 // 2 GB limit – adjust to your GPU size
        };

        // Step 3: Load the image (ensure the file exists)
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);

        // Step 4: Perform OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 5: Output the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Daftar Periksa Cepat

- ✅ **Aspose OCR C# example** berhasil dikompilasi tanpa error.  
- ✅ **GPU diaktifkan** (`Enable = true`).  
- ✅ **Batas memori GPU** diatur ke 2048 MB.  
- ✅ **Gambar dimuat** dari file TIF.  
- ✅ **Teks dikenali** dan dicetak.

## Kesalahan Umum & Cara Menghindarinya

| Gejala | Penyebab kemungkinan | Solusi |
|--------|----------------------|--------|
| `System.DllNotFoundException: cudart64_110.dll` | CUDA runtime tidak terinstal atau versi tidak cocok. | Instal CUDA 11.x (atau 12.x) yang cocok dengan driver Anda. |
| OCR returns empty string | Gambar terlalu gelap atau DPI < 150. | Pra‑proses dengan `image.AdjustContrast()` atau ubah resolusi menjadi 300 dpi. |
| Out‑of‑memory crash on GPU | `MemoryLimitMb` terlalu rendah untuk gambar. | Tingkatkan batasnya atau bagi gambar menjadi ubin melalui `image.Crop`. |
| `Unsupported image format` error | TIFF menggunakan kompresi eksotis (misalnya JPEG‑2000). | Konversi TIFF ke format yang didukung dengan ImageMagick sebelum OCR. |

## Memperluas Demo

Sekarang Anda memiliki **aspose ocr c# example** yang solid, Anda mungkin ingin menjelajahi:

- **Batch processing:** Loop melalui folder TIF, tulis setiap hasil ke file `.txt`.
- **Language packs:** `ocrEngine.Settings.Language = "es"` untuk bahasa Spanyol, atau muat kamus khusus.
- **Bounding boxes:** Gunakan `ocrResult.Regions` untuk mendapatkan koordinat setiap kata—berguna untuk alat redaksi.
- **CPU fallback:** Bungkus blok GPU dalam try/catch; jika gagal, setel `ocrEngine.Settings.Gpu.Enable = false` dan coba lagi.

Ekstensi ini menjaga pola inti tetap utuh sambil menambah nilai untuk penggunaan spesifik —

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}