---
category: general
date: 2026-11-17
description: Cara melakukan OCR pada gambar JPG di C# – pelajari cara mengekstrak
  teks dari gambar, meningkatkan akurasi OCR, dan memuat gambar untuk OCR dengan Aspose
  OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- convert JPG to text
- improve OCR accuracy
- load image for OCR
language: id
lastmod: 2026-11-17
og_description: Cara melakukan OCR pada gambar JPG di C# dan mengekstrak teks dari
  gambar dengan akurasi tinggi menggunakan Aspose OCR. Ikuti tutorial lengkap langkah
  demi langkah.
og_image_alt: Screenshot showing how to perform OCR with Aspose OCR in C#
og_title: Cara melakukan OCR pada gambar JPG dengan Aspose OCR – Panduan C#
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: How to perform OCR on a JPG image in C# – learn to extract text from
    image, improve OCR accuracy, and load image for OCR with Aspose OCR.
  headline: How to perform OCR on a JPG image using Aspose OCR in C#
  type: TechArticle
- description: How to perform OCR on a JPG image in C# – learn to extract text from
    image, improve OCR accuracy, and load image for OCR with Aspose OCR.
  name: How to perform OCR on a JPG image using Aspose OCR in C#
  steps:
  - name: Load image for OCR
    text: The first operation is to give the OCR engine a bitmap to analyze. Aspose
      OCR accepts an `ImageStream` created from a file path, a byte array, or a stream.
      Using a file path is the simplest approach for a quick demo.
  - name: Improve OCR accuracy (optional language hint)
    text: If your image contains non‑Latin characters, specifying the language dramatically
      raises recognition quality. Aspose OCR ships with built‑in language packs such
      as `Cyrillic`, `Arabic`, `ChineseSimplified`, etc.
  - name: Run the OCR process
    text: Calling `Process()` performs the heavy lifting. It returns `true` when the
      engine successfully extracts text; otherwise, you can inspect `ocrEngine.LastError`.
  - name: Extract text from image
    text: When `Process()` succeeds, the recognized plain‑text result is available
      through the `Text` property.
  - name: Display the extracted text
    text: For a console demo, simply write the string to `stdout`. In a real application
      you might store it in a database, feed it to a search index, or pass it to a
      translation service.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Cara melakukan OCR pada gambar JPG menggunakan Aspose OCR di C#
url: /id/net/text-recognition/how-to-perform-ocr-on-a-jpg-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR pada gambar JPG menggunakan Aspose OCR di C#

Jika Anda perlu mengetahui **cara melakukan OCR** pada file gambar, panduan ini memberikan solusi siap‑jalankan. Anda akan melihat cara **memuat gambar untuk OCR**, menjalankan mesin, dan **mengekstrak teks dari gambar** tanpa meninggalkan IDE Anda.

Tutorial ini mencakup setiap langkah yang diperlukan untuk **mengonversi JPG ke teks** dengan Aspose OCR, menjelaskan cara **meningkatkan akurasi OCR** untuk Cyrillic atau bahasa lain, dan menunjukkan cara menampilkan hasilnya dalam aplikasi konsol. Tidak ada layanan eksternal yang diperlukan; semuanya berjalan secara lokal pada .NET 6 atau yang lebih baru.

## Apa yang akan Anda pelajari

* Cara membuat instance mesin OCR dan **memuat gambar untuk OCR**.  
* Properti mana yang mengontrol pemilihan bahasa untuk **meningkatkan akurasi OCR**.  
* Cara menjalankan mesin dan **mengekstrak teks dari gambar** dengan aman.  
* Cara **mengonversi JPG ke teks** dan mencetak output ke konsol.  
* Kesulitan umum dan tip praktik terbaik untuk hasil OCR yang dapat diandalkan.

**Prasyarat**

* .NET 6 SDK (atau versi .NET apa pun yang mendukung C# 10).  
* Paket NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
* File JPG yang ingin Anda baca – misalnya `sample.jpg` yang ditempatkan di folder yang diketahui.

---

## Cara melakukan OCR – panduan langkah‑demi‑langkah

Bagian-bagian berikut memecah proses menjadi langkah-langkah terpisah yang dapat digunakan kembali. Setiap langkah mencakup potongan kode lengkap, penjelasan singkat, dan tip yang membantu Anda **meningkatkan akurasi OCR** bila diperlukan.

### Langkah 1: Memuat gambar untuk OCR

Operasi pertama adalah memberi mesin OCR sebuah bitmap untuk dianalisis. Aspose OCR menerima `ImageStream` yang dibuat dari jalur file, array byte, atau stream. Menggunakan jalur file adalah pendekatan paling sederhana untuk demo cepat.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Load the JPG file – this is the “load image for OCR” step
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\sample.jpg");
```

**Mengapa ini penting:**  
Memuat gambar dengan benar memastikan mesin bekerja dengan data piksel tepat yang ingin Anda proses. Menyediakan format yang rusak atau tidak didukung akan menyebabkan `Process()` mengembalikan `false`.

### Langkah 2: Meningkatkan akurasi OCR (petunjuk bahasa opsional)

Jika gambar Anda berisi karakter non‑Latin, menentukan bahasa secara signifikan meningkatkan kualitas pengenalan. Aspose OCR dilengkapi dengan paket bahasa bawaan seperti `Cyrillic`, `Arabic`, `ChineseSimplified`, dll.

```csharp
        // Optional: set the language to Cyrillic to boost recognition for Russian text
        ocrEngine.Language = Language.Cyrillic;
```

**Tip:**  
Hanya atur bahasa ketika Anda mengetahui skripnya; membiarkannya pada default (`English`) dapat menyebabkan kesalahan pengenalan karakter yang tampak mirip tetapi berasal dari alfabet lain.

### Langkah 3: Menjalankan proses OCR

Memanggil `Process()` melakukan pekerjaan berat. Ia mengembalikan `true` ketika mesin berhasil mengekstrak teks; jika tidak, Anda dapat memeriksa `ocrEngine.LastError`.

```csharp
        // Execute the OCR operation
        if (!ocrEngine.Process())
        {
            Console.WriteLine($"OCR failed: {ocrEngine.LastError}");
            return;
        }
```

**Mengapa ini penting:**  
Memeriksa nilai kembali mencegah Anda bekerja dengan string kosong dan memberi Anda jalur error yang jelas untuk debugging.

### Langkah 4: Mengekstrak teks dari gambar

Ketika `Process()` berhasil, hasil teks polos yang dikenali tersedia melalui properti `Text`.

```csharp
        // Retrieve the recognized plain‑text result
        string recognizedText = ocrEngine.Text;
```

Pada titik ini Anda telah berhasil **mengonversi JPG ke teks**. String tersebut mungkin berisi jeda baris, tanda baca, dan spasi tepat seperti yang dideteksi mesin.

### Langkah 5: Menampilkan teks yang diekstrak

Untuk demo konsol, cukup tulis string ke `stdout`. Dalam aplikasi nyata Anda mungkin menyimpannya di basis data, mengirimkannya ke indeks pencarian, atau meneruskannya ke layanan terjemahan.

```csharp
        // Show the OCR result
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Program lengkap**

Menggabungkan semua bagian memberi Anda aplikasi mandiri yang dapat Anda salin, tempel, dan jalankan:

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        var ocrEngine = new OcrEngine();

        // Load the JPG file – this is the “load image for OCR” step
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\sample.jpg");

        // Optional: improve OCR accuracy by specifying the language
        ocrEngine.Language = Language.Cyrillic; // remove or change for other scripts

        // Run the OCR engine
        if (!ocrEngine.Process())
        {
            Console.WriteLine($"OCR failed: {ocrEngine.LastError}");
            return;
        }

        // Extract and display the recognized text
        string recognizedText = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Output yang diharapkan**

Jika `sample.jpg` berisi frasa “Привет мир” (Hello world dalam bahasa Rusia), konsol akan mencetak:

```
=== OCR Result ===
Привет мир
```

Jika gambar berisi teks bahasa Inggris, output akan sesuai dengan bahasa tersebut. Mengubah `ocrEngine.Language` menjadi `Language.English` (atau menghilangkan baris tersebut) menghasilkan hasil yang serupa.

---

## Kesulitan umum dan tip praktik terbaik

| Masalah | Mengapa terjadi | Cara memperbaikinya |
|-------|----------------|---------------|
| JPG buram atau beresolusi rendah | Mesin OCR membutuhkan tepi yang jelas untuk memisahkan karakter. | Gunakan gambar sumber dengan setidaknya 300 dpi; secara opsional terapkan pra‑pemrosesan gambar (kontras, binarisasi). |
| Pengaturan bahasa yang salah | Mesin mencoba mencocokkan karakter dengan set bahasa Inggris default. | Atur `ocrEngine.Language` ke skrip yang tepat, atau biarkan tidak diatur untuk deteksi multi‑bahasa. |
| Jalur file terlalu panjang | `ImageStream.FromFile` akan melempar error jika jalur melebihi batas OS. | Simpan folder gambar dekat dengan root proyek atau gunakan jalur relatif. |
| Paket NuGet tidak ada | Kompilasi gagal dengan pesan “type or namespace name ‘Aspose’ could not be found”. | Jalankan `dotnet add package Aspose.OCR` sebelum membangun. |

**Tip pro:**  
Jika Anda perlu memproses banyak gambar secara batch, gunakan kembali satu instance `OcrEngine` dan hanya ganti `ocrEngine.Image` di antara panggilan. Ini mengurangi alokasi memori dan mempercepat pemrosesan.

---

## Memperluas solusi

Sekarang Anda tahu **cara melakukan OCR** pada satu JPG, Anda dapat menjelajahi topik terkait berikut:

* **Extract text from image** dalam PDF dengan memuat setiap halaman sebagai gambar terlebih dahulu.  
* **Convert JPG to text** dalam layanan latar belakang menggunakan `Task.Run` untuk paralelisme.  
* **Improve OCR accuracy** lebih lanjut dengan kamus khusus atau dengan melatih model bahasa baru.  
* **Load image for OCR** dari `MemoryStream` ketika gambar berasal dari API web bukan dari sistem file.  

Setiap ekstensi ini dibangun di atas langkah inti yang sama yang ditunjukkan di atas, sehingga Anda dapat menggunakan kembali kode dengan perubahan minimal.

---

## Kesimpulan

Anda kini memiliki contoh lengkap yang siap produksi yang menunjukkan **cara melakukan OCR** pada gambar JPG, **mengekstrak teks dari gambar**, dan **mengonversi JPG ke teks** menggunakan Aspose OCR di C#. Dengan secara opsional mengatur bahasa, Anda dapat **meningkatkan akurasi OCR**, dan pemisahan langkah yang jelas membuat kode mudah dipelihara dan diperluas.

Cobalah mengganti bahasa, memberi gambar yang berbeda, atau mengintegrasikan hasil ke dalam alur kerja yang lebih besar. Pola yang sama bekerja untuk file PNG, BMP, atau TIFF, sehingga Anda dapat menangani hampir semua gambar raster yang berisi teks dapat dibaca.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)
- [Cara mengekstrak teks dari gambar menggunakan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Cara melakukan konversi gambar ke teks dari stream dengan Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}