---
category: general
date: 2026-11-14
description: Pelajari cara mengenali gambar menjadi teks menggunakan Aspose OCR dalam
  C#. Panduan langkah demi langkah ini juga mencakup cara mengekstrak teks dari JPG
  dan mengonversi gambar menjadi teks secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize image to text
- extract text from jpg
- perform OCR on image
- convert image to text
- recognize text from image
language: id
lastmod: 2026-11-14
og_description: Mengenali gambar menjadi teks dengan Aspose OCR di C#. Ikuti tutorial
  lengkap ini untuk mengekstrak teks dari jpg, melakukan OCR pada gambar, dan mengubah
  gambar menjadi teks.
og_image_alt: Screenshot of C# code that recognize image to text using Aspose OCR
og_title: Mengenali gambar menjadi teks dengan Aspose OCR – Panduan C#
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  headline: How to recognize image to text with Aspose OCR in C#
  type: TechArticle
- description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  name: How to recognize image to text with Aspose OCR in C#
  steps:
  - name: Large images
    text: Large files increase memory usage and processing time. Resize the image
      to a maximum of 2000 px on the longest side before calling `RecognizeImage`.
  - name: Missing language model
    text: If the required language pack cannot be downloaded (e.g., offline environment),
      the engine throws `IOException`. Wrap the call in a try‑catch block and provide
      a fallback language.
  - name: Asynchronous processing
    text: For UI applications, avoid blocking the UI thread. Wrap the recognition
      call in `Task.Run`.
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cara mengenali gambar menjadi teks dengan Aspose OCR di C#
url: /id/net/text-recognition/how-to-recognize-image-to-text-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengenali gambar menjadi teks dengan Aspose OCR di C#

Jika Anda perlu mengenali gambar menjadi teks dalam aplikasi .NET, panduan ini menunjukkan langkah‑langkah tepat yang diperlukan. Anda akan melihat cara mengekstrak teks dari file jpg, melakukan OCR pada data gambar, dan mengonversi gambar menjadi teks dengan kode minimal.

Tutorial ini mencakup semua hal mulai dari menginstal paket NuGet Aspose.OCR hingga menangani hasil OCR dengan aman. Tidak diperlukan layanan eksternal, dan kode dapat dijalankan pada .NET 6 atau yang lebih baru.

## Instal paket Aspose OCR

Sebelum menulis kode apa pun, tambahkan pustaka Aspose.OCR ke proyek Anda. Paket ini menyertakan semua model bahasa dan secara otomatis mengunduh file yang diperlukan saat runtime.

```bash
dotnet add package Aspose.OCR
```

Perintah ini menambahkan versi stabil terbaru **Aspose.OCR** ke `csproj` Anda. Langkah ini memastikan Anda dapat memanggil `OcrEngine` tanpa harus mengelola DLL secara manual.

## Buat dan konfigurasikan mesin OCR

Membuat mesin OCR adalah tindakan programatik pertama yang harus Anda lakukan. Mesin ini mengelola pemuatan gambar, pemilihan bahasa, dan pengenalan.

```csharp
using Aspose.OCR;

// Step 1: Instantiate the OCR engine (required modules are downloaded automatically)
OcrEngine ocrEngine = new OcrEngine();
```

`OcrEngine` adalah kelas inti yang melakukan pekerjaan berat. Menginstansiasikannya memicu inisialisasi ringan; pustaka mengunduh paket bahasa hanya ketika Anda memilih sebuah bahasa.

## Pilih model bahasa (ekstrak teks dari jpg)

Memilih model bahasa yang tepat memengaruhi akurasi. Untuk teks Cyrillic, tetapkan `OcrLanguage.Cyrillic`. Pada pertama kali Anda menetapkan bahasa yang belum ada di cache lokal, Aspose akan mengunduh model tersebut di latar belakang.

```csharp
// Step 2: Choose the language model – triggers download if needed
ocrEngine.Language = OcrLanguage.Cyrillic;
```

Jika Anda bekerja dengan skrip Latin, gantilah `Cyrillic` dengan `English` atau nilai enum lainnya. Jalur kode yang sama **perform OCR on image** terlepas dari bahasa yang dipilih.

## Kenali teks dari file JPG (konversi gambar menjadi teks)

Sekarang Anda dapat memberi file gambar ke mesin. Metode `RecognizeImage` menerima jalur file, stream, atau `Bitmap`. Di sini kami menggunakan JPEG karena merupakan format umum untuk dokumen yang dipindai.

```csharp
// Step 3: Recognize text from the image file
OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");
```

Metode ini mengembalikan objek `OcrResult` yang berisi string mentah, skor kepercayaan, dan informasi tata letak opsional. Panggilan ini **recognize text from image** dalam satu baris.

## Tampilkan hasil OCR (ekstrak teks dari jpg)

Setelah pengenalan, keluarkan teks yang terdeteksi ke konsol atau serahkan ke komponen lain.

```csharp
// Step 4: Display the recognized text
Console.WriteLine(ocrResult.Text);
```

Output konsol tipikal terlihat seperti:

```
Пример текста на кириллице
```

Jika gambar tidak mengandung karakter yang dapat dibaca, `ocrResult.Text` akan menjadi string kosong. Selalu periksa kondisi ini sebelum memproses lebih lanjut.

## Tangani kasus tepi umum

### Gambar besar

File besar meningkatkan penggunaan memori dan waktu pemrosesan. Ubah ukuran gambar menjadi maksimum 2000 px pada sisi terpanjang sebelum memanggil `RecognizeImage`.

```csharp
using System.Drawing;

// Load, resize, then recognize
using (Bitmap original = new Bitmap("YOUR_DIRECTORY/large-sample.jpg"))
{
    int maxDim = 2000;
    int width = original.Width;
    int height = original.Height;

    if (width > maxDim || height > maxDim)
    {
        float scale = Math.Min((float)maxDim / width, (float)maxDim / height);
        int newWidth = (int)(width * scale);
        int newHeight = (int)(height * scale);
        using (Bitmap resized = new Bitmap(original, newWidth, newHeight))
        {
            OcrResult result = ocrEngine.RecognizeImage(resized);
            Console.WriteLine(result.Text);
        }
    }
    else
    {
        OcrResult result = ocrEngine.RecognizeImage(original);
        Console.WriteLine(result.Text);
    }
}
```

### Model bahasa tidak tersedia

Jika paket bahasa yang diperlukan tidak dapat diunduh (misalnya, lingkungan offline), mesin akan melempar `IOException`. Bungkus pemanggilan dalam blok try‑catch dan sediakan bahasa cadangan.

```csharp
try
{
    ocrEngine.Language = OcrLanguage.Cyrillic;
    OcrResult result = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(result.Text);
}
catch (IOException ex)
{
    Console.WriteLine($"Language model download failed: {ex.Message}");
    // Fallback to English
    ocrEngine.Language = OcrLanguage.English;
    OcrResult fallback = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(fallback.Text);
}
```

### Pemrosesan asynchronous

Untuk aplikasi UI, hindari memblokir thread UI. Bungkus panggilan pengenalan dalam `Task.Run`.

```csharp
await Task.Run(() =>
{
    OcrResult asyncResult = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(asyncResult.Text);
});
```

## Tips praktis untuk OCR yang andal

- **Pra‑proses gambar**: Terapkan konversi ke grayscale dan peningkatan kontras untuk meningkatkan akurasi ketika Anda **perform OCR on image** dengan pencahayaan buruk.
- **Pilih bahasa yang tepat**: Selalu tetapkan `ocrEngine.Language` sebelum pengenalan. Defaultnya adalah English, yang menghasilkan akurasi rendah untuk skrip Cyrillic atau Asia.
- **Validasi output**: Gunakan regular expression untuk memverifikasi bahwa teks yang dikenali sesuai dengan pola yang diharapkan (misalnya, tanggal, ID) sebelum menyimpannya.
- **Cache paket bahasa**: Unduhan pertama mungkin memakan beberapa detik. Deploy paket yang diperlukan bersama aplikasi Anda jika memerlukan start‑up instan.

## Contoh lengkap

Berikut adalah program mandiri yang mendemonstrasikan seluruh alur kerja—dari instalasi paket hingga menampilkan hasil OCR.

```csharp
// -----------------------------------------------------------
// Recognize image to text with Aspose OCR – complete example
// -----------------------------------------------------------
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1. Create the OCR engine (modules are downloaded automatically)
        OcrEngine ocrEngine = new OcrEngine();

        // 2. Select the language model – triggers download if missing
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 3. Recognize text from a JPG file (convert image to text)
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");

        // 4. Output the recognized string (extract text from jpg)
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output konsol yang diharapkan**

```
Recognized text:
Пример текста на кириллице
```

Menjalankan program pada gambar lain (misalnya, faktur berbahasa Inggris) hanya memerlukan perubahan pada enum `Language` dan jalur file. Kode yang sama **recognize text from image** tanpa modifikasi.

## Kesimpulan

Anda kini tahu cara mengenali gambar menjadi teks dengan Aspose OCR di C#. Tutorial ini mencakup instalasi pustaka, pembuatan dan konfigurasi mesin OCR, konversi gambar menjadi teks, serta penanganan kasus tepi umum. Dengan fondasi ini Anda dapat **extract text from jpg**, **perform OCR on image** data berukuran apa pun, dan mengintegrasikan hasilnya ke dalam alur kerja .NET yang lebih besar.

Selanjutnya, jelajahi fitur lanjutan seperti:

- **OCR PDF multi‑halaman** (gunakan `PdfInput` alih‑alih JPG)
- **Daftar putih karakter khusus** untuk meningkatkan akurasi kode numerik
- **Menyimpan hasil OCR sebagai PDF yang dapat dicari** dengan `OcrEngine.Save`.

Bereksperimenlah dengan model bahasa berbeda dan teknik pra‑proses gambar untuk mencapai tingkat pengenalan terbaik bagi domain Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [kenali teks dari gambar di C# – panduan langkah‑demi‑langkah Aspose OCR](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/)
- [kenali teks dari gambar dengan Aspose OCR – Panduan Async C# Lengkap](/ocr/english/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-async-g/)
- [kenali teks dari gambar di C# – Tutorial Aspose OCR Lengkap](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}