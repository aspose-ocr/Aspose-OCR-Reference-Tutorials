---
category: general
date: 2026-06-22
description: Mengenali teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  otomatis meluruskan gambar, memproses gambar untuk OCR, dan mengaktifkan auto‑deskew
  dalam contoh OCR C# yang singkat.
draft: false
keywords:
- recognize text from image
- auto deskew image
- preprocess image for ocr
- c# ocr example
- enable auto deskew
language: id
og_description: Mengenali teks dari gambar dengan Aspose OCR di C#. Panduan ini menunjukkan
  cara otomatis meluruskan gambar, memproses gambar untuk OCR, dan mengaktifkan pelurusan
  otomatis dalam contoh OCR C# yang praktis.
og_title: Mengenali Teks dari Gambar dalam C# – Contoh OCR Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  headline: Recognize Text from Image in C# – Full OCR Example
  type: TechArticle
- description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  name: Recognize Text from Image in C# – Full OCR Example
  steps:
  - name: 1. Low Contrast or Dark Backgrounds
    text: 'Aspose.OCR offers an extra flag `PreprocessingOptions.ContrastEnhancement`.
      Add it to the `Preprocessing` line:'
  - name: 2. Non‑English Documents
    text: Swap `OcrLanguage.English` for `OcrLanguage.Spanish`, `OcrLanguage.French`,
      etc. The engine auto‑loads the appropriate language model.
  - name: 3. Large Images
    text: 'Processing a 5 MP photo can be memory‑hungry. Scale it down first:'
  - name: 4. Getting Bounding Boxes
    text: 'If you need the exact location of each word (e.g., for a UI overlay), iterate
      over `result.Regions`:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Mengenali Teks dari Gambar di C# – Contoh OCR Lengkap
url: /id/net/ocr-optimization/recognize-text-from-image-in-c-full-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali Teks dari Gambar di C# – Contoh OCR Lengkap

Pernah bertanya-tanya bagaimana cara **recognize text from image** dalam aplikasi C# tanpa harus menggaruk-garuk kepala karena pemindaian yang buram? Anda tidak sendirian. Baik Anda mendigitalkan kwitansi, mengekstrak data dari formulir, atau sekadar bermain dengan trik gambar berbasis AI, mendapatkan hasil OCR yang bersih bergantung pada pra‑pemrosesan yang tepat—pikirkan auto deskew image dan pengurangan noise.  

Dalam tutorial ini kami akan membahas **c# ocr example** yang menggunakan pustaka Aspose.OCR untuk **enable auto deskew**, secara otomatis meluruskan foto yang miring, dan **preprocess image for OCR** dalam hanya beberapa baris kode. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan yang mencetak teks yang dikenali langsung ke konsol.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mereferensikan paket NuGet Aspose.OCR.  
- Menyiapkan `OcrEngine` dengan dukungan bahasa Inggris.  
- Mengaktifkan **auto deskew image** dan opsi pra‑pemrosesan lainnya dalam satu langkah.  
- Menjalankan engine pada foto dunia nyata dan menangani outputnya.  
- Tips menangani kasus tepi seperti gambar yang sangat diputar atau pemindaian dengan kontras rendah.

> **Prerequisites** – Anda memerlukan .NET 6 (atau lebih baru) dan pemahaman dasar tentang C#. Tidak diperlukan pengalaman OCR sebelumnya.

---

## ## Mengenali Teks dari Gambar – Instal Paket Aspose.OCR

Sebelum menulis kode apa pun, pustaka harus ditambahkan ke proyek. Buka terminal di folder solusi Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah ini mengambil versi stabil terbaru dari Aspose.OCR, yang menyertakan mesin OCR, paket bahasa, dan utilitas pra‑pemrosesan yang kami perlukan.  

*Pro tip:* Jika Anda menargetkan .NET Framework bukan .NET Core, gunakan UI Visual Studio NuGet Package Manager—cari “Aspose.OCR” dan klik **Install**.

---

## ## Mengenali Teks dari Gambar – Inisialisasi OCR Engine

Sekarang paket sudah siap, kita dapat membuat engine. Langkah pertama adalah memberi tahu engine bahasa apa yang diharapkan. Dalam kebanyakan kasus bahasa Inggris sudah cukup, tetapi pustaka mendukung puluhan bahasa secara langsung.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine and set the language to English
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,

            // Step 2: Enable preprocessing to automatically deskew and denoise the image
            Preprocessing = PreprocessingOptions.AutoDeskew | PreprocessingOptions.Denoise
        };
```

**Mengapa ini penting:**  
- `Language = OcrLanguage.English` memberi tahu engine set karakter mana yang digunakan, secara dramatis meningkatkan akurasi.  
- Properti `Preprocessing` menggabungkan dua flag—`AutoDeskew` dan `Denoise`. Langkah **auto deskew image** ini memutar gambar kembali ke garis dasar horizontal, sementara `Denoise` menghapus artefak berbutir yang sebaliknya akan membingungkan engine OCR.  

Jika Anda melewatkan pra‑pemrosesan, Anda sering akan melihat output yang berantakan pada kwitansi yang dipindai atau foto yang diambil dengan sudut.

---

## ## Mengenali Teks dari Gambar – Berikan Gambar ke Engine

Dengan engine yang siap, langkah selanjutnya adalah memberikannya file gambar. Aspose.OCR menerima path atau `Stream`, sehingga Anda dapat bekerja dengan file lokal, sumber daya tersemat, atau bahkan gambar yang diunduh dari web.

```csharp
        // Step 3: Recognize text from the input image
        var result = engine.RecognizeImage(@"YOUR_DIRECTORY/skewed_photo.jpg");
```

**Catatan kasus tepi:**  
- Jika gambar **heavily rotated** (> 45°), `AutoDeskew` tetap akan berusaha sebaik mungkin, tetapi Anda mungkin ingin memutar ulang secara manual menggunakan `System.Drawing` atau `ImageSharp` sebelum memberikannya ke engine.  
- Untuk **multi‑page PDFs**, panggil `engine.RecognizePdf` sebagai gantinya; flag pra‑pemrosesan yang sama berlaku.

---

## ## Mengenali Teks dari Gambar – Output Hasil

Akhirnya, kami menampilkan teks yang diekstrak. Objek `result` berisi lebih dari sekadar teks biasa—ia juga menyediakan skor kepercayaan, kotak pembatas, dan gambar asli dengan wilayah yang disorot. Untuk demo cepat, mencetak `result.Text` sudah cukup.

```csharp
        // Step 4: Output the recognized text to the console
        System.Console.WriteLine(result.Text);
    }
}
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!
```

Jika output terlihat berantakan, periksa kembali bahwa gambar sumber jelas, pencahayaannya baik, dan bahwa **preprocess image for OCR** memang diaktifkan (flag `Preprocessing` di atas).  

---

## ## Mengenali Teks dari Gambar – Menangani Kesalahan Umum

### 1. Kontras Rendah atau Latar Belakang Gelap
Aspose.OCR menawarkan flag tambahan `PreprocessingOptions.ContrastEnhancement`. Tambahkan ke baris `Preprocessing`:

```csharp
Preprocessing = PreprocessingOptions.AutoDeskew |
                PreprocessingOptions.Denoise |
                PreprocessingOptions.ContrastEnhancement
```

### 2. Dokumen Non‑English
Ganti `OcrLanguage.English` dengan `OcrLanguage.Spanish`, `OcrLanguage.French`, dll. Engine secara otomatis memuat model bahasa yang sesuai.

### 3. Gambar Besar
Memproses foto 5 MP dapat menghabiskan memori. Skala dulu terlebih dahulu:

```csharp
engine.Image = ImageProcessor.Resize(@"YOUR_DIRECTORY/skewed_photo.jpg", 1024, 768);
```

### 4. Mendapatkan Bounding Boxes
Jika Anda membutuhkan lokasi tepat setiap kata (mis., untuk overlay UI), iterasi melalui `result.Regions`:

```csharp
foreach (var region in result.Regions)
{
    System.Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

---

## ## Mengenali Teks dari Gambar – Contoh Kerja Lengkap

Berikut adalah program **lengkap, yang dapat disalin‑tempel** yang menggabungkan semua tips di atas. Simpan sebagai `Program.cs`, ganti `YOUR_DIRECTORY` dengan folder yang berisi gambar uji Anda, dan jalankan `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,
            // Enable auto deskew, denoise, and contrast enhancement
            Preprocessing = PreprocessingOptions.AutoDeskew |
                            PreprocessingOptions.Denoise |
                            PreprocessingOptions.ContrastEnhancement
        };

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed_photo.jpg";

        // Recognize the image
        var result = engine.RecognizeImage(imagePath);

        // Output plain text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // Optional: print bounding boxes for each detected region
        Console.WriteLine("=== Detected Regions ===");
        foreach (var region in result.Regions)
        {
            Console.WriteLine($"{region.Text}  -->  {region.Bounds}");
        }
    }
}
```

**Output konsol yang diharapkan** (asumsi gambar berisi kwitansi sederhana):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!

=== Detected Regions ===
Invoice #12345  -->  {X=12,Y=34,Width=250,Height=20}
Date: 2026-06-01  -->  {X=12,Y=60,Width=200,Height=18}
Total: $256.78  -->  {X=12,Y=86,Width=180,Height=18}
Thank you for your business!  -->  {X=12,Y=112,Width=300,Height=22}
```

Jika Anda melihat teks tercetak dengan bersih, selamat—Anda telah berhasil **recognize text from image** dengan auto‑deskewing dan pra‑pemrosesan!

---

## ## Mengenali Teks dari Gambar – Langkah Selanjutnya & Topik Terkait

- **Batch processing:** Bungkus pemanggilan engine dalam loop `foreach` untuk menangani puluhan foto sekaligus.  
- **PDF conversion:** Gunakan `engine.RecognizePdf` untuk dokumen multi‑page, lalu gabungkan hasilnya.  
- **Custom dictionaries:** Berikan daftar kata ke `engine.CustomWords` untuk meningkatkan akurasi pada terminologi khusus domain (mis., kode medis).  
- **Performance tuning:** Cache instance `OcrEngine` jika Anda memproses banyak gambar; pembuatan engine adalah langkah paling mahal.  

Ekstensi ini secara alami melibatkan konsep yang sama—**preprocess image for OCR**, **enable auto deskew**, dan **recognize text from image**—sehingga Anda dapat menggunakan kembali pola kode yang baru saja dipelajari.

## Kesimpulan

Kami baru saja membahas **c# ocr example** yang menunjukkan cara **recognize text from image** menggunakan Aspose.OCR, sambil secara otomatis meluruskan dan mengurangi noise gambar. Dengan mengaktifkan `AutoDeskew` (fitur **auto deskew image**) dan menambahkan beberapa flag pra‑pemrosesan, Anda secara dramatis meningkatkan keandalan OCR tanpa menulis satu baris kode manipulasi gambar sekalipun.

Sekarang Anda dapat mengambil kerangka ini, memasukkan gambar Anda sendiri, dan mulai mengekstrak data untuk faktur, KTP, atau jenis dokumen lain yang berada di atas kertas. Memiliki pemindaian yang sulit? Coba opsi pra‑pemrosesan tambahan yang kami sebutkan, atau bereksperimen dengan paket bahasa khusus. Tidak ada batasnya.

Jika panduan ini membantu Anda keluar dari kebuntuan, tinggalkan komentar, bagikan hasil Anda, atau hubungi saya di GitHub—selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menggunakan AspOCR: Filter Pra‑Pemrosesan Gambar OCR untuk .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)
- [Cara Mengekstrak Teks dari Gambar Menggunakan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}