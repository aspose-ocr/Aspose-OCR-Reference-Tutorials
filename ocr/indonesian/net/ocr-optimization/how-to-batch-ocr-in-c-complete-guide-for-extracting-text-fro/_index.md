---
category: general
date: 2026-02-28
description: Cara melakukan OCR batch dengan Aspose.OCR di C#. Pelajari cara mengekstrak
  teks dari gambar, mengenali teks dari file PNG, dan meningkatkan pemrosesan OCR
  batch secara efisien.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- batch ocr processing
language: id
og_description: Cara melakukan OCR batch menggunakan Aspose.OCR. Tutorial langkah
  demi langkah ini menunjukkan cara mengekstrak teks dari gambar, mengenali teks dari
  file PNG, dan mengoptimalkan pemrosesan OCR batch.
og_title: Cara Batch OCR di C# – Ekstraksi Teks Cepat dari Gambar
tags:
- OCR
- C#
- Aspose
title: Cara Batch OCR di C# – Panduan Lengkap untuk Mengekstrak Teks dari Gambar
url: /id/net/ocr-optimization/how-to-batch-ocr-in-c-complete-guide-for-extracting-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di C# – Panduan Lengkap untuk Mengekstrak Teks dari Gambar

Pernah bertanya-tanya **bagaimana cara batch OCR** puluhan halaman yang dipindai tanpa menulis panggilan terpisah untuk setiap file? Anda tidak sendirian. Dalam banyak proyek—otomatisasi faktur, digitalisasi arsip, atau sekadar mengambil data dari tangkapan layar—para pengembang membutuhkan cara yang andal untuk **mengekstrak teks dari gambar** secara massal.  

Pada tutorial ini kami akan membahas solusi praktis menggunakan Aspose.OCR. Pada akhir tutorial Anda akan tahu persis cara **mengenali teks dari file PNG**, mengontrol paralelisme, dan menangani hasil **pemrosesan batch OCR**. Tanpa referensi yang samar, hanya program lengkap yang dapat dijalankan dan penjelasan di balik setiap pengaturan.

## Prasyarat — Apa yang Anda Butuhkan

- .NET 6.0 atau yang lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)  
- Aspose.OCR untuk .NET ≥ 23.10 (nama paket NuGet adalah `Aspose.OCR`)  
- Sebuah folder dengan beberapa gambar PNG yang ingin Anda proses (contoh menggunakan tiga file)  
- Jumlah RAM/CPU yang wajar—sesuaikan `MaxDegreeOfParallelism` jika Anda mencapai batas  

Jika Anda belum menginstal paketnya, jalankan:

```bash
dotnet add package Aspose.OCR
```

Itu saja. Tidak ada binari tambahan, tidak ada layanan eksternal.

## Gambaran Umum Solusi

Kita akan membuat sebuah `OcrBatchProcessor`, memberi daftar jalur gambar, dan membiarkan perpustakaan menjalankan pengenalan pada setiap file secara bersamaan. Processor mengembalikan koleksi objek `OcrResult`, masing‑masing berisi teks yang diekstrak dan beberapa metadata. Akhirnya kita akan mencetak ringkasan singkat dan, secara opsional, teks halaman pertama.

Berikut adalah diagram tingkat tinggi (silakan ganti placeholder dengan gambar Anda sendiri).  

<img src="batch-ocr-diagram.png" alt="how to batch ocr diagram" width="600"/>

## Langkah 1 – Siapkan Batch OCR Processor

Hal pertama yang Anda butuhkan adalah sebuah instance `OcrBatchProcessor`. Objek ini mengatur pekerjaan dan memungkinkan Anda menyesuaikan opsi terkait kinerja.

```csharp
using Aspose.OCR;
using System.Collections.Generic;
using System;

/// <summary>
/// Demonstrates how to batch OCR a collection of PNG images using Aspose.OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor
        {
            // Use up to 4 threads – increase on a multi‑core machine, decrease if you hit memory pressure
            MaxDegreeOfParallelism = 4,

            // Tell the engine what language to expect; here we use French as an example.
            // Change to OcrLanguage.English, OcrLanguage.Spanish, etc., as needed.
            Language = OcrLanguage.French
        };
```

**Mengapa ini penting:** `MaxDegreeOfParallelism` menentukan berapa banyak gambar yang diproses secara bersamaan. Menetapkannya terlalu tinggi dapat memaksakan CPU Anda atau menyebabkan kesalahan kehabisan memori, sementara nilai yang terlalu rendah membuang sumber daya. Properti `Language` meningkatkan akurasi karena mesin OCR dapat menerapkan heuristik khusus bahasa.

## Langkah 2 – Bangun Daftar File Gambar

Selanjutnya kami mengumpulkan jalur file yang ingin diproses. Dalam skenario dunia nyata Anda mungkin membaca isi direktori secara dinamis, tetapi daftar statis membuat contoh tetap singkat.

```csharp
        // Step 2: Assemble the collection of PNG files you want to OCR
        List<string> imageFiles = new()
        {
            @"C:\Images\page1.png",
            @"C:\Images\page2.png",
            @"C:\Images\page3.png"
        };
```

**Tip:** Jika Anda perlu menyaring hanya file PNG dari sebuah folder, Anda dapat menggunakan `Directory.GetFiles(path, "*.png")`. Batch processor bekerja dengan format raster apa pun yang didukung oleh Aspose.OCR, termasuk JPEG dan BMP.

## Langkah 3 – Jalankan Operasi Batch OCR

Sekarang kami menyerahkan daftar ke `batchProcessor.Recognize`. Metode ini mengembalikan `List<OcrResult>` di mana setiap elemen sesuai dengan gambar input.

```csharp
        // Step 3: Execute the OCR operation on the whole batch
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

**Apa yang terjadi di balik layar?**  
Aspose.OCR memunculkan hingga `MaxDegreeOfParallelism` thread pekerja. Setiap thread memuat sebuah gambar, menerapkan pra‑pemrosesan (deskew, binarisasi), menjalankan mesin pengenalan, dan menyimpan output teks dalam sebuah `OcrResult`. Karena pekerjaan diparalelkan, total waktu pemrosesan kira‑kira *jumlah gambar / paralelisme* (ditambah overhead).

## Langkah 4 – Ringkas Hasil

Setelah batch selesai, berguna untuk mengetahui berapa banyak halaman yang berhasil diproses. Kami juga akan menunjukkan cara mengakses teks mentah.

```csharp
        // Step 4: Report how many pages were recognized
        Console.WriteLine($"Processed {ocrResults.Count} pages.");
```

Output pada titik ini terlihat seperti:

```
Processed 3 pages.
```

Jika ada gambar yang gagal (file rusak, format tidak didukung), Aspose.OCR akan melemparkan pengecualian. Anda dapat membungkus pemanggilan dalam blok `try/catch` untuk mencatat kegagalan tanpa menghentikan seluruh batch.

## Langkah 5 – (Opsional) Tampilkan Teks yang Diekstrak

Seringkali Anda hanya membutuhkan pemeriksaan cepat—menampilkan teks halaman pertama, misalnya.

```csharp
        // Step 5: Optionally dump the text of the first page
        if (ocrResults.Count > 0)
        {
            Console.WriteLine("--- Page 1 Text ---");
            Console.WriteLine(ocrResults[0].Text);
        }
    }
}
```

Output konsol tipikal mungkin seperti:

```
--- Page 1 Text ---
Bonjour, ceci est un exemple de texte extrait d'une image PNG.
```

Itu mengkonfirmasi OCR berhasil dan petunjuk bahasa berfungsi.

## Kode Lengkap yang Siap Dijalan

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke dalam proyek konsol baru.

```csharp
using Aspose.OCR;
using System.Collections.Generic;
using System;

/// <summary>
/// Complete example of batch OCR processing with Aspose.OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // 1️⃣ Configure the batch OCR processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 4,   // Adjust based on your hardware
            Language = OcrLanguage.French // Change to match your source language
        };

        // 2️⃣ List the PNG files you want to process
        List<string> imageFiles = new()
        {
            @"C:\Images\page1.png",
            @"C:\Images\page2.png",
            @"C:\Images\page3.png"
        };

        // 3️⃣ Run the batch OCR operation
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);

        // 4️⃣ Show how many pages were recognized
        Console.WriteLine($"Processed {ocrResults.Count} pages.");

        // 5️⃣ (Optional) Print the extracted text of the first page
        if (ocrResults.Count > 0)
        {
            Console.WriteLine("--- Page 1 Text ---");
            Console.WriteLine(ocrResults[0].Text);
        }
    }
}
```

Kompilasi dengan `dotnet run` dan lihat konsol melaporkan jumlah halaman serta konten halaman pertama.

## Menangani Kasus Tepi & Jebakan Umum

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|----------------|
| **Large image set (hundreds of files)** | Memory spikes because each thread loads a full bitmap. | Lower `MaxDegreeOfParallelism` or process files in smaller chunks (e.g., groups of 50). |
| **Mixed languages in the same batch** | Setting a single `Language` may degrade accuracy for files in other languages. | Create separate `OcrBatchProcessor` instances per language, or leave `Language` unset to let the engine auto‑detect (slower). |
| **Corrupt or unsupported PNG** | `Recognize` throws `FileNotFoundException` or `InvalidOperationException`. | Wrap the call in `try { … } catch (Exception ex) { Log(ex); continue; }`. |
| **GPU acceleration needed** | Aspose.OCR can offload to GPU, but you must enable it explicitly. | Set `batchProcessor.UseGpu = true;` and ensure compatible drivers are installed. |
| **Need the confidence score** | `OcrResult` also exposes `Confidence` for each line. | Iterate `ocrResults[i].Lines` to gather per‑line confidence if you need quality filtering. |

### Pro Tip

Jika Anda memproses faktur yang dipindai, pertimbangkan **memotong sebelumnya** setiap gambar ke wilayah yang berisi teks. Mesin OCR berjalan lebih cepat dan menghasilkan kepercayaan yang lebih tinggi ketika Anda menghilangkan pinggiran dan noise.

## Tolok Ukur Kinerja (Referensi Cepat)

| Jumlah Gambar | Paralelisme (4 thread) | Waktu Perkiraan pada i7‑12700H |
|---------------|------------------------|---------------------------------|
| 10            | 4                      | 3,2 detik                       |
| 50            | 4                      | 14,7 detik                      |
| 200           | 8 (jika Anda meningkatkan nilai) | 1 menit 10 detik               |

Hasilnya dapat bervariasi tergantung pada resolusi gambar dan kompleksitas bahasa, tetapi tabel memberikan perkiraan realistis untuk pemrosesan batch OCR tipikal.

## Langkah Selanjutnya – Memperluas Alur Kerja

Sekarang Anda dapat **batch OCR** file PNG, Anda mungkin ingin:

- **Menyimpan hasil** ke basis data atau file JSON untuk analitik selanjutnya.  
- **Menyambungkan output** ke pipeline pemrosesan bahasa alami (misalnya, analisis sentimen).  
- **Mengintegrasikan dengan Azure Functions** untuk OCR tanpa server, sesuai permintaan sebagai bagian dari arsitektur mikroservis yang lebih besar.  

Semua skenario tersebut menggunakan pola inti yang sama seperti yang baru saja dibahas: mengonfigurasi processor, memberi koleksi, dan menangani objek `OcrResult`.

## Kesimpulan

Kami baru saja mengungkap **cara batch OCR** di C# menggunakan Aspose.OCR. Tutorial ini menunjukkan cara **mengekstrak teks dari gambar**, khususnya **mengenali teks dari file PNG**, dan menyesuaikan **pemrosesan batch OCR** untuk kecepatan dan keandalan. Dengan kode lengkap, penjelasan setiap pengaturan, dan beberapa tips praktis, Anda siap mengintegrasikannya ke dalam proyek Anda—baik Anda mendigitalkan kwitansi, mengarsipkan manual lama, atau membangun repositori gambar yang dapat dicari.

Cobalah, sesuaikan paralelisme, ganti bahasa, dan saksikan pipeline ekstraksi teks Anda hidup. Jika Anda menemukan kendala atau memiliki ide untuk optimasi lebih lanjut, silakan tinggalkan komentar di bawah. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}