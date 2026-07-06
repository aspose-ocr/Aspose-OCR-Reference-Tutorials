---
category: general
date: 2026-05-06
description: Pelajari cara melakukan OCR batch di C# dan mengekstrak teks dari pemindaian
  dengan cepat menggunakan Aspose OCR Batch. Ikuti panduan lengkap langkah demi langkah
  dengan kode, tips, dan penanganan kasus khusus.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: id
og_description: Bagaimana cara melakukan OCR batch di C#? Panduan ini menunjukkan
  cara mengekstrak teks dari pemindaian secara efisien dengan Aspose OCR, dukungan
  GPU, dan pemrosesan paralel.
og_title: Cara Batch OCR di C# – Ekstrak Teks dari Pemindaian
tags:
- C#
- OCR
- Aspose
title: Cara Batch OCR di C# – Ekstrak Teks dari Pemindaian
url: /id/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di C# – Ekstrak Teks dari Scan

Pernah bertanya-tanya **bagaimana cara batch OCR** ketika Anda memiliki folder penuh PDF atau JPEG yang dipindai? Anda bukan satu-satunya yang menatap tumpukan gambar dan berpikir, “Harus ada cara yang lebih cepat untuk mengambil teksnya.” Dalam tutorial ini kami akan membahas solusi praktis yang tidak hanya memungkinkan Anda **mengekstrak teks dari scan** tetapi juga mempercepat proses dengan akselerasi GPU dan paralelisme.

Begini: melakukan OCR satu file pada satu waktu sangat memakan waktu, terutama jika Anda menangani puluhan atau ratusan halaman. Pada akhir panduan ini Anda akan memiliki aplikasi konsol C# yang siap‑jalankan yang memproses seluruh direktori dalam satu perintah, memberikan Anda file teks bersih yang siap untuk diindeks, dicari, atau apa pun selanjutnya.

## Prasyarat

- **.NET 6.0 atau lebih baru** (kode menggunakan fitur C# modern).
- **Lisensi untuk Aspose.OCR** (versi percobaan gratis dapat digunakan untuk pengujian).
- Mesin yang **kompatibel dengan GPU** **jika Anda ingin mengaktifkan `UseGpu`**; jika tidak, pustaka akan kembali ke CPU.
- Familiaritas dasar dengan **aplikasi konsol C#**.

Tidak ada layanan eksternal, tidak ada file konfigurasi tersembunyi—hanya SDK dan folder gambar.

## Langkah 1: Instal Paket NuGet Aspose.OCR

Pertama, tambahkan pustaka Aspose OCR ke proyek Anda. Buka terminal di folder solusi Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, Anda juga dapat menambahkan paket melalui UI NuGet Package Manager.

## Langkah 2: Buat Kerangka Aplikasi Konsol

Mari siapkan aplikasi konsol minimal yang akan menampung batch processor kami. Buat file baru bernama `Program.cs` dan tempelkan kerangka berikut:

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

Mengapa membungkus logika di dalam `Main`? Karena aplikasi konsol memberi kami umpan balik instan melalui `Console.WriteLine`, sempurna untuk verifikasi cepat bahwa pekerjaan **batch OCR** memang selesai.

## Langkah 3: Konfigurasikan OcrBatchProcessor

Sekarang inti dari solusi. Kami akan menginstansiasi `OcrBatchProcessor`, menunjuk ke folder input kami, memberi tahu di mana menyimpan hasil, dan menyesuaikan beberapa pengaturan kinerja.

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### Mengapa pengaturan ini penting

| Setting | Apa fungsinya | Kapan Anda mungkin mengubahnya |
|---------|--------------|--------------------------|
| `InputFolder` | Jalur ke scan yang ingin diproses. | Gunakan jalur relatif untuk portabilitas. |
| `OutputFolder` | Tempat teks yang diekstrak dari setiap gambar akan disimpan sebagai file `.txt`. | Arahkan ke share jaringan jika Anda memerlukan penyimpanan terpusat. |
| `Language` | Model bahasa OCR; kami memilih Spanish untuk mengilustrasikan dukungan multibahasa. | Ganti ke `OcrLanguage.English` atau bahasa lain yang didukung. |
| `UseGpu` | Memindahkan perhitungan matriks berat ke GPU. | Set ke `false` pada server tanpa GPU. |
| `MaxDegreeOfParallelism` | Mengontrol berapa banyak gambar yang diproses sekaligus. | Kurangi pada mesin dengan CPU rendah untuk menghindari throttling. |

## Langkah 4: Jalankan Operasi Batch dengan Penanganan Kesalahan

Menjalankan batch sesederhana memanggil `Execute()`, tetapi kami akan membungkusnya dalam blok try‑catch sehingga Anda mendapatkan pesan bantuan jika ada yang salah (mis., folder tidak ada, format gambar tidak didukung).

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

Saat processor selesai, Anda akan melihat **Batch completed.** di konsol, dan setiap gambar sumber akan memiliki file `.txt` yang cocok di `OcrResults`. Nama file mencerminkan yang asli, memudahkan pemetaan kembali ke scan asli.

## Langkah 5: Verifikasi Output – Apa yang Diharapkan

Setelah program dijalankan, buka file apa pun di dalam `YOUR_DIRECTORY/OcrResults`. Anda harus melihat konten teks biasa yang diekstrak dari gambar yang bersangkutan, misalnya:

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

Jika output terlihat berantakan, periksa kembali bahwa `Language` cocok dengan bahasa scan Anda. Aspose OCR mendukung lebih dari 100 bahasa, jadi Anda dapat mengganti `OcrLanguage.Spanish` dengan bahasa apa pun yang Anda butuhkan.

## Menangani Kasus Tepi dan Kesalahan Umum

### 1. GPU Tidak Tersedia

Jika mesin Anda tidak memiliki GPU yang kompatibel, `UseGpu = true` akan diam-diam kembali ke mode CPU, tetapi Anda akan kehilangan percepatan kecepatan. Untuk lebih jelas, Anda dapat mendeteksi kemampuan GPU:

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. File Besar Melebihi Memori

Saat menangani TIFF atau PDF yang sangat besar, pertimbangkan untuk memecahnya menjadi gambar yang lebih kecil terlebih dahulu. Aspose OCR dapat menangani PDF multi‑halaman, tetapi konsumsi memori meningkat seiring jumlah halaman. Langkah pra‑pemrosesan sederhana menggunakan `Aspose.Imaging` dapat memotong dokumen menjadi potongan yang dapat dikelola.

### 3. File Non‑Gambar di Folder Input

Batch processor mengabaikan file yang tidak dapat diparsing, tetapi sebaiknya folder tetap bersih. Anda dapat memfilter berdasarkan ekstensi:

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(Catatan: `FileFilter` adalah properti hipotetis; ganti dengan API aktual jika tersedia.)*

## Contoh Kerja Lengkap

Berikut adalah program lengkap yang siap disalin‑tempel. Ganti `YOUR_DIRECTORY` dengan jalur absolut di mesin Anda.

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Output Konsol yang Diharapkan

```
Batch completed.
```

Dan di `C:\OcrResults` Anda akan menemukan file `.txt` untuk setiap gambar di `C:\MyScans`.

## Kesimpulan

Anda kini memiliki cara yang solid dan siap produksi untuk **batch OCR** di C# dan **mengekstrak teks dari scan** tanpa harus membuka setiap file secara manual. Dengan memanfaatkan batch API Aspose, akselerasi GPU, dan paralelisme yang dapat dikonfigurasi, solusi ini dapat diskalakan dari beberapa halaman hingga ribuan.

Selanjutnya? Coba ide-ide berikut:

- **Integrasikan dengan indeks pencarian** (mis., Elasticsearch) untuk membuat teks yang diekstrak dapat dicari.
- **Tambahkan pemrosesan pasca** seperti pemeriksaan ejaan atau deteksi bahasa.
- **Bungkus aplikasi konsol dalam Windows Service** untuk pemantauan terus-menerus pada folder drop.

Silakan bereksperimen, sesuaikan level paralelisme, atau ganti model bahasa. Jika Anda mengalami kendala, tinggalkan komentar di bawah—selamat OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}