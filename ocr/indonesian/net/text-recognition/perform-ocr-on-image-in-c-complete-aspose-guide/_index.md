---
category: general
date: 2026-06-28
description: Lakukan OCR pada gambar menggunakan Aspose.OCR di C#. Pelajari cara mengenali
  teks dari gambar, mengekstrak teks dari faktur, memuat gambar untuk OCR, dan menulis
  JSON ke file.
draft: false
keywords:
- perform OCR on image
- recognize text from image
- write JSON to file
- extract text from invoice
- load image for OCR
language: id
og_description: Lakukan OCR pada gambar dengan Aspose.OCR di C#. Panduan ini menunjukkan
  cara mengenali teks dari gambar, mengekstrak teks dari faktur, dan menulis JSON
  ke file.
og_title: Lakukan OCR pada Gambar di C# – Tutorial OCR Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  headline: Perform OCR on Image in C# – Complete Aspose Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  name: Perform OCR on Image in C# – Complete Aspose Guide
  steps:
  - name: What if the image contains multiple languages?
    text: 'Aspose.OCR automatically detects the language based on the character set.
      If you need to force a specific language (e.g., English for most invoices),
      set the `Language` property on the engine:'
  - name: How do I handle large PDFs with many pages?
    text: Convert each page to an image first (using a PDF‑to‑image library) and then
      loop through the images, applying the same **perform OCR on image** routine.
      Aggregate the JSON results into a single array if you want a consolidated output.
  - name: Can I stream the JSON instead of writing a whole file?
    text: 'Yes. If you’re building a web API, you can return `json` directly as the
      response body:'
  - name: What about performance?
    text: The OCR engine runs synchronously in the example above. For high‑throughput
      scenarios, wrap the recognition call in `Task.Run` or use the asynchronous versions
      (if available) to keep your UI responsive or to parallelize batch processing.
  type: HowTo
tags:
- Aspose.OCR
- C#
- JSON
- ImageProcessing
title: Lakukan OCR pada Gambar di C# – Panduan Lengkap Aspose
url: /id/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar di C# – Panduan Lengkap Aspose

Pernahkah Anda perlu **perform OCR on image** file tetapi tidak yakin perpustakaan .NET mana yang akan memberikan hasil yang bersih dan terstruktur? Anda tidak sendirian—para pengembang terus menanyakan cara **recognize text from image** aset, terutama saat menangani faktur atau kwitansi. Dalam tutorial ini kami akan memandu contoh langsung yang tidak hanya **loads image for OCR**, tetapi juga **extracts text from invoice** data dan **writes JSON to file** untuk pemrosesan lanjutan.

Pada akhir panduan ini Anda akan memiliki aplikasi konsol siap‑jalankan yang:

* Membuat instance mesin Aspose OCR,
* Memuat gambar PNG (atau JPG),
* Mengenali konten teks,
* Menyerialisasi hasil sebagai JSON berformat cantik,
* Menyimpan JSON tersebut ke disk.

Tanpa layanan eksternal, tanpa keajaiban tersembunyi—hanya kode C# murni yang dapat Anda salin, tempel, dan jalankan.

## Prasyarat

Sebelum kita menyelam lebih dalam, pastikan Anda memiliki:

* .NET 6 SDK atau lebih baru (kode ini bekerja dengan .NET Core dan .NET Framework juga).
* Lisensi Aspose.OCR yang valid atau kunci evaluasi sementara (versi percobaan gratis dapat digunakan untuk pengujian).
* Visual Studio 2022, VS Code, atau IDE apa pun yang Anda sukai.
* File gambar—misalnya `invoice.png`—diletakkan di lokasi yang dapat Anda referensikan dengan jalur penuh atau relatif.

> **Pro tip:** Jika Anda menangani faktur yang dipindai, pertimbangkan pra‑pemrosesan gambar (meluruskan, meningkatkan kontras) sebelum memberi makan ke mesin OCR. Aspose.OCR menangani banyak langkah tersebut secara otomatis, tetapi gambar sumber yang bersih selalu menghasilkan hasil yang lebih baik.

---

## Langkah 1: Siapkan Proyek dan Instal Aspose.OCR

Pertama, buat proyek konsol baru dan tambahkan paket NuGet Aspose.OCR.

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **Mengapa langkah ini penting:** Assembly `Aspose.OCR` menyediakan kelas `OcrEngine` yang akan kita gunakan untuk **perform OCR on image** data. Tanpa paket ini, kompiler tidak akan mengenali tipe‑tipe terkait OCR.

---

## Langkah 2: Muat Gambar untuk OCR

Sekarang kita akan menulis kode yang **load image for OCR**. Metode `OcrImage.FromFile` menerima jalur absolut atau relatif dan membungkus bitmap dalam format yang dipahami mesin.

```csharp
using Aspose.OCR;
using System.IO;

// Replace with the actual path to your invoice image
string imagePath = @"YOUR_DIRECTORY\invoice.png";

// Step 2: Load the image
OcrImage image = OcrImage.FromFile(imagePath);
```

> **Penjelasan:** Dengan memisahkan jalur ke dalam variabel terpisah, kita menjaga kode tetap rapi dan memudahkan penggunaan kembali referensi gambar yang sama nanti (misalnya, saat logging atau debugging). Jika file tidak ditemukan, `FromFile` melempar `FileNotFoundException`, yang dapat Anda tangkap untuk memberikan pesan error yang ramah.

## Langkah 3: Lakukan OCR pada Gambar dan Kenali Teks

Dengan gambar di tangan, kita membuat instance `OcrEngine` dan memintanya untuk **recognize text from image**. Langkah ini adalah inti tutorial—di sinilah keajaiban OCR sebenarnya terjadi.

```csharp
// Step 3: Create OCR engine and recognize text
using var ocrEngine = new OcrEngine();   // IDisposable, so we use 'using'
OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Mengapa kami menggunakan `using var`:** `OcrEngine` menyimpan sumber daya tidak terkelola (perpustakaan native). Membungkusnya dalam blok `using` menjamin pembuangan yang tepat, mencegah kebocoran memori—terutama penting dalam layanan yang berjalan lama.

> **Apa yang Anda dapatkan kembali:** `ocrResult` berisi teks mentah, skor kepercayaan, dan informasi tata letak (baris, kata, kotak pembatas). Untuk sebagian besar alur pemrosesan faktur, properti `Text` sudah cukup, tetapi metadata tambahan dapat membantu dalam validasi atau debugging visual.

## Langkah 4: Konversi Hasil ke JSON Berformat Cantik

Aspose.OCR memudahkan **write JSON to file** karena `OcrResult` menyediakan metode `ToJson`. Dengan memberikan `indent: true` kita mendapatkan output yang dapat dibaca manusia, yang berguna ketika Anda perlu **extract text from invoice** catatan nanti.

```csharp
// Step 4: Serialize OCR result to JSON
string json = ocrResult.ToJson(indent: true);
```

> **Contoh potongan JSON** (truncated for brevity):

```json
{
  "Text": "Invoice #12345\nDate: 2026-06-01\nTotal: $1,250.00",
  "Confidence": 0.97,
  "Regions": [...]
}
```

> **Catatan kasus tepi:** Jika mesin OCR gagal mendeteksi teks apa pun, `ocrResult.Text` akan menjadi string kosong, tetapi JSON tetap akan berisi metadata seperti dimensi gambar. Anda dapat melindungi terhadap hasil kosong sebelum menulis file.

## Langkah 5: Tulis JSON ke File

Sekarang akhirnya **write JSON to file**. Menggunakan `File.WriteAllText` memastikan seluruh string ditulis ke disk dalam satu operasi atomik.

```csharp
// Step 5: Save JSON output
string jsonPath = @"YOUR_DIRECTORY\invoice.json";
File.WriteAllText(jsonPath, json);
Console.WriteLine($"JSON saved to {jsonPath}");
```

> **Tips untuk produksi:** Pertimbangkan menambahkan timestamp ke nama file (`invoice_20260628_1500.json`) untuk menghindari menimpa hasil sebelumnya. Juga, bungkus operasi penulisan dalam blok try/catch untuk menangani masalah izin dengan elegan.

## Langkah 6: Contoh Lengkap yang Berfungsi

Menggabungkan semua bagian, berikut program lengkap yang dapat Anda kompilasi dan jalankan segera. Ganti `YOUR_DIRECTORY` dengan folder yang berisi `invoice.png`.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        string imagePath = @"YOUR_DIRECTORY\invoice.png";
        OcrImage image = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR and recognize text from image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 4: Convert the recognition result to pretty‑printed JSON
        string json = ocrResult.ToJson(indent: true);

        // Step 5: Write JSON to file
        string jsonPath = @"YOUR_DIRECTORY\invoice.json";
        File.WriteAllText(jsonPath, json);

        // Step 6: Inform the user
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

**Output yang diharapkan** saat Anda menjalankan program:

```
JSON saved to C:\Invoices\invoice.json
```

Buka `invoice.json` dan Anda akan melihat representasi data OCR yang diformat dengan rapi, siap untuk parsing atau penyimpanan selanjutnya.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika gambar berisi banyak bahasa?

Aspose.OCR secara otomatis mendeteksi bahasa berdasarkan set karakter. Jika Anda perlu memaksa bahasa tertentu (misalnya, English untuk kebanyakan faktur), atur properti `Language` pada mesin:

```csharp
ocrEngine.Language = OcrLanguage.English;
```

### Bagaimana cara menangani PDF besar dengan banyak halaman?

Konversi setiap halaman menjadi gambar terlebih dahulu (menggunakan perpustakaan PDF‑to‑image) lalu lakukan loop melalui gambar-gambar, menerapkan rutinitas **perform OCR on image** yang sama. Gabungkan hasil JSON ke dalam satu array jika Anda menginginkan output yang terintegrasi.

### Bisakah saya streaming JSON alih-alih menulis seluruh file?

Ya. Jika Anda membangun API web, Anda dapat mengembalikan `json` langsung sebagai body respons:

```csharp
return Results.Json(ocrResult);
```

### Bagaimana dengan performa?

Mesin OCR berjalan secara sinkron dalam contoh di atas. Untuk skenario throughput tinggi, bungkus panggilan pengenalan dalam `Task.Run` atau gunakan versi asynchronous (jika tersedia) untuk menjaga UI tetap responsif atau memparalelkan pemrosesan batch.

## Kesimpulan

Kami telah memandu solusi singkat, end‑to‑end yang **perform OCR on image** file, **recognize text from image**, **extract text from invoice**, dan akhirnya **write JSON to file** menggunakan Aspose.OCR di C#. Kode ini sengaja dibuat sederhana sehingga Anda dapat menyesuaikannya ke alur kerja yang lebih kompleks—baik itu menambahkan pra‑pemrosesan gambar, memasukkan JSON ke dalam basis data, atau mengekspos hasil melalui endpoint REST.

Siap untuk langkah berikutnya? Cobalah mengganti PNG dengan JPEG, bereksperimen dengan pengaturan OCR yang berbeda (seperti `ocrEngine.Dpi`), atau integrasikan langkah konversi PDF‑to‑image untuk menangani seluruh bundel faktur. Langit adalah batasnya setelah Anda menguasai dasar‑dasarnya.

Selamat coding, semoga hasil OCR Anda selalu tajam dan akurat!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menggunakan Aspose OCR untuk Hasil JSON dalam Pengenalan Gambar](/ocr/english/net/text-recognition/get-result-as-json/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar – Kenali Garis dengan Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}