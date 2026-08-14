---
category: general
date: 2026-02-20
description: Tutorial OCR C# yang menunjukkan cara mengekstrak teks dari gambar, mengenali
  teks dari PNG, dan mengubah gambar menjadi teks hanya dengan beberapa baris kode.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to text
- how to extract text
language: id
og_description: Tutorial c# OCR yang memandu Anda melalui proses mengekstrak teks
  dari file gambar, mengenali teks dari PNG, dan mengonversi gambar menjadi teks menggunakan
  Aspose.OCR.
og_title: Tutorial OCR C# – Panduan Cepat untuk Mengekstrak Teks dari Gambar
tags:
- OCR
- C#
- Aspose
title: Tutorial OCR c# – Ekstrak Teks dari Gambar dengan Aspose.OCR
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Ekstrak Teks dari Gambar dengan Aspose.OCR

Pernah membutuhkan **c# ocr tutorial** yang benar‑benar bekerja pada file PNG nyata? Anda bukan satu‑satunya. Dalam banyak proyek—seperti pemindaian faktur, pengarsipan kwitansi, atau parsing screenshot sederhana—para pengembang menemui kebuntuan ketika mereka mencoba **extract text from image** file tanpa perpustakaan yang dapat diandalkan.  

Kabar baiknya, Aspose.OCR membuat seluruh proses menjadi sangat mudah. Dalam panduan ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan **how to extract text** dari PNG, menjelaskan *mengapa* setiap baris penting, dan bahkan menyentuh kasus‑tepi seperti lisensi dan pra‑pemrosesan gambar. Pada akhir tutorial Anda akan dapat **recognize text from png** file dan **convert image to text** hanya dengan beberapa pernyataan C#.

## Apa yang Dibahas dalam Tutorial Ini

- Menyiapkan engine Aspose.OCR dalam aplikasi konsol .NET.  
- Memuat PNG (atau bitmap yang didukung) dari disk.  
- Menjalankan OCR dan mencetak hasilnya ke konsol.  
- Lisensi opsional, penanganan error, dan tips kinerja.  

Tidak ada layanan eksternal, tidak ada sihir tersembunyi—hanya kode C# murni yang dapat Anda copy‑paste dan jalankan. Jika Anda pernah bertanya‑tanya **how to extract text** dari dokumen yang dipindai, tetap di sini; kami akan menjawab itu serta beberapa pertanyaan “what if” di sepanjang jalan.

## Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode juga berfungsi pada .NET Framework 4.7+).  
- Visual Studio 2022 (atau editor apa pun yang Anda suka).  
- Paket NuGet Aspose.OCR for .NET gratis atau berbayar.  
- File gambar bernama `sample.png` ditempatkan di folder yang dapat Anda referensikan.  

Itu saja—tidak diperlukan alat pihak ketiga lainnya.

## c# OCR Tutorial: Menyiapkan Aspose.OCR

Pertama-tama: Anda memerlukan pustaka Aspose.OCR. Buka terminal Anda di folder proyek dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Ini akan mengunduh build stabil terbaru dan menambahkan referensi DLL yang diperlukan. Jika Anda memiliki file lisensi (`Aspose.OCR.lic`), siapkan; jika tidak, versi percobaan gratis akan berfungsi, namun dengan watermark pada hasil OCR.

### Mengapa Lisensi Penting

Tanpa lisensi, engine berjalan dalam mode evaluasi, yang menyisipkan baris “Powered by Aspose” ke dalam output untuk beberapa bahasa. Untuk kode produksi, Anda harus memanggil `SetLicense` lebih awal, seperti yang ditunjukkan pada kode di bawah. Itu hanya satu baris panggilan, namun menghapus watermark dan membuka pemrosesan berkecepatan penuh.

## Ekstrak Teks dari Gambar Menggunakan Aspose.OCR

Sekarang mari kita selami kode OCR sebenarnya. Di bawah ini adalah program **complete, self‑contained** yang dapat Anda kompilasi dan jalankan segera.

```csharp
using System;
using System.Drawing;          // Needed for Image class
using Aspose.OCR;               // Core OCR namespace
using Aspose.OCR.Models;       // For OCR settings (optional)

class LicenseCheck
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2 (Optional): Apply your Aspose.OCR license
        // -------------------------------------------------
        // Uncomment and set the correct path if you have a license file.
        // ocrEngine.SetLicense(@"C:\MyLicenses\Aspose.OCR.lic");

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        // You can use any supported format (png, jpg, bmp, tiff, etc.)
        string imagePath = @"C:\Images\sample.png";
        Image inputImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // Step 4: Recognize text from the loaded image
        // -------------------------------------------------
        // The Recognize method returns a plain string.
        string recognizedText = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Apa yang terjadi di sini?**  

1. **Engine creation** – `OcrEngine` adalah titik masuk utama; ia memuat data bahasa secara internal.  
2. **License loading** – opsional namun disarankan; Anda cukup menunjuk ke file `.lic` Anda.  
3. **Image loading** – `Image.FromFile` bekerja untuk format bitmap apa pun; kami menggunakan PNG karena mempertahankan kualitas lossless, yang penting untuk akurasi OCR.  
4. **Recognition** – `ocrEngine.Recognize` melakukan semua pekerjaan berat, mengembalikan string yang berisi karakter yang terdeteksi.  
5. **Output** – kami menulis hasil ke konsol, tetapi Anda dapat dengan mudah mengirimnya ke file, basis data, atau kontrol UI.

### Output yang Diharapkan

Jika `sample.png` berisi teks “Hello World”, konsol akan menampilkan:

```
=== OCR Result ===
Hello World
```

Jika gambar kabur atau berisi karakter non‑Latin, output mungkin berisi simbol yang rusak. Di sinilah pra‑pemrosesan (penyesuaian kontras, binarisasi) berperan—dibahas pada bagian berikutnya.

## Recognize Text from PNG Files – Tips & Trik

PNG adalah format populer karena menyimpan piksel tanpa artefak kompresi. Namun, tidak semua PNG dibuat sama. Berikut beberapa tips praktis yang mungkin berguna:

- **Resolution matters** – Targetkan setidaknya 300 dpi. Apa pun yang lebih rendah dapat menyebabkan karakter terlewat.  
- **Color vs. Grayscale** – Mengonversi PNG berwarna ke grayscale sebelum OCR dapat meningkatkan kecepatan tanpa mengurangi akurasi.  
- **Noise removal** – Bintik‑bintik kecil sering membingungkan engine; filter median sederhana dapat membantu.

Di bawah ini cuplikan cepat yang menunjukkan cara pra‑memproses gambar sebelum memberikannya ke Aspose.OCR:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
Bitmap grayBitmap = new Bitmap(inputImage.Width, inputImage.Height);
using (Graphics g = Graphics.FromImage(grayBitmap))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}});
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(inputImage, new Rectangle(0,0,grayBitmap.Width,grayBitmap.Height),
                0,0,inputImage.Width,inputImage.Height, GraphicsUnit.Pixel, attributes);
}

// Optional: Apply a simple binary threshold
Bitmap binBitmap = new Bitmap(grayBitmap.Width, grayBitmap.Height);
for (int y = 0; y < grayBitmap.Height; y++)
{
    for (int x = 0; x < grayBitmap.Width; x++)
    {
        Color pixel = grayBitmap.GetPixel(x, y);
        int bw = pixel.R < 128 ? 0 : 255; // threshold at 128
        binBitmap.SetPixel(x, y, Color.FromArgb(bw, bw, bw));
    }
}

// Now run OCR on the cleaned bitmap
string cleanedText = ocrEngine.Recognize(binBitmap);
Console.WriteLine(cleanedText);
```

**Pro tip:** Jika Anda memproses puluhan gambar, buat satu instance `OcrEngine` dan gunakan kembali. Membuat engine baru per gambar menambah beban yang tidak perlu.

## Convert Image to Text – Opsi Lanjutan

Aspose.OCR tidak terbatas pada ekstraksi teks biasa. Anda dapat memintanya mengembalikan **structured data** (seperti kotak pembatas kata) atau mengatur **language hints** untuk meningkatkan akurasi pada dokumen multibahasa.

```csharp
// Set language to English + Spanish (ISO codes)
ocrEngine.Language = Language.English | Language.Spanish;

// Request detailed OCR result
OcrResult result = ocrEngine.RecognizeImage(inputImage, OcrOptions.DetectTextBlocks);

// Iterate over detected words
foreach (var word in result.Words)
{
    Console.WriteLine($"{word.Text} (x:{word.Bounds.X}, y:{word.Bounds.Y})");
}
```

Objek `OcrResult` memberikan koordinat setiap kata, yang berguna untuk menyorot teks dalam UI atau untuk pasca‑pemrosesan (mis., menyensor informasi sensitif).

## Cara Mengekstrak Teks dalam Skenario Dunia‑Nyata

Mari kita bahas beberapa pertanyaan “what if” yang sering muncul di lingkungan produksi.

### Bagaimana jika gambar adalah halaman PDF?

Aspose.OCR dapat membaca PDF secara langsung, tetapi Anda memerlukan pustaka Aspose.PDF untuk meraster setiap halaman menjadi gambar terlebih dahulu. Alur kerjanya:

1. Muat PDF dengan `Aspose.Pdf.Document`.  
2. Konversi halaman menjadi bitmap (`PdfConverter`).  
3. Berikan bitmap ke `OcrEngine.Recognize`.

### Bagaimana jika hasil OCR berisi karakter sampah?

Penyebab umum adalah resolusi rendah, noise berlebih, atau font yang tidak didukung. Coba:

- Membesarkan gambar (`Bitmap` resizing).  
- Menerapkan filter penajaman.  
- Menentukan bahasa yang tepat (seperti yang ditunjukkan di atas).

### Bagaimana jika saya perlu memproses gambar secara paralel?

Karena `OcrEngine` tidak thread‑safe, buat **instance terpisah per thread** atau gunakan pool thread‑local. Contoh dengan `Parallel.ForEach`:

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine(); // each thread gets its own engine
    var img = Image.FromFile(path);
    string text = engine.Recognize(img);
    // Store or log 'text' as needed
});
```

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut versi ringkas yang dapat Anda masukkan ke dalam proyek konsol baru:

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialize OCR engine (single instance for this demo)
        OcrEngine engine = new OcrEngine();

        // Uncomment if you have a license file
        // engine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Path to the PNG you want to read
        string file = @"C:\Images\sample.png";

        // Load, optionally preprocess, then recognize
        using (Image img = Image.FromFile(file))
        {
            string text = engine.Recognize(img);
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(text);
        }
    }
}
```

Kompilasi dengan `dotnet run` dan lihat konsol mencetak teks yang diekstrak. Sederhana, kan? Itulah keindahan dari sebuah well‑des

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}