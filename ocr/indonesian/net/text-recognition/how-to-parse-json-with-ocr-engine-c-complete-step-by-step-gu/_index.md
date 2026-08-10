---
category: general
date: 2026-03-17
description: Pelajari cara mengurai JSON dari hasil OCR di C#. Tutorial ini mencakup
  cara mengekstrak teks, memuat gambar untuk OCR, menjalankan pengenalan OCR, dan
  menggunakan mesin OCR C# secara efisien.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: id
og_description: Cara mengurai JSON dari output OCR di C#. Ikuti panduan kami untuk
  mengekstrak teks, memuat gambar untuk OCR, menjalankan pengenalan OCR, dan menggunakan
  mesin OCR C#.
og_title: Cara Mengurai JSON dengan Mesin OCR C# – Tutorial Lengkap
tags:
- C#
- OCR
- JSON
- Image Processing
title: Cara Mengurai JSON dengan Mesin OCR C# – Panduan Lengkap Langkah demi Langkah
url: /id/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengurai JSON dengan OCR Engine C# – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya‑tanya **bagaimana cara mengurai json** yang keluar langsung dari mesin OCR? Anda tidak sendirian. Kebanyakan pengembang mengalami masalah yang sama—mendapatkan JSON mentah, lalu mencari cara terbaik untuk mengekstrak bagian berguna seperti skor kepercayaan atau teks sebenarnya. Dalam panduan ini kami akan menjelaskan cara memuat gambar untuk OCR, menjalankan pengenalan OCR, dan akhirnya **bagaimana cara mengurai json** secara bersih dan mudah dipelihara.

Pada akhir tutorial Anda akan dapat:

* Memuat gambar untuk OCR dengan hanya beberapa baris kode.  
* Menjalankan pengenalan OCR menggunakan mesin OCR C#.  
* **Bagaimana cara mengekstrak teks** dan metadata lain dari payload JSON.  
* Menangani kasus pinggiran umum (field yang hilang, format tak terduga) tanpa crash.

Tidak perlu dokumentasi eksternal—semua yang Anda butuhkan ada di sini.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* .NET 6.0 atau lebih baru (kode ini juga dapat dikompilasi pada .NET Framework 4.7+).  
* Referensi ke perpustakaan OCR yang Anda gunakan (contoh ini menggunakan kelas hipotetik `OcrEngine`).  
* Paket NuGet `Newtonsoft.Json` untuk penanganan JSON (`Install-Package Newtonsoft.Json`).  
* Sebuah file gambar (misalnya `passport.png`) yang ditempatkan di lokasi yang dapat dibaca aplikasi Anda.

> **Tips pro:** Jika Anda menggunakan SDK OCR komersial, pastikan format output JSON diaktifkan—kebanyakan vendor menyediakan opsi konfigurasi seperti `ocrEngine.Config.OutputFormat`.

## Langkah 1 – Buat dan Konfigurasikan OCR Engine (Kata Kunci Utama dalam Aksi)

Hal pertama yang harus Anda lakukan adalah menginstansiasi engine OCR dan memberitahunya untuk mengembalikan JSON. Di sinilah frasa **bagaimana cara mengurai json** pertama kali muncul dalam kode kami, karena engine akan memberikan string JSON yang nantinya akan kami uraikan.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Mengapa ini penting:** Menetapkan `OutputFormat` ke `Json` memastikan respons berisi teks yang dikenali **dan** metadata berguna seperti skor kepercayaan. Jika Anda melewatkan langkah ini, Anda akan mendapatkan teks biasa, dan **bagaimana cara mengurai json** menjadi tidak relevan.

## Langkah 2 – Muat Gambar untuk OCR

Sekarang kita memuat gambar yang ingin dianalisis. Inilah titik tepat di mana kata kunci sekunder **load image for OCR** bersinar.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **Bagaimana jika file tidak ada?** Bungkus pemanggilan dalam `try/catch` dan tampilkan pesan yang ramah—aplikasi Anda tidak akan crash dan pengguna akan tahu apa yang salah.

## Langkah 3 – Jalankan Pengenalan OCR

Dengan engine siap dan gambar sudah dimuat, langkah logis berikutnya adalah menjalankan proses pengenalan. Ini memenuhi kata kunci sekunder **run OCR recognition**.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

Properti `ocrResult.Text` kini berisi string JSON. Jika Anda mencetaknya ke konsol, Anda akan melihat sesuatu seperti:

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## Langkah 4 – Cara Mengekstrak Teks (dan Field Lain) dari JSON

Berikut adalah inti tutorial: **bagaimana cara mengurai json** dan **bagaimana cara mengekstrak teks** dari payload OCR. Kami akan menggunakan `Newtonsoft.Json.Linq.JObject` karena fleksibilitasnya.

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**Mengapa menggunakan `JObject`?** Ia memungkinkan Anda menavigasi pohon JSON dengan aman tanpa harus mendefinisikan kelas model C# lengkap. Operator null‑conditional (`?.`) melindungi Anda dari `NullReferenceException` jika engine OCR pernah menghilangkan sebuah field.

### Menangani Kasus Pinggiran

* **Field yang hilang:** Pola `?.Value<T>() ?? default` mengembalikan fallback yang masuk akal.  
* **Beberapa halaman:** Loop melalui `jsonObject["Pages"]` jika Anda mengharapkan lebih dari satu halaman.  
* **Kepercayaan bukan angka:** Gunakan `double.TryParse` jika SDK kadang‑kadang mengembalikan string.

## Langkah 5 – Bungkus Semua dalam Metode yang Dapat Digunakan Kembali

Agar tidak perlu menyalin‑tempel boilerplate yang sama, enkapsulasi seluruh alur ke dalam metode pembantu. Ini juga memperlihatkan **use OCR engine C#** secara bersih dan dapat dipakai kembali.

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

Sekarang Anda dapat memanggil `RunOcrAndParseJson(@"C:\Images\passport.png");` dari `Main` atau bagian lain aplikasi Anda.

## Contoh Lengkap yang Berfungsi

Berikut adalah program konsol lengkap yang berdiri sendiri dan dapat Anda salin‑tempel ke dalam proyek `.csproj` baru. Ia mencakup semua bagian yang telah dibahas, plus sedikit penanganan error.

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**Output yang diharapkan** (asumsi OCR berhasil):

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

Jika gambar tidak dapat dibaca, SDK akan melempar exception yang kami tangkap di `Main`, mencetak pesan error yang ramah alih‑alih crash.

## Pertanyaan yang Sering Diajukan (FAQ)

**T: Bagaimana jika engine OCR mengembalikan array halaman?**  
J: Loop melalui `json["Pages"]` dan gabungkan setiap nilai `["Text"]`, atau proses masing‑masing tergantung kebutuhan Anda.

**T: Bisakah saya mendeserialisasi JSON ke dalam kelas C# yang bertipe?**  
J: Tentu saja. Definisikan struktur kelas yang cocok dengan skema JSON dan gunakan `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`. Ini memberi Anda keamanan pada waktu kompilasi tetapi mengharuskan Anda menjaga model tetap sinkron dengan output SDK.

**T: Apakah ini bekerja dengan API OCR async?**  
J: Ya. Ganti `engine.Recognize()` dengan `await engine.RecognizeAsync()` dan ubah `RunOcrAndParseJson` menjadi `async Task`. Bagian parsing JSON tetap sama.

**T: Bagaimana cara menyimpan JSON ke file untuk analisis nanti?**  
J: Setelah `result.Text` diperoleh, panggil `File.WriteAllText(@"output.json", result.Text);`. Anda kemudian dapat memuatnya kembali dengan `JObject.Parse(File.ReadAllText(...))`.

## Selanjutnya

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}