---
category: general
date: 2026-01-09
description: Tutorial OCR c# yang menunjukkan cara mengekstrak teks dari file gambar
  dan mengonversi DJVU menjadi teks menggunakan Aspose.OCR. Pelajari ekstraksi langkah
  demi langkah dalam hitungan menit.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- how to extract text
- convert djvu to text
- extract text from djvu
language: id
og_description: Tutorial OCR c# yang dengan cepat menunjukkan cara mengekstrak teks
  dari file gambar dan mengonversi DJVU ke teks menggunakan Aspose.OCR. Ikuti panduan
  untuk solusi yang berfungsi.
og_title: Tutorial OCR c# – Ekstrak teks dari gambar & DJVU
tags:
- OCR
- C#
- Aspose
title: 'Tutorial OCR c#: Ekstrak teks dari gambar dan file DJVU'
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial OCR c# – Ekstrak teks dari gambar dan file DJVU

Pernah bertanya-tanya bagaimana cara mengekstrak teks dari file gambar tanpa membuat frustasi? Dalam **c# OCR tutorial** ini kami akan membahas contoh lengkap yang siap dijalankan yang mengekstrak teks dari gambar biasa *dan* dokumen DJVU.  

Jika Anda juga mencari cara cepat untuk **convert DJVU to text**, Anda berada di tempat yang tepat—tanpa konverter tambahan, hanya kode C# murni.

## Apa yang akan Anda pelajari

- Cara menyiapkan library Aspose.OCR dalam proyek .NET.  
- Kode tepat yang Anda butuhkan untuk **extract text from image** file.  
- Metode singkat untuk **extracting text from DJVU** file (ya, mesin yang sama melakukannya).  
- Kesalahan umum (file besar, font yang hilang, lisensi) dan cara menghindarinya.  

Yang Anda butuhkan hanyalah .NET SDK terbaru dan koneksi internet untuk mengambil paket NuGet. Tidak diperlukan pengalaman OCR sebelumnya.

## Prasyarat

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | Aspose.OCR menargetkan .NET Standard 2.0, jadi .NET 6+ memberikan kinerja terbaik. |
| Visual Studio 2022 (or VS Code) | IDE membuat manajemen paket menjadi mudah, tetapi editor apa pun dapat digunakan. |
| NuGet package **Aspose.OCR** | Ini adalah engine yang sebenarnya melakukan pekerjaan berat. |
| A sample image (`sample.png`) and a DJVU file (`sample.djvu`) | Kami akan menggunakan ini untuk mendemonstrasikan kedua skenario ekstraksi. |

Anda dapat menginstal paket dengan perintah berikut:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda berada di server CI, tambahkan `--no-restore` ke langkah build dan lakukan restore sekali di awal untuk mempercepat proses.

## Langkah 1: Inisialisasi engine OCR – inti dari tutorial c# OCR

Hal pertama yang kami lakukan adalah membuat instance `OcrEngine`. Anggap saja ini seperti menyalakan pemindai dalam perangkat lunak Anda.

```csharp
using Aspose.OCR;

var ocrEngine = new OcrEngine();
```

Mengapa membuat engine baru setiap kali? Karena engine menyimpan konfigurasi (bahasa, mode deteksi, dll.). Dengan memulai baru Anda menghindari pengaturan lama yang bocor antar proses.

## Langkah 2: Muat dan kenali gambar – cara mengekstrak teks dari gambar

Sekarang kami akan memasukkan bitmap biasa (PNG, JPEG, BMP…) ke dalam engine. Metode `RecognizeImage` mengembalikan string yang terdeteksi.

```csharp
// Path to your image file
string imagePath = @"C:\OCR\sample.png";

// Perform OCR
string imageText = ocrEngine.RecognizeImage(imagePath);

// Show the result
Console.WriteLine("=== Text extracted from image ===");
Console.WriteLine(imageText);
```

Beberapa hal yang perlu dicatat:

* **File existence** – Jika path salah, metode akan melempar `FileNotFoundException`. Bungkus dengan `try/catch` jika Anda mengharapkan path yang diberikan pengguna.
* **Image quality** – OCR bekerja paling baik pada 300 dpi atau lebih tinggi. Scan beresolusi rendah dapat menghasilkan output yang kacau.
* **Language support** – Secara default Aspose.OCR mengasumsikan bahasa Inggris. Untuk mengubahnya, set `ocrEngine.Language = Language.Spanish;` sebelum `RecognizeImage`.

## Langkah 3: Kenali teks dari dokumen DJVU – convert DJVU to text

DJVU adalah format kontainer yang dapat menyimpan banyak halaman. Aspose.OCR dapat menangani langsung; Anda hanya perlu menunjuk ke file.

```csharp
// Path to your DJVU file
string djvuPath = @"C:\OCR\sample.djvu";

// Perform OCR on the DJVU file
string djvuText = ocrEngine.RecognizeImage(djvuPath);

// Output the result
Console.WriteLine("\n=== Text extracted from DJVU ===");
Console.WriteLine(djvuText);
```

Di balik layar, engine mengekstrak setiap halaman sebagai gambar dan menjalankan pipeline pengenalan yang sama. Itulah mengapa Anda tidak memerlukan langkah terpisah “convert DJVU to text”—engine OCR melakukannya untuk Anda.

### Menangani file DJVU multi‑halaman

Jika DJVU Anda berisi beberapa halaman, `RecognizeImage` menggabungkannya secara berurutan. Jika Anda membutuhkan setiap halaman secara terpisah, Anda dapat menggunakan overload yang mengembalikan `List<string>`:

```csharp
var pagesText = ocrEngine.RecognizeImage(djvuPath, true); // true = return per‑page list
for (int i = 0; i < pagesText.Count; i++)
{
    Console.WriteLine($"\n--- Page {i + 1} ---");
    Console.WriteLine(pagesText[i]);
}
```

## Langkah 4: Sesuaikan engine untuk akurasi lebih baik – mengapa ini penting

Hasil bawaan sudah cukup baik, tetapi Anda dapat meningkatkannya dengan menyesuaikan beberapa pengaturan:

```csharp
ocrEngine.Language = Language.English;      // set detection language
ocrEngine.Dpi = 300;                        // enforce 300 DPI processing
ocrEngine.IsDetectOrientation = true;      // auto‑rotate tilted pages
ocrEngine.IsDetectSkew = true;              // correct slanted text
```

Flag ini sangat berguna ketika **how to extract text** dari PDF yang dipindai dan pertama kali disimpan sebagai DJVU. Mengaktifkan deteksi orientasi menghindarkan Anda dari harus memutar gambar secara manual.

## Langkah 5: Menangani lisensi dan error runtime

Aspose.OCR dilengkapi dengan trial gratis yang menambahkan “Demo” pada output setelah beberapa halaman. Untuk menghapus watermark, tambahkan file lisensi Anda:

```csharp
// Assuming you have a license.xml in the project root
var license = new Aspose.OCR.License();
license.SetLicense("license.xml");
```

Jika Anda lupa langkah ini, engine tetap berfungsi, tetapi hasilnya akan berisi kata “Demo”. Juga, waspadai `OutOfMemoryException` saat memproses file DJVU yang sangat besar—pertimbangkan memproses halaman per halaman seperti yang ditunjukkan sebelumnya.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program konsol mandiri yang menggabungkan semuanya. Salin‑tempel, sesuaikan path file, dan tekan **Run**.

```csharp
// Complete c# OCR tutorial – extract text from image and DJVU
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Set up licensing (optional, removes demo watermark)
            // var license = new License();
            // license.SetLicense("license.xml");

            // 2️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = Language.English,
                Dpi = 300,
                IsDetectOrientation = true,
                IsDetectSkew = true
            };

            // 👉 Extract text from a regular image
            string imagePath = @"C:\OCR\sample.png";
            try
            {
                string imageText = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("=== Text extracted from image ===");
                Console.WriteLine(imageText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Image OCR failed: {ex.Message}");
            }

            // 👉 Extract text from a DJVU file (convert DJVU to text)
            string djvuPath = @"C:\OCR\sample.djvu";
            try
            {
                // Single string for all pages
                string djvuText = ocrEngine.RecognizeImage(djvuPath);
                Console.WriteLine("\n=== Text extracted from DJVU ===");
                Console.WriteLine(djvuText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"DJVU OCR failed: {ex.Message}");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Output yang diharapkan** (asumsi file berisi frasa “Hello World”):

```
=== Text extracted from image ===
Hello World

=== Text extracted from DJVU ===
Hello World
```

Jika sumber berisi beberapa baris, mereka akan muncul persis seperti di dokumen asli.

## Pertanyaan umum & penanganan kasus tepi

* **What if the image is black‑and‑white?**  
  OCR berfungsi dengan baik, tetapi Anda dapat meningkatkan kontras dengan `ocrEngine.ImagePreprocessOptions = ImagePreprocessOptions.Contrast;`.

* **Can I extract only numbers?**  
  Ya—set `ocrEngine.CharWhitelist = "0123456789";` sebelum memanggil `RecognizeImage`.

* **Is there a limit on file size?**  
  Engine membaca seluruh file ke memori. Untuk file lebih besar dari ~100 MB, proses per halaman (lihat overload list pada Langkah 3).

* **How does this differ from Tesseract?**  
  Aspose.OCR adalah library komersial dengan dukungan DJVU bawaan dan tanpa dependensi native, sedangkan Tesseract memerlukan binary native dan alat konversi DJVU terpisah.

## Kesimpulan

Anda baru saja menyelesaikan **c# OCR tutorial** yang menunjukkan cara **extract text from image** file dan secara mulus **convert DJVU to text** menggunakan Aspose.OCR. Contoh ini mencakup semua hal mulai dari instalasi paket hingga lisensi, dari ekstraksi gambar satu halaman hingga penanganan DJVU multi‑halaman, bahkan tips untuk meningkatkan akurasi.  

Selanjutnya, Anda dapat mengeksplorasi **how to extract text** dari PDF, mengintegrasikan langkah OCR ke dalam API web, atau bereksperimen dengan paket bahasa untuk dokumen multibahasa. Tidak ada batasan—ingat poin penting: atur engine, beri file, dan baca kembali stringnya.  

Ada pertanyaan lain? Tinggalkan komentar, coba kode pada dokumen Anda sendiri, dan selamat coding! 

![c# OCR tutorial screenshot showing console output](/images/csharp-ocr-tutorial.png "c# OCR tutorial – console output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}