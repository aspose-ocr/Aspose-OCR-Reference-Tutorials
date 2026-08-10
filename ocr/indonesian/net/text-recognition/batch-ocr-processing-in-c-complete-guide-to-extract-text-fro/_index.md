---
category: general
date: 2026-06-16
description: Pemrosesan OCR batch di C# memungkinkan Anda mengonversi gambar menjadi
  teks dengan cepat. Pelajari cara mengekstrak teks dari gambar menggunakan Aspose.OCR
  dengan kode langkah demi langkah.
draft: false
keywords:
- batch OCR processing
- extract text from images
- convert images to text
language: id
og_description: Pemrosesan OCR batch di C# mengubah gambar menjadi teks. Ikuti panduan
  ini untuk mengekstrak teks dari gambar menggunakan Aspose.OCR.
og_title: Pemrosesan OCR Batch di C# – Ekstrak Teks dari Gambar
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  headline: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  type: TechArticle
- description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  name: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  steps:
  - name: Expected Output
    text: 'Assuming you have three images (`invoice1.png`, `receipt2.jpg`, `form3.tif`)
      in the input folder, the output folder will contain:'
  - name: What if some images fail to process?
    text: '`OcrBatchProcessor` logs errors to the console by default and continues
      with the next file. For production use, you can subscribe to the `OnError` event
      to collect failed filenames and retry later.'
  - name: Can I process PDFs directly?
    text: Yes. Aspose.OCR treats each page of a PDF as an image internally. Just point
      `InputFolder` to a directory containing PDFs, and the processor will extract
      text from every page—effectively **convert images to text** even when the source
      is a PDF.
  - name: How do I handle multi‑language documents?
    text: Set `Language` to `OcrLanguage.Multilingual` or specify a list of languages
      if the library version supports it. The engine will attempt to recognize characters
      from all provided languages, which is handy for international invoices.
  - name: What about memory consumption?
    text: The batch processor streams each image, so memory usage stays low even with
      thousands of files. However, enabling a high `MaxDegreeOfParallelism` on a memory‑constrained
      machine could cause spikes. Monitor your RAM and adjust the thread count accordingly.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Pemrosesan OCR Batch di C# – Panduan Lengkap untuk Mengekstrak Teks dari Gambar
url: /id/net/text-recognition/batch-ocr-processing-in-c-complete-guide-to-extract-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pemrosesan OCR Batch di C# – Panduan Lengkap untuk Mengekstrak Teks dari Gambar

Pernah bertanya-tanya bagaimana cara **memproses OCR secara batch** di C# tanpa menulis loop terpisah untuk setiap gambar? Anda tidak sendirian. Ketika Anda memiliki puluhan—atau bahkan ratusan—tanda terima, faktur, atau catatan tulisan tangan yang dipindai, memberi makan setiap file ke mesin OCR secara manual dengan cepat menjadi mimpi buruk.  

Kabar baiknya? Dengan Aspose.OCR Anda dapat *mengonversi gambar menjadi teks* dalam satu operasi yang rapi. Pada tutorial ini kami akan membahas seluruh alur kerja, mulai dari menginstal pustaka hingga menjalankan pekerjaan batch siap produksi yang **mengekstrak teks dari gambar** dan menyimpan hasilnya dalam format yang Anda butuhkan.

> **Apa yang akan Anda dapatkan:** Aplikasi konsol siap‑jalankan yang memproses seluruh folder, menulis file teks biasa (atau JSON, XML, HTML, PDF) berdampingan dengan file asli, dan menunjukkan cara menyesuaikan paralelisme untuk throughput maksimal.

## Prasyarat

- .NET 6.0 SDK atau lebih baru (kode ini bekerja dengan .NET Core dan .NET Framework)
- Visual Studio 2022, VS Code, atau editor C# pilihan Anda
- Lisensi Aspose.OCR NuGet (versi percobaan gratis cukup untuk evaluasi)
- Sebuah folder berisi file gambar (`.png`, `.jpg`, `.tif`, dll.) yang ingin Anda **konversi gambar menjadi teks**

Jika semua poin di atas sudah terpenuhi, mari kita mulai.

![Diagram yang menggambarkan alur pemrosesan batch OCR](batch-ocr-workflow.png "Alur pemrosesan batch OCR")

## Langkah 1: Instal Aspose.OCR via NuGet

Pertama, tambahkan paket Aspose.OCR ke proyek Anda. Buka terminal di direktori proyek dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Atau, jika Anda berada di dalam Visual Studio, klik kanan *Dependencies → Manage NuGet Packages*, cari **Aspose.OCR**, dan klik *Install*. Baris tunggal ini akan mengunduh semua yang Anda perlukan untuk **memproses OCR secara batch**.

> **Pro tip:** Selalu perbarui versi paket; rilis terbaru (per Juni 2026) menambahkan dukungan untuk format gambar baru dan meningkatkan akurasi multibahasa.

## Langkah 2: Buat Kerangka Konsol

Buat aplikasi konsol C# baru (jika belum) dan ganti `Program.cs` yang dihasilkan dengan kerangka berikut. Perhatikan direktif `using Aspose.OCR;` di bagian atas – itulah namespace yang menyediakan kelas `OcrBatchProcessor`.

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // We'll fill this in later.
    }
}
```

Pada titik ini file hanya berisi placeholder, namun merupakan titik awal yang bersih untuk logika **pemrosesan OCR batch** kami.

## Langkah 3: Inisialisasi OcrBatchProcessor

`OcrBatchProcessor` adalah mesin utama yang memindai folder, menjalankan OCR pada setiap gambar yang didukung, dan menulis output. Membuat instansinya semudah:

```csharp
// Step 3: Create an OCR batch processor instance
var ocrBatchProcessor = new OcrBatchProcessor();
```

Mengapa menggunakan batch processor alih‑alih API gambar tunggal? Kelas batch secara otomatis menangani enumerasi file, pencatatan error, dan bahkan eksekusi paralel, yang berarti Anda menghabiskan lebih sedikit waktu menulis loop dan lebih banyak waktu menyempurnakan akurasi.

## Langkah 4: Tentukan Folder Input dan Output Anda

Beritahu processor di mana membaca gambar dan di mana menaruh hasilnya. Ganti path placeholder dengan direktori nyata di mesin Anda.

```csharp
// Step 4: Configure the input folder containing images to process
ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

// Step 5: Set the folder where OCR results will be saved
ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";
```

Kedua folder harus ada sebelum Anda menjalankan aplikasi; jika tidak, Anda akan mendapatkan `DirectoryNotFoundException`. Membuatnya secara programatik mudah, tetapi demi kejelasan contoh tetap sederhana.

## Langkah 5: Pilih Format Output

Aspose.OCR dapat menghasilkan teks biasa, JSON, XML, HTML, atau bahkan PDF. Untuk kebanyakan skenario **mengekstrak teks dari gambar**, teks biasa sudah cukup, tetapi Anda bebas mengubahnya.

```csharp
// Step 6: Choose the desired output format (e.g., plain text)
ocrBatchProcessor.OutputFormat = ResultFormat.Text;   // alternatives: Json, Xml, Html, Pdf, etc.
```

Jika Anda memerlukan data terstruktur untuk pemrosesan selanjutnya, `ResultFormat.Json` adalah pilihan yang solid. Pustaka secara otomatis membungkus teks tiap halaman dalam objek JSON, mempertahankan informasi tata letak.

## Langkah 6: Atur Bahasa dan Paralelisme

Akurasi OCR bergantung pada model bahasa yang tepat. Bahasa Inggris cocok untuk kebanyakan dokumen Barat, tetapi Anda dapat memilih bahasa lain yang didukung (Arab, Cina, dll.). Selain itu, Anda dapat menentukan berapa banyak thread yang dijalankan—maksimum empat secara default.

```csharp
// Step 7: Specify the language for OCR recognition
ocrBatchProcessor.Language = OcrLanguage.English;

// Step 8: Define the level of parallelism (up to 4 concurrent threads)
ocrBatchProcessor.MaxDegreeOfParallelism = 4;
```

**Mengapa paralelisme penting:** Jika Anda memiliki CPU quad‑core, mengatur `MaxDegreeOfParallelism` ke `4` dapat memotong waktu pemrosesan sekitar 75 %. Pada laptop dengan dua core, `2` lebih aman. Eksperimenlah untuk menemukan titik optimal bagi perangkat keras Anda.

## Langkah 7: Jalankan Pekerjaan Batch

Sekarang pekerjaan berat dimulai. Satu baris meluncurkan seluruh pipeline, memproses setiap gambar di folder input dan menulis hasilnya ke folder output.

```csharp
// Step 9: Execute the batch processing of all supported image files
ocrBatchProcessor.Execute();

Console.WriteLine("Batch OCR completed.");
```

Ketika konsol menampilkan *Batch OCR completed.*, Anda akan menemukan file `.txt` (atau format apa pun yang Anda pilih) di samping setiap gambar asli. Nama file cocok dengan sumbernya, sehingga mudah mengaitkan output OCR dengan gambar asal.

## Contoh Program Lengkap

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke `Program.cs` dan jalankan langsung:

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create an OCR batch processor instance
        var ocrBatchProcessor = new OcrBatchProcessor();

        // Step 2: Configure the input folder containing images to process
        ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

        // Step 3: Set the folder where OCR results will be saved
        ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";

        // Step 4: Choose the desired output format (plain text is default)
        ocrBatchProcessor.OutputFormat = ResultFormat.Text; // alternatives: Json, Xml, Html, Pdf, etc.

        // Step 5: Specify the language for OCR recognition
        ocrBatchProcessor.Language = OcrLanguage.English;

        // Step 6: Define the level of parallelism (up to 4 concurrent threads)
        ocrBatchProcessor.MaxDegreeOfParallelism = 4;

        // Step 7: Execute the batch processing of all supported image files
        ocrBatchProcessor.Execute();

        Console.WriteLine("Batch OCR completed.");
    }
}
```

### Output yang Diharapkan

Misalkan Anda memiliki tiga gambar (`invoice1.png`, `receipt2.jpg`, `form3.tif`) di folder input, folder output akan berisi:

```
invoice1.txt
receipt2.txt
form3.txt
```

Setiap file `.txt` berisi karakter mentah yang diekstrak dari gambar yang bersangkutan. Buka file apa pun dengan Notepad, dan Anda akan melihat representasi teks biasa dari hasil scan asli.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika beberapa gambar gagal diproses?

`OcrBatchProcessor` mencatat error ke konsol secara default dan melanjutkan ke file berikutnya. Untuk penggunaan produksi, Anda dapat berlangganan ke event `OnError` untuk mengumpulkan nama file yang gagal dan mencoba lagi nanti.

```csharp
ocrBatchProcessor.OnError += (sender, args) =>
{
    Console.WriteLine($"Failed on {args.FileName}: {args.Exception.Message}");
};
```

### Bisakah saya memproses PDF secara langsung?

Ya. Aspose.OCR memperlakukan tiap halaman PDF sebagai gambar secara internal. Cukup arahkan `InputFolder` ke direktori yang berisi PDF, dan processor akan mengekstrak teks dari setiap halaman—secara efektif **mengonversi gambar menjadi teks** meskipun sumbernya PDF.

### Bagaimana menangani dokumen multibahasa?

Setel `Language` ke `OcrLanguage.Multilingual` atau tentukan daftar bahasa jika versi pustaka mendukungnya. Mesin akan berusaha mengenali karakter dari semua bahasa yang diberikan, sangat berguna untuk faktur internasional.

### Bagaimana dengan konsumsi memori?

Batch processor mem‑stream tiap gambar, sehingga penggunaan memori tetap rendah bahkan dengan ribuan file. Namun, mengaktifkan `MaxDegreeOfParallelism` yang tinggi pada mesin dengan memori terbatas dapat menyebabkan lonjakan. Pantau RAM Anda dan sesuaikan jumlah thread bila diperlukan.

## Tips untuk Akurasi Lebih Baik

- **Pra‑proses gambar**: Bersihkan noise, luruskan (deskew), dan ubah ke skala abu‑abu sebelum OCR. Aspose.OCR menyediakan `ImagePreprocessOptions` yang dapat Anda lampirkan ke `ocrBatchProcessor`.
- **Pilih format yang tepat**: Jika Anda memerlukan preservasi tata letak, `ResultFormat.Html` atau `Pdf` mempertahankan baris baru dan styling dasar.
- **Validasi hasil**: Implementasikan langkah pasca‑pemrosesan sederhana yang memeriksa file output kosong—hal ini sering menandakan pengenalan gagal.

## Langkah Selanjutnya

Setelah Anda menguasai **pemrosesan OCR batch** untuk **mengekstrak teks dari gambar**, Anda mungkin ingin:

- **Integrasikan dengan basis data** – simpan setiap hasil OCR bersama metadata untuk pencarian.
- **Tambahkan UI** – bangun antarmuka WPF atau WinForms kecil untuk memungkinkan pengguna menyeret‑dan‑menjatuhkan folder.
- **Skalakan** – jalankan pekerjaan batch di Azure Functions atau AWS Lambda untuk pemrosesan berbasis cloud.

Setiap topik tersebut dibangun di atas konsep inti yang telah kami bahas, sehingga Anda siap memperluas solusi Anda.

---

**Selamat coding!** Jika Anda menemui kendala atau memiliki ide perbaikan, tinggalkan komentar di bawah. Mari terus berdiskusi dan membuat otomasi OCR semakin mulus.


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}