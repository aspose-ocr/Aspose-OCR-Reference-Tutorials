---
category: general
date: 2026-04-01
description: Pelajari cara mengubah gambar struk menjadi teks menggunakan Aspose OCR.
  Panduan ini menunjukkan cara mengekstrak teks Cyrillic, memuat gambar untuk OCR,
  dan mengenali karakter Cyrillic secara efisien.
draft: false
keywords:
- receipt image to text
- extract cyrillic text
- load image for ocr
- recognize cyrillic characters
- create OCR engine
language: id
og_description: Ubah gambar struk menjadi teks dengan Aspose OCR. Pelajari cara mengekstrak
  teks Cyrillic, memuat gambar untuk OCR, dan mengenali karakter Cyrillic dalam C#.
og_title: Gambar Kwitansi ke Teks – OCR Cyrillic dengan Aspose
tags:
- OCR
- C#
- Aspose
- Cyrillic
title: gambar kwitansi ke teks – OCR Cyrillic dengan Aspose
url: /id/net/text-recognition/receipt-image-to-text-cyrillic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# gambar kwitansi ke teks – OCR Cyrillic dengan Aspose

Pernahkah Anda perlu mengubah **gambar kwitansi menjadi teks** tetapi karakternya semuanya Cyrillic? Anda bukan satu-satunya yang kebingungan dengan hal ini. Dalam banyak aplikasi ritel atau akuntansi, kwitansi muncul dalam skrip Rusia, Bulgaria, atau Serbia, dan Anda tetap menginginkan string yang bersih dan dapat dicari.  

Dalam tutorial ini kami akan menunjukkan secara tepat cara **mengekstrak teks Cyrillic** dari foto kwitansi, **memuat gambar untuk OCR**, dan **mengenali karakter Cyrillic** menggunakan pustaka Aspose OCR. Pada akhir tutorial Anda akan memiliki program C# siap‑jalankan yang menulis hasil OCR ke file `.txt`.

## Apa yang Anda Butuhkan

- **.NET 6** (atau versi .NET terbaru) – kode ini juga berfungsi pada .NET Framework 4.7+.  
- **Aspose.OCR for .NET** paket NuGet – `Install-Package Aspose.OCR`.  
- Contoh gambar kwitansi yang berisi teks Cyrillic (misalnya `cyrillic_receipt.jpg`).  
- Lingkungan pengembangan – Visual Studio, VS Code, atau Rider sudah cukup.  

Tidak ada dependensi native tambahan yang diperlukan; Aspose menyertakan model bahasa dan menangani proses berat secara internal.

## gambar kwitansi ke teks – Menyiapkan OCR Engine

Hal pertama yang harus kita lakukan adalah membuat instance **OCR engine** dan memberi tahu bahasa yang kita minati. Aspose membuat ini sangat mudah:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;   // language and resource handling
using System.Drawing;      // Image class
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Tell Aspose we want Cyrillic support
        ocrEngine.Language = Language.Cyrillic;

        // Optional: Pre‑load the model if you’ll run offline later
        // ResourceManager.Preload(Language.Cyrillic);
```

> **Pro tip:** Memuat model terlebih dahulu menghindari panggilan jaringan pada kali pertama Anda menjalankan program, yang berguna untuk skenario desktop atau embedded.

## Cara mengekstrak teks Cyrillic – Memuat gambar kwitansi

Setelah engine siap, kita perlu **memuat gambar untuk OCR**. Kelas `System.Drawing.Image` bekerja dengan sempurna untuk sebagian besar format bitmap.

```csharp
        // Step 3: Point to your receipt image
        string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

        // Step 4: Load the image inside a using block (ensures disposal)
        using (var image = Image.FromFile(imagePath))
        {
            // Step 5: Run the OCR process
            var recognitionResult = ocrEngine.Recognize(image);
```

Jika file tidak ditemukan, `Image.FromFile` akan melempar `FileNotFoundException`. Anda mungkin ingin membungkus seluruh proses dalam blok `try…catch` untuk kode produksi.

## Mengenali karakter Cyrillic – Mengambil teks

Objek `recognitionResult` berisi teks mentah, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti. Untuk konversi sederhana “gambar kwitansi ke teks” kami cukup menulis properti `Text` ke sebuah file:

```csharp
            // Step 6: Write the extracted text to a .txt file
            string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
            File.WriteAllText(outputPath, recognitionResult.Text);

            // Quick verification: print to console
            Console.WriteLine("OCR completed. Extracted text:");
            Console.WriteLine(recognitionResult.Text);
        }
    }
}
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
OCR completed. Extracted text:
СЧЕТ № 12345
Дата: 01/04/2026
Товар      Кол-во   Цена
Хлеб       2        30,00
Молоко     1        45,00
Итого:               105,00
```

Itulah hasil **gambar kwitansi ke teks** yang Anda cari.

![receipt image to text example](receipt-ocr-example.png "Example of a receipt image being converted to text")

*Teks alt gambar: konversi gambar kwitansi ke teks menampilkan karakter Cyrillic yang diekstrak oleh Aspose OCR.*

## Kasus Edge & Pertanyaan Umum

### Bagaimana jika model bahasa belum diunduh?

Aspose secara otomatis mengunduh model yang diperlukan pada kali pertama Anda mengatur `ocrEngine.Language = Language.Cyrillic;`. Jika mesin tidak memiliki internet, langkah pre‑load opsional akan gagal. Dalam kasus tersebut, sediakan model secara manual (lihat dokumentasi Aspose) atau pastikan perangkat dapat mengakses `download.aspose.com`.

### Bagaimana cara menangani banyak bahasa dalam satu kwitansi?

Anda dapat memberikan daftar yang dipisahkan koma:

```csharp
ocrEngine.Language = Language.Cyrillic | Language.English;
```

Aspose akan berusaha mengenali karakter dari kedua set.

### Kwitansi saya buram – bisakah saya meningkatkan akurasi?

Aspose OCR menawarkan pra‑pemrosesan gambar dasar:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Sharpen = true,
    Binarize = true,
    Denoise = true
};
```

Terapkan ini sebelum memanggil `Recognize`.

### Bagaimana dengan pemrosesan batch besar?

Bungkus loop pengenalan dalam `Parallel.ForEach` dan gunakan kembali instance `OcrEngine` yang sama (aman untuk thread setelah model dimuat). Ingatlah untuk mengunci engine jika Anda menemukan masalah keamanan thread.

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabungkan)

Berikut adalah program lengkap yang siap disalin‑tempel yang menggabungkan pre‑load opsional dan penanganan error dasar:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        try
        {
            // Create OCR engine and select Cyrillic language
            var ocrEngine = new OcrEngine();
            ocrEngine.Language = Language.Cyrillic;

            // Optional: preload model for offline use
            // ResourceManager.Preload(Language.Cyrillic);

            // Path to the receipt image
            string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

            // Verify the file exists
            if (!File.Exists(imagePath))
                throw new FileNotFoundException("Receipt image not found.", imagePath);

            using (var image = Image.FromFile(imagePath))
            {
                // Perform OCR
                var result = ocrEngine.Recognize(image);

                // Output path for extracted text
                string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
                File.WriteAllText(outputPath, result.Text);

                Console.WriteLine("✅ receipt image to text conversion succeeded.");
                Console.WriteLine("Extracted text saved to: " + outputPath);
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine("❌ An error occurred: " + ex.Message);
        }
    }
}
```

Jalankan program (`dotnet run` dari folder proyek) dan Anda akan mendapatkan file `.txt` dengan output **gambar kwitansi ke teks**.

## Kesimpulan

Anda kini memiliki solusi menyeluruh, end‑to‑end untuk mengubah **gambar kwitansi menjadi teks**—khususnya untuk skrip Cyrillic—menggunakan Aspose OCR. Kami telah membahas cara **membuat OCR engine**, **memuat gambar untuk OCR**, **mengekstrak teks Cyrillic**, dan **mengenali karakter Cyrillic** dalam hanya beberapa baris C#.  

Langkah selanjutnya? Coba proses folder berisi kwitansi, bereksperimen dengan `ImagePreprocessor` untuk meningkatkan akurasi, atau gabungkan output OCR dengan basis data untuk pembukuan otomatis. Jika Anda perlu menangani alfabet lain, ganti `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}