---
category: general
date: 2026-01-09
description: Mengenali teks dalam JPG dengan cepat menggunakan Aspose OCR di C#. Pelajari
  cara mengekstrak teks dari gambar, mengonversi gambar ke JSON dan EPUB dalam satu
  tutorial.
draft: false
keywords:
- recognize text in jpg
- extract text from image
- convert image to json
- convert image to epub
- create epub from image
language: id
og_description: Mengenali teks dalam JPG dengan Aspose OCR. Panduan ini menunjukkan
  cara mengekstrak teks dari gambar, mengonversi gambar ke JSON dan EPUB, serta membuat
  ePub dari gambar.
og_title: Mengenali teks dalam jpg – Tutorial C# Lengkap
tags:
- Aspose OCR
- C#
- Image Processing
title: Mengenali Teks dalam JPG dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/text-recognition/recognize-text-in-jpg-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dalam jpg – Panduan Lengkap C#

Pernah perlu **mengenali teks dalam file jpg** tetapi tidak yakin pustaka mana yang harus dipilih? Anda tidak sendirian. Banyak pengembang mengalami hal yang sama ketika pertama kali mencoba mengekstrak kata‑kata dari foto atau dokumen yang dipindai.  

Kabar baiknya? Dengan Aspose OCR Anda dapat **mengekstrak teks dari gambar** dalam beberapa baris kode C#, lalu langsung **mengonversi gambar ke JSON** atau bahkan **mengonversi gambar ke EPUB**—semua tanpa meninggalkan IDE Anda.

Dalam tutorial ini kita akan menelusuri seluruh alur kerja: mulai dari menginstal paket NuGet yang tepat, melalui mengenali teks dalam JPG, hingga menyimpan hasilnya sebagai JSON terstruktur dan sebagai dokumen ePub. Pada akhir tutorial Anda akan dapat **membuat epub dari gambar** secara programatis, trik berguna untuk platform e‑learning, perpustakaan digital, atau aplikasi apa pun yang memerlukan e‑book yang dapat dicari.

---

## Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework 4.6+). Kode ini bekerja pada runtime terbaru apa pun.
- Paket NuGet **Aspose.OCR** – mesin OCR inti.
- Paket NuGet **Aspose.Publishing** – diperlukan untuk format output ePub.
- Sebuah file gambar bernama `input.jpg` yang berada di suatu lokasi di disk Anda (ganti path sesuai kebutuhan).
- Editor teks atau IDE (Visual Studio, VS Code, Rider—pilihan Anda).

Itu saja. Tanpa layanan tambahan, tanpa API eksternal, hanya beberapa pustaka dan file JPG.

---

## Langkah 1: Siapkan Proyek Anda untuk **mengenali teks dalam jpg**

Pertama, buat aplikasi console baru (atau tambahkan ke proyek yang sudah ada). Kemudian tambahkan dua paket Aspose melalui NuGet Package Manager:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.Publishing
```

> **Tip pro:** Jika Anda menggunakan Visual Studio, klik kanan proyek → *Manage NuGet Packages* → cari *Aspose.OCR* dan *Aspose.Publishing*, lalu klik **Install**.

Paket‑paket ini menyediakan semua yang Anda perlukan untuk **mengekstrak teks dari gambar** dan untuk menghasilkan file ePub nanti.

---

## Langkah 2: **Mengekstrak teks dari gambar** Menggunakan Aspose OCR

Sekarang kita akan menulis kode yang benar‑benar membaca JPG dan mengambil karakter‑karakter darinya.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Recognize text from the JPG file
            // Replace the path with the location of your own image
            string inputPath = @"YOUR_DIRECTORY\input.jpg";
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 3️⃣ Show the recognized text in the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Mengapa ini berhasil:** `OcrEngine` menyembunyikan semua pra‑pemrosesan gambar tingkat rendah, deteksi bahasa, dan segmentasi karakter. Anda cukup menunjukannya ke sebuah file dan ia mengembalikan objek `OcrResult` yang berisi string teks polos (`ocrResult.Text`) serta sekumpulan metadata yang kaya.

---

## Langkah 3: **Mengonversi gambar ke JSON** – Mengekspor Hasil OCR

Jika Anda perlu menyimpan output OCR dalam format terstruktur (untuk API, basis data, atau pemrosesan lanjutan), Aspose memudahkan serialisasi hasil ke JSON.

```csharp
// 4️⃣ Convert the OCR result to JSON
string jsonContent = ocrResult.ToJson();

// 5️⃣ Save the JSON to disk
string jsonPath = @"YOUR_DIRECTORY\output.json";
File.WriteAllText(jsonPath, jsonContent);

Console.WriteLine($"JSON saved to: {jsonPath}");
```

JSON yang dihasilkan kira‑kira terlihat seperti ini (dipangkas untuk singkat):

```json
{
  "Text": "Hello world!",
  "Confidence": 0.98,
  "PageCount": 1,
  "Words": [
    { "Value": "Hello", "Confidence": 0.99 },
    { "Value": "world!", "Confidence": 0.97 }
  ]
}
```

**Kapan menggunakannya:** JSON sangat cocok bila Anda mengalirkan data OCR ke layanan web, menyimpannya di penyimpanan NoSQL, atau sekadar membutuhkan representasi portabel yang dapat diparsir oleh bahasa apa pun.

---

## Langkah 4: **Mengonversi gambar ke EPUB** – Menyimpan sebagai eBook

Aspose Publishing menambahkan dukungan untuk beberapa format e‑book, termasuk EPUB. Dengan memanggil `Save` pada `OcrResult` Anda dapat menghasilkan file ePub yang sepenuhnya sesuai standar, berisi teks yang dikenali dan, opsional, gambar asli.

```csharp
// 6️⃣ Save the OCR result as an ePub document
string epubPath = @"YOUR_DIRECTORY\output.epub";
ocrResult.Save(epubPath, OcrOutputFormat.Epub);

Console.WriteLine($"EPUB created at: {epubPath}");
```

**Apa yang Anda dapatkan:** Sebuah ePub yang dapat dibuka di pembaca apa pun (Calibre, Apple Books, Adobe Digital Editions). File tersebut mencakup teks yang diekstrak sebagai konten yang dapat dicari, plus gambar sumber sebagai lapisan latar—ideal untuk membuat pipeline **membuat epub dari gambar**.

---

## Langkah 5: Contoh Lengkap – Dari JPG ke JSON & EPUB

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan. Salin‑tempelkan ke `Program.cs`, sesuaikan jalur file, lalu tekan **F5**.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToEpubDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // Path to the input JPG
            string inputPath = @"YOUR_DIRECTORY\input.jpg";

            // Recognize text
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // Output recognized text to console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine();

            // Export to JSON
            string jsonPath = @"YOUR_DIRECTORY\output.json";
            File.WriteAllText(jsonPath, ocrResult.ToJson());
            Console.WriteLine($"JSON saved to: {jsonPath}");

            // Export to EPUB
            string epubPath = @"YOUR_DIRECTORY\output.epub";
            ocrResult.Save(epubPath, OcrOutputFormat.Epub);
            Console.WriteLine($"EPUB created at: {epubPath}");
        }
    }
}
```

Jalankan program dan Anda akan melihat tiga hal:

1. Teks yang dikenali tercetak di konsol.
2. File `output.json` yang berisi data OCR terstruktur.
3. File `output.epub` yang dapat Anda buka dengan pembaca e‑book apa pun.

---

## Pertanyaan Umum & Kasus Tepi

- **Bagaimana jika gambar berupa PNG atau BMP?**  
  Aspose OCR mendukung sebagian besar format raster (PNG, BMP, TIFF, GIF). Cukup ubah ekstensi file di `inputPath`; kode yang sama tetap berfungsi.

- **Bisakah saya menentukan bahasa selain Inggris?**  
  Ya. Atur `ocrEngine.Language = OcrLanguage.French;` (atau bahasa lain yang didukung) sebelum memanggil `RecognizeImage`.

- **Bagaimana dengan PDF multi‑halaman?**  
  Untuk PDF, Anda harus terlebih dahulu mengonversi tiap halaman menjadi gambar (Aspose.PDF dapat melakukannya) lalu memberi setiap gambar ke `RecognizeImage`. Objek `OcrResult` yang dihasilkan dapat digabungkan sebelum diekspor ke JSON atau EPUB.

- **Saya mendapatkan skor kepercayaan rendah. Bagaimana cara meningkatkan akurasi?**  
  Lakukan pra‑pemrosesan gambar: tingkatkan kontras, luruskan (deskew), atau ubah ke skala abu‑abu. Aspose OCR juga menyediakan `PreprocessOptions` yang dapat Anda sesuaikan.

---

## Kesimpulan

Anda kini memiliki resep lengkap‑ujung‑ke‑ujung untuk **mengenali teks dalam jpg** menggunakan Aspose OCR, lalu **mengonversi gambar ke JSON** untuk pipeline data dan **mengonversi gambar ke EPUB** untuk membangun e‑book yang dapat dicari. Pendekatan ini ringan, hanya memerlukan dua paket NuGet, dan berfungsi pada semua runtime .NET modern.

Selanjutnya Anda dapat:

- Mengintegrasikan output JSON ke dalam indeks pencarian (Azure Cognitive Search, Elastic).
- Memproses batch folder gambar dan menghasilkan perpustakaan buku ePub.
- Memperluas alur kerja dengan API terjemahan untuk membuat e‑book multibahasa secara otomatis.

Cobalah, eksperimen dengan kualitas gambar yang berbeda, dan biarkan mesin OCR melakukan pekerjaan berat. Selamat coding!

---

![tangkapan layar output mengenali teks dalam jpg](placeholder-image.png "contoh output mengenali teks dalam jpg")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}