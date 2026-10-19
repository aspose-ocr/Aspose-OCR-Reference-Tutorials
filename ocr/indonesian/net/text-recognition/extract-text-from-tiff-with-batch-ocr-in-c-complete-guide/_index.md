---
category: general
date: 2026-04-11
description: Ekstrak teks dari file TIFF menggunakan pemrosesan batch Aspose OCR di
  C#. Pelajari cara memproses batch OCR secara efisien dan dapatkan umpan balik kemajuan
  secara waktu nyata.
draft: false
keywords:
- extract text from tiff
- process batch ocr
- OCR batch processing
- Aspose OCR C#
- TIFF image OCR
language: id
og_description: Ekstrak teks dari file TIFF menggunakan pemrosesan batch Aspose OCR
  di C#. Tutorial ini menunjukkan langkah demi langkah cara memproses OCR batch dan
  membaca kemajuan.
og_title: Ekstrak Teks dari TIFF dengan OCR Batch di C# – Panduan Lengkap
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Ekstrak Teks dari TIFF dengan OCR Batch di C# – Panduan Lengkap
url: /id/net/text-recognition/extract-text-from-tiff-with-batch-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari TIFF – Panduan Lengkap Batch OCR

Pernah perlu **mengekstrak teks dari TIFF** tetapi merasa terhambat pada bagian pemrosesan batch? Anda bukan satu-satunya. Dalam banyak proyek otomatisasi dokumen, menangani puluhan gambar TIF resolusi tinggi dapat dengan cepat menjadi bottleneck—terutama ketika Anda menginginkan umpan balik langsung tentang kemajuan.

Berita baik? Dengan Aspose OCR Anda dapat **process batch OCR** dalam beberapa baris kode, mendapatkan event kemajuan secara real‑time, dan menghasilkan teks yang dikenali untuk setiap gambar. Dalam tutorial ini kami akan membahas aplikasi konsol C# siap‑jalankan yang melakukan hal tersebut.

Kami akan membahas semua yang perlu Anda ketahui: paket yang diperlukan, mengapa setiap baris penting, kasus tepi seperti file yang hilang, dan cara memverifikasi hasilnya. Pada akhir tutorial Anda dapat menempatkan contoh ke dalam solusi Anda sendiri dan mulai mengekstrak teks dari gambar TIFF segera.

## Apa yang Anda Butuhkan

- **.NET 6 atau lebih baru** (kode juga dapat dikompilasi dengan .NET Core)  
- **Aspose.OCR untuk .NET** paket NuGet – `Install-Package Aspose.OCR`  
- Sebuah folder yang berisi beberapa gambar **TIFF** yang ingin Anda baca (demo menggunakan `img1.tif`, `img2.tif`, `img3.tif`)  
- IDE apa pun yang Anda suka – Visual Studio, Rider, atau VS Code sudah cukup  

Tidak diperlukan konfigurasi tambahan; pustaka ini dilengkapi dengan mesin OCR-nya sendiri, jadi Anda tidak perlu menginstal binary native eksternal.

---

## Langkah 1 – Buat Instance OCR Engine  

Hal pertama yang Anda lakukan adalah membuat sebuah `OcrEngine`. Anggaplah itu sebagai otak yang akan menganalisis setiap piksel dan mengubahnya menjadi karakter.

```csharp
using Aspose.OCR;

// Step 1: Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Mengapa ini penting:**  
> Engine menyimpan model bahasa internal dan pengaturan (mis., DPI, bahasa). Membuatnya sekali dan menggunakan kembali untuk batch jauh lebih efisien dibandingkan menginstansiasi engine baru untuk setiap gambar.

---

## Langkah 2 – Sambungkan Event Kemajuan Real‑Time  

Jika Anda memproses puluhan file TIFF, indikator kemajuan dapat menyelamatkan Anda dari kebingungan apakah aplikasi terhenti.

```csharp
using Aspose.OCR.Events;

// Step 2: Subscribe to progress updates
ocrEngine.ProgressChanged += Ocr_ProgressChanged;

// Event handler definition (placed later in the file)
```

Event `ProgressChanged` dipicu setelah setiap gambar selesai, memberikan Anda `Current`, `Total`, dan `Percentage`. Ini adalah loop umpan balik **process batch OCR** yang sering dilupakan oleh banyak pengembang.

---

## Langkah 3 – Bangun Daftar Image Stream  

Aspose.OCR bekerja dengan objek `ImageStream`. Cara termudah adalah memuat setiap TIFF dari disk.

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Step 3: Prepare the batch of TIFF images
List<ImageStream> imageFiles = new List<ImageStream>
{
    ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
};
```

> **Tip:**  
> Jika Anda memiliki folder dinamis, ganti daftar yang di‑hard‑code dengan `Directory.GetFiles(path, "*.tif")` dan `Select(ImageStream.FromFile)` – dengan cara itu Anda benar‑benar **process batch OCR** tanpa pembaruan manual.

---

## Langkah 4 – Jalankan Proses Batch OCR  

Sekarang pekerjaan berat dilakukan. `ProcessBatch` mengembalikan daftar read‑only dari objek `OcrResult`, masing‑masing berisi teks yang diekstrak dan skor kepercayaan.

```csharp
// Step 4: Execute batch OCR and collect results
IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);
```

> **Mengapa ini efisien:**  
> Engine menggunakan kembali model bahasa yang sama untuk semua gambar, secara dramatis mengurangi penggunaan memori dibandingkan panggilan satu‑gambar.

---

## Langkah 5 – Tampilkan atau Simpan Teks yang Diakui  

Akhirnya, iterasi hasilnya. Dalam proyek nyata Anda mungkin menuliskannya ke database atau file JSON, tetapi untuk demo ini kami hanya akan mencetak ke konsol.

```csharp
// Step 5: Output the recognised text for each TIFF
foreach (var result in ocrResults)
{
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();
}
```

**Output konsol yang diharapkan** (dipotong untuk singkatnya):

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,250.00

=== OCR Result ===
Meeting Minutes
1. Project kickoff...
```

Jika ada gambar yang gagal, `result.Text` akan menjadi string kosong, dan event `ProgressChanged` tetap melaporkan item sebagai diproses—sehingga Anda dapat mencatat kegagalan secara terpisah.

---

## Handler Event Progress (Kode Lengkap)

Tempatkan metode ini di mana saja di dalam kelas `BatchDemo`—sebaiknya setelah `Main`.

```csharp
private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
{
    // Gives you a live view of how many files have been processed
    Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
}
```

> **Pro tip:**  
> Alihkan output ini ke progress bar UI jika Anda membuat aplikasi desktop; event yang sama bekerja untuk WinForms, WPF, atau bahkan notifikasi ASP.NET Core SignalR.

---

## Contoh Lengkap Siap‑Jalankan  

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Events;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Subscribe to progress events
        ocrEngine.ProgressChanged += Ocr_ProgressChanged;

        // 3️⃣ Load TIFF images into a list
        List<ImageStream> imageFiles = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
        };

        // 4️⃣ Run batch OCR
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);

        // 5️⃣ Print results
        foreach (var result in ocrResults)
        {
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();
        }
    }

    // Progress event handler
    private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
    {
        Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
    }
}
```

Simpan file sebagai `Program.cs`, jalankan `dotnet add package Aspose.OCR`, ganti `YOUR_DIRECTORY` dengan path sebenarnya, dan tekan **Ctrl+F5**. Anda akan melihat angka kemajuan diikuti oleh teks yang diekstrak untuk setiap TIFF.

---

## Menangani Kasus Tepi Umum  

| Situasi | Hal yang Perlu Diperhatikan | Solusi Cepat |
|-----------|-------------------|-----------|
| **TIFF yang hilang atau rusak** | `ImageStream.FromFile` melempar `FileNotFoundException` atau `ArgumentException`. | Bungkus pembuatan daftar dalam `try/catch` dan lewati file yang tidak valid, catat masalahnya. |
| **Gambar sangat besar ( >10 MP )** | OCR dapat mengonsumsi banyak RAM dan melambat. | Kurangi DPI sebelum memproses: `ocrEngine.ImagePreprocessing.Dpi = 300;` |
| **Teks non‑Inggris** | Model bahasa default adalah Inggris. | Set `ocrEngine.Language = Language.Spanish;` (atau bahasa lain yang didukung). |
| **Perlu menyimpan hasil** | Output konsol tidak persisten. | Tulis `result.Text` ke file `.txt` menggunakan `File.WriteAllText`. |

Menangani skenario ini membuat solusi Anda lebih kuat dan menunjukkan bahwa Anda telah mempertimbangkan lebih dari jalur sukses.

---

## Langkah Selanjutnya & Topik Terkait  

- **Ekstrak teks dari PDF** – API serupa, cukup ganti `ImageStream` dengan `PdfDocument`.  
- **Parallel batch OCR** – untuk beban kerja besar, jalankan beberapa instance `OcrEngine` pada thread terpisah; ingat untuk menghormati batas lisensi.  
- **Post‑processing** – jalankan output OCR melalui pemeriksa ejaan atau regex untuk membersihkan artefak OCR umum.  

Semua ekstensi ini tetap bergantung pada ide inti **process batch OCR** dan dapat ditambahkan secara bertahap.

---

## Kesimpulan  

Kami baru saja mendemonstrasikan cara **mengekstrak teks dari TIFF** secara efisien dengan **process batch OCR** menggunakan Aspose OCR di C#. Contoh ini membuat satu engine, berlangganan ke event kemajuan, memuat daftar image stream, menjalankan batch, dan mencetak setiap hasil.

Dari sini Anda dapat mengintegrasikan output ke dalam database, menghasilkan PDF yang dapat dicari, atau mengalirkan teks ke pipeline NLP berikutnya. Tidak ada batasan—cobalah pengaturan bahasa, penyesuaian DPI, dan eksekusi paralel untuk menyesuaikan beban kerja spesifik Anda.

Ada pertanyaan atau ingin berbagi cara Anda menyesuaikan batch? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}