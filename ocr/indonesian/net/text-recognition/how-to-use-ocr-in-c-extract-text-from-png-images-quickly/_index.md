---
category: general
date: 2026-03-29
description: Cara menggunakan OCR dengan Aspose untuk mengekstrak teks dari file PNG
  dan mengonversi gambar menjadi teks. Pelajari OCR async langkah demi langkah di
  C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: id
og_description: Cara menggunakan OCR dengan Aspose di C# untuk mengekstrak teks dari
  file PNG. Panduan ini memandu Anda melalui OCR async, kode, dan tips.
og_title: Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar PNG
tags:
- OCR
- C#
- Aspose
title: Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar PNG dengan Cepat
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar PNG dengan Cepat

Pernah bertanya-tanya **bagaimana cara menggunakan OCR** untuk mengambil teks dari beberapa screenshot PNG? Mungkin Anda memiliki kwitansi yang dipindai, faktur, atau mock‑up UI dan Anda memerlukan teks tersebut dalam format yang dapat dicari. Kabar baiknya? Dengan Aspose.OCR Anda dapat mengonversi gambar menjadi teks hanya dengan beberapa baris kode C# asynchronous.  

Dalam tutorial ini kami akan menunjukkan secara tepat cara mengekstrak teks dari file PNG, menjelaskan mengapa setiap langkah penting, dan memberikan program siap‑jalankan yang mencetak teks yang dikenali untuk setiap halaman. Pada akhir tutorial Anda akan dapat **mengekstrak teks dari gambar** tanpa harus mencari‑cari di dokumentasi.

## Apa yang Akan Anda Pelajari

- Menginstal dan mereferensikan paket NuGet Aspose.OCR.  
- Menginisialisasi mesin OCR dan mengatur bahasa (Inggris dalam contoh ini).  
- Memberi array file PNG ke `RecognizeImagesAsync` untuk pemrosesan cepat dan non‑blocking.  
- Melakukan iterasi pada objek `OcrResult` dan mengeluarkan string yang diekstrak.  

Tanpa layanan eksternal, tanpa callback yang rumit—hanya C# async yang bersih dan bekerja pada .NET 6+.

---

## Prerequisites

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6 SDK (atau lebih baru) | Fitur bahasa modern seperti `async Main`. |
| Visual Studio 2022 atau VS Code | IDE untuk mengompilasi dan menjalankan kode. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | Menyediakan kelas `OcrEngine` yang digunakan dalam contoh. |
| Beberapa gambar PNG (`page1.png`, `page2.png`, …) | File input untuk proses OCR. |

Jika Anda sudah memiliki proyek .NET, cukup jalankan `dotnet add package Aspose.OCR`. Jika belum, buat aplikasi konsol baru dengan `dotnet new console -n OcrDemo`.

---

## Langkah 1: Instal Aspose.OCR dan Siapkan Proyek

Pertama, tambahkan pustaka OCR ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

Mengapa ini penting: Aspose.OCR menyertakan mesin OCR native, paket bahasa, dan API yang sederhana. Dengan mengunduhnya melalui NuGet Anda menjamin kompatibilitas versi dan pembaruan otomatis.

---

## Langkah 2: Inisialisasi Mesin OCR dan Pilih Bahasa

Mesin perlu mengetahui bahasa apa yang harus dicari. Bahasa Inggris adalah yang paling umum, tetapi Anda dapat mengganti dengan `Language.Spanish`, `Language.French`, dll.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Pro tip:** Selalu atur bahasa secara eksplisit; membiarkannya pada nilai default dapat menurunkan akurasi dan meningkatkan waktu pemrosesan.

---

## Langkah 3: Siapkan Daftar File PNG

Anda dapat memberi satu file atau sebuah array. Menyediakan array memungkinkan mesin memproses batch secara asynchronous, yang ideal untuk beberapa halaman.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Jika gambar Anda berada di subfolder, cukup tambahkan jalur relatif (`"images/page1.png"`). Mesin akan melempar `FileNotFoundException` yang jelas jika jalur salah—jadi periksa kembali nama file.

---

## Langkah 4: Jalankan OCR Asynchronous pada Semua Gambar

Metode `RecognizeImagesAsync` mengembalikan array `OcrResult`. Karena bersifat async, UI (atau konsol) tetap responsif sementara OCR berjalan di latar belakang.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Mengapa async?**  
Jika Anda mengintegrasikan OCR ke dalam web API atau aplikasi desktop, Anda tidak ingin thread terblokir saat mesin memindai setiap piksel. `await` melepaskan thread kembali ke thread pool, meningkatkan skalabilitas.

---

## Langkah 5: Tampilkan Teks yang Diekstrak untuk Setiap Halaman

Sekarang kita memiliki hasilnya, iterasikan melalui mereka dan cetak teks yang dikenali. Properti `Text` berisi output teks polos, siap untuk diproses lebih lanjut (misalnya, menyimpan ke basis data).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Output yang Diharapkan

Dengan asumsi `page1.png` berisi “Invoice #12345” dan `page2.png` berisi “Total: $89.99”, Anda akan melihat sesuatu seperti:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Jika OCR gagal menemukan teks apa pun, properti `Text` akan menjadi string kosong—tangani kasus ini dalam kode produksi dengan memeriksa `string.IsNullOrWhiteSpace`.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke `Program.cs`. Program ini mencakup semua directive `using`, `Main` async, dan komentar yang menjelaskan setiap langkah.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Simpan file, letakkan PNG Anda di samping executable (atau sesuaikan jalurnya), dan jalankan:

```bash
dotnet run
```

Anda akan melihat teks yang diekstrak dicetak ke konsol, mengonfirmasi bahwa Anda telah berhasil **mengonversi gambar menjadi teks**.

---

## Menangani Kasus Edge yang Umum

| Situasi | Apa yang Harus Dilakukan |
|-----------|------------|
| **Low‑resolution PNG** | Tingkatkan `ocrEngine.ImageProcessingOptions.Dpi` sebelum pengenalan. |
| **Multiple languages** | Set `ocrEngine.Language = Language.English | Language.Spanish;` (operator OR bitwise). |
| **Large batch (hundreds of files)** | Proses dalam potongan (misalnya 20 file per panggilan `RecognizeImagesAsync`) untuk menghindari lonjakan memori. |
| **Need the confidence score** | Gunakan `ocrResults[i].Confidence` (float antara 0 dan 1) untuk menyaring hasil berkualitas rendah. |

Penyesuaian ini membuat pipeline OCR Anda tetap kuat, terutama saat beralih dari demo ke produksi.

---

## Bonus: Menyimpan Hasil ke File Teks

Jika Anda lebih suka salinan persisten daripada output konsol, tambahkan helper kecil berikut:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Sekarang Anda memiliki satu file yang **mengekstrak teks dari gambar** untuk pemrosesan selanjutnya—sempurna untuk pengindeksan, pencarian, atau memasukkan ke model bahasa.

---

## Kesimpulan

Kami telah membahas **cara menggunakan OCR** di C# dengan Aspose untuk **mengekstrak teks dari file PNG** dan **mengonversi gambar menjadi teks** secara efisien. Pendekatan async memastikan aplikasi Anda tetap responsif, sementara API yang sederhana menjaga kode tetap mudah dibaca dan dipelihara.  

Cobalah dengan dokumen Anda sendiri, bereksperimen dengan bahasa berbeda, dan mungkin bahkan rangkaikan output ke indeks pencarian atau layanan rangkuman. Langit adalah batasnya ketika Anda dapat dengan andal mengubah gambar menjadi string yang dapat dicari.

---

### Langkah Selanjutnya & Topik Terkait

- **Ekstrak teks dari gambar** dalam format lain (JPEG, TIFF) – cukup ubah ekstensi file.  
- **Pemrosesan batch dengan Parallel.ForEach** untuk beban kerja besar.  
- **Pembersihan pasca‑OCR** menggunakan regular expression untuk menormalkan tanggal, jumlah, atau ID.  
- **Integrasi dengan Azure Cognitive Services** jika Anda memerlukan OCR berbasis cloud dengan fitur tambahan.  

Silakan tinggalkan komentar jika Anda mengalami kendala, atau bagikan bagaimana Anda memperluas alur dasar ini. Selamat coding!   (Image: ![OCR result screenshot showing extracted text](/images/ocr-result.png){.align-center alt="how to use OCR example output"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}