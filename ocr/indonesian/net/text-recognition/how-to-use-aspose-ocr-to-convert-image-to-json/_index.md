---
category: general
date: 2026-03-15
description: Cara menggunakan Aspose OCR untuk mengekstrak teks dari gambar dan mengonversi
  gambar ke JSON dalam C#. Pelajari cara mengenali teks dari PNG dan dapatkan output
  terstruktur dengan cepat.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: id
og_description: Cara menggunakan Aspose OCR untuk mengekstrak teks dari gambar dan
  mengonversi gambar ke JSON dalam C#. Panduan ini memandu Anda melalui proses mengenali
  teks dari PNG dan mendapatkan output terstruktur.
og_title: Cara Menggunakan Aspose OCR untuk Mengonversi Gambar ke JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Cara Menggunakan Aspose OCR untuk Mengonversi Gambar ke JSON
url: /id/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Aspose OCR untuk Mengonversi Gambar ke JSON

Cara menggunakan Aspose OCR adalah pertanyaan umum ketika pengembang perlu mengekstrak teks dari gambar. Jika Anda ingin **convert image to JSON** atau **recognize text from PNG**, panduan ini akan membantu Anda—tanpa basa‑basi, hanya solusi praktis end‑to‑end.

Dalam beberapa menit ke depan kami akan membahas semua yang Anda perlukan: menginstal pustaka, mengonfigurasi engine untuk output JSON, memuat PNG struk, menjalankan OCR, dan akhirnya menulis hasilnya ke file `.json`. Pada akhir tutorial Anda akan dapat **extract text from image** file dengan satu pemanggilan metode, dan Anda akan memahami mengapa setiap langkah penting.

> **Pro tip:** Aspose OCR bekerja dengan berbagai format gambar (PNG, JPEG, BMP, TIFF). Kode yang sama di bawah ini akan menangani semuanya, sehingga Anda tidak perlu menulis logika khusus format.

## Apa yang Anda Butuhkan

- .NET 6.0 atau yang lebih baru (kode ini juga berfungsi pada .NET Framework 4.6+)
- Paket NuGet Aspose.OCR yang valid (versi percobaan gratis atau berlisensi)
- File gambar yang ingin Anda proses (misalnya `receipt.png`)
- Visual Studio, VS Code, atau editor C# apa pun yang Anda sukai  

Itu saja—tanpa dependensi tambahan, tanpa layanan eksternal. Siap? Mari kita mulai.

![cara menggunakan mesin aspose OCR](image-placeholder.png "cara menggunakan mesin aspose OCR")

## Cara Menggunakan Aspose OCR – Mengonfigurasi Output JSON

Hal pertama yang harus Anda lakukan ketika **how to use aspose** untuk OCR adalah membuat instance `OcrEngine` dan memberitahukannya untuk menghasilkan JSON. Saklar konfigurasi kecil ini menyelamatkan Anda dari harus men-serialize hasil secara manual nanti.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Why this matters:** Menetapkan `OutputFormat` ke `Json` berarti engine OCR sudah menyusun teks ke dalam hierarki halaman, baris, dan kata. Anda tidak perlu mem-parsing string mentah nanti, yang membuat pemrosesan lanjutan—seperti memasukkan data ke basis data—jauh lebih bersih.

## Mengonversi Gambar ke JSON dengan Aspose OCR

Sekarang engine sudah dikonfigurasi, mari kita bahas bagian **convert image to JSON** secara lebih detail.

1. **Load the image** – `Image.FromFile` berfungsi untuk semua format yang didukung. Jika Anda menangani stream (misalnya file yang diunggah), Anda dapat menggunakan `Image.FromStream` sebagai gantinya.  
2. **Run `Recognize`** – metode ini mengembalikan objek `OcrResult`. Karena kami mengatur output ke JSON, `ocrResult.Text` sudah berisi string JSON.  
3. **Write the file** – `File.WriteAllText` adalah cara termudah untuk menyimpan JSON. Jika Anda perlu menyimpannya di bucket cloud, cukup ganti baris ini dengan pemanggilan SDK yang sesuai.

### Output JSON yang Diharapkan

Payload JSON tipikal terlihat seperti ini (dipangkas untuk singkat):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Anda sekarang dapat memasukkan struktur ini ke sistem downstream mana pun—baik itu alat pelaporan, model machine‑learning, atau file log sederhana.

## Ekstrak Teks dari Gambar Menggunakan Aspose OCR

Jika Anda hanya membutuhkan string mentah (misalnya, Anda tidak memerlukan JSON), cukup ubah format output kembali ke teks biasa:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**Kapan memilih teks biasa?**  
- Debug cepat atau output konsol.  
- Skenario di mana Anda akan menerapkan post‑processing khusus (misalnya ekstraksi regex).  

Namun ingat, **extract text from image** menggunakan JSON memberi Anda data posisi—berguna untuk menyorot teks di UI atau menyelaraskan dengan bidang formulir.

## Mengenali Teks dari File PNG

PNG adalah format lossless, yang sering menghasilkan akurasi OCR lebih baik dibandingkan JPEG yang sangat terkompresi. Berikut checklist cepat untuk memastikan Anda mendapatkan hasil terbaik saat **recognize text from PNG**:

| Item Checklist | Mengapa Membantu |
|----------------|-----------------|
| Gunakan DPI 300+ | Resolusi lebih tinggi memberi engine lebih banyak piksel untuk diproses. |
| Jaga gambar dalam skala abu‑abu | Mengurangi noise; Aspose OCR secara otomatis mengonversi, tetapi pra‑pemrosesan dapat mempercepat proses. |
| Hapus gangguan latar belakang | Latar belakang bersih meningkatkan skor kepercayaan. |

Jika Anda menemui skor kepercayaan rendah, coba tingkatkan DPI atau terapkan filter ambang sederhana sebelum memberi gambar ke Aspose.

## Cara Mengekstrak Hasil OCR Secara Programatis

Selain hanya menyimpan JSON, Anda mungkin ingin membaca bidang tertentu secara programatis—misalnya, total jumlah pada struk. Karena JSON berisi hierarki, Anda dapat mendeserialisasikannya ke objek C#:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Sekarang Anda dapat men-query `ocrData` dengan LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Why this works:** JSON sudah memberi tahu Anda di mana setiap kata berada di halaman, sehingga Anda dapat dengan andal menemukan bidang meskipun tata letak sedikit berubah.

## Kasus Tepi & Kesalahan Umum

- **Null Result:** Jika `ocrEngine.Recognize` mengembalikan `null`, gambar mungkin tidak didukung atau rusak. Selalu lindungi terhadap hal ini:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Large Files:** Untuk gambar multi‑megabyte, pertimbangkan streaming gambar atau mengubah ukurannya sebelum OCR untuk menghindari penggunaan memori berlebih.

- **License Issues:** Versi percobaan menambahkan watermark pada output. Pastikan Anda memuat lisensi Anda di awal program:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Non‑Latin Scripts:** Aspose OCR mendukung banyak bahasa, tetapi Anda harus mengatur properti `Language` sesuai (misalnya, `ocrEngine.Configuration.Language = Language.English;`).

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}