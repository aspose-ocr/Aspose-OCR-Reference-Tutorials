---
category: general
date: 2026-05-21
description: Cara melakukan OCR di C# menggunakan Aspose OCR – pelajari cara mengonversi
  gambar menjadi teks, membaca teks dari JPG, dan memuat gambar untuk OCR dengan cepat
  dan andal.
draft: false
keywords:
- how to perform OCR
- convert image to text
- read text from jpg
- how to extract text from image
- load image for OCR
language: id
og_description: Cara melakukan OCR di C# dengan Aspose OCR. Panduan ini menunjukkan
  cara mengonversi gambar menjadi teks, membaca teks dari JPG, dan memuat gambar untuk
  OCR langkah demi langkah.
og_title: Cara Melakukan OCR di C# – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: How to perform OCR in C# using Aspose OCR – learn to convert image
    to text, read text from jpg, and load image for OCR quickly and reliably.
  headline: How to Perform OCR in C# – Convert Image to Text with Aspose OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Cara Melakukan OCR di C# – Mengonversi Gambar menjadi Teks dengan Aspose OCR
url: /id/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Panduan Lengkap

Pernah bertanya-tanya **how to perform OCR** dalam aplikasi C# tanpa harus berurusan dengan pemrosesan gambar tingkat rendah? Anda tidak sendirian. Banyak pengembang membutuhkan cara yang andal untuk **convert image to text**, terutama saat menangani dokumen yang dipindai atau foto kwitansi. Dalam tutorial ini kami akan memandu langkah‑langkah tepat untuk memuat gambar untuk OCR, menjalankan mesin pengenalan, dan akhirnya membaca teks yang diekstrak—semua dengan Aspose OCR.

Kami juga akan membahas cara **read text from jpg** file, mendiskusikan nuansa **how to extract text from image** sumber, dan memberi Anda cheat‑sheet cepat untuk skenario **load image for OCR**. Pada akhir tutorial, Anda akan memiliki contoh siap‑jalankan yang dapat Anda masukkan ke proyek .NET mana pun.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0 atau lebih baru (kode ini bekerja pada .NET Core dan .NET Framework sekaligus)
- Visual Studio 2022 atau IDE apa pun yang Anda sukai
- File lisensi Aspose OCR untuk .NET (opsional tetapi disarankan untuk mode fitur lengkap)
- Sebuah gambar contoh (misalnya `sample.jpg`) yang ditempatkan di folder yang diketahui
- Akses internet untuk mengunduh paket NuGet `Aspose.OCR`

Jika ada yang terdengar tidak familiar, jangan panik—setiap persyaratan akan dibahas seiring perjalanan.

## Langkah 1 – Instal Aspose OCR via NuGet

Hal pertama yang Anda butuhkan adalah pustaka Aspose OCR. Buka Package Manager Console dan jalankan:

```powershell
Install-Package Aspose.OCR
```

Atau, jika Anda menggunakan CLI:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Menambahkan paket akan memulihkan semua dependensi, sehingga Anda tidak perlu mencari DLL tambahan secara manual.

## Langkah 2 – Muat Gambar untuk OCR

Sekarang pustaka sudah tersedia, kita perlu **load image for OCR**. Langkah ini penting karena mesin mengharapkan objek `ImageStream`, bukan jalur file mentah.

```csharp
using Aspose.OCR;

// Assume the image lives in the same folder as the executable
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");

// Create an ImageStream from the file
ImageStream imgStream = ImageStream.FromFile(imagePath);
```

Perhatikan bagaimana kami membangun jalur lengkap dengan `AppDomain.CurrentDomain.BaseDirectory`. Ini membuat kode menjadi kuat baik Anda menjalankannya dari Visual Studio, console, atau exe yang dipublikasikan. Selain itu, kelas `ImageStream` mendukung banyak format, sehingga Anda dapat dengan mudah **read text from jpg**, **png**, atau **bmp**.

## Langkah 3 – Cara Melakukan OCR pada Gambar yang Dimuat

Berikut inti dari tutorial—**how to perform OCR** menggunakan mesin Aspose. Kami juga akan mengatur bahasa ke English; Anda dapat mengganti `OcrLanguage.English` dengan bahasa lain yang didukung jika diperlukan.

```csharp
// Step 3: Create an OCR engine and specify the language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    Image = imgStream // assign the previously loaded image
};

// Optionally, apply your license to unlock the full feature set
var license = new License();
license.SetLicense(@"YOUR_DIRECTORY\Aspose.OCR.NET.lic");

// Run the recognition process
ocrEngine.Recognize();
```

Mengapa kami mengatur properti `Image` sebelum memanggil `Recognize()`? Mesin memerlukan sumber gambar yang valid; jika tidak, ia akan melempar `NullReferenceException`. Dengan menetapkan `ImageStream` yang kami siapkan pada Langkah 2, kami menjamin eksekusi yang lancar.

## Langkah 4 – Ambil dan Tampilkan Teks yang Diekstrak (Convert Image to Text)

Setelah mesin selesai, teks yang dikenali berada di properti `Text`. Di sinilah keajaiban **convert image to text** sebenarnya terjadi.

```csharp
// Step 4: Get the recognized text
string extractedText = ocrEngine.Text;

// Display it in the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

Output tipikal mungkin terlihat seperti berikut:

```
=== OCR Result ===
Invoice #12345
Date: 2026-04-30
Total: $1,250.00
Thank you for your business!
```

Jika gambar buram atau mengandung font yang kompleks, Anda mungkin melihat karakter yang kacau. Dalam kasus tersebut, pertimbangkan untuk menyesuaikan properti `Resolution` mesin atau melakukan pra‑pemrosesan gambar (misalnya, binarisasi) sebelum memberi ke OCR.

## Langkah 5 – Lanjutan: Cara Mengekstrak Teks dari Gambar dengan Pengaturan Kustom

Kadang pengaturan default tidak cukup. Berikut beberapa penyesuaian yang membantu ketika **how to extract text from image** menjadi masalah yang rumit.

```csharp
// Increase DPI for better accuracy on low‑resolution images
ocrEngine.Image = ImageStream.FromFile(imagePath);
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;

// Enable auto‑rotate if the image might be skewed
ocrEngine.AutoRotate = true;

// Restrict recognition to a specific character set (e.g., digits only)
ocrEngine.RecognitionSettings.Characters = "0123456789.-";
```

Penyesuaian ini dapat secara dramatis meningkatkan hasil saat menangani kwitansi, formulir, atau tabel yang dipindai. Ingat, **how to perform OCR** bukan solusi satu‑ukuran‑untuk‑semua; Anda sering perlu bereksperimen dengan pengaturan berdasarkan materi sumber.

## Langkah 6 – Kesalahan Umum Saat Membaca Teks dari File JPG

Bahkan dengan pustaka yang solid, pengembang dapat menemui hambatan. Berikut beberapa yang mungkin Anda temui saat mencoba **read text from jpg**:

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Low contrast** | Kompresi JPG dapat meratakan warna, membuat teks tidak dapat dibedakan dari latar belakang. | Pra‑proses gambar dengan filter peningkatan kontras (misalnya, `ImageSharp` atau `System.Drawing`). |
| **Incorrect orientation** | Telepon kadang menyimpan metadata orientasi alih‑alih memutar piksel. | Set `ocrEngine.AutoRotate = true` atau secara manual memutar gambar sebelum OCR. |
| **Large file size** | JPG beresolusi sangat tinggi mengonsumsi memori dan memperlambat pengenalan. | Ukur ulang gambar ke DPI yang wajar (misalnya, 300) sebelum memuat. |

Mengingat hal ini akan menghemat Anda berjam‑jam debugging ketika Anda kemudian **load image for OCR** di produksi.

## Langkah 7 – Kode Penutup: Contoh Satu‑File

Berikut program lengkap yang dapat dijalankan yang menggabungkan semua bagian. Salin‑tempel ke proyek console baru dan tekan **F5**.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Set up license (optional but recommended)
        // -------------------------------------------------
        var license = new License();
        // Replace with your actual license path or comment out for trial mode
        license.SetLicense(@"YOUR_DIRECTORY\Aspose.OCR.NET.lic");

        // -------------------------------------------------
        // 2️⃣  Load the image you want to process
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
        ImageStream imgStream = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣  Create OCR engine – this is where we **perform OCR**
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            Image = imgStream,
            AutoRotate = true   // helpful for photos taken at odd angles
        };

        // -------------------------------------------------
        // 4️⃣  Run recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 5️⃣  Retrieve and display the result – **convert image to text**
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

**Output yang diharapkan** (asumsi `sample.jpg` berisi teks English yang jelas):

```
=== OCR Result ===
Hello, world!
This is a sample image for OCR testing.
```

Jika Anda melihat output kosong, periksa kembali jalur gambar dan pastikan file tidak rusak.

## Kesimpulan

Anda kini tahu **how to perform OCR** di C# menggunakan Aspose OCR, mulai dari menginstal paket hingga **loading image for OCR**, menjalankan mesin, dan akhirnya **convert image to text**. Panduan ini juga mencakup tips praktis untuk file **read text from jpg** dan menjawab pertanyaan umum **how to extract text from image** ketika pengaturan default tidak memadai.

Apa selanjutnya? Coba beri mesin PDF (dengan mengonversi setiap halaman menjadi gambar terlebih dahulu), bereksperimen dengan pengenalan multibahasa, atau integrasikan langkah OCR ke dalam pipeline pemrosesan dokumen yang lebih besar. Kemungkinannya tak terbatas, dan dengan fondasi kuat yang baru saja Anda bangun, Anda akan dapat menangani tantangan ekstraksi teks apa pun yang muncul.

Jangan ragu meninggalkan komentar jika Anda mengalami kendala atau menemukan trik cerdas—selamat coding!

![How to perform OCR example](/images/ocr-example.png "How to perform OCR in C# – visual overview")

## Tutorial Terkait

- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Konversi Gambar ke Teks – Lakukan OCR pada Gambar dari URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Cara OCR Gambar – Lakukan OCR pada Gambar dalam Pengenalan Gambar OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}