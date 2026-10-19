---
category: general
date: 2026-04-26
description: Ekstrak teks dari gambar di C# menggunakan Aspose.OCR dan pelajari cara
  mengonversi gambar ke format JSON dan XML dalam hitungan menit.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: id
og_description: Ekstrak teks dari gambar di C# dengan Aspose.OCR. Pelajari langkah
  demi langkah cara mengonversi hasilnya ke JSON dan XML secara instan.
og_title: Ekstrak teks dari gambar di C# – Konversi ke JSON & XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Ekstrak teks dari gambar di C# – Konversi ke JSON & XML
url: /id/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak teks dari gambar dalam C# – Konversi ke JSON & XML

Pernah membutuhkan untuk **mengekstrak teks dari gambar** dalam proyek .NET tetapi merasa terhambat pada “bagaimana cara saya benar‑benar mendapatkan data tersebut?” Anda tidak sendirian. Dalam banyak aplikasi dunia nyata—seperti pemrosesan faktur, pemindaian struk, atau verifikasi lencana—mengambil karakter mentah dari sebuah gambar adalah langkah pertama yang krusial.  

Berita baik? Dengan Aspose.OCR Anda dapat melakukannya dalam beberapa baris kode, lalu langsung **mengonversi gambar ke JSON** atau **mengonversi gambar ke XML** untuk sistem hilir. Dalam panduan ini kami akan menelusuri kode lengkap yang siap dijalankan, menjelaskan mengapa setiap bagian penting, dan menunjukkan beberapa trik untuk menghindari jebakan umum.

---

## Apa yang Anda Butuhkan

- **.NET 6+** (setiap SDK terbaru dapat digunakan; contoh ini menargetkan .NET 6)
- **Aspose.OCR for .NET** paket NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- File gambar (PNG, JPG, dll.) yang berisi teks yang dapat dicetak; kami akan menggunakan `invoice.png` sebagai contoh.
- Editor kode—Visual Studio, VS Code, atau Rider—sesuai preferensi Anda.

Itu saja. Tidak ada mesin OCR tambahan, tidak ada layanan eksternal, hanya satu paket NuGet.

---

## Langkah 1: Siapkan OCR Engine – Cara mengekstrak teks dari gambar

Pertama kita membuat instance `OcrEngine` dan menunjukannya ke file gambar. Langkah ini adalah fondasi; tanpa gambar yang dimuat dengan benar, engine tidak dapat mengenali apa pun.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Mengapa ini penting:**  
- `OcrEngine` mengenkapsulasi semua pra‑pemrosesan gambar tingkat rendah (binarisasi, deskewing).  
- Memuat gambar melalui `ImageStream.FromFile` memastikan engine membaca byte yang tepat, mempertahankan DPI dan kedalaman warna—keduanya dapat memengaruhi akurasi pengenalan.  

> **Pro tip:** Jika gambar sumber Anda berada dalam stream (mis., diunggah melalui web API), gunakan `ImageStream.FromStream(yourStream)` alih‑alih `FromFile`.

---

## Langkah 2: Beri tahu Engine Bahasa yang Diharapkan – ekstrak teks dari gambar secara akurat

Aspose.OCR mendukung banyak alfabet. Menentukan bahasa yang tepat mempersempit set karakter dan meningkatkan akurasi.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Mengapa:**  
Ketika Anda mengatur `Language.Latin`, OCR engine mengabaikan glyph Cyrillic atau Asia, mengurangi false positive. Jika kemudian Anda perlu menangani dokumen multi‑bahasa, Anda dapat beralih ke `Language.Multilingual` atau menggabungkan bahasa.

---

## Langkah 3: Jalankan Proses Pengenalan – ekstrak teks dari gambar dalam satu panggilan

Sekarang kita benar‑benar mengenali teks. Metode `Recognize` mengembalikan objek `RecognitionResult` yang berisi teks mentah, skor kepercayaan, dan bahkan data tata letak.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Mengapa:**  
Memanggil `Recognize` sekali sudah cukup karena engine secara internal melakukan pra‑pemrosesan, segmentasi, dan klasifikasi karakter. Properti `Text` memberikan representasi string biasa, sempurna untuk logging atau validasi cepat.

---

## Langkah 4: Konversi Hasil ke JSON – konversi gambar ke json dengan mudah

Banyak layanan modern lebih menyukai payload JSON. Aspose.OCR menyediakan metode `ToJson` yang nyaman untuk menyerialisasi seluruh `RecognitionResult`, termasuk nilai kepercayaan dan kotak pembatas.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Mengapa Anda mungkin menginginkan JSON:**  
- **Interoperability:** Aplikasi front‑end (React, Angular) dapat langsung mengonsumsi JSON.  
- **Debugging:** JSON mencakup kepercayaan per‑karakter, memungkinkan Anda menandai kata dengan kepercayaan rendah untuk peninjauan manual.  

> **Edge case:** Jika sistem hilir Anda hanya membutuhkan teks biasa, Anda dapat mengekstrak `recognitionResult.Text` dan membungkusnya dalam objek JSON khusus alih‑alih payload Aspose lengkap.

---

## Langkah 5: Konversi Hasil ke XML – konversi gambar ke xml untuk sistem legacy

Beberapa perusahaan masih mengandalkan skema XML untuk pertukaran data. Metode `ToXml` meniru `ToJson` tetapi menghasilkan XML.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Mengapa XML:**  
- **Schema validation:** Anda dapat mendefinisikan XSD yang cocok dengan struktur yang dihasilkan Aspose, menjamin kepatuhan kontrak.  
- **Integration:** ERP atau sistem manajemen dokumen lama seringkali dapat langsung mem‑parse XML.

---

## Contoh Lengkap yang Berfungsi – Kode Semua dalam Satu Tempat

Berikut adalah program lengkap yang menggabungkan semuanya. Salin‑tempel ke dalam proyek konsol baru (`dotnet new console`) dan jalankan.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Output yang diharapkan (console):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

File JSON dan XML akan berisi struktur yang lebih kaya, misalnya:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## Pertanyaan Umum & Kasus Edge

### Bagaimana jika gambar buram atau diputar?

Aspose.OCR secara otomatis melakukan deskew pada kebanyakan gambar, tetapi untuk kasus ekstrem Anda mungkin ingin pra‑memproses dengan `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. Menambahkan sedikit peningkatan kontras (`ImageProcessor.AdjustContrast`) juga dapat meningkatkan skor kepercayaan.

### Bisakah saya mengekstrak teks dari PDF?

Ya—konversi setiap halaman PDF menjadi gambar terlebih dahulu (mis., menggunakan Aspose.PDF atau perpustakaan gratis seperti PDFium) lalu masukkan gambar‑gambar tersebut ke dalam alur OCR yang sama.

### Bagaimana cara menangani banyak bahasa dalam satu dokumen?

Atur `ocrEngine.Language = Language.Multilingual;` atau gabungkan bahasa‑bahasa tertentu:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Sadari bahwa set bahasa yang lebih luas dapat

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}