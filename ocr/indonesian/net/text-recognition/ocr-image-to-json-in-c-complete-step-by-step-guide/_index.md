---
category: general
date: 2026-02-11
description: Konversi gambar OCR ke JSON dalam C#. Pelajari cara mengekstrak teks
  dari gambar, membaca file gambar di C#, memformat output JSON, dan mencetak JSON
  secara rapi di C# dengan Aspose.OCR.
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: id
og_description: Ubah gambar OCR menjadi JSON di C#. Panduan ini menunjukkan cara mengekstrak
  teks dari gambar, membaca file gambar di C#, memformat output JSON, dan mencetak
  JSON secara rapi di C# menggunakan Aspose.OCR.
og_title: OCR gambar ke JSON dalam C# – Panduan Lengkap Langkah demi Langkah
tags:
- OCR
- C#
- JSON
title: OCR gambar ke JSON dalam C# – Panduan Lengkap Langkah demi Langkah
url: /id/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image ke json di C# – Panduan Lengkap Langkah‑per‑Langkah

Pernah membutuhkan **ocr image ke json** tetapi tidak yakin pustaka mana yang harus dipilih atau bagaimana mendapatkan hasil yang terformat rapi? Anda tidak sendirian. Dalam banyak aplikasi dunia nyata—pemindaian struk, verifikasi ID, atau pengarsipan dokumen sederhana—Anda ingin mengekstrak teks dari gambar dan menghasilkan payload JSON bersih yang dapat dikonsumsi layanan hilir.

Dalam tutorial ini kita akan menelusuri seluruh alur: mulai dari membaca file gambar di C# hingga mengekstrak teks dengan Aspose.OCR, kemudian meminta mesin menghasilkan output JSON terstruktur, dan akhirnya mem‑pretty‑print JSON tersebut agar mudah dibaca manusia. Pada akhir tutorial Anda akan memiliki potongan kode mandiri, siap produksi, yang dapat Anda sisipkan ke proyek .NET apa pun.  

Kami juga akan membahas jebakan umum (seperti paket bahasa yang hilang) dan menunjukkan beberapa variasi cepat—misalnya, beralih ke output XML atau menangani PDF multi‑halaman. Tidak perlu dokumentasi eksternal; semua yang Anda butuhkan ada di sini.

## Apa yang Anda Butuhkan

- **.NET 6+** (kode ini juga bekerja dengan .NET Framework 4.7+)
- **Aspose.OCR untuk .NET** – instal melalui NuGet (`Install-Package Aspose.OCR`)
- Sebuah gambar contoh (misalnya `receipt.png`) yang ditempatkan di lokasi yang dapat Anda referensikan
- Familiaritas dasar dengan sintaks C# (jika Anda pernah menulis “Hello World”, Anda sudah siap)

> *Tips pro:* Jika Anda menjalankan di server CI, atur `AutomaticResourceDownload = true` sehingga Aspose mengunduh data bahasa secara otomatis—tanpa harus mengatur DLL secara manual.

## Langkah 1: Baca file gambar C# dan buat mesin OCR  

Hal pertama yang kita lakukan adalah memuat gambar dari disk. Menggunakan `System.Drawing.Image` membuat kode singkat dan bekerja untuk PNG, JPEG, BMP, bahkan TIFF multi‑halaman (mesin akan mengambil halaman pertama secara default).

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**Mengapa ini penting:**  
- `AutomaticResourceDownload` mencegah crash runtime ketika file bahasa Inggris tidak tersedia secara lokal.  
- Menetapkan `OutputFormat` ke `Json` berarti mesin sudah melakukan pekerjaan berat mengonversi hasil OCR mentah menjadi objek terstruktur—tanpa perlu parsing string manual.

## Langkah 2: Jalankan OCR dan dapatkan output JSON  

Sekarang kita memasukkan bitmap yang telah dimuat ke dalam mesin. Metode `Recognize` mengembalikan `OcrResult` yang berisi properti `Text` yang memuat string JSON.

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**Kasus tepi:** Jika gambar rusak atau path salah, `Image.FromFile` akan melempar `FileNotFoundException`. Bungkus blok ini dengan `try/catch` jika Anda mengharapkan input yang tidak dapat diandalkan.

## Langkah 3: Parse dan format JSON – pretty print JSON C#  

JSON mentah dari mesin OCR bersifat padat dan sulit dibaca. Dengan menggunakan `System.Text.Json` kita dapat mendeserialisasikannya menjadi `JsonDocument`, lalu menyerialisasikannya kembali dengan indentasi.

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**Apa yang akan Anda lihat:**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

JSON kini mencakup teks baris‑per‑baris, kotak pembatas, bahasa yang terdeteksi, dan skor kepercayaan—sempurna untuk dikirim ke analitik hilir atau komponen UI.

## Langkah 4: Bonus – Mengubah format output atau bahasa  

Jika Anda pernah perlu **format json output** menjadi XML atau ingin OCR struk berbahasa Spanyol, cukup ubah konfigurasi mesin:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

Sisa kode tetap sama; Anda hanya mengubah langkah deserialisasi (gunakan `XmlDocument` untuk XML).

## Contoh Lengkap yang Berfungsi  

Menggabungkan semuanya, berikut satu file yang dapat Anda salin‑tempel ke aplikasi console:

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

Menjalankan program ini akan mencetak payload JSON yang terindentasi dengan rapi ke konsol dan menyimpannya ke `C:\Temp\ocr_pretty.json`. Blok `try/catch` memastikan bahwa meskipun gambar tidak dapat dibaca, Anda akan mendapatkan pesan error yang jelas alih‑alih crash diam‑diam.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai  

- **Bagaimana jika OCR mengembalikan teks kosong?**  
  Biasanya ini berarti gambar terlalu berisik atau bahasa tidak cocok. Coba tingkatkan kontras gambar atau ubah `Language` menjadi `AutoDetect`.  

- **Bisakah saya memproses banyak gambar dalam loop?**  
  Tentu saja. Bungkus blok `using (var img = Image.FromFile(...))` di dalam loop `foreach (var file in Directory.GetFiles(...))` dan kumpulkan setiap `prettyJson` ke dalam list atau tulis ke file terpisah.  

- **Apakah skema JSON stabil?**  
  Aspose menjamin kompatibilitas mundur untuk format output `Json`, tetapi selalu periksa atribut `Version` dalam respons jika Anda menargetkan versi API tertentu.  

- **Apakah saya memerlukan lisensi untuk Aspose.OCR?**  
  Kunci evaluasi gratis berlaku hingga 100 halaman. Untuk produksi, beli lisensi dan atur dengan `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.

## Kesimpulan  

Anda kini memiliki **solusi lengkap, mandiri untuk ocr image ke json** di C#. Dengan membaca file gambar, mengonfigurasi mesin OCR, meminta output JSON, dan mem‑pretty‑print‑nya, Anda dapat mengintegrasikan ekstraksi teks ke layanan .NET apa pun tanpa harus mengutak‑atik string.  

Selanjutnya Anda dapat menjelajahi **extract text from image** untuk tipe file lain (PDF, TIFF multi‑halaman), bereksperimen dengan bahasa berbeda, atau mengalirkan JSON ke penyimpanan NoSQL untuk analitik. Langit adalah batasnya—ingatlah untuk menangani error dengan elegan dan perhatikan lisensi saat skala meningkat.

Selamat coding, semoga pipeline OCR Anda selalu akurat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}