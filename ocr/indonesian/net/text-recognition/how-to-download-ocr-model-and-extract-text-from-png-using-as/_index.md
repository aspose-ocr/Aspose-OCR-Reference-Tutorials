---
category: general
date: 2026-09-16
description: Unduh model OCR dan ekstrak teks dari PNG dengan Aspose.OCR. Pelajari
  cara mengonversi gambar menjadi teks dan membaca teks dari gambar dalam C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- download OCR model
- extract text from PNG
- convert image to text
- recognize text from image
- read text from image
language: id
lastmod: 2026-09-16
og_description: Unduh model OCR dan ekstrak teks dari PNG di C#. Tutorial langkah
  demi langkah ini menunjukkan cara mengonversi gambar menjadi teks dan membaca teks
  dari gambar menggunakan Aspose.OCR.
og_image_alt: Diagram showing OCR engine loading a model, processing a PNG, and outputting
  recognized text
og_title: Unduh model OCR dan ekstrak teks dari PNG dengan Aspose.OCR – Panduan C#
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: download OCR model and extract text from PNG with Aspose.OCR. Learn
    to convert image to text and read text from image in C#.
  headline: How to download OCR model and extract text from PNG using Aspose.OCR in
    C#
  type: TechArticle
tags:
- OCR
- Aspose.OCR
- C#
- image-processing
title: Cara mengunduh model OCR dan mengekstrak teks dari PNG menggunakan Aspose.OCR
  di C#
url: /id/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengunduh model OCR dan mengekstrak teks dari PNG menggunakan Aspose.OCR di C#

Jika Anda perlu **mengunduh model OCR** untuk Aspose.OCR, panduan ini menunjukkan cara **mengekstrak teks dari PNG** dengan cepat dan andal. Anda akan melihat cara **mengonversi gambar menjadi teks**, **mengenali teks dari gambar**, dan akhirnya **membaca teks dari gambar** dalam aplikasi konsol C# yang bersih.

Tutorial ini mencakup semua yang Anda butuhkan—dari menginstal SDK hingga menangani jebakan umum—sehingga Anda dapat mengintegrasikan OCR ke dalam proyek .NET apa pun tanpa harus mencari sumber tambahan.

## Apa yang Anda butuhkan

| Prasyarat | Alasan |
|--------------|--------|
| .NET 6.0 SDK atau yang lebih baru | Menyediakan runtime untuk aplikasi konsol |
| Visual Studio 2022 (atau IDE apa pun) | Memudahkan pengeditan dan debugging |
| Paket NuGet Aspose.OCR untuk .NET | Menyediakan mesin OCR dan model bahasa |
| File gambar (`input.png`) yang berisi teks | Sumber yang akan Anda **convert image to text** |

Anda dapat menambahkan paket Aspose.OCR melalui konsol NuGet:

```bash
dotnet add package Aspose.OCR
```

> **Tips pro:** Pada pertama kali Anda mengatur properti `Language`, Aspose.OCR secara otomatis **mengunduh model OCR** ke cache lokal pengguna. Tidak diperlukan unduhan manual.

## Cara mengunduh model OCR untuk Aspose.OCR

Mesin OCR tidak menyertakan data bahasa secara bawaan untuk menjaga pustaka tetap ringan. Ketika Anda menetapkan sebuah bahasa (mis., Cyrillic) SDK memeriksa cache; jika model tidak ada, ia mengunduhnya dari CDN Aspose.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Models;   // contains Language enum
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Select the required language model.
        // This triggers a download if the model is not present locally.
        ocrEngine.Language = Language.Cyrillic;
        Console.WriteLine("OCR model for Cyrillic is ready.");
```

Baris `Console.WriteLine` mengonfirmasi bahwa langkah **download OCR model** selesai dengan sukses. Unduhan hanya terjadi sekali per mesin, setelah itu model yang di‑cache akan digunakan kembali.

### Mengapa unduhan otomatis penting

* **Reduced bundle size** – Aplikasi Anda tetap kecil karena paket bahasa diunduh sesuai permintaan.  
* **Up‑to‑date accuracy** – Aspose memperbarui model secara teratur; versi terbaru selalu diambil.  
* **Simplified deployment** – Tidak perlu menyertakan file `.dat` besar dalam installer Anda.  

## Cara mengekstrak teks dari PNG menggunakan C#

Dengan model bahasa siap, langkah berikutnya adalah memuat file PNG yang ingin Anda proses. PNG bersifat lossless, sehingga mempertahankan kualitas tepi teks dan meningkatkan akurasi pengenalan.

```csharp
        // Step 3: Load the image that contains the text.
        // ImageStream.FromFile reads the file into a stream compatible with Aspose.OCR.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
        Console.WriteLine("Image loaded successfully.");
```

> **Kasus khusus:** Jika PNG Anda menggunakan palet warna terindeks, konversikan ke RGB 24‑bit sebelum memberikannya ke mesin OCR untuk menghindari kesalahan pengenalan.

## Mengonversi gambar menjadi teks: mengenali teks dari gambar

Sekarang Anda menjalankan proses OCR. Metode `Recognize` melakukan semua pekerjaan berat—pra‑pemrosesan, segmentasi, klasifikasi karakter, dan pasca‑pemrosesan.

```csharp
        // Step 4: Run the OCR process.
        // Recognize returns an OcrResult object that holds the recognized text and confidence scores.
        OcrResult result = ocrEngine.Recognize();

        // Verify that the engine actually found text.
        if (result == null || string.IsNullOrWhiteSpace(result.Text))
        {
            Console.WriteLine("No text was recognized. Check image quality or language settings.");
            return;
        }
```

Objek `result` berisi tidak hanya string mentah tetapi juga properti opsional seperti `ResultPage` (untuk gambar multi‑halaman) dan `Confidence` (skor kepercayaan keseluruhan). Anda dapat menggunakan ini untuk validasi lanjutan atau umpan balik UI.

## Membaca teks dari gambar dan menangani hasil

Akhirnya, tampilkan atau simpan string yang dikenali. Ini adalah langkah **read text from image** yang menyelesaikan alur konversi.

```csharp
        // Step 5: Retrieve and display the recognized text.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);

        // Optional: Write the output to a .txt file for later processing.
        System.IO.File.WriteAllText("output.txt", result.Text);
        Console.WriteLine("Text saved to output.txt");
    }
}
```

**Output yang diharapkan** (contoh untuk gambar sederhana yang berisi “Hello World”):

```
=== Recognized Text ===
Hello World
Text saved to output.txt
```

### Variasi umum

| Variation | When to use | Code tweak |
|-----------|-------------|------------|
| **English language** | Sebagian besar dokumen Barat | `ocrEngine.Language = Language.English;` |
| **Multiple languages** | Halaman dengan bahasa campuran | `ocrEngine.Language = Language.English | Language.Russian;` |
| **Custom DPI scaling** | Pemindaian beresolusi rendah | `ocrEngine.Image = ImageStream.FromFile(...).Resize(2.0);` |
| **PDF input** | Ketika sumbernya adalah halaman PDF | Konversikan PDF ke gambar terlebih dahulu, kemudian berikan bitmap ke `ocrEngine.Image`. |

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin, tempel, dan jalankan. Ganti `YOUR_DIRECTORY` dengan jalur yang berisi `input.png`.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Models;
using System;

class Program
{
    static void Main()
    {
        // Create OCR engine instance (downloads model if needed)
        var ocrEngine = new OcrEngine();

        // Choose language – this triggers the automatic model download
        ocrEngine.Language = Language.Cyrillic;
        Console.WriteLine("OCR model for Cyrillic downloaded (if not cached).");

        // Load the PNG image containing the text
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
        Console.WriteLine("PNG image loaded.");

        // Perform OCR
        OcrResult result = ocrEngine.Recognize();

        // Validate result
        if (result == null || string.IsNullOrWhiteSpace(result.Text))
        {
            Console.WriteLine("No text recognized. Verify image quality or language settings.");
            return;
        }

        // Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);

        // Save to a file for further processing
        System.IO.File.WriteAllText("output.txt", result.Text);
        Console.WriteLine("Recognized text saved to output.txt");
    }
}
```

Jalankan program dengan:

```bash
dotnet run
```

Jika semuanya telah disiapkan dengan benar, konsol akan mencetak teks yang diekstrak dari `input.png` dan menuliskannya ke `output.txt`.

## Praktik terbaik dan pemecahan masalah

* **Image quality** – Targetkan setidaknya 300 dpi; gambar yang buram atau berisik menurunkan skor kepercayaan.  
* **Language selection** – Selalu sesuaikan bahasa dengan teks sumber. Bahasa yang tidak cocok menyebabkan output berantakan.  
* **Cache location** – Secara default Aspose menyimpan model di `%USERPROFILE%\.Aspose\Aspose.OCR`. Bersihkan folder hanya jika Anda perlu memaksa unduhan ulang.  
* **Performance** – Untuk pemrosesan batch, gunakan kembali satu instance `OcrEngine` alih-alih membuat yang baru untuk setiap gambar.  
* **Error handling** – Bungkus pemanggilan OCR dalam blok try‑catch untuk menangkap kesalahan jaringan selama unduhan model.  

## Kesimpulan

Anda kini tahu cara **download OCR model**, **extract text from PNG**, **convert image to text**, **recognize text from image**, dan **read text from image** menggunakan Aspose.OCR di C#. Contoh lengkap menunjukkan alur siap produksi yang dapat Anda kembangkan untuk konversi PDF, pemrosesan multi‑halaman, atau integrasi dengan pipeline analisis teks hilir.

**Langkah selanjutnya**

- Jelajahi **handwritten text recognition** dengan beralih ke `Language.EnglishHandwritten`.  
- Gabungkan OCR dengan **Aspose.PDF** untuk menyematkan teks yang diekstrak kembali ke PDF yang dapat dicari.  
- Bereksperimen dengan **image pre‑processing** (deskew, peningkatan kontras) untuk meningkatkan akurasi pada pemindaian ber kualitas rendah.

Silakan sesuaikan kode untuk proyek Anda sendiri, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image in C# – Offline OCR with Aspose (Step‑by‑Step Guide)](/ocr/english/net/text-recognition/extract-text-from-image-in-c-offline-ocr-with-aspose-step-by/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}