---
category: general
date: 2026-04-17
description: Pelajari contoh Aspose OCR untuk membaca file gambar dengan C#, mengekstrak
  teks gambar dengan C#, dan menulis file JSON dengan C#. Tutorial OCR C# lengkap
  langkah demi langkah.
draft: false
keywords:
- aspose ocr example
- write json file c#
- read image file c#
- extract text image c#
- c# ocr tutorial
language: id
og_description: Kuasi contoh Aspose OCR untuk membaca gambar, mengekstrak teks, dan
  menulis file JSON menggunakan C#. Ikuti tutorial OCR C# yang singkat ini.
og_title: contoh aspose ocr – Mengonversi Teks Gambar ke JSON dalam C#
tags:
- Aspose
- OCR
- C#
- JSON
title: contoh aspose ocr – Mengonversi Teks Gambar ke JSON dalam C#
url: /id/net/text-recognition/aspose-ocr-example-convert-image-text-to-json-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aspose ocr example – Mengonversi Teks Gambar ke JSON dalam C#

Pernah membutuhkan **aspose ocr example** yang tidak hanya membaca gambar tetapi juga menghasilkan JSON rapi untuk pemrosesan lanjutan? Anda tidak sendirian. Dalam banyak proyek—otomatisasi faktur, pemindaian kwitansi, atau bahkan pengarsipan dokumen sederhana—para pengembang menghadapi masalah yang sama: “Bagaimana cara mendapatkan hasil OCR dalam format yang disukai API saya?”  

Berita baik? Dengan Aspose.OCR Anda dapat melakukannya dalam beberapa baris kode, dan saya akan menunjukkan cara tepatnya. Pada akhir panduan ini Anda akan tahu cara **read image file C#**, **extract text image C#**, dan **write JSON file C#**—semua dibungkus dalam tutorial OCR C# yang bersih dan dapat digunakan kembali.

## Apa yang Anda Butuhkan

- .NET 6.0 atau yang lebih baru (kode ini juga dapat dikompilasi dengan .NET Core)  
- Paket NuGet Aspose.OCR untuk .NET (`Install-Package Aspose.OCR`)  
- Sebuah gambar (`input.jpg`) yang berisi teks yang jelas dan dapat dibaca mesin  
- Editor teks atau Visual Studio (IDE apa pun dapat digunakan)  

Tidak ada file konfigurasi tambahan, tidak ada keajaiban tersembunyi—hanya SDK dan sebuah gambar.

## Langkah 1 – Membaca file gambar C# dengan Aspose.OCR

Hal pertama yang harus dilakukan: Anda harus memberi mesin OCR gambar yang valid. Aspose.OCR mengharapkan objek `OcrImage`, yang dapat Anda buat langsung dari jalur file.

```csharp
using Aspose.OCR;
using System.IO;

// Path to the source picture
string imagePath = @"C:\MyProject\Images\input.jpg";

// Load the image – this is the “read image file C#” part
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

*Mengapa ini penting:* Memuat gambar lebih awal memungkinkan Anda memvalidasi keberadaan file dan menangkap masalah format sebelum mesin mulai memproses piksel. Jika file tidak ada, `FromFile` akan melemparkan pengecualian yang jelas yang dapat Anda tangani di kemudian hari.

## Langkah 2 – Menginisialisasi mesin Aspose OCR

Membuat mesin ini murah, tetapi Anda harus membungkusnya dalam pernyataan `using` agar sumber daya segera dibebaskan.

```csharp
// Create the OCR engine – it holds all the recognition settings
using var ocrEngine = new OcrEngine();
```

*Tips profesional:* Mesin default bekerja baik untuk kebanyakan teks berbasis Latin. Jika Anda membutuhkan bahasa lain, Anda dapat mengatur `ocrEngine.Language = Language.YourLanguage;` sebelum memanggil `Recognize`.

## Langkah 3 – Ekstrak teks gambar C# – Lakukan pengenalan

Sekarang pekerjaan berat terjadi. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi teks mentah, skor kepercayaan, dan kotak pembatas untuk setiap kata.

```csharp
// Run OCR – this is the “extract text image C#” step
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

Anda akan melihat `ocrResult.Text` berisi string biasa, sementara `ocrResult.Regions` memberikan data posisi jika Anda perlu menyorot kata dalam UI.

## Langkah 4 – Menulis file JSON C# – Serialisasi hasil

Serialisasi ke JSON mudah dilakukan dengan `System.Text.Json`. Kami akan mencetak output dengan format rapi sehingga mudah dibaca manusia.

```csharp
using System.Text.Json;

// Convert the OCR result to nicely formatted JSON
string json = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true });
```

*Mengapa kami menggunakan `System.Text.Json`*: Ini sudah terintegrasi dalam .NET, cepat, dan tidak memerlukan dependensi tambahan. Jika Anda lebih suka Newtonsoft, kode hanya berubah beberapa baris.

## Langkah 5 – Menyimpan JSON ke disk

Akhirnya, tulis string ke sebuah file. Ini menyelesaikan bagian **write json file c#**.

```csharp
// Destination path for the JSON output
string jsonOutputPath = @"C:\MyProject\Output\ocrResult.json";

// Save the JSON – now you have a portable data file
File.WriteAllText(jsonOutputPath, json);

Console.WriteLine("OCR data saved as JSON.");
```

### Output JSON yang Diharapkan (contoh)

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑01\nTotal: $1,234.56",
  "Regions": [
    {
      "BoundingBox": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Confidence": 0.98,
      "Text": "Invoice #12345"
    },
    {
      "BoundingBox": { "X": 10, "Y": 60, "Width": 150, "Height": 30 },
      "Confidence": 0.96,
      "Text": "Date: 2024‑03‑01"
    },
    {
      "BoundingBox": { "X": 10, "Y": 100, "Width": 180, "Height": 30 },
      "Confidence": 0.99,
      "Text": "Total: $1,234.56"
    }
  ]
}
```

*Catatan:* Angka-angka tepat akan berbeda tergantung pada gambar Anda, tetapi struktur tetap sama—sempurna untuk dimasukkan ke API, basis data, atau visualizer front‑end.

## Tutorial OCR C# Lengkap – Semua langkah digabungkan

Berikut adalah program lengkap yang siap disalin‑tempel yang menggabungkan semua langkah. Tidak ada bagian yang hilang, tidak ada jalan pintas “lihat dokumentasi”.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\MyProject\Images\input.jpg";
        var ocrImage = OcrImage.FromFile(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine();
        // Example: ocrEngine.Language = Language.English; // optional

        // -------------------------------------------------
        // Step 3: Perform OCR recognition
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // -------------------------------------------------
        // Step 4: Serialize the result to indented JSON
        // -------------------------------------------------
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // -------------------------------------------------
        // Step 5: Write the JSON to a file
        // -------------------------------------------------
        string jsonOutputPath = @"C:\MyProject\Output\output.json";
        File.WriteAllText(jsonOutputPath, json);

        // -------------------------------------------------
        // Step 6: Let the user know we’re done
        // -------------------------------------------------
        Console.WriteLine("OCR data saved as JSON.");
    }
}
```

### Menjalankan kode

1. Ganti kedua jalur `@"C:\MyProject\…"` dengan direktori Anda yang sebenarnya.  
2. Bangun proyek (`dotnet build`) dan jalankan (`dotnet run`).  
3. Buka `output.json`—Anda akan melihat representasi teks gambar yang terstruktur dengan baik.

## Pertanyaan Umum & Kasus Tepi

**Bagaimana jika gambar saya buram?**  
Aspose.OCR menawarkan opsi pra‑pemrosesan seperti `ocrEngine.ImagePreprocessOptions.Deskew = true;`. Aktifkan sebelum memanggil `Recognize` untuk meningkatkan akurasi.

**Bisakah saya membatasi output hanya ke teks biasa?**  
Tentu—cukup serialisasikan `ocrResult.Text` alih-alih seluruh objek:

```csharp
string plainJson = JsonSerializer.Serialize(
    new { Text = ocrResult.Text },
    new JsonSerializerOptions { WriteIndented = true });
```

**Apakah saya perlu menangani PDF multi‑halaman?**  
Contoh ini berfokus pada satu gambar, tetapi Anda dapat melakukan loop pada setiap gambar halaman, menjalankan langkah yang sama, dan menggabungkan hasil ke dalam array JSON.

## Tips Pro & Hal-hal yang Perlu Diwaspadai

- **Jalur file:** Gunakan `Path.Combine` untuk menghindari backslash yang ditulis keras, terutama jika Anda beralih ke Linux.  
- **Memori:** Untuk batch besar, gunakan kembali satu instance `OcrEngine` alih-alih membuat yang baru untuk setiap gambar.  
- **Ukuran JSON:** Jika Anda hanya membutuhkan teks, hilangkan properti `Regions` untuk menjaga payload tetap kecil.  
- **Pemeriksaan versi:** Tutorial ini diuji dengan Aspose.OCR 23.9.0; versi yang lebih baru mempertahankan antarmuka API yang sama, tetapi selalu periksa catatan rilis untuk perubahan yang memecah kompatibilitas.

![Contoh output JSON OCR – aspose ocr example](https://example.com/sample-ocr-json.png "pratinjau JSON contoh aspose ocr")

## Kesimpulan

Kami telah melewati contoh **aspose ocr example** lengkap yang membaca gambar, mengekstrak teksnya, dan menulis hasilnya ke file JSON menggunakan C# murni. Solusinya mandiri, siap produksi, dan mudah diperluas—baik Anda ingin menambahkan dukungan bahasa, menyesuaikan ambang kepercayaan, atau mengirim JSON ke layanan downstream.

Jika Anda mencari langkah selanjutnya, coba rangkaikan tutorial ini dengan **C# OCR tutorial** yang mengunggah JSON ke Azure Cognitive Search, atau bereksperimen dengan mengekstrak tabel dari faktur. Langit adalah batasnya setelah Anda memiliki JSON.

Punya variasi yang ingin Anda bagikan? Tinggalkan komentar, fork repositori, atau hubungi saya di GitHub. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}