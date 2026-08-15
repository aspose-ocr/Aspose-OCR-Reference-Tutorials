---
category: general
date: 2026-04-29
description: Pelajari cara mengenali teks dari gambar secara offline menggunakan Aspose
  OCR. Termasuk langkah-langkah untuk mengekstrak teks dari PNG dan memuat gambar
  untuk OCR dalam satu aplikasi C#.
draft: false
keywords:
- recognize text from image
- extract text from png
- load image for ocr
- Aspose OCR offline
- C# OCR example
language: id
og_description: Mengenali teks dari gambar secara offline dengan Aspose OCR di C#.
  Panduan langkah demi langkah untuk mengekstrak teks dari PNG dan memuat gambar untuk
  OCR.
og_title: Mengenali Teks dari Gambar – Panduan OCR Offline Lengkap
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Mengenali teks dari gambar di C# – Tutorial OCR Offline
url: /id/net/text-recognition/recognize-text-from-image-in-c-offline-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali Teks dari Gambar – Panduan OCR Offline Lengkap

Pernahkah Anda perlu **mengenali teks dari gambar** saat aplikasi Anda berjalan pada mesin tanpa akses internet? Mungkin Anda sedang membangun pemindai perangkat lapangan, kiosk aman, atau hanya ingin menghindari latensi layanan cloud. Dalam tutorial ini kami akan membahas program C# yang berdiri sendiri yang **mengenali teks dari gambar** menggunakan Aspose OCR, dan kami juga akan menunjukkan cara **mengekstrak teks dari png** dan **memuat gambar untuk ocr** secara tepat ketika sumber daya berada di disk.

Kami akan membahas semua yang Anda perlukan: paket NuGet yang tepat, tata letak folder untuk modul OCR yang sudah diunduh sebelumnya, dan beberapa tips yang membuat kode Anda tetap kuat ketika terjadi masalah. Pada akhir tutorial Anda akan memiliki aplikasi konsol yang dapat dijalankan dan mencetak teks yang dikenali ke konsol—tanpa panggilan jaringan sama sekali.

## Prasyarat

- .NET 6 (atau runtime .NET terbaru) terpasang secara lokal.  
- Visual Studio 2022 atau VS Code—IDE favorit Anda akan cukup.  
- Aspose.OCR NuGet package (`dotnet add package Aspose.OCR`).  
- File sumber daya OCR offline yang diunduh dari portal Aspose (hanya beberapa MB).  
- Gambar PNG (`offline_test.png`) yang ingin Anda proses.

> **Pro tip:** Simpan folder sumber daya di samping executable Anda; ini memudahkan resolusi jalur relatif.

## Langkah 1 – Buat Instance Mesin OCR

Hal pertama yang kami lakukan adalah menginstansiasi `OcrEngine`. Anggaplah ini sebagai otak yang nantinya akan menganalisis piksel.

```csharp
using Aspose.OCR;
using System;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

Mengapa membuat instance baru setiap kali dijalankan? Ini menjamin keadaan bersih, terutama ketika Anda mengubah opsi seperti unduhan sumber daya otomatis. Pada layanan yang berjalan lama Anda mungkin dapat menggunakan kembali mesin, tetapi untuk demo sederhana pendekatan ini paling aman.

## Langkah 2 – Arahkan Mesin ke Sumber Daya Offline Anda

Aspose OCR biasanya mengambil paket bahasa dari cloud. Karena kami ingin **mengenali teks dari gambar** secara offline, kami harus memberi tahu mesin di mana file-file tersebut berada.

```csharp
        // Step 2: Point the engine to the folder containing the pre‑downloaded OCR modules
        ocrEngine.Config.ResourcesPath = @"YOUR_DIRECTORY";
```

Ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif yang berisi folder `ocrdata` yang Anda ekstrak dari unduhan Aspose. Jika jalurnya salah, mesin akan melempar `FileNotFoundException`—jadi periksa kembali ejaannya.

## Langkah 3 – Nonaktifkan Unduhan Sumber Daya Otomatis

Secara default Aspose mencoba mengunduh modul yang hilang secara otomatis. Untuk skenario offline kami secara eksplisit menonaktifkan fitur tersebut.

```csharp
        // Step 3: Disable automatic resource download to enforce offline operation
        ocrEngine.Config.AllowAutomaticResourceDownload = false;
```

Jika Anda lupa menambahkan baris ini, mesin akan mencoba melakukan panggilan jaringan, yang gagal secara diam‑diam di banyak firewall korporat dan menghasilkan output kosong. Menonaktifkannya juga mempercepat proses pengenalan pertama karena mesin melewatkan pemeriksaan unduhan.

## Langkah 4 – Muat Gambar dan Jalankan OCR

Sekarang kami akhirnya **memuat gambar untuk ocr**. Helper statis `LoadImage` menerima jalur file dan mengembalikan objek `Image` yang dapat diproses oleh mesin.

```csharp
        // Step 4: Load the image to be processed and run OCR
        var ocrResult = ocrEngine.Recognize(
            OcrEngine.LoadImage(@"YOUR_DIRECTORY/offline_test.png"));
```

Perhatikan bahwa kami menggunakan file PNG—sangat cocok untuk ekstraksi teks tanpa kehilangan kualitas. Jika Anda memiliki JPEG, pemanggilan yang sama tetap berfungsi, tetapi PNG biasanya menghasilkan hasil yang lebih bersih karena tidak ada artefak kompresi.

## Langkah 5 – Tampilkan Teks yang Dikenali

Metode `Recognize` mengembalikan `OcrResult` yang berisi properti `Text`. Kami cukup menuliskannya ke konsol.

```csharp
        // Step 5: Display the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
Hello, Aspose OCR!
This is an offline test.
```

Jika output kosong, periksa kembali `ResourcesPath` dan pastikan modul bahasa (misalnya `English`) ada.

![mengenali teks dari gambar menggunakan Aspose OCR](/images/offline_ocr_demo.png "mengenali teks dari gambar")

*Tangkap layar di atas menunjukkan output konsol setelah mengekstrak teks dari png.*

## Kasus Tepi Umum & Cara Menanganinya

### 1. Gambar Terlalu Besar

PNG dengan resolusi sangat tinggi dapat menimbulkan tekanan memori. Skala gambar ke ukuran lebih kecil sebelum memberikannya ke mesin:

```csharp
using System.Drawing;

// Load, resize, then pass to OCR
var original = (Bitmap)Image.FromFile(@"YOUR_DIRECTORY/offline_test.png");
var resized = new Bitmap(original, new Size(original.Width / 2, original.Height / 2));
var tempPath = Path.Combine(Path.GetTempPath(), "temp_resized.png");
resized.Save(tempPath);
var ocrResult = ocrEngine.Recognize(OcrEngine.LoadImage(tempPath));
```

### 2. Bahasa Tidak Terdeteksi

Jika Anda mencoba **mengekstrak teks dari png** yang berisi bahasa selain Inggris, tetapkan bahasa secara eksplisit:

```csharp
ocrEngine.Config.Language = Language.French; // or Language.Spanish, etc.
```

Pastikan paket bahasa yang bersangkutan ada di folder sumber daya offline Anda.

### 3. Gambar Kosong atau Kontras Rendah

OCR kesulitan dengan kontras rendah. Pralakukan gambar dengan ambang sederhana:

```csharp
using System.Drawing.Imaging;

var bitmap = new Bitmap(@"YOUR_DIRECTORY/offline_test.png");
for (int y = 0; y < bitmap.Height; y++)
{
    for (int x = 0; x < bitmap.Width; x++)
    {
        var pixel = bitmap.GetPixel(x, y);
        var gray = (pixel.R + pixel.G + pixel.B) / 3;
        var bw = gray > 128 ? Color.White : Color.Black;
        bitmap.SetPixel(x, y, bw);
    }
}
bitmap.Save(@"YOUR_DIRECTORY/processed.png");
```

Kemudian arahkan mesin OCR ke `processed.png`. Penyesuaian kecil ini sering mengubah tingkat keberhasilan 30 % menjadi ekstraksi hampir sempurna.

## Contoh Kerja Lengkap

Berikut adalah *seluruh* program yang dapat Anda salin‑tempel ke `Program.cs`. Ingat untuk mengganti `YOUR_DIRECTORY` dengan jalur sebenarnya di mesin Anda.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set offline resources folder
        ocrEngine.Config.ResourcesPath = @"C:\OCRResources";

        // 3️⃣ Prevent any network calls
        ocrEngine.Config.AllowAutomaticResourceDownload = false;

        // 4️⃣ Load PNG and recognize
        string imagePath = @"C:\OCRResources\offline_test.png";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        var ocrResult = ocrEngine.Recognize(OcrEngine.LoadImage(imagePath));

        // 5️⃣ Output the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output yang diharapkan** (asumsi PNG berisi “Hello World!”):

```
=== OCR Output ===
Hello World!
```

Jalankan dengan `dotnet run` dari folder proyek dan saksikan konsol mencetak string yang diekstrak.

## Ringkasan – Apa yang Kami Capai

- **mengenali teks dari gambar** sepenuhnya offline menggunakan Aspose OCR.  
- Menunjukkan cara **mengekstrak teks dari png** tanpa layanan eksternal apa pun.  
- Menampilkan cara yang tepat untuk **memuat gambar untuk ocr** dan mengonfigurasi mesin untuk operasi offline.  

Semua ini dapat dimuat dalam satu aplikasi konsol C# yang berdiri sendiri.

## Langkah Selanjutnya & Topik Terkait

- **Batch processing** – iterasi melalui direktori PNG dan tulis setiap hasil ke file `.txt`.  
- **Different file formats** – coba `LoadImage` dengan TIFF atau BMP untuk pemindaian dengan fidelitas lebih tinggi.  
- **Performance tuning** – aktifkan pengenalan multi‑threaded jika Anda memiliki banyak core.  
- **Integration with ASP.NET Core** – expose endpoint API yang menerima gambar yang diunggah dan mengembalikan hasil OCR, tetap offline.

Jika Anda penasaran tentang penanganan PDF, lihat panduan kami tentang “mengenali teks dari PDF menggunakan Aspose PDF”. Untuk pra‑pemrosesan gambar yang lebih maju, pelajari binding C# OpenCV.

---

*Selamat coding! Jika Anda mengalami kendala, silakan tinggalkan komentar di bawah—saya akan berusaha membantu Anda mengekstrak teks dari gambar apa pun, sekecil apa pun tantangannya.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}