---
category: general
date: 2026-02-22
description: mengenali teks dari gambar menggunakan Aspose OCR di C#. Panduan langkah
  demi langkah untuk mengekstrak teks dari png, mengonversi gambar menjadi teks, dan
  membaca sumber daya tersemat C# untuk lisensi.
draft: false
keywords:
- recognize text from image
- extract text from png
- convert image to text
- read embedded resource c#
- perform ocr on image
language: id
og_description: Mengenali teks dari gambar secara instan dengan Aspose OCR. Pelajari
  cara mengekstrak teks dari PNG, mengonversi gambar menjadi teks, dan membaca sumber
  daya tersemat C# untuk lisensi yang mulus.
og_title: Mengenali teks dari gambar dalam C# – Tutorial Lengkap Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Mengenali teks dari gambar di C# dengan Aspose OCR
url: /id/net/text-recognition/recognize-text-from-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar di C# dengan Aspose OCR

Pernah membutuhkan untuk **recognize text from image** tetapi tidak yakin harus mulai dari mana di C#? Anda tidak sendirian—sebagian besar pengembang mengalami hal yang sama saat pertama kali bertemu OCR. Dalam tutorial ini kami akan langsung menyelami solusi yang berfungsi yang memungkinkan Anda **extract text from png**, **convert image to text**, dan bahkan **read embedded resource c#** untuk lisensi tanpa kesulitan.  

Kami akan membahas semuanya mulai dari memuat lisensi Aspose OCR yang ter-embed hingga mencetak string akhir di konsol. Pada akhir tutorial Anda akan memiliki program mandiri yang dapat Anda masukkan ke proyek .NET apa pun dan jalankan hari ini.

## Apa yang Anda Butuhkan

- **.NET 6+** (kode dapat dikompilasi pada .NET Framework juga, tetapi .NET 6 adalah LTS saat ini)
- **Aspose.OCR for .NET** paket NuGet (versi 23.9 atau lebih baru)
- Sebuah gambar **sample PNG** yang berisi teks bahasa Inggris yang jelas dan tercetak
- Sebuah **Aspose OCR license file** (`Aspose.OCR.lic`) yang ditambahkan ke proyek Anda sebagai *Embedded Resource*  

Jika ada yang terdengar tidak familiar, jangan khawatir—setiap langkah di bawah ini menjelaskan cara menyiapkannya.

## Langkah 1: Membaca Embedded Resource C# License  

Sebelum mesin OCR dapat bekerja, Aspose memerlukan lisensi yang valid. Menyimpan file `.lic` sebagai embedded resource menjaga file tersebut tetap di luar pohon sumber dan membuat penyebaran menjadi mudah.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Load the embedded Aspose OCR license
        // ------------------------------------------------------------
        var assembly = Assembly.GetExecutingAssembly();

        // The resource name follows the folder hierarchy in the project.
        // Adjust "MyApp.Resources.Aspose.OCR.lic" if yours differs.
        using (var licenseStream = assembly.GetManifestResourceStream(
               "MyApp.Resources.Aspose.OCR.lic"))
        {
            if (licenseStream == null)
            {
                Console.Error.WriteLine(
                    "License file not found. Make sure it's marked as Embedded Resource.");
                return;
            }

            var license = new License();
            license.SetLicenseFromStream(licenseStream);
        }

        // Continue with OCR steps...
```

**Mengapa ini penting:**  
Menyematkan lisensi mencegah paparan tidak sengaja di kontrol sumber dan menjamin file tersebut ikut bersama DLL yang dikompilasi. Jika aliran (`stream`) bernilai `null`, program akan berhenti lebih awal—ini adalah pemeriksaan defensif pertama kami.

## Langkah 2: Menginisialisasi OCR Engine (Melakukan OCR pada Gambar)  

Sekarang lisensi sudah dimuat, kita dapat membuat instance `OcrEngine`. Kami akan mengatur bahasa ke English karena itu yang digunakan oleh sample PNG kami.

```csharp
        // ------------------------------------------------------------
        // 2️⃣ Initialise the OCR engine – this is where we perform OCR on image
        // ------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // change to Language.French etc. if needed
        };
```

**Tip:** Enum `Language` mendukung lebih dari 30 bahasa. Mengganti bahasa semudah `Language.Spanish`. Jika Anda membutuhkan deteksi multi‑bahasa, buat instance engine terpisah atau gunakan `ocrEngine.AutoDetectLanguage = true` (tersedia pada versi Aspose yang lebih baru).

## Langkah 3: Memuat Gambar PNG (Extract Text from PNG)  

Aspose OCR bekerja dengan kelas `Image` miliknya sendiri, bukan `System.Drawing.Image`. Arahkan ke jalur file, atau berikan `Stream` jika Anda lebih suka.

```csharp
        // ------------------------------------------------------------
        // 3️⃣ Load the image – this is the step where we extract text from png
        // ------------------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/sample.png";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Image not found at {imagePath}");
            return;
        }

        var image = Image.Load(imagePath);
```

**Edge case:** Jika PNG Anda mengandung kanal alfa (latar belakang transparan), Aspose mungkin salah menafsirkan spasi putih. Solusi cepat adalah memproses gambar terlebih dahulu dengan `ImageProcessor` untuk meratakan, tetapi untuk kebanyakan dokumen yang dipindai pemuat default sudah cukup baik.

## Langkah 4: Menjalankan Pengakuan (Convert Image to Text)  

Dengan engine dan gambar siap, pemanggilan OCR sebenarnya hanya satu baris. Objek hasil memberikan string mentah dan skor kepercayaan.

```csharp
        // ------------------------------------------------------------
        // 4️⃣ Recognise the image – this is where we convert image to text
        // ------------------------------------------------------------
        var ocrResult = ocrEngine.Recognize(image);

        // Optional: check confidence (0‑100)
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

**Mengapa Anda mungkin peduli dengan confidence:**  
Confidence rendah (mis., < 70%) biasanya menandakan pemindaian yang buram atau font yang tidak didukung. Dalam produksi Anda dapat beralih ke engine OCR lain atau meminta pengguna untuk memindai ulang.

## Langkah 5: Mengoutput Teks yang Diakui  

Akhirnya, cetak string yang diekstrak. Dalam aplikasi nyata Anda mungkin menuliskannya ke basis data, file JSON, atau memasukkannya ke indeks pencarian.

```csharp
        // ------------------------------------------------------------
        // 5️⃣ Output the recognised text – the final result of recognize text from image
        // ------------------------------------------------------------
        Console.WriteLine("\n--- Recognised Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Output Konsol yang Diharapkan

```
Confidence: 96%
--- Recognised Text ---
Hello, world!
This is a sample PNG used for OCR testing.
```

Jika Anda melihat teks di atas (atau sesuatu yang serupa), selamat—Anda telah berhasil **recognize text from image** dengan Aspose OCR!

## Kesalahan Umum & Cara Menghindarinya  

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| `License not set` exception | File lisensi tidak di-embed atau nama resource salah | Verifikasi `Build Action = Embedded Resource` dan periksa kembali nama lengkap (fully‑qualified) |
| Output kosong | DPI gambar terlalu rendah (di bawah 150) | Ulangi sampling PNG menjadi setidaknya 150 DPI sebelum diberikan ke Aspose |
| Karakter kacau | Bahasa yang dipilih salah | Setel `ocrEngine.Language` ke nilai enum `Language` yang benar |
| `OutOfMemoryException` pada gambar besar | Memuat PNG besar (10 MB+) secara langsung | Gunakan `Image.Load(stream, maxWidth: 2000, maxHeight: 2000)` untuk mengurangi ukuran secara langsung |

## Pro Tip: Pemrosesan Batch  

Jika Anda perlu **recognize text from image** file secara massal, bungkus logika inti dalam loop `foreach` dan gunakan kembali instance `OcrEngine` yang sama. Menggunakan kembali engine menghemat beberapa milidetik per file karena pustaka native yang mendasari tetap terload.

```csharp
var images = System.IO.Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var path in images)
{
    var img = Image.Load(path);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{path} → {result.Text.Trim()}");
}
```

## Langkah Selanjutnya  

- **Fine‑tune preprocessing** – coba `ImageProcessor` untuk meningkatkan kontras atau menghilangkan noise.  
- **Explore other output formats** – `ocrResult.GetWords()` memberikan bounding box, berguna untuk menyorot teks di UI.  
- **Combine with Azure Cognitive Services** jika Anda membutuhkan dukungan tulisan tangan berbasis cloud.  

Semua ekstensi tersebut masih mengandalkan pola inti yang sama: memuat lisensi, membuat engine, memberi gambar, dan membaca teks.

![Tangkapan layar konsol yang menampilkan teks yang dikenali dari gambar](/images/ocr-result.png "screenshot hasil mengenali teks dari gambar")

## Kesimpulan  

Kami telah melewati contoh lengkap yang siap produksi yang menunjukkan cara **recognize text from image** di C# menggunakan Aspose OCR. Dari membaca embedded resource untuk lisensi hingga memuat PNG, melakukan OCR, dan mencetak hasil, setiap bagian telah dibahas.  

Sekarang Anda dapat **extract text from png**, **convert image to text**, dan bahkan **read embedded resource c#** untuk lisensi—semua dalam beberapa lusin baris kode. Jangan ragu untuk bereksperimen dengan bahasa yang berbeda, batch gambar yang lebih besar, atau mengintegrasikan output ke dalam pipeline pemrosesan dokumen Anda sendiri. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}