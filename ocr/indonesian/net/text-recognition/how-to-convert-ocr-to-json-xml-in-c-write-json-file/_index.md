---
category: general
date: 2026-04-01
description: Cara mengonversi output OCR ke JSON dan XML di C# – pelajari cara mengekstrak
  teks dari gambar dan menulis file JSON di C# menggunakan Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: id
og_description: Cara mengonversi hasil OCR menjadi file JSON dan XML terstruktur dengan
  C#. Panduan langkah demi langkah untuk mengekstrak teks dari gambar dan menulis
  file JSON C#.
og_title: Cara Mengonversi OCR ke JSON & XML dalam C# – Menulis File JSON
tags:
- OCR
- C#
- Aspose
title: Cara Mengonversi OCR ke JSON & XML di C# – Menulis File JSON
url: /id/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengonversi OCR ke JSON & XML di C# – Menulis File JSON

**Cara mengonversi OCR** menjadi sesuatu yang benar‑benar dapat Anda gunakan adalah pertanyaan yang sering diajukan oleh banyak pengembang. Dalam panduan ini kami akan menunjukkan cara mengekstrak teks dari gambar, mengubah output OCR menjadi JSON dan XML yang terformat rapi, lalu menulis file‑file tersebut ke disk dengan C#.

Jika Anda pernah menatap string OCR mentah dan berpikir, “Harusnya ada cara yang lebih baik untuk menyimpan ini,” Anda berada di tempat yang tepat. Pada akhir tutorial Anda akan memiliki program lengkap yang dapat dijalankan, yang tidak hanya **mengekstrak teks dari file gambar** tetapi juga tahu cara **menulis file JSON C#** dan **menulis file XML C#** tanpa kesulitan.

## Apa yang Anda Butuhkan

- **.NET 6.0** atau yang lebih baru (kode ini juga bekerja dengan .NET Framework 4.6+).  
- Paket NuGet **Aspose.OCR** – instal dengan `dotnet add package Aspose.OCR`.  
- Sebuah gambar yang berisi teks (misalnya `invoice.png`).  
- IDE apa saja yang Anda suka – Visual Studio, Rider, atau VS Code sudah cukup.

> **Tip pro:** Simpan file gambar Anda dalam folder khusus (misalnya `Resources/`) agar jalurnya tetap rapi.

## Langkah 1: Menyiapkan OCR Engine – Cara Mengonversi OCR

Pertama, kita buat instance `OcrEngine` dan beri tahu bahasa apa yang harus dicari. Dalam kebanyakan kasus bahasa Inggris sudah cukup, tetapi Anda dapat mengganti `Language.English` dengan bahasa lain yang didukung.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Mengapa ini penting:** Menginisialisasi engine dengan bahasa yang tepat secara signifikan meningkatkan akurasi, terutama untuk skrip non‑Latin.

## Langkah 2: Mengenali Teks – Ekstrak Teks dari Gambar

Sekarang kita beri gambar ke engine. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi teks mentah serta data lokasi.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Jika gambar tidak dapat ditemukan, `Recognize` akan melempar `FileNotFoundException`. Untuk menyederhanakan demo, kami mengasumsikan jalurnya benar, tetapi dalam produksi Anda sebaiknya membungkusnya dengan blok try‑catch.

## Langkah 3: Mengonversi Hasil ke JSON – Menulis File JSON C#

Aspose.OCR membuat serialisasi menjadi sangat mudah. Metode `ToJson` menerima flag `indent` untuk menghasilkan output yang terformat rapi, yang sangat cocok ketika Anda berencana membuka file di editor teks.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Contoh JSON yang Diharapkan

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **Cara mengekstrak teks:** Properti `Text` memberi Anda string polos yang dapat Anda kirim ke layanan lain (indeks pencarian, basis data, dll.).

## Langkah 4: Menyimpan JSON – Menulis File JSON C# (Lanjutan)

Setelah string JSON siap, kita cukup menulisnya ke file menggunakan `File.WriteAllText`. Ini secara default memastikan enkoding UTF‑8.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Sekarang Anda memiliki `invoice.json` yang berada di samping gambar, siap untuk diproses lebih lanjut.

## Langkah 5: Mengonversi Hasil ke XML – Menulis File XML C#

Jika Anda lebih suka XML untuk sistem warisan, metode `ToXml` melakukan pekerjaan berat. Seperti `ToJson`, ia juga mendukung pencetakan rapi.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Contoh XML yang Diharapkan

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Langkah 6: Menyimpan XML – Menulis File XML C# (Lanjutan)

Menyimpan XML sama persis dengan langkah JSON; cukup gunakan ekstensi `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Contoh Program Lengkap yang Berfungsi

Menggabungkan semua langkah, berikut program lengkap yang dapat Anda salin‑tempel ke aplikasi console:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Jalankan program, dan Anda akan menemukan dua file baru—`invoice.json` dan `invoice.xml`—di lokasi yang Anda tentukan. Buka file‑file tersebut untuk memverifikasi bahwa struktur sesuai dengan contoh di atas.

## Pertanyaan Umum & Kasus Tepi

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika gambar berisi banyak bahasa?** | Buat instance `OcrEngine` terpisah untuk tiap bahasa atau gunakan `Language.Multi` jika didukung. |
| **Bisakah saya mengontrol format output (mis., mengecualikan data wilayah)?** | Ya. Baik `ToJson` maupun `ToXml` menerima parameter opsional untuk memfilter bidang; lihat dokumentasi Aspose.OCR untuk `ExportOptions`. |
| **Bagaimana menangani PDF besar dengan banyak halaman?** | Proses setiap halaman secara terpisah, gabungkan hasilnya, lalu serialisasikan sekali. |
| **Apakah outputnya aman UTF‑8?** | Tentu—Aspose.OCR menggunakan Unicode secara internal, dan `File.WriteAllText` menulis UTF‑8 secara default. |
| **Bagaimana dengan performa?** | OCR memakan banyak CPU. Untuk pekerjaan batch pertimbangkan paralelisasi lintas core atau gunakan API cloud Aspose. |

## Kesimpulan

Anda kini tahu **cara mengonversi OCR** menjadi JSON dan XML menggunakan C#. Dengan mengikuti langkah‑langkah di atas Anda dapat **mengekstrak teks dari gambar**, lalu **menulis file JSON C#** dan **menulis file XML C#** hanya dengan beberapa baris kode. Pendekatan ini cepat, dapat diandalkan, dan bekerja dengan tipe gambar apa pun yang didukung Aspose.OCR.

Siap untuk tantangan berikutnya? Cobalah memberi masukan pada

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}