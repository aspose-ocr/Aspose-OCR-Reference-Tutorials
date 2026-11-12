---
category: general
date: 2026-06-16
description: Lakukan OCR pada gambar menggunakan Aspose OCR di C#. Pelajari langkah
  demi langkah cara mendapatkan hasil JSON, menangani file, dan mengatasi masalah
  umum.
draft: false
keywords:
- perform OCR on image
- Aspose OCR C#
- JSON result handling
- C# image recognition
- OCR engine configuration
language: id
og_description: Lakukan OCR pada gambar dengan Aspose OCR di C#. Panduan ini memandu
  Anda melalui output JSON, penyiapan mesin, dan tips praktis.
og_title: Lakukan OCR pada Gambar di C# – Tutorial Lengkap Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Perform OCR on image using Aspose OCR in C#. Learn step‑by‑step how
    to get JSON results, handle files, and troubleshoot common issues.
  headline: Perform OCR on Image in C# with Aspose – Complete Programming Guide
  type: TechArticle
- questions:
  - answer: Aspose.OCR handles PNG, JPEG, BMP, TIFF, and GIF. If you need to work
      with PDFs, convert each page to an image first (Aspose.PDF can help).
    question: What image formats are supported?
  - answer: Yes – set `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`. JSON
      is preferred when you need more metadata.
    question: Can I get plain text instead of JSON?
  - answer: Feed each page image to `RecognizeImage` in a loop and concatenate the
      results, or use `RecognizePdf` which returns a combined JSON structure.
    question: How do I handle multi‑page documents?
  - answer: For batch processing, reuse a single `OcrEngine` instance rather than
      creating a new one per image. Also, enable `RecognitionMode.Fast` if accuracy
      can be traded for speed.
    question: Performance concerns?
  - answer: Without a license, the output JSON will include a watermark field. Apply
      your license early in `Main` with `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.
    question: License warnings?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Lakukan OCR pada Gambar di C# dengan Aspose – Panduan Pemrograman Lengkap
url: /id/net/text-recognition/perform-ocr-on-image-in-c-with-aspose-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Melakukan OCR pada Gambar di C# – Panduan Pemrograman Lengkap

Pernah perlu **melakukan OCR pada gambar** tetapi tidak yakin bagaimana mengubah piksel mentah menjadi teks yang dapat digunakan? Anda tidak sendirian. Baik Anda memindai struk, mengekstrak data dari paspor, atau mendigitalkan dokumen lama, kemampuan untuk **melakukan OCR pada gambar** secara programatik adalah pengubah permainan bagi setiap pengembang .NET.

Dalam tutorial ini kami akan membimbing Anda melalui contoh praktis yang menunjukkan secara tepat cara **melakukan OCR pada gambar** menggunakan pustaka Aspose.OCR, menangkap hasilnya dalam JSON, dan menyimpannya untuk pemrosesan lanjutan. Pada akhir tutorial Anda akan memiliki aplikasi konsol yang siap dijalankan, penjelasan jelas tentang setiap langkah konfigurasi, dan beberapa tips profesional untuk menghindari jebakan umum.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0 SDK atau yang lebih baru terpasang (Anda dapat mengunduhnya dari situs Microsoft).  
- Lisensi Aspose.OCR yang valid atau percobaan gratis – pustaka berfungsi tanpa lisensi tetapi akan menambahkan watermark.  
- File gambar (PNG, JPEG, atau TIFF) yang ingin Anda **melakukan OCR pada gambar** – untuk panduan ini kami akan menggunakan `receipt.png`.  
- Visual Studio 2022, VS Code, atau editor apa pun yang Anda sukai.

Tidak ada paket NuGet tambahan selain `Aspose.OCR` yang diperlukan.

## Langkah 1: Siapkan Proyek dan Instal Aspose.OCR

Pertama, buat proyek konsol baru dan tambahkan pustaka OCR.

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, Anda dapat menambahkan paket melalui UI NuGet Package Manager. Ini secara otomatis memulihkan dependensi, menghemat Anda harus menjalankan `dotnet restore` secara manual nanti.

Sekarang buka `Program.cs` – kami akan mengganti isinya dengan kode yang benar‑benar **melakukan OCR pada gambar**.

## Langkah 2: Buat dan Konfigurasikan OCR Engine

Inti dari setiap alur kerja Aspose OCR adalah kelas `OcrEngine`. Di bawah ini kami menginstansiasinya dan memberi tahu engine untuk mengeluarkan hasil dalam format JSON – format yang mudah di‑parse nanti.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine we want JSON output.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: tweak language or recognition speed.
        // ocrEngine.Settings.Language = Language.English; // default is English
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Fast; // or Accurate
```

**Mengapa mengatur `ResultFormat` ke JSON?**  
JSON bersifat bahasa‑agnnostik dan dapat dideserialisasi menjadi objek bertipe kuat di C#, JavaScript, Python, atau lingkungan apa pun yang Anda integrasikan. JSON juga mempertahankan skor kepercayaan dan koordinat kotak pembatas, yang berguna untuk validasi lanjutan.

## Langkah 3: Lakukan OCR pada Gambar dan Tangkap JSON

Setelah engine siap, kita benar‑benar **melakukan OCR pada gambar** dengan memanggil `RecognizeImage`. Metode ini mengembalikan string yang berisi payload JSON.

```csharp
        // Step 3: Perform OCR on the image and capture the JSON output.
        // Replace the path with the location of your own image file.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);
```

> **Kasus tepi:** Jika gambar rusak atau pathnya salah, `RecognizeImage` akan melempar `FileNotFoundException`. Bungkus pemanggilan dalam blok `try/catch` jika Anda memerlukan penanganan error yang lebih halus.

## Langkah 4: Simpan Hasil JSON untuk Pemrosesan Lebih Lanjut

Menyimpan output OCR memungkinkan Anda memasukkannya ke basis data, API, atau komponen UI nanti. Berikut cara sederhana menulis JSON ke disk.

```csharp
        // Step 4: Save the JSON result for later use.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);
```

Jika Anda bekerja di lingkungan cloud, Anda dapat mengganti `File.WriteAllText` dengan panggilan ke Azure Blob Storage atau AWS S3 – string JSON tetap berfungsi dengan cara yang sama.

## Langkah 5: Beri Tahu Pengguna dan Bersihkan

Pesan konsol kecil mengonfirmasi bahwa semuanya berhasil. Dalam aplikasi dunia nyata Anda mungkin mencatatnya ke file atau mengirimnya ke layanan pemantauan.

```csharp
        // Step 5: Inform the user that the JSON file has been saved.
        Console.WriteLine("JSON result saved to " + outputPath);
    }
}
```

Itulah seluruh alur! Jalankan program dengan `dotnet run` dan Anda akan melihat pesan konfirmasi, plus file `receipt.json` yang berisi sesuatu seperti:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $23.45",
          "Confidence": 0.98,
          "Rectangle": { "X": 120, "Y": 340, "Width": 150, "Height": 20 }
        }
      ]
    }
  ]
}
```

## Contoh Lengkap yang Dapat Dijalankan

Untuk melengkapi, berikut adalah file *tepat* yang dapat Anda salin‑tempel ke `Program.cs`. Tidak ada bagian yang hilang.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Configure the engine to return results in JSON format.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: adjust language or recognition mode if needed.
        // ocrEngine.Settings.Language = Language.English;
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Accurate;

        // Step 3: Perform OCR on the image and capture the JSON output.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);

        // Step 4: Save the JSON result for further processing.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);

        // Step 5: Notify that the JSON file has been saved.
        Console.WriteLine($"JSON result saved to {outputPath}");
    }
}
```

> **Tip:** Ganti `YOUR_DIRECTORY` dengan path absolut atau relatif berdasarkan root proyek. Menggunakan `Path.Combine(Environment.CurrentDirectory, "receipt.png")` menghindari hard‑coded separator pada Windows vs. Linux.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

- **Format gambar apa yang didukung?**  
  Aspose.OCR menangani PNG, JPEG, BMP, TIFF, dan GIF. Jika Anda perlu bekerja dengan PDF, konversi setiap halaman menjadi gambar terlebih dahulu (Aspose.PDF dapat membantu).

- **Bisakah saya mendapatkan teks biasa alih‑alih JSON?**  
  Ya – atur `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`. JSON lebih disarankan ketika Anda memerlukan metadata lebih banyak.

- **Bagaimana menangani dokumen multi‑halaman?**  
  Kirim setiap gambar halaman ke `RecognizeImage` dalam loop dan gabungkan hasilnya, atau gunakan `RecognizePdf` yang mengembalikan struktur JSON gabungan.

- **Kekhawatiran performa?**  
  Untuk pemrosesan batch, gunakan kembali satu instance `OcrEngine` alih‑alih membuat yang baru untuk tiap gambar. Juga, aktifkan `RecognitionMode.Fast` jika akurasi dapat ditukar dengan kecepatan.

- **Peringatan lisensi?**  
  Tanpa lisensi, JSON output akan menyertakan bidang watermark. Terapkan lisensi Anda di awal `Main` dengan `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.

## Gambaran Visual

Berikut diagram singkat yang memvisualisasikan alur data dari file gambar → OCR engine → output JSON → penyimpanan. Ini membantu Anda melihat di mana setiap langkah cocok dalam pipeline yang lebih besar.

![Diagram alur melakukan OCR pada gambar](https://example.com/ocr-workflow.png "Diagram alur melakukan OCR pada gambar")

*Alt text: Diagram yang menunjukkan cara melakukan OCR pada gambar menggunakan Aspose OCR, mengonversi ke JSON dan menyimpan ke file.*

## Memperluas Contoh

Sekarang Anda sudah tahu cara **melakukan OCR pada gambar** dan memperoleh payload JSON, Anda mungkin ingin:

- **Menganalisis JSON** dengan `System.Text.Json` atau `Newtonsoft.Json` untuk mengekstrak bidang tertentu.  
- **Menyisipkan teks ke dalam basis data** untuk arsip yang dapat dicari.  
- **Mengintegrasikan dengan API web** sehingga klien dapat mengunggah gambar dan menerima hasil OCR secara instan.  
- **Menerapkan pra‑pemrosesan gambar** (deskew, peningkatan kontras) menggunakan `Aspose.Imaging` untuk akurasi yang lebih baik.

Setiap topik ini dibangun di atas fondasi yang telah kami bahas, dan instance `OcrEngine` yang sama dapat dipakai kembali di semua kasus.

## Kesimpulan

Anda baru saja mempelajari cara **melakukan OCR pada gambar** di C# menggunakan Aspose OCR, mengonfigurasi engine untuk output JSON, dan menyimpan hasilnya untuk penggunaan selanjutnya. Tutorial ini mencakup setiap baris kode, menjelaskan mengapa setiap pengaturan penting, serta menyoroti kasus tepi yang mungkin Anda temui di produksi.

Mulai sekarang, bereksperimenlah dengan bahasa yang berbeda (`ocrEngine.Settings.Language`), sesuaikan `RecognitionMode`, atau hubungkan JSON ke pipeline analitik downstream. Langit adalah batasnya ketika Anda menggabungkan OCR yang andal dengan alat .NET modern.

Jika panduan ini membantu, pertimbangkan memberi bintang pada repositori Aspose.OCR di GitHub, membagikan artikel ini kepada rekan tim, atau meninggalkan komentar dengan tips Anda sendiri. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menggunakan Aspose OCR untuk Hasil JSON dalam Pengenalan Gambar](/ocr/english/net/text-recognition/get-result-as-json/)
- [Cara Mengekstrak Teks dari Gambar Menggunakan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Konversi Gambar ke Teks – Lakukan OCR pada Gambar dari URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}