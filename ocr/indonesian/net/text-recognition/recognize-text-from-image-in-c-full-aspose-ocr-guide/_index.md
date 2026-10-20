---
category: general
date: 2026-04-03
description: Mengenali teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  memuat gambar untuk OCR, mengekstrak teks dari gambar, menulis file JSON di C#,
  dan melakukan OCR pada PNG.
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: id
og_description: Mengenali teks dari gambar dengan Aspose OCR di C#. Panduan langkah
  demi langkah untuk memuat gambar untuk OCR, mengekstrak teks dari gambar, menulis
  file JSON di C#, dan melakukan OCR pada PNG.
og_title: Mengenali teks dari gambar di C# – Tutorial Lengkap Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Mengenali teks dari gambar di C# – Panduan Lengkap Aspose OCR
url: /id/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar dalam C# – Tutorial Lengkap Aspose OCR

Pernah membutuhkan untuk **mengenali teks dari gambar** tetapi tidak yakin library mana yang harus dipilih? Mungkin Anda memiliki sekumpulan kwitansi yang dipindai, tangkapan layar PNG, atau catatan tulisan tangan yang ingin diubah menjadi data yang dapat dicari. Kabar baiknya: dengan Aspose.OCR Anda dapat melakukannya dalam beberapa baris kode C#, dan Anda bahkan akan mendapatkan file JSON yang rapi yang dapat Anda masukkan ke sistem lain.

Dalam tutorial ini kami akan membahas cara memuat gambar untuk OCR, mengekstrak teks dari gambar, menyerialisasi hasil ke file JSON, dan akhirnya menangani file PNG tanpa kesulitan. Pada akhir tutorial Anda akan memiliki aplikasi console yang siap dijalankan yang **mengenali teks dari gambar** dan menulis output ke *output.json*.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework)
- Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- PNG (atau format lain yang didukung) yang ingin Anda proses
- Visual Studio, VS Code, atau editor C# apa pun yang Anda sukai

Tidak diperlukan pustaka pihak ketiga tambahan—hanya mesin Aspose OCR dan serializer bawaan `System.Text.Json`.

## Langkah 1: Mengenali teks dari gambar menggunakan Aspose OCR

Hal pertama yang harus Anda lakukan adalah membuat instance `OcrEngine`. Objek ini melakukan pekerjaan berat di belakang layar.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**Mengapa ini penting:** Menginstansiasi `OcrEngine` sekali dan menggunakannya kembali lebih efisien daripada membuat mesin baru untuk setiap file. Pemanggilan `RecognizeToResult` mengembalikan objek `OcrResult` yang sudah berisi teks yang diekstrak, skor kepercayaan, dan kotak pembatas—sempurna untuk pemrosesan lanjutan.

## Langkah 2: Memuat gambar untuk OCR – menangani berbagai format

Aspose OCR dapat membaca PNG, JPEG, BMP, dan banyak format lainnya. Jika Anda menangani PNG yang mengandung transparansi, Anda mungkin ingin meratakannya terlebih dahulu untuk menghindari kekosongan yang tidak terduga.

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**Tips profesional:** Selalu pastikan bahwa dimensi gambar wajar (mis., lebar > 50 px). Gambar yang sangat kecil dapat menyebabkan mesin OCR melewatkan karakter, menghasilkan skor kepercayaan yang rendah.

## Langkah 3: Menulis file JSON C# – membuat output dapat dikonsumsi

Serializer `System.Text.Json` cepat dan bawaan, tetapi Anda dapat menggantinya dengan `Newtonsoft.Json` jika memerlukan konverter khusus. Contoh di atas sudah menggunakan `WriteIndented = true` sehingga file yang dihasilkan dapat dibaca manusia.

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

Menyimpan data OCR dalam format JSON memudahkan Anda mengimpornya ke basis data, mengirimnya melalui HTTP, atau memasukkannya ke pipeline pembelajaran mesin.

## Langkah 4: Memverifikasi hasil – pemeriksaan cepat

Setelah program dijalankan, buka `output.json` dan cari field `"Text"`. Jika berisi string yang diharapkan, Anda telah berhasil **mengekstrak teks dari gambar**. Jika kepercayaan rendah, pertimbangkan pra‑pemrosesan gambar (mis., meningkatkan kontras atau menerapkan ambang biner).

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

Menjalankan console akan mencetak sesuatu seperti:

```
Extracted text: Hello World
Overall confidence: 98.00%
```

Itu merupakan tanda kuat bahwa OCR berfungsi sesuai yang diharapkan.

## Kesalahan Umum & Kasus Tepi

| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **Output kosong** | Gambar terlalu gelap atau memiliki ruang warna yang tidak didukung | Konversi ke skala abu‑abu, tingkatkan kecerahan, atau ratakan PNG (lihat Langkah 2) |
| **Karakter sampah** | DPI rendah (< 72) atau noise berat | Perbesar gambar atau terapkan filter penghilang noise sebelum mengirim ke `RecognizeToResult` |
| **File besar menyebabkan tekanan memori** | Memuat PNG multi‑megapiksel ke dalam `Bitmap` mengonsumsi RAM | Proses gambar dalam potongan atau perkecil ukurannya sambil mempertahankan keterbacaan |
| **Kesalahan serialisasi JSON** | `OcrResult` mengandung referensi melingkar (tidak mungkin) | Gunakan `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## Bonus: Melakukan OCR pada PNG dalam loop batch

Jika Anda memiliki folder berisi file PNG, Anda dapat memperluas demo untuk mengiterasi mereka:

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

Sekarang program **melakukan OCR pada PNG** secara massal, menulis file JSON yang cocok untuk setiap gambar.

## Kesimpulan

Anda baru saja belajar cara **mengenali teks dari gambar** dalam C# dengan Aspose OCR, **memuat gambar untuk OCR**, **mengekstrak teks dari gambar**, dan **menulis file JSON C#** untuk menyimpan hasilnya. Contoh lengkap yang dapat dijalankan mencakup langkah‑langkah penting, menjelaskan mengapa setiap bagian penting, dan bahkan menunjukkan cara menangani keanehan khusus PNG.

Langkah selanjutnya? Coba masukkan JSON ke dalam indeks pencarian, gabungkan dengan deteksi bahasa, atau integrasikan ke dalam API web yang memproses unggahan secara langsung. Anda juga dapat menjelajahi dukungan Aspose untuk pengenalan tulisan tangan jika kasus penggunaan Anda memerlukannya.

Ada pertanyaan tentang kasus tepi atau penyetelan kinerja? Tinggalkan komentar di bawah—selamat coding! 

![demo mengenali teks dari gambar](/images/ocr-demo.png "Diagram yang menunjukkan bagaimana Aspose OCR mengenali teks dari gambar")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}