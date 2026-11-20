---
category: general
date: 2026-11-20
description: Cara menggunakan OCR di C# untuk mengenali teks dari gambar. Pelajari
  cara memuat OCR gambar, mengatur bahasa OCR, dan mengekstrak teks dari file JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text image
- load image OCR
- recognize text JPEG
- set OCR language
language: id
lastmod: 2026-11-20
og_description: Cara menggunakan OCR di C# untuk mengekstrak teks dari gambar. Panduan
  ini menunjukkan cara memuat gambar, mengatur bahasa OCR, dan mengenali teks dari
  file JPEG.
og_image_alt: Screenshot of C# code demonstrating how to use OCR to recognize text
  from an image
og_title: Cara menggunakan OCR di C# – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to use OCR in C# to recognize text from an image. Learn to load
    image OCR, set OCR language, and extract text from JPEG files.
  headline: How to use OCR in C# with image recognition
  type: TechArticle
tags:
- OCR
- C#
- Image processing
- Text extraction
title: Cara menggunakan OCR di C# dengan pengenalan gambar
url: /id/net/text-recognition/how-to-use-ocr-in-c-with-image-recognition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan OCR di C# dengan pengenalan gambar

Jika Anda perlu **cara menggunakan OCR** dalam aplikasi C#, panduan ini akan membawa Anda melalui seluruh proses. Baik Anda mendigitalkan kontrak yang dipindai maupun mengekstrak informasi dari foto, Anda akan belajar **mengenali teks gambar** dengan cepat dan andal.

Tutorial ini mencakup memuat gambar, mengonfigurasi mesin OCR, dan mengambil teks yang dikenali dari file JPEG. Pada akhir tutorial Anda akan memiliki contoh yang berdiri sendiri, dapat dijalankan, dan dapat dimasukkan ke proyek .NET mana pun.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 (atau lebih baru) terpasang.
* Akses ke pustaka OCR yang menyediakan `OcrEngine`, `ImageStream`, dan modul bahasa (misalnya, **Leadtools**, **Aspose.OCR**, atau paket kompatibel lainnya).
* Sebuah gambar contoh bernama `sample.jpg` di direktori yang diketahui.

Tidak ada layanan eksternal tambahan yang diperlukan—mesin OCR akan mengunduh paket bahasa yang hilang secara otomatis.

## Langkah 1: Muat gambar untuk OCR

Memuat gambar adalah langkah pertama dalam setiap alur kerja OCR. Kode di bawah ini membuat `ImageStream` dari file JPEG di disk.

```csharp
// Step 1: Load the image to be recognized
var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
var image = ImageStream.FromFile(imagePath);
```

*Mengapa ini penting:* Objek `ImageStream` mengabstraksi penanganan file dan menyediakan data piksel yang dikonsumsi oleh mesin OCR. Jika file tidak ditemukan, `FromFile` akan melemparkan pengecualian yang jelas, sehingga proses debug menjadi mudah.

## Langkah 2: Buat instance mesin OCR (auto‑dispose)

Menggunakan blok `using` menjamin bahwa sumber daya yang tidak dikelola dibebaskan segera setelah pekerjaan OCR selesai.

```csharp
// Step 2: Create an OCR engine instance (automatically disposes when done)
using var ocrEngine = new OcrEngine();
```

*Tips profesional:* Pernyataan `using` lebih disarankan dibandingkan pemanggilan manual `Dispose()` karena menghilangkan risiko lupa membebaskan memori native, yang dapat menyebabkan kebocoran memori pada layanan yang berjalan lama.

## Langkah 3: Atur bahasa OCR (opsional tetapi disarankan)

Jika Anda mengetahui bahasa dokumen sumber, mengaturnya akan meningkatkan akurasi dan mempercepat pemrosesan. Contoh ini mengatur bahasa ke Cyrillic; Anda dapat menggantinya dengan enum bahasa yang didukung apa pun.

```csharp
// Step 3 (optional): Specify the language module, e.g., Cyrillic
// The required language pack will be downloaded automatically if missing
ocrEngine.Language = OcrLanguage.Cyrillic;
```

*Mengapa mengatur bahasa?* Mesin OCR memiliki model karakter yang spesifik per bahasa. Dengan memilih yang tepat, Anda mengurangi hasil positif palsu dan menghindari substitusi karakter yang tidak diperlukan.

## Langkah 4: Lakukan OCR pada gambar yang telah dimuat

Sekarang mesin memproses bitmap dan mengembalikan teks yang dikenali sebagai string.

```csharp
// Step 4: Perform OCR on the loaded image
string recognizedText = ocrEngine.Recognize(image);
```

*Kasus tepi:* Jika gambar beresolusi rendah atau sangat terkompresi, mesin mungkin mengembalikan hasil parsial. Pertimbangkan pra‑pemrosesan (misalnya, binarisasi) untuk hasil yang lebih baik.

## Langkah 5: Keluarkan teks yang dikenali

Akhirnya, tampilkan teks yang diekstrak di konsol atau teruskan ke komponen lain.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

**Output yang diharapkan**

```
=== Recognized Text ===
Пример текста, полученного из изображения.
```

Konten tepatnya tergantung pada gambar sumber, tetapi konsol akan menampilkan string lengkap yang dideteksi oleh mesin OCR.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua langkah menghasilkan program ringkas yang dapat Anda kompilasi dan jalankan segera.

```csharp
using System;
using System.IO;

// Ensure you reference the OCR library that provides these types
// e.g., using Leadtools.OCR;

class Program
{
    static void Main()
    {
        // Load the image to be recognized
        var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
        var image = ImageStream.FromFile(imagePath);

        // Create an OCR engine instance (auto‑dispose)
        using var ocrEngine = new OcrEngine();

        // Optional: set the language (Cyrillic in this case)
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // Perform OCR
        string recognizedText = ocrEngine.Recognize(image);

        // Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

Salin kode ke proyek konsol baru, ganti `YOUR_DIRECTORY` dengan path ke gambar Anda, dan jalankan `dotnet run`. Program akan mencetak teks yang dikenali ke konsol.

## Pertanyaan umum dan pemecahan masalah

| Pertanyaan | Jawaban |
|----------|--------|
| **Bagaimana jika paket bahasa tidak diunduh?** | Pustaka OCR akan berusaha mengunduhnya secara otomatis. Pastikan mesin memiliki akses internet, atau pra‑instal paket bahasa sesuai dokumentasi pustaka. |
| **Apakah saya dapat mengenali teks dari file PNG atau BMP?** | Ya. `ImageStream.FromFile` bekerja dengan format apa pun yang didukung oleh pustaka gambar di bawahnya. Cukup ubah ekstensi file. |
| **Bagaimana cara meningkatkan akurasi untuk pemindaian yang berisik?** | Lakukan pra‑pemrosesan gambar (penyesuaian kontras, penghapusan noise) sebelum mengirimnya ke `Recognize`. Banyak pustaka menyediakan kelas `ImageProcessor` untuk tujuan ini. |
| **Apakah aman menjalankan OCR pada file yang diunggah pengguna?** | Validasi ukuran dan tipe file, serta jalankan OCR dalam lingkungan sandbox untuk menghindari payload berbahaya. |

## Kesimpulan

Anda kini tahu **cara menggunakan OCR** di C# untuk **mengenali teks gambar**, **memuat gambar OCR**, **mengatur bahasa OCR**, dan **mengenali teks JPEG** secara andal. Contoh lengkap menunjukkan alur kerja yang bersih dan dapat dibuang, yang dapat Anda kembangkan dengan pra‑pemrosesan tambahan, dukungan multi‑bahasa, atau integrasi ke pipeline pemrosesan dokumen yang lebih besar.

### Langkah selanjutnya

* Jelajahi pemrosesan batch dengan melakukan iterasi pada direktori berisi JPEG.  
* Gabungkan OCR dengan Natural Language Processing (NLP) untuk mengekstrak data terstruktur.  
* Bereksperimen dengan modul bahasa lain seperti `OcrLanguage.English` atau `OcrLanguage.Arabic`.  

Silakan sesuaikan kode dengan kebutuhan spesifik Anda, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Use Windows.Media.Ocr to recognize text image in C# – Full OCR Guide](/ocr/english/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/)
- [How to Use OCR in C# – Extract Text from Image Asynchronously](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/)
- [How to Use OCR in C# – Extract Text from Image with Aspose OCR](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}