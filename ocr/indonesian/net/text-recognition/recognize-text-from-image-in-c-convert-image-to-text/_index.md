---
category: general
date: 2026-06-19
description: 'Mengenali teks dari gambar menggunakan Aspose OCR di C#: panduan langkah
  demi langkah untuk mengonversi gambar menjadi teks dan mengekstrak teks dari file
  JPG.'
draft: false
keywords:
- recognize text from image
- extract text from jpg
- convert image to text
- perform ocr on image
- set ocr language
language: id
og_description: Mengenali teks dari gambar dengan Aspose OCR di C#. Pelajari cara
  mengatur bahasa OCR, mengekstrak teks dari jpg, dan mengonversi gambar menjadi teks
  dalam hitungan menit.
og_title: Mengenali teks dari gambar di C# – Mengonversi Gambar ke Teks
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  headline: recognize text from image in C# – Convert Image to Text
  type: TechArticle
- description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  name: recognize text from image in C# – Convert Image to Text
  steps:
  - name: 5.1 Low‑Resolution Images
    text: OCR accuracy drops sharply below 100 dpi. If you notice garbled output,
      try pre‑processing the image (increase contrast, resize, or apply a sharpening
      filter) before feeding it to Aspose OCR.
  - name: 5.2 Multi‑Page Documents
    text: "Even though Community mode caps at 100 pages, you can still process PDFs
      or multi‑page TIFFs. The engine will return concatenated text, preserving page
      breaks with `\f`."
  - name: 5.3 Non‑English Languages
    text: 'Switch the `Language` enum to another supported value:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Mengenali Teks dari Gambar di C# – Mengonversi Gambar ke Teks
url: /id/net/text-recognition/recognize-text-from-image-in-c-convert-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar dalam C# – Mengonversi Gambar ke Teks

Pernahkah Anda perlu **mengenali teks dari gambar** tetapi tidak yakin perpustakaan mana yang memungkinkan Anda melakukannya tanpa biaya lisensi yang tinggi? Anda tidak sendirian. Dalam tutorial ini kami akan menjelaskan cara menggunakan mode Community gratis Aspose OCR untuk **mengonversi gambar ke teks**, mengekstrak teks dari file jpg, dan bahkan **mengatur bahasa OCR** untuk skenario multibahasa.

Kami akan membahas semuanya mulai dari menginstal paket NuGet hingga menangani kasus‑tepi seperti PDF multi‑halaman atau gambar beresolusi rendah. Pada akhir tutorial Anda akan memiliki aplikasi konsol yang dapat dijalankan yang dapat **melakukan OCR pada gambar** dalam sekejap.

## Apa yang Anda Butuhkan

- .NET 6 SDK atau yang lebih baru (kode ini juga bekerja dengan .NET Core 3.1+)  
- Visual Studio 2022 atau editor apa pun yang Anda sukai  
- File gambar (JPG, PNG, BMP…) yang berisi teks yang dapat dibaca  
- Akses internet untuk mengunduh paket NuGet `Aspose.OCR`

Itu saja—tanpa DLL tambahan, tanpa layanan eksternal, hanya C# murni.

![contoh mengenali teks dari gambar](https://example.com/ocr-screenshot.png "contoh mengenali teks dari gambar")

*(Tangkapan layar menunjukkan output konsol setelah mengenali JPG contoh.)*

## Langkah 1: Instal Aspose  OCR via NuGet

Pertama, tambahkan pustaka Aspose  OCR ke proyek Anda. Buka terminal di folder proyek dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Paket ini dilengkapi dengan **mode Community** yang membatasi pemrosesan hingga 100 halaman per eksekusi, yang sempurna untuk percobaan skala kecil. Jika Anda membutuhkan batas yang lebih tinggi, Anda dapat meningkatkan ke lisensi berbayar nanti—tanpa perlu mengubah kode.

## Langkah 2: Konfigurasikan Mesin OCR (Atur Bahasa OCR)

Sebelum Anda dapat **melakukan OCR pada gambar**, Anda harus memberi tahu mesin bahasa apa yang diharapkan. Defaultnya adalah Bahasa Inggris, tetapi Anda dapat beralih ke Bahasa Spanyol, Prancis, atau bahkan Mandarin dengan satu baris.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Choose the language you need – here we stick with English.
var ocrConfig = new OcrEngineConfig
{
    Language = Language.English,      // set ocr language
    MaxPagesPerRun = 100              // enforced limit in Community mode
};
```

Mengapa bahasa penting? Model OCR dilatih pada set karakter; memberikan dokumen berbahasa Prancis ke model Bahasa Inggris akan melewatkan aksen dan ligatur. Mengatur bahasa yang tepat meningkatkan akurasi secara dramatis.

## Langkah 3: Buat Mesin OCR dan Kenali Gambar

Dengan konfigurasi siap, buat instance mesin di dalam blok `using` sehingga sumber daya dilepaskan secara otomatis. Kemudian panggil `RecognizeImage` dengan path ke JPG Anda (atau format lain yang didukung).

```csharp
// Step 3: Create the OCR engine and recognize the image
using var ocrEngine = new OcrEngine(ocrConfig);

// Replace with the actual path to your image file.
string imagePath = @"YOUR_DIRECTORY/sample.jpg";

// Perform OCR – this will **recognize text from image**.
var ocrResult = ocrEngine.RecognizeImage(imagePath);
```

Beberapa hal yang perlu dicatat:

- **Keamanan thread:** Instance `OcrEngine` tidak thread‑safe. Jika Anda berencana memproses banyak gambar secara bersamaan, buat mesin terpisah per thread.
- **Format yang didukung:** Selain JPG, Anda dapat menggunakan PNG, BMP, TIFF, dan bahkan PDF. Metode yang sama berlaku, sehingga Anda dapat **mengekstrak teks dari jpg** atau gambar raster lainnya.

## Langkah 4: Output Teks yang Dikenali (Mengonversi Gambar ke Teks)

Sekarang mesin OCR telah menyelesaikan tugasnya, hasilnya disimpan dalam objek `OcrResult`. Properti `Text`-nya berisi representasi teks biasa dari semua yang dapat dibaca mesin.

```csharp
// Step 4: Write the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Jika Anda menjalankan program dengan tangkapan layar yang jelas dari sebuah struk, Anda akan melihat sesuatu seperti:

```
=== OCR Output ===
Item        Qty   Price
Apple       2     $1.20
Banana      5     $0.75
Total               $5.55
```

Itulah inti dari **mengonversi gambar ke teks**—gambar kini menjadi string yang dapat Anda simpan, cari, atau masukkan ke sistem lain.

## Langkah 5: Menangani Kasus‑tepi Umum

### 5.1 Gambar Resolusi Rendah

Akurasi OCR turun tajam di bawah 100 dpi. Jika Anda melihat output yang berantakan, coba pra‑proses gambar (tingkatkan kontras, ubah ukuran, atau terapkan filter penajaman) sebelum memberikannya ke Aspose OCR.

```csharp
// Example: Resize a low‑dpi image to improve accuracy
using var bitmap = new Bitmap(imagePath);
var highRes = new Bitmap(bitmap, new Size(bitmap.Width * 2, bitmap.Height * 2));
highRes.Save("highres_sample.jpg");
var highResResult = ocrEngine.RecognizeImage("highres_sample.jpg");
```

### 5.2 Dokumen Multi‑Halaman

Meskipun mode Community dibatasi hingga 100 halaman, Anda masih dapat memproses PDF atau TIFF multi‑halaman. Mesin akan mengembalikan teks yang digabungkan, mempertahankan jeda halaman dengan `\f`.

```csharp
var multiPageResult = ocrEngine.RecognizeImage("multi_page.pdf");
Console.WriteLine(multiPageResult.Text); // contains form‑feed characters between pages
```

### 5.3 Bahasa Non‑Inggris

Ubah enum `Language` ke nilai lain yang didukung:

```csharp
ocrConfig.Language = Language.French; // now the engine expects French characters
```

Ingat untuk menginstal paket bahasa yang sesuai jika Anda melampaui set default; Aspose menyediakan paket tersebut sebagai paket NuGet terpisah.

## Langkah 6: Contoh Kerja Lengkap

Menggabungkan semuanya, berikut adalah aplikasi konsol lengkap yang siap disalin‑tempel yang **mengenali teks dari gambar**, **mengekstrak teks dari jpg**, dan **mengatur bahasa OCR** sesuai kebutuhan.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Configuration;

class OcrDemo
{
    static void Main()
    {
        // 1️⃣ Configure OCR – change Language to match your source.
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,   // set ocr language
            MaxPagesPerRun = 100
        };

        // 2️⃣ Create the engine inside a using block.
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 3️⃣ Path to the image you want to process.
        string imagePath = @"YOUR_DIRECTORY/sample.jpg";

        // 4️⃣ Perform OCR – this **recognize text from image**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 5️⃣ Output – now you have **convert image to text** results.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output yang diharapkan** (asumsi gambar contoh berisi teks “Hello World!”):

```
=== OCR Output ===
Hello World!
```

Jalankan program dengan `dotnet run` dan Anda akan melihat konsol menampilkan string yang diekstrak.

## Tips Pro & Kesalahan Umum

- **Tips pro:** Bungkus pemanggilan OCR dalam blok `try/catch` untuk menangani file yang rusak dengan elegan.  
- **Waspadai:** Gambar dengan watermark atau noise latar belakang yang berat; mereka sering membingungkan mesin.  
- **Tips:** Jika Anda perlu memproses sekumpulan file, iterasi entri direktori dan gunakan kembali instance `OcrEngine` yang sama—hanya ingat untuk mengatur ulang pengaturan per‑gambar.  
- **Ingat:** Batas 100 halaman mode Community berlaku per eksekusi, bukan per file. Bagi PDF besar jika Anda mencapai batas.

## Kesimpulan

Anda kini memiliki potongan kode yang solid dan siap produksi yang **mengenali teks dari gambar** menggunakan Aspose OCR dalam C#. Dari menginstal paket NuGet hingga **mengatur bahasa OCR**, menangani gambar beresolusi rendah, dan akhirnya **mengonversi gambar ke teks**, setiap langkah telah dibahas. Jangan ragu untuk bereksperimen—ganti bahasa, gunakan PNG, atau rangkaikan output ke indeks pencarian downstream.

Selanjutnya, Anda dapat menjelajahi **mengekstrak teks dari jpg** secara skala dengan mengintegrasikan kode ini ke dalam Azure Function, atau menyelami lebih dalam fitur lanjutan Aspose OCR seperti analisis tata letak dan pengenalan tulisan tangan. Kemungkinannya tak terbatas, dan fondasi yang Anda bangun hari ini akan membuat ekstensi tersebut mudah.

Selamat coding, dan semoga gambar Anda selalu dapat dibaca!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [mengenali teks gambar dengan Aspose OCR untuk banyak bahasa](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}