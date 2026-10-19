---
category: general
date: 2026-01-13
description: Pelajari cara mengenali teks dari gambar dan mengekstrak teks dari kwitansi
  dengan cepat menggunakan Aspose OCR. Termasuk langkah memuat gambar untuk OCR dan
  mengatur ID perangkat GPU.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: id
og_description: Kenali teks dari gambar secara instan dengan Aspose OCR. Ikuti panduan
  langkah demi langkah ini untuk memuat gambar untuk OCR, mengatur ID perangkat GPU,
  dan mengekstrak teks dari struk.
og_title: Mengenali teks dari gambar – Panduan C# Lengkap yang Dipercepat GPU
tags:
- Aspose OCR
- C#
- GPU computing
title: Mengenali teks dari gambar dengan Aspose OCR – Tutorial C# yang Dipercepat
  GPU
url: /id/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar – Panduan C# Berakselerasi GPU Lengkap

Pernah perlu **recognize text from image** tetapi menemukan versi CPU sangat lambat? Mungkin Anda mencoba **extract text from receipt** dan latensi mengganggu pengalaman pengguna Anda. Kabar baiknya, Anda tidak perlu puas dengan kinerja lambat—paket GPU Aspose OCR dapat mempercepat proses, dan kodenya hanya beberapa baris.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan cara **load image for OCR**, mengonfigurasi GPU dengan **set GPU device ID**, dan akhirnya mengambil hasil teks biasa. Pada akhir tutorial Anda akan memiliki potongan kode siap pakai yang berfungsi di mesin Windows atau Linux modern dengan kartu NVIDIA yang didukung.

---

## Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework 4.7.2+) – API bekerja dengan keduanya.
- **Aspose.OCR** paket NuGet **plus** add‑on **Aspose.OCR.Gpu**.
- GPU NVIDIA dengan setidaknya 2 GB VRAM (demo membatasi penggunaan pada 1 GB).
- Contoh gambar, misalnya, kwitansi yang dipindai (`receipt.jpg`).

Jika Anda sudah memiliki proyek, cukup jalankan `dotnet add package Aspose.OCR` dan `dotnet add package Aspose.OCR.Gpu`. Tidak diperlukan pustaka native tambahan; SDK menyertakan binary CUDA yang diperlukan.

## Implementasi Langkah‑per‑Langkah

### ## Cara mengenali teks dari gambar menggunakan Aspose OCR dan GPU

Berikut adalah **program lengkap yang berdiri sendiri**. Salin‑tempel ke dalam proyek konsol baru dan tekan `Ctrl+F5`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Pro tip:** Jika mesin Anda memiliki beberapa GPU, ubah `DeviceId` menjadi `1`, `2`, dll., untuk memilih kartu yang kurang sibuk. SDK akan melempar `GpuDeviceNotFoundException` yang jelas jika ID berada di luar jangkauan.

### ### Langkah 1: Load image for OCR

`OcrImage.FromFile` tidak hanya membaca bitmap—ia melakukan pra‑pemrosesan gambar (deskew, binarisasi) berdasarkan heuristik internal. Inilah mengapa **load image for OCR** menjadi langkah terpisah: Anda dapat mengganti dengan `MemoryStream` jika gambar berada di basis data.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

Jika Anda perlu **recognize text from image** yang sudah berada di memori:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### Langkah 2: Set GPU device ID and memory limits

Sumber daya GPU terbatas. Dengan mengekspos `DeviceId` dan `MaxMemoryMb`, Aspose memungkinkan Anda **set GPU device ID** dengan aman, mencegah satu proses menguasai seluruh kartu.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

Jika Anda melebihi batas memori, mesin akan otomatis beralih ke RAM sistem, yang lebih lambat tetapi mencegah crash.

### ### Langkah 3: Extract text from receipt (recognize text from image)

Metode `Recognize` melakukan pekerjaan berat. Anda dapat memberikan bahasa apa pun yang didukung oleh Aspose OCR; untuk kwitansi, bahasa Inggris biasanya cukup, tetapi Anda juga dapat menambahkan `OcrLanguage.Spanish` atau paket bahasa khusus.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Output yang diharapkan** (contoh):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## Variasi Umum & Kasus Tepi

| Situasi | Apa yang Diubah | Mengapa |
|-----------|----------------|-----|
| **Beberapa kwitansi dalam satu gambar** | Panggil `ocrEngine.Recognize` pada setiap wilayah yang dipotong (gunakan `OcrImage.Crop`) | Meningkatkan akurasi karena mesin melihat area yang lebih kecil dan bersih. |
| **Pemindaian resolusi rendah (<150 dpi)** | Tingkatkan skala terlebih dahulu dengan `receiptImage.Resize(2.0)` sebelum pengenalan | Kepadatan piksel yang lebih tinggi memberi GPU lebih banyak data untuk diproses. |
| **Kwitansi non‑Inggris** | Berikan `OcrLanguage.French` (atau `.traineddata` khusus) | Model khusus bahasa mengurangi false positive. |
| **GPU tidak tersedia** | Gunakan fallback ke `OcrEngine` (CPU) dalam blok try‑catch | Menjamin aplikasi tetap berfungsi di server tanpa tampilan. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

## Tips untuk OCR Siap Produksi

- **Pemrosesan batch:** Bungkus loop pengenalan dalam `Parallel.ForEach` tetapi batasi tingkat paralelisme ke jumlah stream GPU yang dapat dialokasikan (biasanya 1‑2 per kartu).
- **Kebersihan memori:** Segera dispose objek `OcrImage` (`receiptImage.Dispose()`), terutama saat memproses ribuan kwitansi.
- **Logging:** Tangkap `ocrResult.Confidence` untuk setiap baris; kepercayaan rendah dapat memicu alur kerja tinjauan manual.
- **Keamanan:** Saat menangani kwitansi sensitif, pastikan file gambar disimpan di folder sementara terenkripsi dan dihapus setelah diproses.

## Kesimpulan

Anda kini memiliki **contoh lengkap yang dapat dijalankan** yang menunjukkan cara **recognize text from image** dengan akselerasi GPU Aspose OCR, **load image for OCR**, **set GPU device ID**, dan akhirnya **extract text from receipt** dalam beberapa langkah singkat. Kode siap untuk disalin‑tempel, dan penjelasannya memberi Anda cukup konteks untuk menyesuaikannya ke skenario multi‑bahasa, multi‑GPU, atau throughput tinggi.

Siap untuk tantangan berikutnya? Cobalah memasukkan aliran video langsung ke `GpuOcrEngine` untuk pemindaian kwitansi real‑time, atau integrasikan hasilnya ke API pembukuan. Tidak ada batasnya ketika Anda menggabungkan OCR GPU cepat dengan desain C# yang bersih.

*Selamat coding, semoga OCR Anda selalu cepat!*

![mengenali teks dari gambar demo screenshot](placeholder-image.png "contoh mengenali teks dari gambar")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}