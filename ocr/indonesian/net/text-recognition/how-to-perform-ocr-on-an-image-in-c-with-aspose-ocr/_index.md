---
category: general
date: 2026-10-21
description: Pelajari cara melakukan OCR pada JPG, mengekstrak teks dari gambar, dan
  memuat gambar untuk OCR menggunakan Aspose.OCR di C#. Panduan lengkap langkah demi
  langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from jpg
- load image for OCR
- perform OCR on image
language: id
lastmod: 2026-10-21
og_description: Cara melakukan OCR pada gambar di C# dengan Aspose.OCR. Ikuti panduan
  ini untuk memuat gambar untuk OCR, mengenali teks dari JPG, dan mengekstrak teks
  dari gambar.
og_image_alt: Screenshot showing how to perform OCR on a Cyrillic image in C#
og_title: Cara melakukan OCR pada gambar di C# – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to perform OCR on a JPG, extract text from image and load
    image for OCR using Aspose.OCR in C#. Complete step‑by‑step guide.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
- Image processing
- Text extraction
title: Cara melakukan OCR pada gambar di C# dengan Aspose.OCR
url: /id/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR pada gambar di C# dengan Aspose.OCR

Jika Anda perlu **cara melakukan OCR** pada sebuah gambar, tutorial ini menunjukkan solusi lengkap yang siap dijalankan. Anda akan belajar cara memuat gambar untuk OCR, mengenali teks dari file JPG, dan mengekstrak teks dari gambar menggunakan pustaka Aspose.OCR.

Panduan ini mencakup semua hal mulai dari menginstal paket NuGet hingga menangani model bahasa dan mencetak hasil yang dikenali. Pada akhir tutorial Anda akan dapat mengintegrasikan OCR ke dalam proyek .NET apa pun dan memproses teks Cyrillic atau bahasa lain tanpa meninggalkan IDE.

## Apa yang Anda butuhkan

- .NET 6.0 atau lebih baru (kode juga berfungsi pada .NET Framework 4.7+)
- Visual Studio 2022 (atau editor C# apa saja)
- Akses internet untuk pertama kali dijalankan (Aspose.OCR mengunduh model bahasa secara otomatis)
- Gambar contoh, misalnya `cyrillic_sample.jpg`, ditempatkan di folder yang dapat Anda referensikan dari kode

## Langkah 1: Instal Aspose.OCR

Buka NuGet Package Manager dan tambahkan **Aspose.OCR** ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

Paket ini berisi mesin OCR, model bahasa, dan kelas pembantu yang diperlukan untuk pemrosesan gambar. Tidak ada DLL tambahan yang diperlukan.

## Langkah 2: Buat mesin OCR – cara melakukan OCR

Tugas nyata pertama dalam **cara melakukan OCR** adalah menginstansiasi mesin. Objek ini mengelola seluruh pipeline pengenalan.

```csharp
using Aspose.OCR;

// Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

`OcrEngine` ringan; Anda dapat menggunakan kembali instance yang sama untuk beberapa gambar, yang meningkatkan kinerja saat memproses batch.

## Langkah 3: Memuat gambar untuk OCR

Sebelum pengenalan Anda harus menyediakan data gambar. Langkah **memuat gambar untuk OCR** menerima banyak format, tetapi contoh ini fokus pada file JPEG.

```csharp
// Load the image you want to process
engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

`OcrImage.FromFile` membaca file ke memori dan menyiapkannya untuk mesin. Jika jalur file tidak valid, `ArgumentException` akan dilempar, jadi pastikan jalurnya benar.

## Langkah 4: Pilih bahasa yang sesuai (opsional tetapi disarankan)

Jika gambar Anda berisi karakter Cyrillic, atur bahasa ke `Cyrillic`. Model yang diperlukan akan diunduh secara otomatis pada eksekusi pertama.

```csharp
// Choose the language model
engine.Language = OcrLanguage.Cyrillic;
```

Anda dapat beralih ke bahasa lain (misalnya `OcrLanguage.English`) dengan mengubah properti ini. Pustaka ini mendukung lebih dari 60 bahasa.

## Langkah 5: Kenali teks dari JPG – cara melakukan OCR pada JPEG

Sekarang panggil metode `Recognize`. Ini adalah inti dari **cara melakukan OCR** dan menerjemahkan bitmap menjadi teks Unicode.

```csharp
// Perform the recognition
engine.Recognize();
```

Metode ini akan memblokir hingga proses OCR selesai. Untuk gambar besar Anda mungkin ingin menjalankannya pada thread latar belakang agar UI tetap responsif.

## Langkah 6: Ekstrak teks dari gambar

Setelah pengenalan, mesin menyimpan hasilnya di properti `Text`. Ini menyelesaikan langkah **mengekstrak teks dari gambar**.

```csharp
// Retrieve the extracted text
string extractedText = engine.Text;

// Output the recognized text to the console
Console.WriteLine(extractedText);
```

Output akan berisi karakter persis yang ditemukan dalam gambar, mempertahankan jeda baris dan tanda baca.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua langkah memberikan satu program yang dapat Anda salin, tempel, dan jalankan:

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image for OCR
        engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");

        // Step 3: Choose the language model (Cyrillic in this case)
        engine.Language = OcrLanguage.Cyrillic;

        // Step 4: Perform OCR on the image
        engine.Recognize();

        // Step 5: Extract text from image
        string extractedText = engine.Text;

        // Step 6: Output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

### Output yang diharapkan

Jika `cyrillic_sample.jpg` berisi frasa “Привет мир” (Hello world), konsol akan menampilkan:

```
=== OCR Result ===
Привет мир
```

Font atau kualitas gambar yang berbeda dapat memengaruhi akurasi, tetapi Aspose.OCR umumnya mencapai >95 % pengenalan pada cetakan yang jelas.

## Jebakan umum dan tips praktis

- **Kualitas gambar penting** – JPEG beresolusi rendah atau berisik mengurangi akurasi. Pralakukan gambar (mis., tingkatkan kontras) menggunakan `engine.Image.AdjustContrast()` bila diperlukan.
- **Unduhan model bahasa** – eksekusi pertama mengunduh model ke `%USERPROFILE%\.Aspose\OCR`. Pastikan proses memiliki izin menulis.
- **Pemrosesan batch** – gunakan kembali instance `OcrEngine` yang sama dan hanya ubah `engine.Image` di antara file. Ini menghindari pemuatan model berulang.
- **Penggunaan memori** – gambar besar mengonsumsi lebih banyak RAM. Panggil `engine.Image.Dispose()` setelah setiap pengenalan jika Anda memproses banyak file dalam loop.
- **Keamanan thread** – `OcrEngine` tidak thread‑safe. Buat instance terpisah per thread saat memparalelkan.

## Kesimpulan

Anda kini tahu **cara melakukan OCR** pada JPEG, **memuat gambar untuk OCR**, dan **mengekstrak teks dari gambar** menggunakan Aspose.OCR di C#. Solusi lengkap ini menunjukkan cara mengatur bahasa, mengenali teks dari JPG, dan mencetak hasilnya, memberi Anda fondasi yang kuat untuk proyek ekstraksi teks apa pun.

Selanjutnya, jelajahi topik terkait seperti **melakukan OCR pada gambar** secara batch, mengintegrasikan OCR dengan API ASP.NET Core, atau mengonversi teks yang diekstrak menjadi PDF yang dapat dicari. Bereksperimenlah dengan bahasa berbeda dan pra‑pemrosesan gambar untuk memaksimalkan kualitas pengenalan.

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Melakukan OCR di C# – Mengonversi Gambar ke Teks dengan Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/)
- [Cara Melakukan OCR di C# – Mengenali Teks dari Gambar](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/)
- [Cara mengekstrak teks dari gambar menggunakan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}