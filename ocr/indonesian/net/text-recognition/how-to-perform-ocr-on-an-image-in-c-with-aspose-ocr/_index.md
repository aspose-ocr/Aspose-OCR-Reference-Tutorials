---
category: general
date: 2026-10-18
description: Lakukan OCR pada gambar di C# dengan cepat. Pelajari cara mengekstrak
  teks dari JPG, mengonversi gambar menjadi teks, dan membaca teks dari gambar menggunakan
  Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: id
lastmod: 2026-10-18
og_description: Lakukan OCR pada gambar di C# dengan Aspose.OCR. Tutorial ini menunjukkan
  cara mengekstrak teks dari JPG, mengonversi gambar menjadi teks, dan membaca teks
  dari gambar dalam hitungan menit.
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: Lakukan OCR pada gambar di C# – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: Cara melakukan OCR pada gambar di C# dengan Aspose.OCR
url: /id/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR pada gambar di C# dengan Aspose.OCR

Jika Anda perlu **perform OCR on an image** dalam aplikasi .NET, panduan ini menunjukkan solusi lengkap yang siap‑to‑run. Anda akan melihat cara **load image for OCR**, mengenali karakter Cyrillic, dan **extract text from JPG** tanpa menulis kode pemrosesan gambar tingkat rendah.

Dalam tutorial ini Anda akan:

* Instal paket NuGet Aspose.OCR.  
* Muat file gambar (JPG, PNG, BMP, dll.).  
* Jalankan mesin OCR untuk **convert image to text**.  
* **Read text from image** output di konsol.  

Langkah-langkah ini bekerja dengan gambar apa pun yang kompatibel dengan .NET, sehingga Anda dapat menyesuaikannya untuk PDF, kwitansi yang dipindai, atau tangkapan layar.

## Prasyarat

* .NET 6.0 SDK atau yang lebih baru (kode juga berfungsi dengan .NET Framework 4.7+).  
* Visual Studio 2022 atau editor C# apa pun yang Anda sukai.  
* Akses internet untuk pertama kali menjalankan – Aspose.OCR mengunduh modul bahasa Cyrillic secara otomatis.  

> **Pro tip:** Jaga paket NuGet tetap up‑to‑date; versi yang lebih baru meningkatkan akurasi pengenalan dan menambahkan paket bahasa.

## Langkah 1: Instal Aspose.OCR

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Paket ini berisi kelas `OcrEngine` yang digunakan untuk **perform OCR on image**. Setelah perintah selesai, referensi paket muncul di file *.csproj* Anda.

## Langkah 2: Buat kerangka program konsol

Buat proyek konsol baru jika Anda belum memilikinya:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Ganti *Program.cs* yang dihasilkan dengan kode yang ditampilkan pada bagian berikut. Kerangka ini mencakup direktif `using` yang diperlukan dan metode `Main` yang menjalankan proses OCR.

## Langkah 3: Muat gambar untuk OCR

Baris kode fungsional pertama **loads the image** yang ingin Anda analisis. Aspose.OCR menerima stream apa pun, sehingga Anda dapat memuat file dari disk, URL web, atau sumber daya yang disematkan.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*Mengapa ini penting*: Menggunakan `ImageStream.FromFile` mengabstraksi penanganan format, memastikan mesin OCR menerima bitmap yang konsisten terlepas dari tipe file asli. Ini juga secara otomatis menutup stream berkat pernyataan `using`.

## Langkah 4: Inisialisasi mesin OCR dan atur bahasa (opsional)

Secara default Aspose.OCR mencoba mendeteksi bahasa secara otomatis. Untuk teks Cyrillic Anda dapat secara eksplisit meminta modul `Language.Cyrillic`, yang mempercepat pengunduhan pertama kali.

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

Jika Anda melewatkan penetapan bahasa, mesin akan mengunduh modul yang diperlukan pada pertama kali Anda memanggil `Recognize`. Pengunduhan terjadi melalui HTTPS dan disimpan dalam cache secara lokal untuk eksekusi berikutnya.

## Langkah 5: Lakukan OCR dan konversi gambar ke teks

Sekarang Anda benar‑benar **perform OCR on image** dan memperoleh string teks biasa. Metode `Recognize` melakukan semua pekerjaan berat: pra‑pemrosesan, analisis tata letak, dan klasifikasi karakter.

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

`recognizedText` yang dikembalikan berisi jeda baris yang sesuai dengan tata letak asli, memudahkan proses lanjutan atau penyimpanan ke basis data.

## Langkah 6: Tampilkan hasil – read text from image

Akhirnya, **read text from image** dengan menuliskan hasil ke konsol. Langkah ini memverifikasi bahwa OCR berhasil dan menunjukkan apa yang diekstrak.

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Saat Anda menjalankan program (`dotnet run`), Anda akan melihat output serupa dengan:

```
=== OCR Result ===
Пример текста на кириллице
```

> **Catatan:** Output tepatnya tergantung pada kualitas JPG sumber. Gambar yang jelas dan beresolusi tinggi menghasilkan hasil terbaik.

## Kode sumber lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke *Program.cs* dan jalankan tanpa modifikasi (kecuali jalur gambar).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Menjalankan program mencetak karakter yang diekstrak ke konsol, membuktikan bahwa Anda telah berhasil **extracted text from JPG** dan **converted image to text**.

## Menangani variasi umum

| Scenario | Adjustment |
|----------|------------|
| **Bahasa berbeda** | Set `engine.Language = Language.English;` atau enum lain yang didukung. |
| **PDF multi‑halaman** | Konversi setiap halaman menjadi gambar (mis., menggunakan `Aspose.PDF`) dan panggil loop OCR untuk setiap gambar. |
| **Batch besar** | Bungkus pemanggilan OCR dalam loop `Parallel.ForEach`; gunakan kembali satu instance `OcrEngine` untuk mengurangi beban memori. |
| **Gambar beresolusi rendah** | Pra‑proses dengan `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` untuk mengurangi noise sebelum pengenalan. |

## Tips kinerja

* **Cache language modules** – unduhan pertama mungkin memakan beberapa detik; eksekusi berikutnya instan. |
* **Reuse the `OcrEngine`** instance untuk beberapa gambar guna menghindari biaya inisialisasi berulang. |
* **Limit image size** – foto yang sangat besar meningkatkan penggunaan memori. Ubah ukuran menjadi maksimum 2000 px lebar sebelum memberi ke mesin. |

## Kesimpulan

Sekarang Anda tahu cara **perform OCR on image** file di C# menggunakan Aspose.OCR. Dengan memuat gambar, mengonfigurasi mesin, dan memanggil `Recognize`, Anda dapat **extract text from JPG**, **convert image to text**, dan **read text from image** hanya dengan beberapa baris kode.  

Dari sini Anda dapat menjelajahi:

* Menyimpan hasil OCR dalam basis data untuk arsip yang dapat dicari.  
* Mengintegrasikan alur kerja ke dalam API web yang menerima gambar yang diunggah.  
* Menggunakan modul bahasa lain (Arab, Hindi, dll.) untuk memperluas jangkauan aplikasi Anda.

Silakan bereksperimen dengan format gambar, bahasa, dan strategi pemrosesan batch yang berbeda. Pola inti—**load image for OCR → recognize → handle the plain‑text output**—tetap sama, memberikan Anda fondasi yang kuat untuk proyek ekstraksi teks apa pun.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun pada teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to extract text from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}