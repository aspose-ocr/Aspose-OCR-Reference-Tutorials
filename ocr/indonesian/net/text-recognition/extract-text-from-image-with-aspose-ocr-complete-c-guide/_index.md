---
category: general
date: 2026-05-28
description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  mengekstrak teks OCR, memuat gambar untuk OCR, dan mengenali teks dari file TIF
  dengan cepat.
draft: false
keywords:
- extract text from image
- how to extract ocr text
- load image for ocr
- recognize text from tif
language: id
og_description: Ekstrak teks dari gambar menggunakan Aspose OCR dalam C#. Tutorial
  ini menunjukkan cara mengekstrak teks OCR, memuat gambar untuk OCR, dan mengenali
  teks dari file TIF.
og_title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Extract text from image using Aspose OCR in C#. Learn how to extract
    OCR text, load image for OCR, and recognize text from TIF files quickly.
  headline: Extract Text from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract text from image using Aspose OCR in C#. Learn how to extract
    OCR text, load image for OCR, and recognize text from TIF files quickly.
  name: Extract Text from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: '**Wrong file path** – A typo leads to a `FileNotFoundException`. Double‑check
      the path or use `Path.Combine` for cross‑platform safety.'
    text: '**Wrong file path** – A typo leads to a `FileNotFoundException`. Double‑check
      the path or use `Path.Combine` for cross‑platform safety.'
  - name: '**Unsupported format** – Aspose OCR supports PNG, JPEG, BMP, and TIFF.
      Trying a PDF directly will throw an `UnsupportedFormatException`. Convert first
      if needed.'
    text: '**Unsupported format** – Aspose OCR supports PNG, JPEG, BMP, and TIFF.
      Trying a PDF directly will throw an `UnsupportedFormatException`. Convert first
      if needed.'
  - name: '**Large image size** – Very high‑resolution TIFFs can consume memory. Consider
      down‑scaling with `engine.Options.Dpi = 300` before recognition.'
    text: '**Large image size** – Very high‑resolution TIFFs can consume memory. Consider
      down‑scaling with `engine.Options.Dpi = 300` before recognition.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Lengkap C#

Mengekstrak teks dari gambar adalah tantangan umum ketika Anda perlu mendigitalisasi dokumen yang dipindai, kwitansi, atau bahkan foto papan putih. Jika Anda bertanya-tanya **bagaimana cara mengekstrak teks OCR** dalam proyek .NET, Anda berada di tempat yang tepat—panduan ini akan membawa Anda melalui seluruh proses, mulai dari memuat gambar hingga mengambil karakter yang dikenali dari file TIF.

Kami akan membahas semua yang perlu Anda ketahui: membuat mesin OCR, memuat gambar untuk OCR, melakukan pengenalan secara asynchronous, dan akhirnya mencetak teks yang diekstrak ke konsol. Pada akhir panduan Anda akan memiliki potongan kode yang dapat dijalankan yang bekerja dengan TIFF apa pun (atau format lain yang didukung) serta pemahaman yang kuat mengapa setiap bagian penting.

## Apa yang Anda Butuhkan

- .NET 6 atau lebih baru (kode ini juga dapat dikompilasi pada .NET Core 3.1+)
- Paket NuGet Aspose.OCR (`Aspose.OCR`) yang terpasang di proyek Anda
- Sebuah contoh gambar TIFF (`page1.tif`) yang ditempatkan di lokasi yang dapat Anda referensikan
- Editor kode atau IDE (Visual Studio, VS Code, Rider—apa pun yang Anda suka)

Tidak ada file konfigurasi tambahan, tidak ada mesin OCR berat yang harus diinstal secara lokal—Aspose menangani pekerjaan berat untuk Anda.

---

## Ekstrak Teks dari Gambar – Langkah 1: Inisialisasi Mesin OCR

Sebelum gambar apa pun dapat diproses, Anda memerlukan sebuah instance `OcrEngine`. Anggap mesin ini sebagai otak yang tahu cara membaca karakter; tanpa itu, sisa alur tidak memiliki apa pun untuk dijalankan.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static async Task Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();
```

> **Mengapa ini penting:** `OcrEngine` mengenkapsulasi algoritma pengenalan dan paket bahasa. Menginstansiasinya sekali per operasi menjaga penggunaan memori tetap rendah dan memberi Anda titik bersih untuk menyesuaikan pengaturan nanti (mis., bahasa, DPI).

---

## Cara Mengekstrak Teks OCR – Langkah 2: Memuat Gambar untuk OCR

Sekarang mesin sudah siap, kita harus mengarahkannya ke gambar yang ingin dibaca. Aspose menyediakan `ImageStream.FromFile`, yang men-stream file tanpa memuat seluruh bitmap ke memori—keuntungan performa yang bagus untuk TIFF berukuran besar.

```csharp
        // Step 2: Load the image to be recognized
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/page1.tif");
```

> **Tip pro:** Ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif ke gambar Anda. Jika Anda menjalankan aplikasi dari folder proyek, `@"./page1.tif"` berfungsi dengan baik.  
> **Kasus khusus:** File TIFF dapat berisi beberapa halaman. `ImageStream.FromFile` membaca halaman pertama secara default; jika Anda membutuhkan halaman lain, gunakan `ImageStream.FromFile(path, pageNumber)`.

---

## Mengenali Teks dari TIF – Langkah 3: Lakukan OCR Asinkron

Memblokir thread pemanggil saat mesin OCR bekerja dapat membekukan aplikasi UI atau membuang sumber daya server. Menggunakan `RecognizeAsync` memungkinkan operasi berjalan di latar belakang, mengembalikan `Task<string>` yang menghasilkan teks yang diekstrak.

```csharp
        // Step 3: Perform OCR asynchronously (does not block the calling thread)
        string extractedText = await engine.RecognizeAsync();
```

> **Mengapa async?** Pada API web atau aplikasi desktop, Anda ingin thread pool tetap responsif. `await` mengembalikan kontrol ke pemanggil hingga OCR selesai, menjaga UI tetap lancar atau thread permintaan bebas untuk pekerjaan lain.

---

## Output Teks yang Diekstrak – Langkah 4: Cetak atau Simpan

Akhirnya, kami cukup menulis hasilnya ke konsol. Dalam skenario dunia nyata Anda mungkin menulis ke database, file, atau mengirim string ke layanan lain.

```csharp
        // Step 4: Output the recognized text
        Console.WriteLine(extractedText);
    }
}
```

### Output yang Diharapkan

Jika `page1.tif` berisi teks *“Hello, Aspose OCR!”*, konsol akan menampilkan:

```
Hello, Aspose OCR!
```

Jika gambar berisik, Anda mungkin melihat baris tambahan atau karakter yang salah dikenali—sesuaikan `Options` mesin (mis., `engine.Options.DetectLanguage = true`) untuk meningkatkan akurasi.

---

## Kesalahan Umum Saat Memuat Gambar untuk OCR

1. **Jalur file salah** – Kesalahan ketik menyebabkan `FileNotFoundException`. Periksa kembali jalur atau gunakan `Path.Combine` untuk keamanan lintas‑platform.  
2. **Format tidak didukung** – Aspose OCR mendukung PNG, JPEG, BMP, dan TIFF. Mencoba PDF secara langsung akan melempar `UnsupportedFormatException`. Konversi terlebih dahulu jika diperlukan.  
3. **Ukuran gambar besar** – TIFF beresolusi sangat tinggi dapat mengonsumsi memori. Pertimbangkan menurunkan skala dengan `engine.Options.Dpi = 300` sebelum pengenalan.

---

## Lebih Lanjut: Menyesuaikan Pengaturan Pengenalan

Aspose.OCR dilengkapi dengan sejumlah opsi yang dapat Anda sesuaikan:

```csharp
engine.Options.Language = Language.English;      // Force English if you know the language
engine.Options.Dpi = 200;                       // Reduce DPI for faster processing
engine.Options.IsAutoRotate = true;            // Auto‑rotate skewed pages
```

Eksperimen dengan ini untuk menemukan keseimbangan antara kecepatan dan akurasi.

---

## Contoh Lengkap yang Dapat Dijalankan (Siap Salin‑Tempel)

Di bawah ini adalah program lengkap yang dapat Anda masukkan ke dalam proyek konsol baru. Ini mencakup pengaturan opsional yang dibahas di atas.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static async Task Main()
    {
        // Create the OCR engine
        var engine = new OcrEngine();

        // Optional: fine‑tune recognition
        engine.Options.Language = Language.English;
        engine.Options.Dpi = 200;
        engine.Options.IsAutoRotate = true;

        // Load the image (replace with your actual path)
        engine.Image = ImageStream.FromFile(@"./page1.tif");

        // Run OCR asynchronously
        string extractedText = await engine.RecognizeAsync();

        // Show the result
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

Simpan file sebagai `Program.cs`, jalankan `dotnet add package Aspose.OCR`, lalu `dotnet run`. Anda akan melihat teks yang diekstrak dicetak ke konsol.

---

## Ringkasan

Kami baru saja mendemonstrasikan **cara mengekstrak teks OCR** dari gambar TIFF menggunakan Aspose OCR dalam C#. Langkah‑langkah—inisialisasi mesin, memuat gambar untuk OCR, mengenali teks dari TIF secara asinkron, dan mengoutput hasil—mencakup seluruh siklus hidup mengekstrak teks dari file gambar.  

Jika Anda siap melangkah lebih jauh dari teks biasa, jelajahi `PdfConverter` Aspose untuk menyematkan output OCR ke dalam PDF yang dapat dicari, atau gunakan `engine.Options` untuk menangani dokumen multi‑bahasa.

## Apa Selanjutnya?

- **Pemrosesan batch:** Loop melalui folder TIFF dan menyimpan setiap hasil ke dalam database.  
- **Pra‑pemrosesan gambar:** Gunakan `System.Drawing` atau `ImageSharp` untuk membersihkan pemindaian berisik sebelum memberi ke mesin OCR.  
- **Integrasi dengan ASP.NET Core:** Membuka endpoint yang menerima gambar yang diunggah dan mengembalikan teks yang dikenali sebagai JSON.

Silakan bereksperimen, memecahkan masalah, dan kemudian kembali ke panduan ini untuk penyegaran. Jika Anda menemui kendala, dokumentasi Aspose OCR adalah pendamping yang solid, namun pola inti tetap sama: **ekstrak teks dari gambar**, **muat gambar untuk OCR**, **kenali teks dari TIF**, dan tangani hasilnya.

Selamat coding, dan semoga gambar Anda selalu jernih!

## Tutorial Terkait

- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)
- [Cara Mengekstrak Teks dari Gambar dengan Menyiapkan Persegi Panjang dalam OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}