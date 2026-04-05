---
category: general
date: 2026-04-04
description: Cara melakukan OCR batch dengan Aspose.OCR di C#. Pelajari cara mengekstrak
  teks dari gambar, mengekspor ringkasan CSV, dan menangani OCR gambar massal secara
  efisien.
draft: false
keywords:
- how to batch ocr
- extract text images
- how to export csv
- bulk image ocr
- batch ocr images
language: id
og_description: Cara melakukan OCR batch di C# dengan Aspose.OCR. Dapatkan solusi
  lengkap untuk mengekstrak teks dari gambar dan mengekspor ringkasan CSV.
og_title: Cara Batch OCR di C# – Tutorial Langkah-demi-Langkah Lengkap
tags:
- OCR
- C#
- Aspose
- Automation
title: Cara Batch OCR di C# – Panduan Lengkap untuk Ekstraksi Teks Gambar secara Massal
url: /id/net/text-recognition/how-to-batch-ocr-in-c-complete-guide-for-bulk-image-text-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR – Tutorial C# Lengkap

Pernah bertanya‑tanya **bagaimana cara batch OCR** seluruh folder gambar tanpa menulis rutinitas terpisah untuk setiap file? Anda tidak sendirian. Dalam banyak proyek dunia nyata—seperti pemrosesan faktur, pengarsipan buku yang dipindai, atau digitalisasi massal kwitansi—para pengembang membutuhkan cara yang cepat dan andal untuk mengekstrak teks dari puluhan bahkan ribuan gambar.  

Dalam panduan ini kami akan menelusuri contoh lengkap yang siap dijalankan yang menunjukkan **cara batch OCR**, **mengekstrak teks dari gambar**, dan **mengekspor ringkasan CSV** menggunakan Aspose.OCR. Pada akhir tutorial Anda akan memiliki satu program C# yang dapat mengambil direktori gambar apa pun, mengubahnya menjadi file teks yang dapat dicari, dan memberikan laporan CSV yang rapi tentang operasi tersebut. Tidak ada misteri, hanya kode yang jelas dan tips praktis.

## Apa yang Akan Anda Pelajari

- Menyiapkan mesin Aspose.OCR untuk bahasa Inggris (atau bahasa lain yang didukung).  
- Memproses seluruh folder gambar sekaligus—sempurna untuk OCR gambar dalam jumlah besar.  
- Menyimpan setiap hasil OCR sebagai file `.txt` sambil secara opsional menghasilkan file CSV yang mencantumkan nama gambar sumber dan panjang teks yang diekstrak.  
- Menangani kasus tepi umum seperti tipe file yang tidak didukung, folder kosong, dan karakter Unicode.  

**Prasyarat** – Anda memerlukan .NET 6+ (atau .NET Framework 4.7.2+), Visual Studio 2022 atau IDE pilihan Anda, dan lisensi Aspose.OCR yang valid (versi percobaan gratis cukup untuk demo). Tidak ada pustaka pihak ketiga lain yang diperlukan.

![diagram batch OCR](https://example.com/ocr-flow.png "diagram alur batch OCR")

## Langkah 1: Instal Aspose.OCR dan Buat Proyek Konsol Baru

Untuk memulai, tambahkan paket NuGet Aspose.OCR ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, Anda juga dapat klik kanan proyek → *Manage NuGet Packages* → cari *Aspose.OCR* → instal.

Buat aplikasi konsol baru (`dotnet new console -n BulkOcrDemo`) dan buka `Program.cs`. Ini akan menjadi tempat semua kode kita.

## Langkah 2: Inisialisasi Mesin OCR – Pilih Bahasa yang Tepat

Mesin OCR perlu mengetahui bahasa apa yang harus dicari. Bahasa Inggris adalah yang paling umum, tetapi Anda dapat menggantinya dengan bahasa Spanyol, Prancis, dll., dengan mengubah `Language.English`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

// Step 2: Set up the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // You can switch to Language.Spanish, Language.French, etc.
    Language = Language.English
};
```

**Mengapa ini penting:** Menentukan bahasa meningkatkan akurasi karena mesin dapat menerapkan kamus dan set karakter khusus bahasa tersebut. Jika Anda melewatkannya, mesin akan menggunakan model generik yang mungkin salah mengartikan karakter.

## Langkah 3: Tentukan Jalur Sumber, Output, dan CSV Opsional

Kita memerlukan tiga folder:

| Jalur | Tujuan |
|------|---------|
| `sourceFolder` | Tempat gambar asli berada. |
| `outputFolder` | Tempat setiap hasil OCR (`.txt`) akan disimpan. |
| `csvSummaryPath` | (Opsional) File CSV yang mencatat setiap nama gambar dan panjang teks yang diekstrak. |

```csharp
// Step 3: Folder locations – update these to match your environment
string sourceFolder = @"C:\OcrDemo\Images\Bulk";
string outputFolder = @"C:\OcrDemo\Output\BulkResults";
string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional
```

> **Tip:** Gunakan `Path.Combine` untuk kompatibilitas lintas‑platform; secara otomatis menyisipkan pemisah direktori yang tepat.

## Langkah 4: Jalankan Batch Processor

Aspose.OCR menyediakan `BatchProcessor` yang praktis untuk melakukan pekerjaan berat. Ia akan mengiterasi setiap gambar yang didukung (`.png`, `.jpg`, `.tif`, dll.), menjalankan OCR, dan menulis hasilnya.

```csharp
// Step 4: Process the entire folder
BatchProcessor.ProcessFolder(
    sourceFolder: sourceFolder,
    outputFolder: outputFolder,
    engine: ocrEngine,
    csvSummaryPath: csvSummaryPath);
```

### Apa yang Terjadi di Balik Layar?

1. **Penemuan file** – Processor memindai `sourceFolder` untuk file gambar.  
2. **Eksekusi OCR** – Setiap gambar diberikan ke `ocrEngine`.  
3. **Penyimpanan teks** – Teks yang dikenali ditulis ke file `.txt` dengan nama dasar yang sama di `outputFolder`.  
4. **Pencatatan CSV** – Jika `csvSummaryPath` disediakan, processor menambahkan baris: `ImageName,CharactersExtracted,ProcessingTimeMs`.  

## Langkah 5: Tambahkan Penanganan Error dan Dukungan Kasus Tepi

Job batch yang kuat harus dapat bertahan dari file yang hilang, format yang tidak didukung, dan direktori kosong. Bungkus pemanggilan proses dalam blok `try/catch` dan validasi input terlebih dahulu.

```csharp
try
{
    // Validate folders
    if (!Directory.Exists(sourceFolder))
        throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

    Directory.CreateDirectory(outputFolder); // ensures output exists

    // Optional: clean previous CSV
    if (File.Exists(csvSummaryPath))
        File.Delete(csvSummaryPath);

    // Run the batch
    BatchProcessor.ProcessFolder(
        sourceFolder: sourceFolder,
        outputFolder: outputFolder,
        engine: ocrEngine,
        csvSummaryPath: csvSummaryPath);

    Console.WriteLine("✅ Batch OCR completed successfully!");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
}
```

**Mengapa menambahkan ini?** Tanpa validasi, program dapat gagal secara diam‑diam, meninggalkan folder output kosong tanpa petunjuk mengapa. Pesan eksplisit memudahkan proses debug.

## Langkah 6: Verifikasi Hasil – Apa yang Diharapkan

Setelah proses selesai, buka `outputFolder`. Anda akan melihat file `.txt` untuk setiap gambar:

```
C:\OcrDemo\Output\BulkResults\invoice_001.txt
C:\OcrDemo\Output\BulkResults\receipt_2023-03-15.txt
...
```

Setiap file berisi output OCR mentah—teks polos yang dapat Anda masukkan ke indeks pencarian, basis data, atau pipeline NLP selanjutnya.

Jika Anda menyediakan `csvSummaryPath`, buka `summary.csv`. Isinya akan terlihat seperti:

```
ImageName,CharactersExtracted,ProcessingTimeMs
invoice_001.png,1245,312
receipt_2023-03-15.jpg,378,98
...
```

CSV memudahkan pembuatan laporan, mengidentifikasi hasil yang terlalu pendek (kemungkinan kegagalan pemindaian), atau mengirim metrik ke dasbor pemantauan.

## Langkah 7: Perluas Solusi – Variasi Umum

### 7.1 Ubah Format Output

Alih‑alih file `.txt` biasa, Anda mungkin menginginkan PDF atau JSON. `BatchProcessor` memungkinkan Anda menyediakan callback khusus:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    (imagePath, ocrResult) =>
    {
        // Example: save as JSON
        var json = System.Text.Json.JsonSerializer.Serialize(new { Text = ocrResult.Text });
        string jsonPath = Path.ChangeExtension(Path.Combine(outputFolder,
                              Path.GetFileNameWithoutExtension(imagePath)), ".json");
        File.WriteAllText(jsonPath, json);
    });
```

### 7.2 Proses Banyak Bahasa

Jika folder Anda berisi dokumen multibahasa, Anda dapat mendeteksi bahasa per gambar atau menjalankan dua kali proses:

```csharp
ocrEngine.Language = Language.Spanish; // first pass
BatchProcessor.ProcessFolder(...);
ocrEngine.Language = Language.English; // second pass
BatchProcessor.ProcessFolder(...);
```

### 7.3 Lewati File Korup dengan Elegan

Tambahkan filter di dalam loop (atau gunakan overload yang menerima predicate) untuk mengabaikan file yang menimbulkan exception:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    filter: path => !Path.GetFileName(path).StartsWith("ignore_"));
```

## Contoh Kerja Lengkap

Berikut adalah `Program.cs` lengkap yang dapat Anda salin‑tempel ke proyek konsol baru. Ganti jalur folder dengan milik Anda.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BulkOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine – set language to English
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Define folders – adjust these for your environment
            string sourceFolder = @"C:\OcrDemo\Images\Bulk";
            string outputFolder = @"C:\OcrDemo\Output\BulkResults";
            string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional

            try
            {
                // 3️⃣ Validate folders
                if (!Directory.Exists(sourceFolder))
                    throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

                Directory.CreateDirectory(outputFolder); // creates if missing

                // 4️⃣ Clean previous CSV (optional)
                if (File.Exists(csvSummaryPath))
                    File.Delete(csvSummaryPath);

                // 5️⃣ Run the batch OCR
                BatchProcessor.ProcessFolder(
                    sourceFolder: sourceFolder,
                    outputFolder: outputFolder,
                    engine: ocrEngine,
                    csvSummaryPath: csvSummaryPath);

                Console.WriteLine("✅ Batch OCR completed successfully!");
                Console.WriteLine($"📂 Text files are in: {outputFolder}");
                Console.WriteLine($"📄 CSV summary (if requested) at: {csvSummaryPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Output Konsol yang Diharapkan

```
✅ Batch OCR completed successfully!
📂 Text files are in: C:\OcrDemo\Output\BulkResults
📄 CSV summary (if requested) at: C:\OcrDemo\Output\BulkResults\summary.csv
```

Buka salah satu file `.txt` yang dihasilkan dan Anda akan melihat teks yang diekstrak, siap untuk diproses lebih lanjut.

## Pertanyaan yang Sering Diajukan

**Apakah ini bekerja dengan input PDF?**  
Aspose.OCR dapat menangani halaman PDF jika Anda terlebih dahulu mengonversinya menjadi gambar (misalnya, menggunakan Aspose.PDF). Batch processor sendiri hanya mencari format gambar raster.

**Bagaimana jika saya harus memproses 10.000 gambar?**  
`BatchProcessor` bawaan memproses setiap file satu per satu, sehingga penggunaan memori tetap rendah. Untuk beban kerja yang sangat besar Anda dapat memproses sub‑folder secara paralel, tetapi ingat bahwa OCR sangat intensif CPU—perhatikan jumlah core mesin Anda.

**Bisakah saya mengubah pengaturan akurasi OCR?**  
Ya. `ocrEngine` menyediakan properti seperti `Resolution` dan `PreprocessOptions`. Menyesuaikannya dapat meningkatkan hasil pada pemindaian berkualitas rendah, dengan mengorbankan kecepatan.

**Bagaimana cara melisensikan Aspose.OCR untuk produksi?**  
Letakkan file lisensi Anda (`Aspose.OCR.lic`) di direktori executable dan muat pada saat startup:

```csharp
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

## Kesimpulan

Anda kini memiliki **solusi lengkap dan siap produksi untuk cara batch OCR** menggunakan C#. Tutorial ini mencakup semua hal mulai dari instalasi Aspose.OCR, inisialisasi mesin, memproses seluruh folder, hingga mengekspor ringkasan CSV

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}