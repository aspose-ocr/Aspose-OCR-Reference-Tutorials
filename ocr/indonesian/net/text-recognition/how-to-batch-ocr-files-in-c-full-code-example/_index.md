---
category: general
date: 2026-02-17
description: Cara melakukan OCR batch pada banyak PDF dan gambar di C# menggunakan
  Aspose OCR. Pelajari cara mengekstrak teks dari PDF, mengonversi PDF ke teks, dan
  mengenali teks dari gambar.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: id
og_description: Cara melakukan OCR batch pada banyak dokumen di C# dengan Aspose OCR.
  Dapatkan kode langkah‑demi‑langkah untuk mengekstrak teks dari PDF, mengonversi
  PDF ke teks, dan mengenali teks dari gambar.
og_title: Cara Memproses OCR File Secara Batch di C# – Panduan Lengkap
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Cara melakukan batch OCR file di C# – Contoh Kode Lengkap
url: /id/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan batch OCR file di C# – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara batch OCR** sekumpulan PDF dan pemindaian gambar tanpa menulis loop terpisah untuk setiap file? Anda tidak sendirian. Kebanyakan pengembang menemui kendala ini ketika harus mengambil teks dari puluhan halaman sekaligus. Kabar baiknya? Dengan Aspose OCR Anda dapat memberi koleksi file ke satu mesin dan membiarkannya melakukan pekerjaan berat.

Dalam tutorial ini kita akan membahas solusi praktis yang memungkinkan Anda **mengekstrak teks dari pdf**, **mengonversi pdf ke teks**, dan **mengenali teks dari gambar** dalam satu kali batch. Pada akhir tutorial Anda akan memiliki aplikasi console siap‑jalankan yang mencetak hasil OCR untuk setiap halaman, dan Anda akan memahami alasan di balik setiap langkah sehingga dapat menyesuaikannya dengan proyek Anda sendiri.

## Prasyarat – Apa yang Anda Butuhkan Sebelum Memulai

- **.NET 6.0 atau lebih baru** (kode ini juga bekerja di .NET Framework, tetapi .NET 6+ disarankan)
- **Paket NuGet Aspose.OCR** – instal dengan `dotnet add package Aspose.OCR`
- Beberapa file contoh: PDF multi‑halaman (`doc1.pdf`) dan TIFF yang dipindai (`doc2.tif`). Letakkan di folder yang dapat Anda referensikan, misalnya `C:\OCRSamples`.
- Pengetahuan dasar C# – Anda harus nyaman dengan pernyataan `using` dan koleksi.

> Pro tip: Jika Anda belum memiliki lisensi, Aspose menawarkan kunci sementara gratis yang menghapus batas 100 halaman selama pengembangan.

## Langkah 1: Siapkan Proyek dan Impor Namespace

Pertama, buat proyek console baru (atau tambahkan ke yang sudah ada) dan impor namespace yang diperlukan.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Mengapa ini penting:** Mengimpor `Aspose.OCR.Image` memberi Anda metode praktis `ImageStream.FromFile`, yang secara otomatis memecah halaman PDF menjadi aliran gambar terpisah. Itulah rahasia yang membuat pemrosesan batch menjadi mudah.

## Langkah 2: Inisialisasi OCR Engine

Engine adalah tenaga kerja yang berkomunikasi dengan mesin OCR di bawahnya. Anda hanya memerlukan satu instance untuk seluruh batch.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Penjelasan:** Menggunakan kembali `OcrEngine` yang sama mengurangi churn memori dan mempercepat pemrosesan karena perpustakaan native tetap terload di antara halaman.

## Langkah 3: Bangun Daftar Image Stream

Di sini kita mengumpulkan setiap dokumen yang ingin diproses. `ImageStream.FromFile` cukup pintar untuk memecah PDF menjadi halaman‑halaman individual, sehingga PDF tiga‑halaman menjadi tiga aliran terpisah di balik layar.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Kasus tepi:** Jika Anda memiliki campuran PDF, TIFF, JPEG, atau PNG, cukup tambahkan semuanya ke daftar yang sama – Aspose menangani deteksi format secara otomatis.

## Langkah 4: Jalankan Operasi Batch OCR

Sekarang kita serahkan daftar tersebut ke engine. `RecognizeBatch` mengembalikan koleksi objek `OcrResult`, satu per halaman.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Mengapa batch?** Menjalankan OCR halaman‑per‑halaman dalam loop manual memaksa engine untuk menginisialisasi ulang setiap kali, yang dapat menggandakan waktu proses. `RecognizeBatch` menjaga engine tetap hangat dan mengalirkan hasil saat tersedia.

## Langkah 5: Output Teks yang Dikenali

Akhirnya, kita loop melalui hasil dan menuliskan teks setiap halaman ke console. Di sinilah Anda dapat mengganti `Console.WriteLine` dengan penulisan ke file, penyisipan ke database, atau tindakan downstream lainnya.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Output Console yang Diharapkan

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Jika Anda menjalankan program dengan file contoh, Anda akan melihat blok teks untuk setiap halaman, membuktikan bahwa Anda telah berhasil **mengekstrak teks dari pdf yang dipindai** dalam satu kali proses.

## Menangani Kendala Umum

| Masalah | Mengapa Terjadi | Solusi Cepat |
|---------|----------------|--------------|
| **Kesalahan out‑of‑memory** | PDF besar menghasilkan banyak gambar resolusi tinggi. | Batasi DPI saat memuat PDF: `ocrEngine.Settings.ImageDpi = 200;` |
| **Karakter garbled** | Pemindaian sumber berkualitas rendah atau menggunakan bahasa yang tidak didukung. | Atur bahasa secara eksplisit: `ocrEngine.Language = Language.English;` |
| **Hasil parsial** | Daftar batch berisi file yang rusak. | Bungkus `RecognizeBatch` dalam try/catch dan log `e.Message` untuk file yang bermasalah. |
| **Bottleneck performa** | Menjalankan pada satu thread di mesin multi‑core. | Gunakan `Parallel.ForEach` dengan instance `OcrEngine` terpisah per thread (lanjutan). |

## Bonus: Menyimpan Hasil OCR ke File Teks

Jika Anda lebih suka menyimpan file `.txt` terpisah per halaman, cukup tambahkan blok penulisan kecil di dalam loop:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Sekarang Anda telah mengubah **mengonversi pdf ke teks** menjadi folder rapi berisi file teks biasa—sempurna untuk pengindeksan atau pencarian downstream.

## Contoh Lengkap yang Siap Pakai

Berikut adalah program lengkap yang dapat Anda salin‑tempel. Tanpa dependensi tersembunyi, tanpa skrip eksternal.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Jalankan `dotnet run` dari folder proyek dan saksikan console terisi dengan teks yang diekstrak. Itulah **cara melakukan batch OCR** pada kumpulan dokumen hanya dengan beberapa baris C#.

## Ringkasan – Apa yang Telah Kita Bahas

- Menyiapkan aplikasi console .NET dan menginstal Aspose.OCR.  
- Membuat satu instance `OcrEngine` untuk menjaga proses tetap efisien.  
- Membuat daftar objek `ImageStream` yang otomatis memecah PDF menjadi halaman.  
- Menjalankan `RecognizeBatch` untuk **mengekstrak teks dari pdf** dan format gambar lainnya dalam satu kali proses.  
- Mencetak hasil dan opsional menyimpannya sebagai file `.txt` individual, menyelesaikan alur kerja **mengonversi pdf ke teks**.  

## Langkah Selanjutnya dan Topik Terkait

- **Skalakan**: Gunakan `Parallel.ForEach` dengan pool objek `OcrEngine` untuk memproses ratusan file secara bersamaan.  
- **Paket bahasa**: Ganti `Language.English` dengan `Language.French` atau muat kamus khusus ketika Anda perlu **mengenali teks dari gambar** dalam bahasa lain.  
- **Pasca‑pemrosesan**: Alirkan output OCR melalui pemeriksa ejaan atau parser bahasa alami untuk meningkatkan akurasi pada kontrak yang dipindai.  
- **Pustaka alternatif**: Bandingkan Aspose OCR dengan Tesseract.NET jika Anda mencari opsi open‑source—keduanya dapat **mengekstrak teks dari pdf yang dipindai** tetapi berbeda dalam lisensi dan akurasi out‑of‑the‑box.

---

![how to batch OCR example](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}