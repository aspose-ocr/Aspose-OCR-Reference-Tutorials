---
category: general
date: 2026-03-05
description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  membaca file gambar di C#, mengonversi DJVU menjadi teks, dan dapatkan hasil OCR
  gambar ke string dengan cepat.
draft: false
keywords:
- extract text from image
- read image file c#
- convert djvu to text
- ocr image to string
- recognize text from djvu
language: id
og_description: Ekstrak teks dari gambar dengan Aspose OCR di C#. Panduan ini menunjukkan
  cara membaca file gambar di C#, mengonversi DJVU ke teks, dan menangani OCR gambar
  menjadi string dengan mudah.
og_title: Ekstrak teks dari gambar di C# – Panduan Lengkap Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Ekstrak teks dari gambar di C# – Aspose OCR langkah demi langkah
url: /id/net/text-recognition/extract-text-from-image-in-c-aspose-ocr-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ekstrak teks dari gambar di C# – Panduan Lengkap Aspose OCR

Pernah perlu **mengekstrak teks dari gambar** tetapi tidak yakin pustaka mana yang memberikan hasil dapat diandalkan? Mungkin Anda memiliki sekumpulan pemindaian DJVU dan hanya menginginkan teks polos tanpa harus berurusan dengan alat pihak ketiga. Dalam tutorial ini kita akan menyelesaikan masalah itu dalam beberapa menit menggunakan Aspose OCR untuk .NET.

Kita akan melangkah melalui membaca file gambar di C#, mengonversi dokumen DJVU ke teks, dan mengubah gambar OCR apa pun menjadi string bersih. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang mencetak teks yang dikenali ke konsol. Tanpa tautan “lihat dokumentasi” yang samar—hanya solusi lengkap yang dapat disalin‑tempel.

## Apa yang Anda Butuhkan

- **.NET 6.0** atau yang lebih baru (kode ini juga bekerja pada .NET Framework 4.6+).  
- Paket NuGet **Aspose.OCR for .NET** (lisensi percobaan gratis cukup untuk pengujian).  
- File DJVU atau gambar yang didukung (PNG, JPEG, BMP, dll.).  
- Visual Studio, Rider, atau editor favorit Anda.

Jika Anda belum memiliki salah satu dari itu, cukup instal paket NuGet:

```bash
dotnet add package Aspose.OCR
```

Itu saja persiapan yang diperlukan. Mari kita mulai.

## Langkah 1: Inisialisasi OCR Engine – ekstrak teks dari gambar

Hal pertama yang Anda lakukan adalah membuat instance `OcrEngine`. Anggaplah ini sebagai otak yang akan membaca piksel dan mengubahnya menjadi karakter.

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

Mengapa kita menginstansiasi engine *sebelum* memuat file? Desain Aspose memisahkan konfigurasi (seperti lisensi) dari data gambar sebenarnya, sehingga Anda dapat menggunakan engine yang sama untuk beberapa file tanpa harus membuat objek baru—sebuah peningkatan performa kecil.

## Langkah 2: Terapkan Lisensi Aspose OCR Anda (opsional tetapi disarankan)

Jika Anda memiliki lisensi komersial, atur sekarang. Melewatkan langkah ini akan memaksa mode demo, yang menambahkan watermark pada output dan membatasi jumlah halaman.

```csharp
        // Apply license – remove this line if you’re using the free trial
        ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Tips profesional:** Simpan file lisensi di luar kontrol sumber (misalnya, dalam variabel lingkungan) untuk menghindari commit tidak sengaja.

## Langkah 3: Muat Gambar – membaca file gambar c# menjadi mudah

Aspose dapat membaca banyak format, termasuk DJVU yang kurang umum. Kita akan menggunakan helper `ImageStream.FromFile` untuk memuat file ke dalam engine.

```csharp
        // Load the image (DJVU, PNG, JPEG, etc.)
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.djvu");
```

Jika Anda lebih suka bekerja dengan `byte[]` (misalnya, ketika gambar berasal dari basis data), Anda dapat menggunakan `ImageStream.FromBytes(byteArray)` sebagai gantinya. Fleksibilitas ini berguna ketika Anda perlu **membaca file gambar C#** dari stream alih‑alih dari disk.

## Langkah 4: Lakukan OCR – ocr image to string dalam satu panggilan

Sekarang keajaiban terjadi. Memanggil `Recognize()` menjalankan engine OCR dan mengembalikan `RecognitionResult` yang berisi teks yang diekstrak, skor kepercayaan, dan lainnya.

```csharp
        // Run OCR and get the result
        var result = ocrEngine.Recognize();

        // Extract plain text
        string recognizedText = result.Text;
```

Mengapa tidak langsung memanggil `Recognize().Text`? Memisahkan panggilan memungkinkan Anda memeriksa `result.Confidence` atau `result.Regions` jika membutuhkan data yang lebih detail nanti—berguna untuk debugging atau membangun UI yang menyoroti kata dengan kepercayaan rendah.

## Langkah 5: Tampilkan Teks yang Diekstrak – output akhir Anda

Akhirnya, tuliskan teks ke konsol. Pada aplikasi nyata Anda mungkin menulis ke file, basis data, atau mengirimnya melalui API.

```csharp
        // Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Jika engine OCR tidak dapat mengenali karakter apa pun, `recognizedText` akan menjadi string kosong. Dalam kasus itu, periksa kembali kualitas gambar atau coba sesuaikan pengaturan bahasa engine (misalnya, `ocrEngine.Language = Language.English;`).

## Mengonversi DJVU ke Teks – mengenali teks dari djvu secara massal

Anda mungkin memiliki puluhan file DJVU untuk diproses. Bungkus logika sebelumnya dalam sebuah loop:

```csharp
string[] files = Directory.GetFiles("YOUR_DIRECTORY", "*.djvu");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string text = ocrEngine.Recognize().Text;
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), text);
    Console.WriteLine($"Converted {Path.GetFileName(file)} → {Path.GetFileNameWithoutExtension(file)}.txt");
}
```

Potongan kode ini **mengonversi DJVU ke teks** secara otomatis, membuat file `.txt` di samping setiap sumber. Ini cara cepat untuk membangun arsip yang dapat dicari dari dokumen pemindaian lama.

## Menangani Kasus Tepi – bagaimana jika gambar berisik?

Akurasi OCR menurun ketika gambar blur, kontras rendah, atau memiliki latar belakang berwarna. Aspose OCR menawarkan opsi pra‑pemrosesan:

```csharp
// Example: Binarize the image to improve contrast
ocrEngine.Image = ImageProcessing.Binarize(ocrEngine.Image, threshold: 128);
```

Sebagai alternatif, Anda dapat mengatur engine untuk mendeteksi bahasa secara otomatis:

```csharp
ocrEngine.Language = Language.Detect; // Detects language based on content
```

Penyesuaian ini sering mengubah hasil akurasi 60 % menjadi 95 %. Bereksperimenlah dengan metode `Threshold`, `Denoise`, atau `Deskew` jika Anda menemui masalah.

## Contoh Lengkap yang Siap Pakai – salin, tempel, jalankan

Berikut adalah seluruh program, siap untuk dikompilasi. Ganti `"YOUR_DIRECTORY/input.djvu"` dengan path ke file Anda dan pastikan file lisensi dapat diakses.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Apply license (optional)
        // ocrEngine.SetLicense("Aspose.OCR.lic"); // Uncomment if you have a license

        // 3️⃣ Load the image (DJVU, PNG, JPEG, etc.)
        string imagePath = "YOUR_DIRECTORY/input.djvu";
        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 4️⃣ Perform OCR
        var result = ocrEngine.Recognize();
        string recognizedText = result.Text;

        // 5️⃣ Output the text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

Jalankan dengan:

```bash
dotnet run
```

Anda akan melihat teks yang diekstrak dicetak ke konsol, persis seperti pada contoh sebelumnya.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

- **Apakah ini bekerja dengan file PDF?**  
  Tidak secara langsung. Aspose OCR menangani gambar raster; untuk PDF Anda harus terlebih dahulu mengonversi setiap halaman menjadi gambar (misalnya, menggunakan Aspose.PDF) lalu memberi gambar‑gambar tersebut ke engine OCR.

- **Bagaimana jika saya perlu memproses batch besar di server?**  
  Instansiasi **satu** `OcrEngine` dan gunakan kembali di seluruh thread. Engine bersifat thread‑safe untuk operasi baca‑saja, tetapi Anda harus menghindari berbagi instance `Image` yang sama secara bersamaan.

- **Bisakah saya mengekstrak teks berformat (font, ukuran)?**  
  Aspose OCR hanya mengembalikan teks Unicode polos. Untuk ekstraksi yang mempertahankan tata letak, Anda memerlukan solusi yang lebih canggih seperti OCR‑ML atau pustaka PDF yang menyimpan layout.

## Langkah Selanjutnya – perluas alur kerja Anda

Sekarang Anda dapat **mengekstrak teks dari gambar** secara andal, pertimbangkan:

- Menyimpan hasil ke Elasticsearch untuk pencarian teks penuh.  
- Mengirim teks ke model bahasa untuk rangkuman.  
- Menambahkan UI sederhana dengan ASP.NET Core untuk mengunggah file dan melihat hasil OCR secara instan.  

Semua ini dibangun di atas kode inti yang baru saja kita bahas, sehingga Anda berada pada posisi yang tepat untuk memperluas solusi.

---

### Ringkasan Cepat

- Kami **menginisialisasi** `OcrEngine` (jantung Aspose OCR).  
- Menerapkan **lisensi** untuk membuka semua fitur.  
- **Memuat** file DJVU menggunakan `ImageStream.FromFile`.  
- Memanggil `Recognize()` untuk mendapatkan hasil **ocr image to string**.  
- Mencetak **teks yang diekstrak** ke konsol.  

Itulah resep lengkap untuk mengubah gambar apa pun—termasuk DJVU—menjadi teks yang dapat dicari dengan C#.

---

Silakan bereksperimen dengan format gambar lain, sesuaikan pengaturan pra‑pemrosesan, atau rangkaikan kode ini dengan pustaka Aspose lainnya. Jika Anda menemui kendala, tinggalkan komentar di bawah—selamat coding!  

![contoh ekstrak teks dari gambar](/images/ocr-example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}