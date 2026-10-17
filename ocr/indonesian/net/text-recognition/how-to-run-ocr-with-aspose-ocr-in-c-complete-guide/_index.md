---
category: general
date: 2026-02-28
description: cara menjalankan OCR di C# menggunakan Aspose OCR – pelajari cara mengekstrak
  teks dari gambar, mengonversi gambar ke JSON atau XML dalam beberapa langkah saja.
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: id
og_description: cara menjalankan OCR di C# menggunakan Aspose OCR – temukan cara mengekstrak
  teks dari gambar dan mengonversi gambar ke JSON atau XML dengan contoh siap pakai.
og_title: cara menjalankan OCR dengan Aspose OCR di C# – Panduan Lengkap
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cara Menjalankan OCR dengan Aspose OCR di C# – Panduan Lengkap
url: /id/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara menjalankan OCR dengan Aspose OCR di C# – Panduan Lengkap

Jika Anda bertanya-tanya **cara menjalankan OCR** pada gambar struk menggunakan C#, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan membahas **mengekstrak teks dari gambar** dan kemudian **mengonversi gambar ke JSON** atau **mengonversi gambar ke XML** dengan Aspose OCR—semua dalam satu program yang berdiri sendiri.

Bayangkan Anda sedang membangun aplikasi pelacakan pengeluaran dan perlu mengambil item baris dari struk yang difoto. Mengetik setiap entri secara manual memang merepotkan, bukan? Pada akhir panduan ini Anda akan memiliki potongan kode yang dapat digunakan kembali untuk membaca gambar apa pun, mengembalikan teks terstruktur, dan memberikan representasi JSON serta XML yang siap diproses lebih lanjut.

## Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode ini juga berfungsi pada .NET Framework 4.8)
- Visual Studio 2022 (atau editor apa pun yang Anda sukai)
- Paket NuGet **Aspose.OCR** yang aktif (`Install-Package Aspose.OCR`)
- Contoh gambar (misalnya `receipt.png`) yang ditempatkan di folder yang dapat Anda referensikan

Tidak ada konfigurasi tambahan yang diperlukan; pustaka ini sudah menyertakan semua model OCR yang diperlukan.

![Gambar struk untuk pemrosesan OCR – cara menjalankan OCR](receipt.png)

> *Teks alternatif: Gambar struk untuk pemrosesan OCR – cara menjalankan OCR*

## Implementasi Langkah‑per‑Langkah

Di bawah ini kami membagi solusi menjadi bagian‑bagian logis. Setiap langkah menjelaskan **mengapa** kami melakukannya, bukan hanya **apa** yang terlihat pada kode.

### 1️⃣ Inisialisasi OCR Engine – fondasi dari **cara menjalankan OCR**

Kelas `OcrEngine` adalah titik masuk. Membuat instance-nya memuat model bahasa internal dan menyiapkan mesin untuk pengenalan.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **Pro tip:** Menggunakan kembali `OcrEngine` yang sama untuk beberapa gambar mengurangi beban memori dan mempercepat pemrosesan batch.

### 2️⃣ Memuat Gambar – inti dari **mengekstrak teks dari gambar**

Aspose OCR bekerja dengan pembungkus `Image` miliknya. Menggunakan pernyataan `using` memastikan handle file dilepaskan dengan cepat.

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

Jika gambar berada dalam format berbeda (BMP, TIFF, PDF), metode `Load` yang sama dapat menanganinya—tanpa konversi tambahan.

### 3️⃣ Jalankan Pengenalan OCR – inti dari **cara menjalankan OCR**

Memanggil `Recognize` melakukan pekerjaan berat: analisis tata letak, segmentasi karakter, dan klasifikasi spesifik bahasa.

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

`OcrResult` yang dikembalikan berisi teks mentah, skor kepercayaan, dan pohon tata letak terperinci yang dapat diserialisasi.

### 4️⃣ Mengonversi Gambar ke JSON – cara langsung untuk **mengonversi gambar ke json**

JSON sangat cocok untuk API web atau penyimpanan NoSQL. Metode `ToJson` memberikan string yang diformat rapi, memudahkan proses debugging.

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

Output JSON tipikal terlihat seperti ini (dipotong untuk singkat):

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

Anda kini dapat mengirim JSON ini langsung ke endpoint REST atau menyimpannya di Azure Cosmos DB.

### 5️⃣ Mengonversi Gambar ke XML – ketika **mengonversi gambar ke xml** diperlukan

Beberapa sistem warisan masih menggunakan XML. Aspose menyediakan `ToXml` untuk representasi yang bersih dan kompatibel dengan skema.

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

Contoh potongan XML:

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

Kedua format mempertahankan data hierarkis yang sama, sehingga Anda dapat memilih mana yang paling cocok untuk alur kerja downstream Anda.

## Kesalahan Umum & Cara Mengekstrak Teks dengan Andal

Bahkan dengan pustaka yang kuat, gambar dunia nyata dapat menimbulkan tantangan. Berikut tiga masalah yang mungkin Anda temui beserta solusinya.

### 📏 Gambar Resolusi Rendah

**Mengapa penting:** Font kecil dapat menyatu, menurunkan skor kepercayaan.  
**Solusi:** Pra‑proses gambar—perbesar dengan `Image.Resize` atau terapkan filter penajaman sebelum memanggil `Recognize`.

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 Kontras Buruk

**Mengapa penting:** Teks terang pada latar belakang gelap membingungkan algoritma segmentasi.  
**Solusi:** Inversi warna atau sesuaikan kecerahan/kontras melalui `Image.AdjustBrightnessContrast`.

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 Dokumen Multi‑Bahasa

**Mengapa penting:** Model bahasa default adalah Bahasa Inggris; bahasa campuran menghasilkan output yang berantakan.  
**Solusi:** Setel `ocrEngine.Language = OcrLanguage.Multilingual;` sebelum melakukan pengenalan.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

Menangani kasus tepi ini memastikan bahwa **cara mengekstrak teks** dari gambar apa pun menjadi rutinitas yang dapat diandalkan, bukan sekadar tebak‑tebakan.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah program lengkap, siap untuk dikompilasi dan dijalankan. Cukup ganti `YOUR_DIRECTORY` dengan path ke gambar Anda dan tekan F5.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**Output konsol yang diharapkan** (diformat untuk keterbacaan) menampilkan struktur JSON dan XML yang berisi teks yang diekstrak serta kotak pembatas.

## Ringkasan – Apa yang Telah Dibahas

- **cara menjalankan OCR** dengan Aspose OCR di C#
- Proses langkah‑per‑langkah untuk **mengekstrak teks dari gambar**
- Dua opsi serialisasi: **mengonversi gambar ke json** dan **mengonversi gambar ke xml**
- Tips menangani gambar resolusi rendah, kontras rendah, dan skenario multi‑bahasa
- Contoh kode lengkap yang siap disalin‑tempel yang dapat Anda masukkan ke proyek .NET mana pun

## Apa Selanjutnya?

Sekarang Anda dapat **mengekstrak teks** dan mendapatkan data terstruktur, pertimbangkan ide‑ide lanjutan berikut:

- Kirim JSON ke Azure Function yang menyimpan struk di Cosmos DB.
- Gunakan output XML untuk mengisi sistem akuntansi berbasis SOAP yang sudah ada.
- Gabungkan Aspose OCR dengan model machine‑learning untuk mengkategorikan tipe pengeluaran secara otomatis.

Silakan bereksperimen—ganti `receipt.png` dengan faktur, kartu nama, atau catatan tulisan tangan. Pola yang sama bekerja di seluruh

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}