---
category: general
date: 2026-02-09
description: Cara menggunakan Aspose OCR dengan percepatan GPU di C#. Pelajari cara
  mengenali teks dari JPG, mengekstrak teks dari gambar, dan mengaktifkan GPU dalam
  hitungan menit.
draft: false
keywords:
- how to use aspose
- recognize text from jpg
- extract text from image
- how to enable gpu
- how to set gpu
language: id
og_description: Cara menggunakan Aspose OCR dengan GPU di C#. Panduan ini menunjukkan
  cara mengenali teks dari JPG dan mengekstrak teks dari gambar menggunakan percepatan
  GPU.
og_title: Cara Menggunakan Aspose OCR dengan GPU – Panduan Pemrograman Lengkap
tags:
- Aspose
- OCR
- C#
- GPU Acceleration
title: Cara Menggunakan Aspose OCR dengan GPU – Panduan Langkah demi Langkah
url: /id/net/ocr-optimization/how-to-use-aspose-ocr-with-gpu-step-by-step-guide/
---

is.

Now produce final output with same structure, preserving shortcodes at start and end.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Aspose OCR dengan GPU – Panduan Pemrograman Lengkap

Pernahkah Anda perlu memproses tumpukan faktur yang dipindai dalam sekejap, tetapi CPU terus melambat? Itu adalah masalah klasik ketika Anda mencoba **how to use aspose** untuk OCR dalam skala besar. Dalam tutorial ini kami akan memandu Anda melalui contoh dunia nyata yang menunjukkan **how to use aspose** untuk mengenali teks dari file jpg, mengekstrak teks dari gambar, dan memaksimalkan pemanfaatan GPU Anda.

Anggap saja ini sebagai panduan singkat saat istirahat kopi—tanpa basa‑basi, hanya bagian yang dapat Anda salin‑tempel ke Visual Studio dan menyaksikan keajaibannya. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# yang berdiri sendiri dan dapat dijalankan pada mesin Windows modern apa pun dengan GPU NVIDIA atau AMD.

![cara menggunakan aspose OCR dengan GPU](/images/aspose-gpu-example.png)

## Apa yang Anda Butuhkan

- **.NET 6.0** (atau lebih baru) – kode menargetkan .NET 6 tetapi dapat bekerja dengan .NET 5 dan .NET Framework 4.8 dengan sedikit penyesuaian.
- **Aspose.OCR for .NET** paket NuGet – instal dengan perintah `dotnet add package Aspose.OCR`.
- Sebuah mesin yang **GPU‑enabled** – tutorial ini menunjukkan cara **how to enable gpu** dan **how to set gpu** batas memori, tetapi kode akan secara elegan kembali ke CPU jika tidak ada GPU yang kompatibel.
- Sebuah gambar seperti `invoice_01.jpg` yang ditempatkan di folder yang dapat Anda referensikan.

Sudah siap? Bagus, mari kita mulai.

## Cara Menggunakan Aspose OCR dengan GPU – Penyiapan Awal

Hal pertama yang harus Anda lakukan adalah membuat instance dari mesin OCR dan memberitahukannya untuk menggunakan GPU. Langkah ini penting karena tanpa flag tersebut, Aspose akan secara default menggunakan pemrosesan CPU, yang menghilangkan tujuan peningkatan kinerja kami.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 1: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the core of **how to use aspose** with a graphics card
ocrEngine.Configuration.UseGpu = true;

// Optional: limit GPU memory to avoid OOM on low‑end cards
ocrEngine.Configuration.GpuMemoryLimit = 1024; // in MB
```

**Mengapa ini penting:** Mengaktifkan GPU memindahkan kernel pemrosesan gambar yang berat ke prosesor grafis, yang dapat 10‑20× lebih cepat daripada CPU untuk gambar berukuran besar. `GpuMemoryLimit` berfungsi sebagai katup pengaman; mengaturnya ke 1024 MB bekerja untuk kebanyakan kartu menengah sambil menjaga aplikasi tetap responsif.

> **Tips pro:** Jika Anda menjalankan aplikasi pada mesin tanpa GPU yang kompatibel, Aspose secara otomatis akan kembali ke mode CPU dan mencatat peringatan. Tidak ada crash, hanya proses yang lebih lambat.

## Mengenali Teks dari JPG – Memuat Gambar

Setelah mesin siap, kita perlu memberinya sebuah gambar. Contoh ini menggunakan JPEG karena **recognize text from jpg** merupakan skenario umum untuk faktur, kwitansi, dan paspor.

```csharp
// Step 2: Load the JPEG image you want to process
// Replace the path with the location of your own image
var inputImage = ImageStream.FromFile(@"C:\OCR\Samples\invoice_01.jpg");

// Verify that the file exists (helps avoid a FileNotFoundException)
if (!System.IO.File.Exists(@"C:\OCR\Samples\invoice_01.jpg"))
{
    Console.WriteLine("Image file not found. Check the path and try again.");
    return;
}
```

**Mengapa kami memeriksa file:** File yang hilang adalah penyebab paling sering terjadinya error runtime dalam demo singkat. Dengan menanganinya lebih awal, tutorial tetap ramah pemula.

## Mengekstrak Teks dari Gambar – Menjalankan Mesin OCR

Dengan gambar di tangan, langkah selanjutnya adalah menjalankan proses OCR. Di sinilah Aspose melakukan pekerjaan berat dan mengembalikan objek `OcrResult` yang berisi teks polos, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti.

```csharp
// Step 3: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Step 4: Output the extracted plain‑text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.PlainText);
```

**Apa yang akan Anda lihat:** Konsol mencetak karakter mentah yang dideteksi oleh Aspose. Untuk faktur yang bersih, Anda mungkin mendapatkan sesuatu seperti:

```
=== Extracted Text ===
Invoice #: 2023‑00123
Date: 02/08/2023
Total: $1,245.67
...
```

Jika output terlihat berantakan, Anda mungkin perlu menyesuaikan kualitas gambar atau mengaktifkan opsi pra‑pemrosesan tambahan (misalnya, deskew, binarisasi). Hal tersebut berada di luar lingkup panduan singkat ini tetapi terdokumentasi dalam referensi API Aspose.

## Cara Mengaktifkan GPU – Mengonfigurasi Mesin

Anda mungkin bertanya-tanya **how to enable gpu** untuk Aspose jika Anda melewatkan langkah pertama. Jawabannya cukup dengan mengaktifkan flag `UseGpu` pada objek konfigurasi mesin, seperti yang ditunjukkan sebelumnya. Berikut cuplikan kode yang dipadatkan yang dapat Anda masukkan ke proyek yang sudah ada:

```csharp
ocrEngine.Configuration.UseGpu = true;   // Enables GPU
```

Di balik layar, Aspose memuat pustaka native CUDA/OpenCL yang sesuai dengan perangkat keras Anda. Jika runtime tidak dapat menemukan pustaka tersebut, ia mencatat peringatan dan kembali ke CPU. Tidak ada langkah instalasi tambahan yang diperlukan untuk kebanyakan pengaturan Windows.

## Cara Mengatur GPU – Menyetel Penggunaan Memori

Kadang-kadang Anda akan mengalami error “out of memory” pada GPU kelas rendah. Di sinilah batas memori **how to set gpu** menjadi berguna. Properti `GpuMemoryLimit` menerima nilai integer yang mewakili megabyte.

```csharp
// Example: restrict GPU usage to 512 MB
ocrEngine.Configuration.GpuMemoryLimit = 512;
```

**Kapan menyesuaikan:** Jika Anda memproses banyak gambar secara paralel, turunkan batasnya agar kartu tidak jenuh. Sebaliknya, pada workstation dengan 8 GB VRAM Anda dapat meningkatkan batas hingga 4096 MB untuk pemrosesan batch yang lebih cepat.

## Contoh Lengkap yang Dapat Dijalankan

Berikut adalah program lengkap yang dapat Anda salin ke proyek konsol baru (`dotnet new console`). Program ini mencakup semua bagian yang telah dibahas, plus sedikit penanganan error agar lebih kuat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine and enable GPU
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.Configuration.UseGpu = true;            // how to enable gpu
        ocrEngine.Configuration.GpuMemoryLimit = 1024;   // how to set gpu

        // -------------------------------------------------
        // Step 2: Load the JPEG image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\OCR\Samples\invoice_01.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        var inputImage = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // Step 3: Run the OCR engine
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

**Output yang diharapkan:** Setelah menjalankan `dotnet run`, konsol akan mencetak teks mentah yang diekstrak dari `invoice_01.jpg`. Jika gambar berisi teks cetak yang jelas, hasilnya akan hampir identik dengan dokumen asli.

## Kesalahan Umum & Cara Menghindarinya

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **GPU tidak terdeteksi** | Driver CUDA tidak terpasang atau GPU tidak didukung | Instal driver NVIDIA/AMD terbaru; verifikasi dengan `nvidia-smi` atau setara |
| **Error kehabisan memori** | `GpuMemoryLimit` terlalu tinggi untuk kartu | Turunkan batas menjadi 512 MB atau lebih rendah |
| **Output tidak jelas** | JPG beresolusi rendah atau kompresi berat | Gunakan gambar sumber dengan kualitas lebih tinggi atau aktifkan `ocrEngine.Preprocessing.Deskew = true` |
| **`ocrResult` null** | Aliran gambar gagal dimuat | Periksa kembali jalur file dan pastikan file tidak terkunci |

Menangani hal ini sebelumnya akan menyelamatkan Anda dari mengejar jejak stack trace yang cryptic di kemudian hari.

## Langkah Selanjutnya

Sekarang Anda telah menguasai **how to use aspose** untuk OCR cepat, Anda mungkin ingin menjelajahi:

- **Batch processing** – iterasi melalui direktori JPG dan menulis setiap hasil ke file `.txt`.
- **Structured extraction** – gunakan `ocrResult.Regions` untuk mendapatkan kotak pembatas dan mengekstrak bidang spesifik seperti nomor faktur.
- **Hybrid CPU/GPU mode** – jalankan CPU untuk gambar kecil dan beralih ke GPU hanya untuk file besar demi menyeimbangkan kecepatan dan memori.

Semua ekstensi tersebut dibangun di atas fondasi yang baru saja Anda siapkan, dan mereka merupakan topik yang sempurna untuk petualangan tutorial Anda berikutnya.

---

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah atau hubungi forum komunitas Aspose. GPU sudah siap—mari buat OCR secepat kilat.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}