---
category: general
date: 2026-05-28
description: Tutorial OCR Bahasa Korea menggunakan Aspose di C#. Pelajari cara memuat
  gambar dari aliran, mengekstrak teks biasa, mengonversi gambar ke PDF, dan mengekspor
  PDF yang dapat dicari.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: id
og_description: OCR Bahasa Korea di C# menggunakan Aspose. Panduan langkah demi langkah
  untuk memuat gambar dari aliran, mengekstrak teks biasa, mengonversi gambar ke PDF,
  dan mengekspor PDF yang dapat dicari.
og_title: OCR Bahasa Korea – Konversi Gambar ke PDF & Ekstrak Teks (Panduan C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR Bahasa Korea dengan Aspose: Mengonversi Gambar ke PDF dan Mengekstrak
  Teks dalam C#'
url: /id/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bahasa Korea dengan Aspose: Mengonversi Gambar ke PDF dan Mengekstrak Teks dalam C#

Pernah bertanya-tanya bagaimana cara menjalankan **Korean Language OCR** pada sebuah gambar tanpa mengirim apa pun ke cloud? Anda tidak sendirian. Baik Anda sedang mendigitalkan rambu jalan, memproses struk, atau membangun indeks pencarian multibahasa, kemampuan mengenali karakter Korea secara lokal dapat menghemat waktu, uang, dan masalah privasi.

Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang dapat dijalankan, yang menunjukkan cara **memuat gambar dari stream**, **mengekstrak teks biasa**, **mengonversi gambar ke PDF**, dan akhirnya **mengekspor PDF yang dapat dicari**—semua dengan Aspose.OCR dan beberapa baris C#. Tanpa layanan eksternal, tanpa sihir tersembunyi—hanya kode .NET murni yang dapat Anda masukkan ke dalam aplikasi console apa pun.

## Apa yang Akan Anda Dapatkan

- Program console yang berfungsi dan membaca file JPEG melalui file stream.  
- Teks Korea yang diekstrak sebagai string Unicode biasa.  
- Laporan JSON terperinci tentang proses OCR untuk debugging atau analitik.  
- PDF yang dapat dicari yang dapat Anda buka di pembaca PDF apa pun dan benar‑benar memilih kata‑kata Korea.  

**Prasyarat**  
- .NET 6.0 atau lebih baru (kode ini juga bekerja pada .NET Framework 4.7+).  
- Paket NuGet Aspose.OCR untuk .NET terpasang (`Install-Package Aspose.OCR`).  
- Sebuah folder yang berisi `korean_sign.jpg` dan lokasi yang dapat ditulisi untuk file output.  

Jika semua sudah siap, bagus—mari kita mulai.

## Langkah 1: Inisialisasi OCR Engine untuk Korean Language OCR

Hal pertama yang Anda perlukan adalah instance `OcrEngine`. Mengaktifkan GPU (jika Anda memilikinya) mempercepat pengenalan secara dramatis, dan mematikan unduhan sumber daya otomatis memaksa perpustakaan menggunakan paket bahasa offline yang Anda sediakan.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Mengapa ini penting:**  
> *GPU acceleration* dapat memotong waktu pemrosesan dari detik menjadi milidetik untuk batch besar. Menetapkan `AutomaticResourceDownload` ke `false` memastikan demo berjalan offline—suatu keharusan bagi banyak lingkungan perusahaan.

## Langkah 2: Muat Gambar dari Stream

Membaca gambar melalui stream memberi Anda fleksibilitas: Anda dapat mengambil file dari disk, share jaringan, atau bahkan blob yang disimpan di memori. Di sini kami membuka file JPEG lokal, tetapi pola yang sama bekerja untuk `Stream` apa pun.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Pro tip:** Jika Anda perlu memproses gambar yang diunggah melalui API web, cukup ganti `File.OpenRead` dengan `IFormFile.OpenReadStream()` yang masuk—sisanya tetap sama.

## Langkah 3: Pilih Bahasa Korea dan Terapkan Filter Pra‑Pemrosesan

Aspose.OCR mendukung beberapa langkah pra‑pemrosesan yang membersihkan gambar sebelum pengenalan. Untuk rambu Korea, deskewing dan denoising biasanya sudah cukup.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Apa yang terjadi di balik layar?**  
> Filter `Deskew` meluruskan teks yang miring, sementara `Denoise` menghilangkan noise yang dapat membingungkan klasifikator karakter. Melewatkan langkah‑langkah ini sering menghasilkan output yang berantakan, terutama pada foto beresolusi rendah.

## Langkah 4: Ekstrak Teks Biasa Secara Asinkron

Sekarang saatnya menguji—meminta engine mengenali karakter dan memberikan string bersih. Menggunakan `RecognizeAsync` membuat UI tetap responsif jika Anda menyematkannya ke dalam aplikasi desktop atau web.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
OCR complete. Extracted text:
서울시청
```

> **Mengapa async?**  
> OCR dapat memakan banyak CPU. Eksekusi asinkron mencegah thread Anda terblokir, yang sangat berguna di ASP.NET Core dimana kelaparan thread menjadi masalah nyata.

## Langkah 5: Dapatkan Hasil Pengakuan Terperinci dan Simpan sebagai JSON

Kadang‑kadang Anda membutuhkan lebih dari sekadar string mentah—mungkin skor kepercayaan, kotak pembatas, atau data gambar asli. Metode `RecognizeDetailed` mengembalikan objek `RecognitionResult` yang dapat diserialisasi ke JSON untuk analisis selanjutnya.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Membuka `korean_ocr.json` akan menampilkan struktur serupa dengan:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Kapan menggunakan ini?**  
> Jika Anda membangun indeks pencarian, nilai confidence memungkinkan Anda menyaring hasil berkualitas rendah. Jika Anda perlu menyorot teks dalam UI, kotak pembatas adalah peta Anda.

## Langkah 6: Konversi Gambar ke PDF dan Ekspor PDF yang Dapat Dicari

Aspose membuat transisi dari raster ke vektor menjadi mudah. Dengan mengatur `OutputFormat` ke `SearchablePdf`, perpustakaan menyisipkan gambar asli dan menambahkan lapisan teks tak terlihat yang berisi output OCR. PDF yang dihasilkan dapat dicari, disalin, dan diindeks seperti PDF native mana pun.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Buka `korean_searchable.pdf` di Adobe Reader atau penampil PDF apa pun, tekan **Ctrl+F**, ketik kata Korea, dan lihat hasilnya melompat ke posisi tepat di halaman. Itulah kekuatan PDF yang dapat dicari.

> **Tip tambahan:** Jika Anda hanya membutuhkan PDF visual tanpa lapisan teks tersembunyi, ubah `OutputFormat` menjadi `Pdf` saja.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap—salin, tempel, ganti `YOUR_DIRECTORY` dengan path yang sebenarnya, dan tekan **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Output Console yang Diharapkan

```
OCR complete. Extracted text:
서울시청
```

Dan Anda akan menemukan tiga file baru di samping gambar sumber Anda:

- `korean_ocr.json` – data pengenalan lengkap.  
- `korean_searchable.pdf` – PDF yang dapat Anda cari.  
- (opsional) log menengah apa pun yang Anda tambahkan.

## Pertanyaan Umum & Kasus Tepi

**Bagaimana jika saya tidak memiliki GPU?**  
Setel `EnableGpu = false`; fallback ke CPU sudah cukup baik untuk batch kecil.

**Bisakah saya memproses banyak gambar dalam satu run?**  
Tentu. Bungkus logika inti dalam loop `foreach (var file in Directory.GetFiles(...))` dan setel kembali `ocrEngine.Image` setiap iterasi.

**Bagaimana cara menangani bahasa lain bersama Korean?**  
Aspose.OCR memungkinkan Anda mengatur `Language = Language.AutoDetect` atau menggabungkan bahasa dengan operator OR bitwise (misalnya, `Language.Korean | Language.English`).

**Bagaimana jika confidence OCR rendah?**  
Periksa `detailedResult.Pages[0].Words` dan saring entri dengan `Confidence < 0.7`. Anda juga dapat menyesuaikan filter pra‑pemrosesan—coba tambahkan `PreprocessFilter.ContrastEnhancement`.

## Penutup

Anda baru saja melihat cara melakukan **Korean Language OCR** secara menyeluruh, dari **memuat gambar dari stream** hingga **mengekstrak teks biasa**, kemudian **mengonversi gambar ke PDF** dan akhirnya **mengekspor PDF yang dapat dicari**. Pendekatannya modular, sehingga Anda dapat mengganti sumber gambar, mengubah format output, atau menyalurkan JSON ke pipeline downstream mana pun.

Apa selanjutnya


## Tutorial Terkait

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}