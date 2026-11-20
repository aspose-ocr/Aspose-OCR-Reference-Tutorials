---
category: general
date: 2026-03-26
description: Bagaimana melakukan OCR batch di C# memudahkan ekstraksi teks dari file
  PNG. Ikuti tutorial OCR C# langkah demi langkah ini untuk ekstraksi teks batch dengan
  Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: id
og_description: Cara melakukan OCR batch di C# memungkinkan Anda dengan cepat mengekstrak
  teks dari file PNG. Panduan ini membawa Anda melalui tutorial OCR C# lengkap dengan
  ekstraksi teks secara batch.
og_title: Cara melakukan OCR batch di C# – Ekstrak teks dari PNG
tags:
- OCR
- C#
- Aspose
title: Cara melakukan OCR batch di C# – Ekstrak teks dari PNG
url: /id/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan batch OCR di C# – Ekstrak teks dari PNG

Pernah bertanya-tanya **bagaimana melakukan batch OCR** pada sekumpulan screenshot tanpa menulis program terpisah untuk tiap file? Anda tidak sendirian. Dalam banyak proyek kami berakhir dengan puluhan PNG yang perlu teksnya diambil, dan melakukannya satu‑per‑satu sangat merepotkan.  

Kabar baik? Dengan Aspose OCR Anda dapat membuat aplikasi konsol C# kecil yang memproses semua gambar tersebut secara paralel, memberikan **ekstraksi teks batch** yang cepat dan hasil yang bersih. Dalam panduan ini kami akan menelusuri **c# ocr tutorial** lengkap, menjelaskan mengapa setiap bagian penting, dan menunjukkan tepat seperti apa outputnya.

Pada akhir artikel ini Anda akan dapat:

* Memuat daftar file PNG (atau gambar lain yang didukung) sekaligus.  
* Mengonfigurasi `OcrEngine` bersama sehingga pengaturan tetap konsisten di seluruh batch.  
* Menjalankan antrian pengenalan dengan hingga empat pekerja paralel.  
* Mengambil teks yang dikenali untuk setiap halaman dan mencetaknya ke konsol.

Tidak ada sulap, hanya kode solid yang dapat Anda tambahkan ke solusi Anda hari ini.

## Apa yang Anda perlukan

Sebelum kita mulai, pastikan Anda memiliki:

* .NET 6 SDK (atau versi .NET terbaru).  
* Lisensi Aspose OCR yang valid atau kunci evaluasi sementara.  
* Folder yang berisi file PNG yang ingin Anda proses.  
* Visual Studio 2022 atau editor favorit Anda.

Itu saja—tidak ada paket NuGet tambahan selain `Aspose.OCR` dan `System.Collections.Generic` standar.

## Cara melakukan batch OCR – Menyiapkan proyek

Langkah pertama, buat proyek konsol baru dan tambahkan pustaka Aspose OCR.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Setelah proses restore selesai, buka **Program.cs** (atau buat file baru) dan tambahkan direktif `using` biasa:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Kerangka sederhana ini memberi kita akses ke `OcrEngine`, `RecognitionQueue`, dan kelas pembantu yang akan kita gunakan nanti.

## Ekstrak teks dari PNG – Menyiapkan daftar gambar

Sekarang kita perlu memberi tahu program **PNG mana** yang akan diproses oleh OCR. Cara paling sederhana adalah membangun `List<string>` yang berisi path absolut atau relatif.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Ganti `YOUR_DIRECTORY` dengan path folder yang sebenarnya. Jika Anda memiliki kumpulan dinamis, Anda juga dapat menggunakan `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` dan memasukkan hasilnya ke dalam daftar. Intinya, **ekstrak teks dari PNG** hanyalah soal memberi nama file yang tepat ke antrian.

![How to batch OCR workflow](https://example.com/placeholder.png "Diagram illustrating how to batch OCR a collection of PNG files")

*Image alt text: diagram alur kerja batch OCR*

## C# OCR tutorial – Mengonfigurasi antrian pengenalan

Inti dari operasi batch adalah `RecognitionQueue`. Anggap saja sebagai konveyor yang menyerahkan setiap gambar ke `OcrEngine` bersama. Dengan berbagi engine kita menjaga penggunaan memori tetap rendah dan menjamin pengaturan identik untuk setiap halaman.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Mengapa mengatur `MaxDegreeOfParallelism` ke 4? Pada laptop quad‑core tipikal itu memberikan throughput terbaik tanpa membuat OS kelaparan sumber daya. Jika Anda menjalankan di server dengan lebih banyak core, naikkan angka tersebut sesuai kebutuhan.

### Pro tip

Jika Anda memerlukan paket bahasa khusus, pengaturan DPI, atau pemotongan region‑of‑interest, lakukan **sekali** pada `Engine` bersama sebelum menambahkan gambar ke antrian. Contohnya:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Semua pengenalan selanjutnya mewarisi opsi ini secara otomatis—itulah esensi **cara membuat OCR** pipeline yang tetap konsisten.

## Ekstraksi teks batch – Menambahkan gambar ke antrian dan menjalankan antrian

Setelah antrian siap, langkah berikutnya adalah memasukkan setiap gambar ke dalamnya. Metode `Enqueue` menerima instance `OcrImage`, yang kita buat dari path file.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Setelah semua file berada dalam antrian, kita jalankan prosesnya:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` akan memblokir hingga setiap gambar selesai, lalu mengembalikan daftar di mana setiap elemen sesuai dengan urutan input. Ini menjamin bahwa hasil halaman 1 berada pada indeks 0, halaman 2 pada indeks 1, dan seterusnya—sangat berguna ketika Anda perlu memetakan hasil kembali ke file sumber.

## Cara membuat OCR – Menampilkan hasil

Akhirnya, mari cetak teks yang dikenali ke konsol. Di sinilah Anda benar‑benar melihat **ekstraksi teks batch** beraksi.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Saat Anda menjalankan program (`dotnet run`), Anda akan melihat sesuatu seperti:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Jika ada gambar yang gagal (misalnya, file rusak), `OcrResult` yang bersangkutan akan memiliki properti `Text` kosong dan Anda dapat memeriksa `ocrResults[i].Exception` untuk diagnostik.

## Cara membuat OCR – Tips, kasus tepi, dan praktik terbaik

### Menangani batch besar

Memproses ratusan PNG masih dapat memakan memori jika Anda menyimpan semua objek `OcrResult` sekaligus. Dalam kasus seperti itu, alirkan output ke file atau basis data segera setelah setiap hasil tiba:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Menghadapi format non‑PNG

Aspose OCR juga mendukung JPEG, BMP, dan TIFF secara bawaan. Cukup ubah ekstensi file dalam daftar Anda atau gunakan pencarian wildcard. Langkah **c# ocr tutorial** yang sama berlaku—tanpa perubahan kode.

### Melewatkan halaman kosong

Jika Anda memiliki PDF yang dipindai dan kadang‑kadang berisi halaman kosong, Anda dapat memfilter hasil:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Pertimbangan lisensi

Versi evaluasi menandai setiap halaman dengan watermark. Untuk penggunaan produksi, pastikan Anda menyematkan file lisensi di awal `Main`:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Penyetelan paralelisme

`MaxDegreeOfParallelism` defaultnya adalah `Environment.ProcessorCount`. Jika Anda melihat penggunaan CPU tinggi atau tekanan memori, turunkan nilainya. Sebaliknya, pada VM cloud dengan banyak core, naikkan untuk memanfaatkan perangkat keras secara maksimal.

## Ringkasan

Anda kini memiliki solusi **cara melakukan batch OCR** lengkap di C# yang dapat **mengekstrak teks dari PNG**, menjalankannya secara paralel, dan memberikan hasil yang bersih serta berurutan. Dengan berbagi satu `OcrEngine`, Anda telah belajar **cara membuat OCR** pipeline yang efisien memori dan mudah dipelihara. **c# ocr tutorial** ini juga menunjukkan cara menskalakan **ekstraksi teks batch** untuk ratusan gambar dengan hanya beberapa baris tambahan.

---

### Apa selanjutnya?

* Coba tambahkan deteksi bahasa (`Engine.Language = Language.AutoDetect`).  
* Eksperimen dengan format output—tulis hasil ke JSON atau CSV untuk analitik lanjutan.  
* Gabungkan batch OCR ini dengan langkah konversi PDF‑ke‑gambar untuk memproses dokumen yang dipindai secara keseluruhan.

Silakan sesuaikan paralelisme, ganti sumber gambar Anda, atau sambungkan hasilnya ke indeks pencarian. Langit adalah batasnya ketika Anda menguasai **cara melakukan batch OCR** di C#.

Selamat coding, semoga proses OCR Anda cepat dan bebas error!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}