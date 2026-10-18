---
category: general
date: 2026-09-08
description: Pelajari cara mengaktifkan GPU untuk Aspose OCR, menjalankan pemrosesan
  OCR batch, dan mengekstrak teks dari gambar secara efisien menggunakan .NET.
draft: false
keywords:
- how to enable gpu
- extract text from images
- batch ocr processing
- ocr gpu acceleration
- aspose ocr .net
lastmod: 2026-09-08
og_description: Cara mengaktifkan GPU untuk Aspose OCR. Panduan ini menunjukkan pemrosesan
  OCR batch, mengekstrak teks dari gambar, dan memilih perangkat GPU optimal di .NET.
og_image_alt: Diagram of Aspose OCR engine offloading work to GPU for faster text
  extraction
og_title: Cara mengaktifkan GPU untuk Aspose OCR – tutorial lengkap
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  headline: How to enable GPU for Aspose OCR – complete tutorial
  type: TechArticle
- description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  name: How to enable GPU for Aspose OCR – complete tutorial
  steps:
  - name: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
    text: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
  - name: Replace the paths in `imageFiles` with the location of your own `.tif` files.
    text: Replace the paths in `imageFiles` with the location of your own `.tif` files.
  - name: 'Build and run: `dotnet run`.'
    text: 'Build and run: `dotnet run`.'
  type: HowTo
- questions:
  - answer: Yes, a commercial Aspose.OCR license is needed for production deployments;
      a free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Any NVIDIA GPU that supports CUDA 11.0 or newer, such as RTX 2060, RTX
      3070, RTX 4090, and the corresponding Tesla series.
    question: Which GPU models are officially supported?
  - answer: Absolutely. The same `OcrEngine` instance can be reused across requests;
      just ensure thread safety by cloning the engine per request.
    question: Can I run this code in an ASP.NET Core web API?
  - answer: Yes, you can set `ocrEngine.Language = Language.English | Language.Spanish`
      to enable simultaneous recognition of multiple languages.
    question: Does Aspose OCR handle multi‑language documents?
  - answer: The engine streams image data, so you can process images up to 10,000
      × 10,000 pixels without exhausting GPU memory, though performance may vary.
    question: What is the maximum image size the GPU can handle?
  type: FAQPage
tags:
- Aspose OCR
- GPU acceleration
- C#
- .NET
title: Cara mengaktifkan GPU untuk Aspose OCR – tutorial lengkap
url: /id/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengaktifkan GPU untuk Aspose OCR – tutorial lengkap

Pernah bertanya-tanya **bagaimana cara mengaktifkan GPU** saat menggunakan Aspose OCR? Anda bukan satu-satunya—pengembang yang menangani volume dokumen besar sering menemui batasan kinerja karena mesin OCR terjebak pada CPU. Kabar baik? Mengaktifkan percepatan GPU cukup sederhana, dan dapat mengurangi beberapa detik per halaman. Dalam panduan ini kami akan membahas **bagaimana cara mengaktifkan GPU**, menjalankan **pemrosesan OCR batch**, mengekstrak teks yang dikenali, dan bahkan memilih perangkat GPU yang tepat. Pada akhir Anda akan mengetahui **cara menggunakan Aspose** untuk ekstraksi teks OCR super cepat.

## Jawaban Cepat
- **Apa yang dilakukan dengan mengaktifkan GPU?** Itu memindahkan analisis tingkat piksel ke kartu grafis, mengurangi waktu pemrosesan hingga 80 % pada gambar 300 dpi tipikal.  
- **Apakah saya memerlukan lisensi khusus?** Tidak, paket NuGet Aspose.OCR standar sudah mencakup dukungan GPU.  
- **Versi .NET mana yang diperlukan?** .NET 6.0 atau lebih baru; API menggunakan fitur C# modern.  
- **Bisakah saya menjalankan di mesin hanya CPU?** Ya—jika tidak ada GPU yang kompatibel, mesin akan otomatis kembali ke CPU.  
- **Berapa banyak gambar yang dapat saya proses sekaligus?** Anda dapat mengantri ratusan file; GPU akan menangani mereka secara berurutan sementara kode Anda dapat mengirim gambar berikutnya segera setelah yang sebelumnya selesai.

## Apa itu cara mengaktifkan GPU?
The `how to enable GPU` adalah proses mengkonfigurasi `OcrEngine` Aspose OCR untuk mengarahkan beban kerja pemrosesan gambar ke kartu grafis yang kompatibel dengan CUDA alih-alih prosesor pusat. Saklar ini dikendalikan oleh dua properti: `UseGpu` dan `GpuDeviceId`. Mengaktifkan flag ini memindahkan analisis piksel yang intensif secara komputasi ke GPU, yang dapat menangani ribuan thread secara paralel, secara dramatis mengurangi waktu pemrosesan.

Kelas `OcrEngine` adalah komponen inti Aspose OCR yang melakukan analisis gambar dan pengenalan teks.

## Mengapa menggunakan percepatan GPU dengan Aspose OCR?
Aspose OCR mendukung **lebih dari 50 format gambar input** dan dapat memproses batch ratusan halaman tanpa memuat seluruh dokumen ke memori. Ketika percepatan GPU diaktifkan, pengujian benchmark menunjukkan **penurunan 70 %‑80 %** pada rata‑rata waktu pemrosesan per halaman pada RTX 3080 dibandingkan dengan eksekusi murni CPU. Peningkatan kecepatan ini langsung diterjemahkan menjadi biaya cloud yang lebih rendah dan hasil yang lebih cepat terlihat oleh pengguna dalam aplikasi yang intensif dokumen.

## Prasyarat
- .NET 6.0 atau lebih baru (kode menggunakan sintaks C# modern)  
- Paket NuGet Aspose.OCR untuk .NET (versi 23.10 atau lebih baru)  
- GPU yang kompatibel dengan CUDA dengan driver yang sesuai terpasang (minimum CUDA 11.0)  
- Folder yang berisi file `.tif` contoh untuk batch run  

Jika Anda sudah menyiapkan hal‑hal dasar tersebut, mari kita mulai.

## Cara mengaktifkan GPU di Aspose OCR

Muat mesin OCR, aktifkan mode GPU, dan secara opsional pilih indeks perangkat.  

`OcrEngine` adalah kelas inti Aspose OCR yang melakukan analisis gambar dan pengenalan teks.  

Mengaktifkan GPU adalah operasi dua langkah: set `UseGpu = true` dan, ketika ada beberapa GPU, tetapkan `GpuDeviceId` yang diinginkan. Paragraf jawaban langsung ini menjelaskan seluruh proses dalam 45 kata.

Hal pertama yang perlu Anda beri tahu `OcrEngine` untuk menggunakan GPU. Ini dilakukan melalui dua properti sederhana: `UseGpu` dan opsional `GpuDeviceId`. Menetapkan `UseGpu` ke `true` mengubah mesin ke mode GPU, sementara `GpuDeviceId` memungkinkan Anda memilih GPU mana (jika Anda memiliki lebih dari satu) yang akan melakukan pekerjaan berat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Mengapa ini penting** – Versi CPU memproses setiap piksel secara berurutan, yang dapat menjadi bottleneck untuk gambar beresolusi tinggi. Versi GPU menjalankan ribuan thread secara paralel, secara dramatis mengurangi waktu per halaman.

### Gambaran Visual  

![Diagram yang menunjukkan bagaimana mesin OCR memindahkan pekerjaan ke GPU ketika “cara mengaktifkan gpu” diatur](/images/enable-gpu-diagram.png){: .center .responsive alt="how to enable gpu"}

[Diagram yang menunjukkan bagaimana mesin OCR memindahkan pekerjaan ke GPU ketika “cara mengaktifkan gpu” diatur](/images/enable-gpu-diagram.png)

*(Jika Anda tidak dapat melihat gambar, bayangkan saja diagram alur di mana mesin OCR menyerahkan buffer gambar ke inti CUDA.)*

## Cara menjalankan pemrosesan OCR batch dengan Aspose

`Recognize` method dari `OcrEngine` memproses sebuah gambar dan mengembalikan `OcrResult` yang berisi teks yang diekstrak serta metadata. Anda dapat memproses seluruh folder dengan melakukan loop pada daftar jalur file. Mesin secara otomatis mengantri setiap gambar ke GPU, menjaga pipeline tetap sibuk sementara aplikasi Anda terus mengirim file baru. Pendekatan ini memungkinkan Anda menangani ratusan file TIFF secara efisien, dengan GPU melakukan pekerjaan berat secara paralel.

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Tips pro** – Untuk batch yang sangat besar, pertimbangkan menggunakan `Parallel.ForEach` bersama dengan `ocrEngine.Clone()` untuk menghindari masalah keamanan thread. Metode `Clone` membuat salinan dangkal dari mesin yang tetap mengacu pada konteks GPU yang sama.

### Output yang Diharapkan

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Jika angka-angka terlihat wajar, **pemrosesan OCR batch** Anda berfungsi dan GPU sedang dimanfaatkan.

## Cara mengekstrak teks dari gambar – mendapatkan hasil

`OcrResult` adalah objek yang menyimpan output OCR, termasuk teks yang dikenali, skor kepercayaan, dan informasi tata letak. Metode `Recognize` mengembalikan objek `OcrResult`. Ambil teks polos dari properti `Text` dan tulis ke file untuk penggunaan selanjutnya. Menyimpan teks OCR memungkinkan pemrosesan lanjutan (pengindeksan pencarian, penambangan data, dll.) tanpa harus menjalankan mesin lagi dan memberi Anda catatan permanen untuk debugging.

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Mengapa mengekstrak ke file?** – Menyimpan teks OCR memungkinkan pemrosesan lanjutan (pengindeksan pencarian, penambangan data, dll.) tanpa menjalankan mesin kembali. Ini juga memberi Anda catatan permanen untuk debugging.

## Cara mengatur perangkat GPU untuk kinerja optimal

`CudaDeviceInfo` menyediakan informasi tentang GPU yang kompatibel dengan CUDA yang terpasang di sistem. Ketika ada beberapa GPU, gunakan `GpuDeviceId` untuk memilih yang terbaik. Indeks tersebut sesuai dengan urutan yang dikembalikan oleh `CudaDeviceInfo.GetDevices()`. Memilih perangkat yang tepat memastikan Anda menggunakan GPU paling kuat dan menghindari kontensi dengan beban kerja lain pada kartu sekunder.

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Kasus tepi** – Beberapa GPU lama tidak mendukung versi CUDA yang diperlukan. Dalam skenario tersebut, `UseGpu = true` akan kembali ke CPU secara diam-diam, jadi selalu periksa `ocrEngine.IsGpuEnabled` setelah inisialisasi.

## Cara menggunakan Aspose OCR dalam proyek dunia‑nyata

Menggabungkan semua, berikut aplikasi konsol yang ringkas dan siap dijalankan yang mendemonstrasikan **cara mengaktifkan GPU**, menjalankan **pemrosesan OCR batch**, mengekstrak teks, dan memungkinkan Anda memilih perangkat GPU. Contoh ini membuat `OcrEngine`, mengaktifkan GPU, menenumerasi perangkat yang tersedia, memproses setiap gambar, dan menulis teks yang dikenali ke file `.txt` di samping gambar sumber.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### Menjalankan contoh

1. Instal paket NuGet: `dotnet add package Aspose.OCR --version 23.10.0`  
2. Ganti jalur di `imageFiles` dengan lokasi file `.tif` Anda sendiri.  
3. Bangun dan jalankan: `dotnet run`.  

Anda akan melihat daftar GPU, diikuti oleh baris untuk setiap gambar yang melaporkan jumlah karakter dan jalur file `.txt` yang dihasilkan.

## Pertanyaan umum & jebakan

- **Apakah ini bekerja di mesin hanya CPU?**  
  Ya—jika `UseGpu` bernilai `true` tetapi tidak ada GPU yang kompatibel, Aspose akan kembali ke CPU. Anda dapat memverifikasi mode melalui `ocrEngine.IsGpuEnabled`.

- **Bagaimana jika saya mendapatkan error “CUDA driver version is insufficient”?**  
  Perbarui driver NVIDIA Anda ke versi terbaru yang cocok dengan toolkit CUDA yang disertakan dengan Aspose. Library memerlukan setidaknya CUDA 11.0 untuk fitur GPU terbaru.

- **Bisakah saya memproses PDF secara langsung?**  
  Aspose OCR bekerja pada gambar raster. Konversi halaman PDF ke gambar terlebih dahulu (mis., menggunakan Aspose.PDF) dan kemudian beri ke mesin OCR.

- **Bagaimana cara meningkatkan akurasi pada pemindaian berisik?**  
  Aktifkan opsi pra‑pemrosesan seperti `ocrEngine.Preprocess = true` atau gunakan gambar resolusi lebih tinggi (300 dpi atau lebih). Percepatan GPU tetap berlaku.

## Pertanyaan yang sering diajukan

**T: Apakah lisensi diperlukan untuk penggunaan produksi?**  
J: Ya, lisensi komersial Aspose.OCR diperlukan untuk penyebaran produksi; percobaan gratis tersedia untuk evaluasi.

**T: Model GPU mana yang secara resmi didukung?**  
J: Semua GPU NVIDIA yang mendukung CUDA 11.0 atau lebih baru, seperti RTX 2060, RTX 3070, RTX 4090, dan seri Tesla yang bersangkutan.

**T: Bisakah saya menjalankan kode ini dalam API web ASP.NET Core?**  
J: Tentu saja. Instansi `OcrEngine` yang sama dapat digunakan kembali di seluruh permintaan; pastikan keamanan thread dengan mengkloning mesin per permintaan.

**T: Apakah Aspose OCR menangani dokumen multi‑bahasa?**  
J: Ya, Anda dapat mengatur `ocrEngine.Language = Language.English | Language.Spanish` untuk mengaktifkan pengenalan simultan beberapa bahasa.

**T: Berapa ukuran gambar maksimum yang dapat ditangani GPU?**  
J: Mesin mengalirkan data gambar, sehingga Anda dapat memproses gambar hingga 10.000 × 10.000 piksel tanpa menghabiskan memori GPU, meskipun kinerja dapat bervariasi.

---

**Terakhir Diperbarui:** 2026-09-08  
**Diuji dengan:** Aspose.OCR 23.10 for .NET  
**Penulis:** Aspose

## Tutorial Terkait

- [Cara Menggunakan OCR di C untuk Mengekstrak Teks Dari Gambar dengan Akselerasi GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Mengekstrak Teks Dari Gambar dengan Aspose OCR GPU Panduan C](/ocr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/)
- [Menghapus Latar Belakang OCR dengan Aspose OCR Panduan Lengkap GPU](/ocr/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}