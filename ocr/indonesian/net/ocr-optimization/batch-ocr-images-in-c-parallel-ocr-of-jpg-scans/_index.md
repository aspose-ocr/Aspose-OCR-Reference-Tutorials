---
category: general
date: 2026-04-29
description: Lakukan OCR batch pada gambar dengan cepat menggunakan Aspose OCR di
  C#. Pelajari cara mengekstrak teks dari file jpg, membaca teks dari pemindaian,
  dan memproses daftar gambar secara paralel.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: id
og_description: Lakukan OCR gambar secara batch dengan cepat menggunakan Aspose OCR.
  Panduan ini menunjukkan cara mengekstrak teks dari JPG, membaca teks dari pemindaian,
  dan memproses daftar gambar secara paralel.
og_title: Batch OCR Gambar di C# – OCR Paralel pada Scan JPG
tags:
- C#
- OCR
- Aspose
- Image Processing
title: OCR Gambar Secara Batch di C# – OCR Paralel pada Scan JPG
url: /id/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batch OCR Images in C# – OCR Paralel pada Scan JPG

Pernah membutuhkan untuk **batch OCR images** tetapi tidak yakin bagaimana menskalakan pekerjaan ke banyak file? Anda tidak sendirian—para pengembang sering menemui kendala saat mencoba membaca teks dari scan satu per satu. Kabar baiknya, dengan Aspose OCR Anda dapat **extract text from jpg** file, **read text from scans**, dan **process image list** item secara paralel hanya dengan beberapa baris C#.

Dalam tutorial ini kami akan menelusuri contoh lengkap yang siap‑jalankan yang menunjukkan persis cara melakukannya. Pada akhir tutorial Anda akan memiliki aplikasi konsol mandiri yang mengenali folder berisi scan JPEG, mencetak teks setiap halaman, dan memberi tahu berapa lama setiap operasi berlangsung. Tanpa dokumen eksternal yang harus dikejar, tanpa potongan kode setengah jadi—hanya solusi penuh yang dapat Anda tempelkan ke Visual Studio dan jalankan.

## Apa yang Anda Butuhkan

- **.NET 6.0** atau lebih baru (kode juga dapat dikompilasi pada .NET Framework 4.6+)
- Paket NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)
- Sekelompok file JPG atau gambar hasil scan yang ingin diproses
- IDE apa saja yang Anda suka; saya menggunakan Visual Studio 2022, tetapi VS Code juga berfungsi dengan baik

Itu saja. Jika Anda sudah memiliki paket NuGet, Anda siap melanjutkan.

## Langkah 1 – Inisialisasi Mesin OCR (Pengaturan Batch OCR Images)

Hal pertama yang kami lakukan adalah membuat instance `OcrEngine` dan memberi tahu bahasa yang akan dicari. Dalam kebanyakan kasus bahasa Inggris sudah cukup, tetapi Anda dapat mengganti `OcrLanguage.English` dengan bahasa lain yang didukung.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*Mengapa ini penting:* Menginisialisasi mesin sekali dan menggunakannya kembali untuk semua gambar jauh lebih efisien daripada membuat instance baru per file. Ini juga memungkinkan Aspose berbagi sumber daya internal, yang esensial untuk **parallel OCR processing**.

## Langkah 2 – Membuat Daftar Gambar (Process Image List)

Selanjutnya kami mendefinisikan koleksi jalur file yang ingin dimasukkan ke dalam batch recogniser. Anda dapat menghasilkan daftar ini secara dinamis dengan `Directory.GetFiles`, tetapi demi kejelasan kami akan menuliskan beberapa entri secara manual.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*Tip:* Jika Anda memiliki ribuan scan, pertimbangkan menggunakan `Directory.EnumerateFiles` dengan filter seperti `*.jpg` untuk menghindari memuat seluruh daftar ke memori sekaligus.

## Langkah 3 – Menjalankan Batch Recognition (Parallel OCR Processing)

Sekarang masuk ke inti masalah: memanggil `BatchRecognize`. Metode ini menerima argumen `maxDegreeOfParallelism`, yang mengontrol berapa banyak thread yang akan dibuat Aspose. Secara default ia menggunakan empat thread, tetapi Anda dapat meningkatkan angka tersebut jika CPU Anda memiliki lebih banyak core.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*Apa yang terjadi di balik layar?* Aspose membagi koleksi `imagePaths` menjadi beberapa bagian, memberikan setiap bagian ke thread terpisah, dan menggabungkan hasilnya. Ini adalah cara paling efisien untuk **extract text from jpg** file ketika Anda memiliki **process image list** yang dapat ditangani secara bersamaan.

## Langkah 4 – Menampilkan Hasil (Read Text from Scans)

Akhirnya kami melakukan iterasi pada koleksi `recognitionResults` dan mencetak teks serta waktu pemrosesan masing‑masing file. Objek `OcrResult` juga memberikan nama file sumber, yang membantu ketika Anda perlu mencatat atau menyimpan output.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**Output yang diharapkan (contoh):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

Perhatikan bagaimana setiap blok memberi tahu nama file, berapa lama OCR berlangsung, dan teks yang diekstrak. Itulah informasi tepat yang Anda butuhkan saat **reading text from scans** dalam alur produksi.

## Menangani Kasus Edge Umum

| Situasi | Hal yang Perlu Diperhatikan | Perbaikan Cepat |
|-----------|-------------------|-----------|
| **Missing file** | `FileNotFoundException` dilempar di dalam `BatchRecognize` | Validasi jalur dengan `File.Exists` sebelum menambahkannya ke `imagePaths`. |
| **Unsupported format** | Aspose hanya menangani gambar raster (JPG, PNG, BMP, TIFF). | Konversi PDF ke gambar terlebih dahulu (gunakan Aspose.PDF) atau lewati file tersebut. |
| **Memory pressure** | Gambar sangat besar dapat menghabiskan RAM ketika banyak thread berjalan. | Turunkan `maxDegreeOfParallelism` atau ubah ukuran gambar sebelum OCR. |
| **Non‑English text** | Pengaturan bahasa ke English akan melewatkan skrip lain. | Ubah menjadi `Language = OcrLanguage.French` (atau kombinasi multibahasa). |

Tips ini membuat pekerjaan batch Anda lebih tangguh, terutama ketika Anda **processing an image list** yang berasal dari unggahan pengguna atau arsip scan.

## Pro Tip – Menyetel Parallelism

Jika Anda menjalankannya pada mesin 8‑core, naikkan parallelism menjadi 6 atau 8 dan lihat peningkatan kecepatan. Namun, ingat bahwa setiap thread juga mengonsumsi memori untuk bitmap. Aturan praktis yang baik:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

Masukkan `maxThreads` ke dalam `BatchRecognize` untuk konfigurasi dinamis yang menyesuaikan dengan mesin.

## Contoh Lengkap yang Siap Pakai (Copy‑Paste Ready)

Berikut adalah program lengkap, siap untuk dikompilasi. Ganti saja `YOUR_DIRECTORY` dengan jalur yang berisi scan JPG Anda.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Catatan:** Baris `using System.IO;` diperlukan untuk helper `Directory`. Kode mencetak pesan ramah jika tidak ada JPG yang ditemukan, mencegah kegagalan diam.

## Kesimpulan

Kami baru saja mendemonstrasikan alur kerja **batch OCR images** yang bersih, yang **extracts text from jpg** file, **reads text from scans**, dan secara efisien **processes an image list** menggunakan **parallel OCR processing**. Contoh lengkap yang dapat dijalankan menunjukkan persis cara menyiapkan mesin, memberi koleksi file, dan menangani hasil—semua sambil menjaga penggunaan memori dan jumlah thread tetap terkendali.

Siap untuk langkah berikutnya? Coba ganti bahasa ke French, tambahkan konversi PDF‑ke‑gambar, atau simpan teks OCR ke basis data. Polanya tetap sama: inisialisasi sekali, beri daftar, dan biarkan Aspose melakukan pekerjaan berat secara paralel.

Ada pertanyaan atau ingin berbagi modifikasi Anda? Tinggalkan komentar di bawah, dan selamat coding! 

![Batch OCR images processing flow](https://example.com/placeholder.png "Diagram illustrating batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}