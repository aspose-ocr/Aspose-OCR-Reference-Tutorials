---
category: general
date: 2026-01-07
description: Cara melakukan OCR dan mengekstrak teks dari gambar menggunakan Aspose
  OCR di C#. Pelajari cara membaca teks dari gambar, mengenali teks Hindi, dan dapatkan
  contoh kode lengkap.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from image
- recognize hindi text
- how to extract text from image
language: id
og_description: Cara melakukan OCR di C# untuk mengekstrak teks dari gambar. Tutorial
  ini menunjukkan cara membaca teks dari gambar, mengenali teks Hindi, dan mengekstrak
  teks dari gambar menggunakan Aspose OCR.
og_title: Cara Melakukan OCR di C# – Panduan Lengkap
tags:
- OCR
- C#
- Aspose
title: Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar dengan Aspose OCR
url: /id/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar dengan Aspose OCR

Pernah bertanya‑tanya **cara melakukan OCR** pada faktur yang dipindai atau foto sebuah tanda? Anda tidak sendirian. Dalam banyak proyek dunia nyata Anda perlu **mengekstrak teks dari gambar**, baik itu struk, pemindaian paspor, atau catatan tulisan tangan. Kabar baik? Dengan Aspose.OCR Anda dapat melakukannya dalam beberapa baris kode C#, dan Anda bahkan akan belajar cara **mengenali teks Hindi** sekaligus.

Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang **membaca teks dari gambar**, menunjukkan cara **mengekstrak teks dari gambar** menggunakan mesin OCR Aspose, serta menjelaskan “mengapa” di balik setiap langkah. Tanpa referensi samar ke dokumen eksternal—hanya solusi mandiri yang dapat Anda salin‑tempel dan jalankan hari ini.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode juga dapat dikompilasi terhadap .NET Standard 2.0)
- Visual Studio 2022 (atau IDE lain yang Anda sukai)
- Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- File gambar yang berisi teks Hindi (misalnya `hindi_invoice.jpg`)
- Folder sumber daya bahasa OCR yang disertakan dengan Aspose (unduh dari situs Aspose)

> **Pro tip:** Simpan folder sumber daya OCR di samping proyek Anda untuk memudahkan penanganan path.

## Implementasi Langkah‑per‑Langkah

Berikut kami membagi proses menjadi enam langkah logis. Setiap langkah memiliki heading H2 sendiri (agar mesin pencari dan model AI dapat dengan cepat menemukan informasi) dan sub‑heading H3 singkat yang secara alami menyertakan kata kunci sekunder.

### Langkah 1 – Atur Path Sumber Daya OCR  
**Mengapa ini penting:** Aspose.OCR bergantung pada paket bahasa (font, kamus, dan file model) yang berada dalam folder yang Anda tunjukkan. Jika path salah, mesin akan melempar `FileNotFoundException` dan Anda tidak akan mendapatkan teks apa pun dari gambar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Tell the OCR engine where to find language resources
OcrEngine.SetResourcesPath(@"C:\MyProject\OcrResources");
```

### Langkah 2 – Buat Instance OcrEngine  
**Mengapa ini penting:** `OcrEngine` adalah objek berat yang memuat model pengenalan ke memori. Membungkusnya dalam blok `using` menjamin pembuangan yang tepat, yang sangat penting saat Anda memproses banyak gambar secara batch.

```csharp
// Instantiate the OCR engine inside a using block
using (var ocrEngine = new OcrEngine())
{
    // Subsequent steps go here...
}
```

### Langkah 3 – Konfigurasikan Pengaturan Pengenalan (Pilih Bahasa Hindi)  
**Mengapa ini penting:** Secara default Aspose mencoba mendeteksi bahasa secara otomatis, tetapi secara eksplisit menetapkan `Language.Hindi` meningkatkan akurasi untuk skrip Devanagari dan mempercepat proses.

```csharp
    // Configure the engine to recognize Hindi text
    var recognitionSettings = new RecognitionSettings
    {
        Language = Language.Hindi   // Recognize Hindi characters
    };
```

### Langkah 4 – Muat Gambar yang Ingin Dibaca  
**Mengapa ini penting:** `ImageStream.FromFile` mengabstraksi penanganan bitmap di bawahnya dan menyalurkan data secara efisien. Anda juga dapat menggunakan `MemoryStream` jika gambar berasal dari permintaan web.

```csharp
    // Load the target image (replace with your own path)
    var imageStream = ImageStream.FromFile(@"C:\MyProject\Images\hindi_invoice.jpg");
```

### Langkah 5 – Jalankan Proses OCR  
**Mengapa ini penting:** Metode `Recognize` melakukan pekerjaan berat—pra‑pemrosesan, segmentasi, klasifikasi karakter, dan akhirnya perakitan teks. Ia mengembalikan string biasa yang dapat Anda simpan, tampilkan, atau proses lebih lanjut.

```csharp
    // Execute OCR and capture the recognized text
    string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

### Langkah 6 – Tampilkan Teks yang Diekstrak  
**Mengapa ini penting:** Untuk debugging cepat Anda biasanya ingin menuliskan hasil ke konsol atau file log. Dalam produksi Anda mungkin menyimpannya ke basis data atau mengirimnya ke alur kerja downstream.

```csharp
    // Output the result to the console
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(recognizedText);
}
```

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang dapat Anda masukkan ke dalam proyek aplikasi konsol. Pastikan Anda mengganti path placeholder dengan direktori Anda yang sebenarnya.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Set the folder that contains language resources
        OcrEngine.SetResourcesPath(@"C:\MyProject\OcrResources");

        // 2️⃣ Create the OCR engine (auto‑disposed)
        using (var ocrEngine = new OcrEngine())
        {
            // 3️⃣ Tell the engine to look for Hindi characters
            var recognitionSettings = new RecognitionSettings
            {
                Language = Language.Hindi
            };

            // 4️⃣ Load the image you want to read
            var imageStream = ImageStream.FromFile(@"C:\MyProject\Images\hindi_invoice.jpg");

            // 5️⃣ Perform OCR
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);

            // 6️⃣ Show the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);
        }

        // Keep console open (useful when running from VS)
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== OCR Result ===
Invoice No: 12345
Date: 01/01/2024
Amount: ₹ 15,000
धन्यवाद
```

Jika Anda melihat karakter acak alih‑alih karakter Hindi, periksa kembali bahwa folder sumber daya mengarah ke versi paket bahasa Hindi yang tepat.

## Kesalahan Umum & Cara Mengatasinya  

| Masalah | Mengapa Terjadi | Solusi Cepat |
|-------|----------------|-----------|
| **Karakter sampah** | Sumber daya bahasa salah atau tidak ada | Pastikan `SetResourcesPath` mengarah ke folder yang berisi `Hindi.cognates` dan file terkait |
| **Kesalahan out‑of‑memory** | Memuat gambar sangat besar tanpa skala | Gunakan `ImageStream.FromFile(..., maxWidth: 2000)` untuk menurunkan skala secara langsung |
| **Performa lambat** | Mode auto‑detect memindai banyak bahasa | Tetapkan secara eksplisit `Language = Language.Hindi` (atau bahasa target lain) |
| **Tidak ada output sama sekali** | Gambar sepenuhnya putih/blur | Lakukan pra‑pemrosesan gambar (kontras, binarisasi) sebelum diberikan ke OCR |

## Memperluas Solusi: Bahasa & Skenario Lain  

Jika Anda perlu **membaca teks dari gambar** dalam bahasa Inggris, Spanyol, atau bahasa lain, cukup ubah enum `Language`:

```csharp
recognitionSettings.Language = Language.English;   // or Language.Spanish, etc.
```

Anda juga dapat menggabungkan beberapa bahasa:

```csharp
recognitionSettings.Language = Language.English | Language.Hindi;
```

Untuk pemrosesan batch, bungkus blok `using (var ocrEngine = new OcrEngine())` di sekitar loop `foreach` yang mengiterasi folder berisi gambar. Mesin akan menggunakan kembali model yang sudah dimuat, secara dramatis mengurangi beban inisialisasi.

## Menguji Akurasi OCR Anda  

1. Jalankan program dengan gambar uji yang diketahui (Anda dapat membuat PNG sederhana dengan teks Hindi menggunakan editor grafis apa pun).  
2. Bandingkan output konsol dengan teks asli.  
3. Jika tingkat kesalahan lebih tinggi dari 5 %, pertimbangkan menyesuaikan kualitas gambar (tingkatkan DPI ke 300 dpi) atau menerapkan langkah pra‑pemrosesan seperti `imageStream = imageStream.ApplyGaussianBlur(1.5)` (Aspose menyediakan filter dasar).

## Kesimpulan  

Kami telah menunjukkan **cara melakukan OCR** di C# menggunakan Aspose.OCR, mendemonstrasikan cara **mengekstrak teks dari gambar**, dan menelusuri contoh dunia nyata yang **mengenali teks Hindi**. Dengan mengikuti enam langkah—menetapkan path sumber daya, membuat engine, mengonfigurasi bahasa, memuat gambar, menjalankan pengenalan, dan menampilkan hasil—Anda kini memiliki blok bangunan yang dapat diandalkan untuk proyek digitalisasi dokumen apa pun.

Selanjutnya, coba ganti `Language.Hindi` dengan bahasa lain, atau alirkan output OCR ke pipeline pemrosesan bahasa alami untuk secara otomatis mengkategorikan faktur. Kemungkinannya tak terbatas, dan pola inti tetap sama: **baca teks dari gambar**, lalu lakukan apa pun yang aplikasi Anda perlukan dengan teks tersebut.

Ada pertanyaan tentang kasus tepi, penyetelan performa, atau lisensi? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}