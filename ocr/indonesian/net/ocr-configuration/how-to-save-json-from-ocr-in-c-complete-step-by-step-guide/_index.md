---
category: general
date: 2026-03-02
description: Pelajari cara menyimpan JSON saat mengekstrak teks dari gambar menggunakan
  Aspose OCR. Termasuk kode menulis file JSON, tips memuat gambar bitmap, dan contoh
  lengkap C#.
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: id
og_description: Temukan cara menyimpan JSON saat mengekstrak teks dari gambar dengan
  Aspose OCR. Kode C# lengkap, langkah‑langkah menulis file JSON, dan tips praktis.
og_title: Cara Menyimpan JSON dari OCR di C# – Tutorial Pemrograman Lengkap
tags:
- C#
- OCR
- Aspose
- JSON
title: Cara Menyimpan JSON dari OCR di C# – Panduan Lengkap Langkah demi Langkah
url: /id/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyimpan JSON dari OCR di C# – Panduan Lengkap Langkah‑ demi‑Langkah

Pernah bertanya‑tanya **cara menyimpan JSON** yang berisi teks yang baru saja Anda ambil dari gambar? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika harus *mengekstrak teks dari data gambar* dan kemudian menyimpan informasi tersebut sebagai file JSON yang terformat rapi. Kabar baik? Solusinya cukup sederhana setelah Anda memiliki komponen yang tepat.

Dalam tutorial ini kami akan membahas skenario dunia nyata: menggunakan Aspose.OCR untuk **mengekstrak teks dari gambar**, kemudian **menulis output file JSON**, dan akhirnya **cara menyimpan JSON** ke disk. Sepanjang jalan kami juga akan menunjukkan cara **memuat objek gambar bitmap** dengan benar, serta membahas beberapa kasus tepi yang mungkin Anda temui. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# yang berdiri sendiri dan melakukan semua hal mulai dari memuat gambar hingga menghasilkan dokumen JSON siap pakai.

## Apa yang Anda Butuhkan

- .NET 6.0 atau yang lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)
- Aspose.OCR untuk .NET (Anda dapat mengunduh paket NuGet trial gratis)
- Contoh gambar PNG atau JPG yang berisi teks bahasa Inggris
- Visual Studio, VS Code, atau IDE lain yang mendukung C#

Tidak ada pustaka tambahan yang diperlukan—hanya namespace standar `System.Drawing` untuk penanganan bitmap dan `System.Text.Json` untuk serialisasi.

---

## Langkah 1 – Memuat Gambar Bitmap (bagian “load bitmap image”)

Sebelum OCR dapat dijalankan, Anda harus memuat gambar ke memori sebagai `Bitmap`. Anggap saja ini seperti membuka buku sebelum Anda mulai membaca halamannya.

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **Tip profesional:** Jika gambar berukuran besar, pertimbangkan untuk mengubah ukurannya terlebih dahulu guna meningkatkan performa. Mesin OCR bekerja lebih cepat pada gambar di bawah 2 MB.

---

## Langkah 2 – Mengonfigurasi Aspose OCR Engine

Setelah bitmap siap, kita memerlukan `OcrEngine`. Objek ini tahu cara **mengekstrak teks dari gambar** dan secara opsional memberikan data geometri seperti bounding box.

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

Mengapa mengaktifkan `ExportBoundingBoxes`? Jika Anda pernah perlu menyorot kata‑kata di UI, koordinat tersebut sangat berharga. Jika tidak diperlukan, Anda dapat mengatur flag menjadi `false` dan JSON akan menjadi sedikit lebih ramping.

---

## Langkah 3 – Menjalankan OCR dan Mendapatkan Hasil Terstruktur

Dengan mesin yang sudah dikonfigurasi, langkah selanjutnya adalah operasi **cara mengekstrak teks** yang sebenarnya. Metode `RecognizeToOcrResult` mengembalikan objek kaya yang berisi teks yang dikenali, skor kepercayaan, dan data tata letak opsional.

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

Variabel `ocrResult` kini menyimpan semua yang Anda perlukan. Jika Anda memeriksanya di debugger, Anda akan melihat hierarki objek `Page`, `Paragraph`, `Line`, dan `Word`, masing‑masing dengan properti `Text`‑nya.

---

## Langkah 4 – Menserealkan Hasil ke String JSON yang Diformat

Di sinilah keajaiban **cara menyimpan json** benar‑benar dimulai. Kita akan menggunakan `System.Text.Json` karena sudah built‑in, cepat, dan mendukung pretty printing secara default.

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

Jika Anda memerlukan konvensi penamaan yang berbeda (misalnya camelCase), cukup tambahkan `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` ke opsi.

---

## Langkah 5 – Menulis JSON ke Disk (langkah “write json file”)

Akhirnya, kita **menulis file JSON** ke sistem berkas. Inilah jawaban konkret untuk **cara menyimpan json** dalam lingkungan C#.

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

Setelah baris ini dieksekusi, Anda akan menemukan file `sample-page.json` yang terindentasikan rapi di samping gambar asli Anda. Buka dengan editor teks apa pun atau kirimkan ke layanan lain—data OCR Anda kini dapat dipindahkan.

---

## Langkah 6 – Memverifikasi Output (Apa yang Harus Anda Lihat?)

Menjalankan program seharusnya mencetak konfirmasi singkat ke konsol:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

Buka file JSON yang dihasilkan dan Anda akan melihat sesuatu seperti:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Jika flag `ExportBoundingBoxes` bernilai true, setiap kata juga akan berisi koordinat `Rectangle`. Ini sangat berguna untuk pekerjaan UI selanjutnya.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika jalur gambar tidak valid?

Bungkus pemuatan bitmap dalam blok `try/catch` dan tampilkan error yang jelas:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### Bagaimana cara menangani bahasa non‑Inggris?

Cukup ubah properti `Language`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose mendukung lebih dari 50 bahasa, jadi pilih yang sesuai dengan materi sumber Anda.

### Apakah saya perlu membuang (dispose) objek `Bitmap`?

Ya. `Bitmap` mengimplementasikan `IDisposable`, jadi bungkus dalam pernyataan `using` untuk membebaskan sumber daya native dengan cepat.

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### Bagaimana jika saya menginginkan JSON yang ringkas tanpa indentasi?

Ganti `JsonSerializerOptions`:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

Itu akan mengurangi ukuran file—berguna untuk skenario dengan bandwidth terbatas.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut adalah program lengkap yang menggabungkan semua langkah, penanganan error, dan tip praktik terbaik yang dibahas di atas. Simpan sebagai `Program.cs` dan jalankan lewat command line atau IDE Anda.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**Apa yang dilakukan program ini:**  
1. Memeriksa apakah gambar ada.  
2. Memuatnya dengan aman menggunakan blok `using`.  
3. Menjalankan OCR untuk **mengekstrak teks dari gambar**.  
4. Menserealkan hasil ke string JSON yang terindentasikan rapi.  
5. Menyimpan string tersebut ke disk, menjawab pertanyaan inti **cara menyimpan json**.

Jalankan `dotnet run` (atau tekan F5 di Visual Studio) dan Anda akan melihat pesan konfirmasi setelah file berhasil ditulis.

---

## Kesimpulan

Anda kini memiliki resep lengkap, siap produksi, untuk **cara menyimpan JSON** yang berasal dari ekstraksi teks berbasis OCR. Dari memuat gambar bitmap hingga menulis file JSON bersih, setiap langkah dijelaskan beserta “mengapa” di balik kode, sehingga Anda dapat menyesuaikan solusi ini untuk proyek Anda sendiri.  

Jika Anda penasaran dengan frontier berikutnya, pertimbangkan:

- **Cara mengekstrak teks** dari PDF dengan mengonversi tiap halaman menjadi gambar terlebih dahulu.  
- Menggunakan data bounding‑box untuk menyorot kata di UI WPF atau WinForms.  
- Men-stream JSON langsung ke API web alih‑alih menulis file (gunakan `HttpClient`).

Cobalah, sesuaikan opsinya, dan biarkan data OCR menggerakkan aplikasi apa pun yang Anda bangun. Ada pertanyaan? Tinggalkan komentar, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}