---
category: general
date: 2026-08-22
description: Pelajari cara mengenali teks dari gambar menggunakan Aspose.OCR. Panduan
  ini juga mencakup OCR gambar ke teks dan mengekstrak teks dari JPG dalam beberapa
  langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- ocr image to text
- extract text from jpg
- convert image to text
- read cyrillic text image
language: id
lastmod: 2026-08-22
og_description: Mengenali teks dari gambar menggunakan Aspose.OCR di C#. Ikuti tutorial
  ini untuk OCR gambar menjadi teks, mengekstrak teks dari jpg, dan membaca gambar
  teks Cyrillic.
og_image_alt: Screenshot of C# console output showing recognized Cyrillic text from
  a JPG image
og_title: Mengenali teks dari gambar dengan Aspose.OCR – panduan langkah demi langkah
  C#
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: Learn to recognize text from image using Aspose.OCR. This guide also
    covers OCR image to text and extract text from jpg in a few steps.
  headline: How to recognize text from image with Aspose.OCR in C#
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Cara mengenali teks dari gambar dengan Aspose.OCR di C#
url: /id/net/text-recognition/how-to-recognize-text-from-image-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali teks dari gambar dengan Aspose.OCR – tutorial lengkap C# 

Jika Anda perlu mengenali teks dari gambar dalam proyek .NET, tutorial ini menunjukkan solusi siap‑jalan. Anda akan melihat cara menyiapkan mesin OCR, memilih modul bahasa yang tepat, dan menghasilkan karakter yang diekstrak. Contoh ini juga menunjukkan cara melakukan OCR gambar ke teks untuk gambar Cyrillic, yang mencakup kasus umum membaca file gambar teks Cyrillic.

Selain langkah-langkah inti, Anda akan belajar cara mengekstrak teks dari file jpg, mengonversi gambar ke teks untuk format lain, dan menangani situasi di mana modul bahasa harus diunduh secara otomatis. Tidak ada layanan eksternal yang diperlukan selain paket NuGet Aspose.OCR.

## Prasyarat

- .NET 6.0 SDK atau yang lebih baru terinstal  
- Visual Studio 2022 (atau editor apa pun yang mendukung C#)  
- Akses internet untuk menjalankan pertama kali (modul bahasa Cyrillic diunduh sesuai permintaan)  
- Paket NuGet Aspose.OCR (`dotnet add package Aspose.OCR`)  

Item-item ini memungkinkan Anda mengompilasi dan menjalankan kode tanpa konfigurasi tambahan.

## Langkah 1: Buat proyek konsol baru

Buka terminal dan jalankan perintah berikut untuk membuat aplikasi konsol minimal:

```bash
dotnet new console -n ImageOcrDemo
cd ImageOcrDemo
dotnet add package Aspose.OCR
```

Perintah `dotnet new console` membuat file `Program.cs` dan file proyek yang merujuk ke pustaka Aspose.OCR. Menambahkan paket menyelesaikan semua assembly yang diperlukan.

## Langkah 2: Impor namespace Aspose.OCR

Edit **Program.cs** dan tambahkan direktif `using Aspose.OCR;` di bagian atas file. Ini membuat kelas OCR tersedia tanpa nama lengkap.

```csharp
using System;
using Aspose.OCR;
```

Pernyataan `using` meningkatkan keterbacaan dan menjaga kode tetap fokus pada alur kerja OCR.

## Langkah 3: Inisialisasi mesin OCR

Buat instance `OcrEngine`. Mesin ini menyimpan konfigurasi seperti modul bahasa dan pengaturan pengenalan.

```csharp
// Initialise the OCR engine
var ocrEngine = new OcrEngine();
```

Membuat mesin satu kali per aplikasi efisien karena pustaka native yang mendasarinya hanya dimuat satu kali.

## Langkah 4: Pilih modul bahasa

Untuk teks Cyrillic, set properti `Language` ke `Language.Cyrillic`. Aspose.OCR secara otomatis mengunduh modul jika belum ada, sehingga eksekusi pertama mungkin memakan beberapa detik.

```csharp
// Choose Cyrillic language module – it will be downloaded if absent
ocrEngine.Language = Language.Cyrillic;
```

Jika Anda kemudian perlu melakukan OCR gambar ke teks dalam bahasa lain (mis., Inggris atau Arab), ganti `Language.Cyrillic` dengan nilai enum yang sesuai. Fleksibilitas ini memungkinkan Anda mengonversi gambar ke teks untuk skrip apa pun yang didukung.

## Langkah 5: Kenali teks dari file JPG

Panggil `RecognizeImage` dengan jalur lengkap ke gambar. Metode ini mengembalikan `OcrResult` yang berisi string yang diekstrak.

```csharp
// Path to the source image – replace with your own file
string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

// Perform OCR – this extracts text from the JPG file
OcrResult result = ocrEngine.RecognizeImage(imagePath);
```

Pemanggilan ini bekerja dengan format gambar raster apa pun yang didukung oleh Aspose.OCR (JPG, PNG, BMP, TIFF). Menggunakan JPG memastikan Anda dapat mengekstrak teks dari file jpg tanpa langkah konversi tambahan.

## Langkah 6: Keluarkan teks yang dikenali

Akhirnya, tulis teks yang dikenali ke konsol. Ini menunjukkan cara sederhana membaca gambar teks Cyrillic dan menampilkannya.

```csharp
// Show the recognised text in the console
Console.WriteLine("Recognised text:");
Console.WriteLine(result.Text);
```

Saat Anda menjalankan program, Anda akan melihat karakter Cyrillic dicetak persis seperti yang muncul di gambar sumber.

## Contoh kerja lengkap

Berikut adalah file **Program.cs** lengkap yang dapat Anda salin, tempel, dan jalankan segera.

```csharp
using System;
using Aspose.OCR;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Choose the language module required for recognition (Cyrillic in this case)
            // The language module will be downloaded automatically if not present
            ocrEngine.Language = Language.Cyrillic;

            // Step 3: Provide the path to the image you want to process
            // You can replace the file name with any JPG, PNG, BMP, or TIFF image
            string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

            // Step 4: Recognise text from the image file
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Step 5: Output the recognised text
            Console.WriteLine("Recognised text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

### Output yang diharapkan

```
Recognised text:
Пример текста на кириллице
```

Output tepat tergantung pada konten `sample_image.jpg`. Jika gambar berisi teks Inggris, kode yang sama akan mengembalikan string Inggris selama Anda mengatur `ocrEngine.Language = Language.English;`.

## Menangani jebakan umum

| Masalah | Mengapa terjadi | Cara mengatasinya |
|-------|----------------|----------------|
| Modul bahasa tidak ditemukan | Eksekusi pertama mencoba mengunduh modul tetapi proses gagal karena pembatasan firewall. | Pastikan mesin dapat mengakses `https://downloads.aspose.com/ocr` atau unduh modul secara manual dari portal Aspose dan letakkan di folder default (`%APPDATA%\Aspose\OCR\`). |
| Akurasi rendah pada gambar berisik | Mesin OCR bergantung pada kontras yang jelas antara teks dan latar belakang. | Pra‑proses gambar (mis., tingkatkan kontras, konversi ke grayscale) sebelum memanggil `RecognizeImage`. Aspose.OCR menyediakan opsi `ImagePreprocessing` yang dapat Anda jelajahi. |
| Format non‑JPG | Beberapa pengembang menganggap kode hanya berfungsi dengan file JPG. | API juga menerima PNG, BMP, dan TIFF. Ubah ekstensi file di `imagePath` sesuai. |
| File besar menyebabkan waktu pemrosesan lama | Gambar yang lebih besar membutuhkan lebih banyak memori dan siklus CPU. | Ubah ukuran gambar ke resolusi yang wajar (mis., 1500 × 1500) sebelum pengenalan. |

Tips ini membantu Anda mengonversi gambar ke teks secara andal di berbagai skenario.

## Memperluas solusi

Setelah Anda dapat mengenali teks dari gambar, Anda mungkin ingin:

- **Simpan hasil ke file** – tulis `result.Text` ke dokumen `.txt` atau `.docx`.  
- **Proses batch folder** – iterasi semua file dalam direktori dan terapkan logika OCR yang sama.  
- **Gabungkan dengan ekspresi reguler** – ekstrak nomor telepon, tanggal, atau pola lain dari string yang dikenali.  

Semua ekstensi ini menggunakan kembali kode inti yang sama, menjaga implementasi tetap ringkas.

## Kesimpulan

Anda kini memiliki panduan lengkap untuk mengenali teks dari gambar menggunakan Aspose.OCR dalam C#. Tutorial ini mencakup cara menyiapkan proyek, menginisialisasi mesin OCR, memilih modul bahasa Cyrillic, dan mengekstrak teks dari file JPG. Dengan mengikuti langkah‑langkah ini Anda juga dapat melakukan OCR gambar ke teks untuk bahasa lain, mengekstrak teks dari file jpg, dan mengonversi gambar ke teks dalam aplikasi .NET apa pun.

Silakan bereksperimen dengan bahasa tambahan, batch yang lebih besar, atau logika pasca‑pemrosesan. Jika Anda perlu membaca gambar teks Cyrillic dalam konteks berbeda—seperti API web atau layanan Windows—pola yang sama berlaku. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [ocr preprocessing pipeline – How to Recognize Text from Image in C#](/ocr/english/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}