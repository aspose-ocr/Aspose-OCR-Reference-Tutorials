---
category: general
date: 2026-02-14
description: Cara melakukan OCR di C# menggunakan Aspose.OCR – pelajari cara mengekstrak
  teks dari gambar, memuat gambar dari file, dan menjalankan OCR pada gambar dengan
  cepat.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: id
og_description: Cara melakukan OCR di C# dengan Aspose.OCR. Panduan ini menunjukkan
  cara mengekstrak teks dari gambar, memuat gambar dari file, dan menjalankan OCR
  pada gambar secara efisien.
og_title: Cara Melakukan OCR di C# – Tutorial Pemrograman Lengkap
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cara Melakukan OCR di C# – Panduan Langkah demi Langkah
url: /id/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

ose website" but not a link. There's no markdown link. So fine.

Now produce final output with all content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Tutorial Pemrograman Lengkap

Pernah bertanya-tanya **bagaimana cara melakukan OCR** pada gambar yang baru saja Anda ambil dengan ponsel? Mungkin Anda perlu mengambil teks tanda jalan dari JPEG untuk aplikasi navigasi, atau Anda memiliki sekumpulan kontrak yang dipindai dan ingin mengubahnya menjadi teks yang dapat dicari. Singkatnya, Anda ingin *mengekstrak teks dari gambar* tanpa mengirim apa pun ke cloud.

Berita baiknya, Anda dapat melakukan semua itu secara lokal dengan Aspose.OCR untuk .NET. Dalam tutorial ini kami akan memandu Anda memuat gambar dari file, mengenali teks dari JPG, dan akhirnya **menjalankan OCR pada gambar** secara lengkap offline. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalankan yang mencetak teks Arab yang dikenali ke konsol.

> **Apa yang akan Anda dapatkan:** program C# yang berdiri sendiri dan dapat dijalankan, penjelasan mengapa setiap baris penting, serta tips untuk menangani kasus tepi umum seperti sumber daya yang hilang atau bahasa yang tidak didukung.

## Prasyarat

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6.0 atau lebih baru (atau .NET Framework 4.7+) | Aspose.OCR menargetkan .NET Standard 2.0, sehingga runtime modern apa pun dapat digunakan. |
| Visual Studio 2022 (atau VS Code dengan ekstensi C#) | IDE memudahkan mengelola paket NuGet dan menjalankan aplikasi console. |
| Paket NuGet Aspose.OCR (`Aspose.OCR`) | Ini adalah pustaka yang sebenarnya melakukan pekerjaan OCR. |
| Folder yang berisi sumber daya OCR offline (unduh dari Aspose) | Sumber daya offline menghindari panggilan HTTP selama pengenalan. |
| File gambar (mis., `arabic_sign.jpg`) | Kami akan menggunakan JPEG yang berisi teks Arab, tetapi bahasa apa pun dapat digunakan. |

Jika Anda belum memiliki salah satu dari ini, dapatkan sekarang—tidak ada gunanya memulai tutorial hanya untuk menemukan ketergantungan yang hilang di tengah jalan.

## Langkah 1: Instal Aspose.OCR dan Siapkan Sumber Daya

Pertama, tambahkan paket Aspose.OCR ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

Setelah paket terinstal, unduh **paket sumber daya OCR offline** dari situs web Aspose. Ekstrak ke sebuah folder di mesin Anda, misalnya:

```
C:\OCRResources\
```

> **Mengapa ini penting:** Memuat sumber daya sekali saat startup menghilangkan latensi jaringan dan membuat solusi Anda ramah GDPR karena tidak ada yang keluar dari mesin.

## Langkah 2: Buat Engine OCR dan Arahkan ke Folder Sumber Daya

Sekarang kami akan menginstansiasi kelas `Engine` dan memberi tahu di mana sumber daya berada. Ini adalah inti dari **cara melakukan OCR** secara lokal.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

> **Tips pro:** Bungkus pemanggilan `LoadResources` dalam blok try‑catch jika Anda menduga jalur folder mungkin salah. Pengecualian akan memberi tahu secara tepat file mana yang hilang.

## Langkah 3: Muat Gambar dari File

Selanjutnya, kita perlu **memuat gambar dari file** agar engine dapat menganalisisnya. Aspose.OCR bekerja dengan pembungkus `ImageStream` miliknya sendiri.

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

Jika gambar Anda berada di lokasi lain, cukup ubah jalurnya. Kelas `ImageStream` mengabstraksi penanganan bitmap di bawahnya, sehingga Anda tidak perlu khawatir tentang kompatibilitas GDI+.

## Langkah 4: Kenali Teks dari JPG Menggunakan Pengaturan Bahasa

Sekarang masuk ke inti **cara melakukan OCR**—yaitu mengenali karakter secara aktual. Kami akan meminta pengenalan bahasa Arab, tetapi Anda dapat mengganti `Language.Arabic` dengan bahasa lain yang didukung.

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

> **Mengapa menentukan bahasa?** Engine OCR menggunakan kamus dan model karakter khusus bahasa. Menyediakan bahasa yang tepat secara dramatis meningkatkan akurasi, terutama untuk skrip dengan bentuk kompleks seperti Arab.

## Langkah 5: Tampilkan Teks yang Diekstrak

Akhirnya, mari **ekstrak teks dari gambar** dan cetak ke layar. Ini adalah cara paling sederhana untuk memverifikasi bahwa OCR berhasil.

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

Saat Anda menjalankan program, Anda akan melihat frasa Arab yang ada pada tanda tercetak di konsol. Jika output terlihat berantakan, periksa kembali bahwa bahasa yang tepat telah dipilih dan folder sumber daya berisi file data Arab.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap dikompilasi yang menggabungkan semua langkah. Salin‑tempel ke proyek console baru (`dotnet new console`) dan tekan **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Output yang diharapkan (contoh):**

```
=== OCR Result ===
مطار القاهره الدولي
```

Jika Anda mengganti gambar dengan tanda berbahasa Inggris dan mengatur `Language.English`, kode yang sama akan menghasilkan teks Inggris. Itu menunjukkan betapa fleksibelnya **menjalankan OCR pada gambar**.

## Ekstrak Teks dari Gambar – Menangani Skenario Umum

### 1. Beberapa Halaman atau Gambar Multi‑Frame

Beberapa format gambar (seperti TIFF) dapat berisi beberapa halaman. Untuk **mengekstrak teks dari gambar** dalam kasus tersebut, lakukan loop pada setiap frame:

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. Gambar Resolusi Rendah

Akurasi OCR turun drastis di bawah 70 dpi. Jika Anda mendapatkan hasil yang buram, pertimbangkan untuk memperbesar gambar terlebih dahulu:

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. Paket Bahasa Hilang

Jika Anda mendapatkan pengecualian seperti *“Language data not found”*, periksa kembali bahwa file `.dat` yang bersangkutan ada di `ResourceFolder` Anda. Aspose menyediakan zip terpisah untuk setiap bahasa.

## Menjalankan OCR pada Gambar – Tips Kinerja

- **Cache the Engine:** Membuat `Engine` baru untuk setiap gambar menambah beban. Simpan satu instance tetap hidup untuk pemrosesan batch.
- **Parallelize Safely:** `Engine` aman untuk operasi baca‑saja setelah `LoadResources`. Anda dapat memulai beberapa tugas yang masing‑masing memanggil `Recognize` pada gambar yang berbeda.
- **Dispose When Done:** Meskipun `Engine` mengimplementasikan `IDisposable`, GC .NET akan membersihkan pada akhirnya. Memanggil secara eksplisit `ocrEngine.Dispose()` dalam blok `using` adalah kebiasaan yang baik.

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## Kenali Teks dari JPG – Kasus Tepi yang Perlu Diwaspadai

| Situasi | Apa yang Diperiksa | Perbaikan |
|-----------|-------------------|-----------|
| **Corrupted JPEG** | `ImageStream.FromFile` throws `FileNotFoundException` or `ArgumentException`. | Verifikasi integritas file, mungkin simpan ulang gambar dengan editor grafis. |
| **Unsupported language** | `Language` enum doesn’t contain your target language. | Perbarui Aspose.OCR ke versi terbaru; bahasa baru ditambahkan secara berkala. |
| **Mixed‑script images** (e.g., English + Arabic) | Opsi bahasa tunggal mungkin melewatkan skrip sekunder. | Jalankan OCR dua kali dengan opsi bahasa berbeda dan gabungkan hasilnya. |

## Ringkasan – Anda Sekarang Tahu Cara Melakukan OCR di C#

Dalam panduan ini kami membahas **cara melakukan OCR** menggunakan Aspose.OCR, mulai dari menginstal paket NuGet hingga mencetak teks yang dikenali. Anda belajar **memuat gambar dari file**, **mengekstrak teks dari gambar**, **mengenali teks dari jpg**, dan dengan aman **menjalankan OCR pada gambar** dalam cara yang siap produksi.

### Apa Selanjutnya?

- **Eksperimen dengan format file lain** seperti PNG atau BMP—cukup ubah ekstensi file.
- **Integrasikan dengan basis data** untuk menyimpan hasil OCR bagi arsip yang dapat dicari.
- **Gabungkan dengan computer‑vision** (mis., deteksi wilayah teks sebelum OCR) untuk meningkatkan kecepatan.

Silakan ubah pengaturan bahasa, proses folder secara batch, atau hubungkan output ke API web. OCR adalah blok bangunan; kekuatan sebenarnya muncul ketika Anda mengintegrasikannya ke dalam alur kerja yang lebih besar.

Selamat coding, dan semoga gambar Anda selalu jernih!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}