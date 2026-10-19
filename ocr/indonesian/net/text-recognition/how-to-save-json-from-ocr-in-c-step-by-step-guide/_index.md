---
category: general
date: 2026-02-19
description: Cara menyimpan JSON dari output OCR di C# – pelajari cara mengekstrak
  teks dari gambar, menulis file JSON di C#, dan mengonversi gambar ke JSON dengan
  Aspose OCR.
draft: false
keywords:
- how to save json
- extract text from image
- write json file c#
- convert image to json
- c# ocr tutorial
language: id
og_description: Cara menyimpan JSON dari hasil OCR di C# itu mudah. Ikuti tutorial
  ini untuk mengekstrak teks dari gambar dan menulis file JSON dengan gaya C#.
og_title: Cara Menyimpan JSON dari OCR di C# – Panduan Lengkap
tags:
- C#
- OCR
- JSON
title: Cara Menyimpan JSON dari OCR di C# – Panduan Langkah demi Langkah
url: /id/net/text-recognition/how-to-save-json-from-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyimpan JSON dari OCR di C# – Tutorial Lengkap

Menyimpan json dari hasil OCR di C# adalah kebutuhan umum ketika Anda mengubah dokumen yang dipindai menjadi data terstruktur. Dalam panduan ini Anda akan melihat secara tepat cara mengekstrak teks dari gambar, mengonversinya menjadi json, dan akhirnya menulis file json gaya C#—tanpa basa-basi, hanya solusi yang berfungsi.

Pernah mencoba membaca struk dengan pemindai, hanya untuk berakhir dengan gambar buram yang tidak dapat dicari? Itulah masalah yang dihadapi banyak pengembang ketika mereka perlu mengambil data dari gambar. Pada akhir artikel ini Anda akan memiliki aplikasi konsol kecil yang membaca sebuah gambar, mengambil teks dengan Aspose OCR, dan menyimpan file json bersih yang dapat Anda berikan ke layanan downstream mana pun.

Kami akan membahas semuanya: paket NuGet yang Anda perlukan, kode lengkap (lengkap, dapat dijalankan, dan sangat berkomentar), jebakan umum, dan cara cepat memverifikasi output. Tidak diperlukan pengalaman OCR sebelumnya—hanya pemahaman dasar tentang C# dan .NET.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6 SDK atau lebih baru (kode menargetkan .NET 6 tetapi bekerja pada .NET 5+)
- Visual Studio 2022, VS Code, atau editor apa pun yang Anda suka
- Sebuah file gambar (`input.png`) yang ingin Anda proses
- Akses internet untuk mengunduh paket NuGet **Aspose.OCR**

Jika ada yang belum ada, dapatkan sekarang; jika tidak, Anda akan membuang waktu nanti.  

> **Pro tip:** Aspose OCR menawarkan kunci percobaan gratis—sempurna untuk bereksperimen tanpa lisensi.

## Langkah 1: Instal Paket NuGet Aspose OCR

Langkah pertama, tambahkan pustaka yang melakukan pekerjaan berat. Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah tunggal itu mengunduh binari Aspose OCR terbaru dan menambahkan referensi ke `.csproj` Anda.  

> **Mengapa langkah ini penting:** Tanpa paket tersebut, kelas `OcrEngine` tidak ada, dan Anda akan mendapatkan error saat kompilasi.  

Setelah paket terpasang, mari buat kerangka aplikasi konsol kita.

## Langkah 2: Siapkan Struktur Proyek

Buat proyek konsol baru jika belum melakukannya:

```bash
dotnet new console -n JsonExportOcr
cd JsonExportOcr
```

Di dalam `Program.cs` ganti konten default dengan contoh lengkap di bawah ini. Kami akan menjelaskan setiap baris nanti, tetapi memiliki file siap membantu Anda menyalin‑tempel tanpa kehilangan kurung kurawal.

## Langkah 3: Inisialisasi OCR Engine (Ekstrak Teks dari Gambar)

Baris kode pertama yang sebenarnya membuat mesin OCR dan memberi tahu untuk mencari karakter bahasa Inggris. Anda dapat beralih ke `Language.Spanish` atau bahasa lain yang didukung, tetapi bahasa Inggris adalah kasus paling umum.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3.1: Create an OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Step 3.2: Recognize text from the input image
        // Replace the path with where your image actually lives
        string inputPath = @"YOUR_DIRECTORY/input.png";
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);
```

**Apa yang terjadi?**  
- `OcrEngine` adalah titik masuk untuk Aspose OCR.  
- Menetapkan `Language` meningkatkan akurasi karena mesin dapat menerapkan heuristik khusus bahasa.  
- `RecognizeImage` mengembalikan objek `OcrResult` yang berisi semua kata yang dikenali, skor kepercayaan, dan kotak pembatas.

Jika gambar tidak ada atau rusak, klausa penjaga mencetak pesan ramah dan menghentikan proses—pemeriksaan kecil ini menyelamatkan Anda dari error null‑reference yang membingungkan nanti.

## Langkah 4: Konversi Hasil OCR ke JSON (Ubah Gambar menjadi JSON)

Aspose OCR menyertakan pembantu bernama `JsonResultWriter`. Ia menserialisasi `OcrResult` menjadi string JSON bersih yang mencerminkan struktur yang Anda harapkan dari sebuah REST API.

```csharp
        // Step 4: Convert the OCR result to a JSON string
        string jsonResult = JsonResultWriter.Write(ocrResult);
```

**Mengapa menggunakan `JsonResultWriter`?**  
- Ia menangani objek kompleks (seperti koleksi `Word` bersarang) secara otomatis.  
- Anda menghindari menulis serializer sendiri, yang dapat melewatkan bidang halus seperti persentase kepercayaan.

Pada titik ini `jsonResult` kira‑kira terlihat seperti ini (diprint dengan indah untuk keterbacaan):

```json
{
  "PageCount": 1,
  "Pages": [
    {
      "PageNumber": 1,
      "Words": [
        {
          "Text": "Hello",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 50, "Height": 15 }
        },
        // … more words …
      ]
    }
  ]
}
```

Anda dapat menyalin potongan itu ke penampil JSON untuk menjelajahi strukturnya.  

> **Kasus tepi:** Jika gambar Anda berisi beberapa halaman, JSON akan menyertakan array `Pages`—pastikan konsumen downstream dapat menanganinya.

## Langkah 5: Tulis JSON ke Disk (Cara Menyimpan JSON)

Sekarang tiba inti tutorial: **cara menyimpan json** ke file di disk. Kelas .NET `File` menjadikannya satu baris kode, tetapi kami akan menambahkan sedikit penanganan error untuk ketahanan.

```csharp
        // Step 5: Write the JSON string to an output file
        string outputPath = @"YOUR_DIRECTORY/output.json";
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
```

Itulah saat Anda akhirnya menjawab pertanyaan *bagaimana cara menyimpan json*—file dibuat, ditimpa jika sudah ada, dan Anda mendapatkan pesan konsol yang jelas mengonfirmasi keberhasilan.

## Langkah 6: Verifikasi Hasil

Setelah program selesai, buka `output.json` di editor apa pun (VS Code, Notepad++, atau bahkan browser). Anda harus melihat representasi JSON yang terformat rapi dari output OCR. Jika Anda menemukan array `"Words": []` yang kosong, periksa kembali kualitas gambar—OCR kesulitan dengan kontras rendah atau noise berat.

Anda juga dapat menjalankan pemeriksaan cepat dari baris perintah:

```bash
dotnet run
```

Anda harus melihat:

```
JSON saved to YOUR_DIRECTORY/output.json
```

Jika muncul error, konsol akan memberi tahu apakah file input tidak ada atau operasi penulisan gagal.

## Contoh Lengkap yang Berfungsi

Berikut adalah program **lengkap** yang dapat Anda salin‑tempel ke `Program.cs`. Ganti `YOUR_DIRECTORY` dengan folder yang berisi `input.png`. Tidak diperlukan file lain.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3: Initialize OCR engine (extract text from image)
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Define file paths
        string inputPath = @"YOUR_DIRECTORY/input.png";
        string outputPath = @"YOUR_DIRECTORY/output.json";

        // Validate input image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        // Recognize text
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Convert OCR result to JSON (convert image to json)
        string jsonResult = JsonResultWriter.Write(ocrResult);

        // Write JSON to disk (how to save json)
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
    }
}
```

Jalankan program, buka file yang dihasilkan, dan Anda telah berhasil menyelesaikan **tutorial ocr c#** yang menunjukkan **cara menyimpan json** dari sebuah gambar.

## Jebakan Umum & Tips (Menulis File JSON C#)

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Array `Words` kosong** | Gambar terlalu gelap atau resolusi rendah | Praproses gambar (tingkatkan kontras, gunakan DPI lebih tinggi) |
| **`File.WriteAllText` melempar UnauthorizedAccessException** | Mencoba menulis ke folder baca‑saja | Pilih direktori yang dapat ditulis (mis. `%TEMP%` atau folder proyek Anda) |
| **Paket NuGet hilang** | Lupa menjalankan `dotnet add package Aspose.OCR` | Jalankan kembali perintah tersebut dan rebuild |
| **JSON dalam satu baris** | `WriteAllText` menulis string mentah tanpa format | Gunakan `JsonResultWriter.Write(ocrResult, true)` jika overload tersedia, atau proses output melalui `JsonSerializer` dengan `WriteIndented = true` |

Pemeriksaan cepat ini menjaga alur kerja **menulis file json c#** Anda tetap lancar dan mencegah momen “tidak ada apa‑apa” yang menakutkan.

## Langkah Selanjutnya (Ekstrak Teks dari Gambar & Lebih Banyak)

Sekarang Anda sudah tahu **cara menyimpan json**, Anda mungkin ingin:

- **Simpan hasil**...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}