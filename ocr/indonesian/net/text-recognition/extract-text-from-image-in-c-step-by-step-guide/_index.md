---
category: general
date: 2026-05-06
description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  mengonversi JPG menjadi teks, mengatur bahasa OCR, dan membaca teks dari JPG secara
  efisien.
draft: false
keywords:
- extract text from image
- convert jpg to text
- image to text c#
- read text from jpg
- set OCR language
language: id
og_description: Ekstrak teks dari gambar di C# dengan Aspose OCR. Panduan ini menunjukkan
  cara mengonversi JPG menjadi teks, mengatur bahasa OCR, dan membaca teks dari JPG.
og_title: Ekstrak Teks dari Gambar di C# – Tutorial Lengkap
tags:
- OCR
- C#
- Aspose
title: Ekstrak Teks dari Gambar di C# – Panduan Langkah demi Langkah
url: /id/net/text-recognition/extract-text-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di C# – Panduan Pemrograman Lengkap

Pernah membutuhkan untuk **mengekstrak teks dari gambar** tetapi tidak yakin pustaka mana yang harus dipilih? Anda tidak sendirian—para pengembang terus bertanya, “Bagaimana cara mengonversi JPG ke teks tanpa mengirim data ke cloud?” Kabar baiknya, Aspose OCR memberikan solusi sepenuhnya offline yang bekerja langsung di dalam aplikasi .NET Anda.

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui: mulai dari menginstal paket NuGet Aspose OCR, hingga **menetapkan bahasa OCR** untuk teks Rusia, dan akhirnya **membaca teks dari file JPG**. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali yang dapat Anda sisipkan ke dalam proyek C# mana pun dan mulai mengekstrak teks dari gambar secara instan.

> **Apa yang akan Anda dapatkan**  
> • Contoh yang jelas dan dapat dijalankan yang **mengekstrak teks dari gambar**.  
> • Pengetahuan tentang cara **mengonversi JPG ke teks** menggunakan mesin Aspose OCR.  
> • Tips mengonfigurasi **set OCR language** untuk skenario multibahasa.  
> • Penanganan kasus tepi untuk gambar yang tidak dapat dibaca dan paket bahasa yang hilang.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| .NET 6.0 atau lebih baru (runtime .NET terbaru apa pun) | Aspose OCR menargetkan .NET Standard 2.0+, sehingga runtime yang lebih baru memberikan kinerja terbaik. |
| Visual Studio 2022 (atau VS Code dengan ekstensi C#) | IDE yang ramah membantu Anda men-debug alur OCR dengan cepat. |
| Akses internet **sekali** untuk mengunduh paket NuGet Aspose OCR | Setelah instalasi pertama Anda dapat mengaktifkan **offline resources** untuk menghindari unduhan lebih lanjut. |
| Contoh gambar JPG (`input.jpg`) yang berisi teks Rusia (atau bahasa apa pun yang akan Anda gunakan) | Tutorial ini menggunakan contoh bahasa Rusia, tetapi Anda dapat mengganti dengan paket bahasa apa pun yang telah Anda instal. |

Jika ada yang terdengar tidak familiar, jangan panik. Menginstal paket NuGet semudah mengetik satu perintah, dan langkah-langkah selanjutnya bekerja sama untuk setiap format gambar yang didukung oleh Aspose.

## Gambaran Umum Solusi

Secara umum prosesnya terlihat seperti ini:

1. **Buat** sebuah `OcrEngine` dengan offline resources sehingga pustaka tidak akan mencoba mengunduh data bahasa saat runtime.  
2. **Setel** bahasa yang diinginkan (misalnya, Russian) menggunakan enum `OcrLanguage`.  
3. **Panggil** `RecognizeImage` pada file JPG lokal.  
4. **Cetak** string yang diekstrak ke konsol atau alirkan ke alur kerja Anda sendiri.

Berikut adalah diagram singkat yang menggambarkan aliran data:

![Extract text from image using Aspose OCR in C#](https://example.com/placeholder-image.png){.align-center alt="extract text from image using Aspose OCR in C#"}

*Diagram ini hanya bersifat ilustratif; kode yang melakukan pekerjaan berat.*

## Ekstrak Teks dari Gambar – Konsep Inti

Sebelum kita mulai menulis kode, mari kita uraikan beberapa konsep yang sering membuat pengembang kebingungan:

- **OfflineResources** – Ketika `true`, Aspose OCR mencari paket bahasa yang telah Anda unduh sebelumnya. Ini menghilangkan langkah “auto‑download” yang dapat memperlambat startup di lingkungan produksi.  
- **OcrLanguage** – Enum ini berisi puluhan identifier bahasa (`English`, `Russian`, `Japanese`, …). Memilih yang tepat secara dramatis meningkatkan akurasi karena mesin dapat menerapkan heuristik khusus bahasa.  
- **Image quality** – OCR bekerja paling baik pada gambar dengan kontras tinggi dan bebas noise. Jika Anda mendapatkan hasil yang berantakan, pertimbangkan pra‑pemrosesan (misalnya, binarisasi) sebelum memberi gambar ke mesin.

Memahami poin‑poin ini akan membantu Anda memutuskan kapan harus **set OCR language** secara manual dibandingkan mengandalkan auto‑detect, dan mengapa **convert JPG to text** bukan hanya satu baris kode.

## Langkah 1: Instal Paket NuGet Aspose OCR

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

*Pro tip:* Setelah instalasi pertama, tambahkan `-v latest` untuk memastikan Anda selalu mendapatkan build stabil terbaru. Ukuran paket kira‑kira 15 MB, yang wajar untuk kebanyakan penyebaran desktop atau server.

## Langkah 2: Convert JPG to Text – Inisialisasi Mesin

Sekarang pustaka sudah ada di mesin Anda, mari buat `OcrEngine` yang bekerja secara offline.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine with offline resources.
        // This prevents the SDK from trying to download language data at runtime.
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            OfflineResources = true   // <-- crucial for production stability
        });

        // Step 2.2: Choose the language pack you need.
        // Here we use Russian; replace with OcrLanguage.English for English text.
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 2.3: Perform OCR on a local JPG file.
        // The file path can be absolute or relative to the executable.
        var result = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.jpg");

        // Step 2.4: Output the extracted text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(result.Text);
    }
}
```

### Mengapa ini penting

- **Offline mode** menjamin waktu startup yang deterministik—tidak ada panggilan jaringan yang tak terduga ketika Anda menyebarkan ke server yang terkunci.  
- **Setting the language** (`OcrLanguage.Russian`) memberi tahu mesin untuk menggunakan set karakter Rusia, yang meningkatkan akurasi pengenalan dari ~70 % menjadi >95 % untuk gambar bersih.  
- Metode `RecognizeImage` menerima format gambar apa pun yang didukung Aspose (`.jpg`, `.png`, `.tiff`, …). Itulah mengapa kita dapat **read text from JPG** tanpa langkah konversi tambahan.

## Langkah 3: Set OCR Language – Menangani Banyak Bahasa

Kadang-kadang Anda perlu memproses dokumen yang berisi bahasa campuran (mis., Rusia dan Inggris). Aspose OCR memungkinkan Anda menentukan array bahasa *fallback*:

```csharp
// Example: Russian primary, English secondary
ocrEngine.Language = OcrLanguage.Russian;
ocrEngine.AdditionalLanguages = new[] { OcrLanguage.English };
```

Ketika bahasa utama gagal mengenali sebuah karakter, mesin secara otomatis memeriksa daftar tambahan. Teknik ini sangat berguna untuk faktur yang mencampur nama perusahaan Cyrillic dengan kode produk berbahasa Inggris.

> **Catatan:** Paket bahasa harus ada di folder `Resources` proyek Anda. Jika Anda mendapatkan `FileNotFoundException`, unduh paket yang hilang dari portal Aspose dan letakkan di samping executable.

## Langkah 4: Read Text from JPG – Kendala Umum & Solusinya

Bahkan dengan paket bahasa yang tepat, Anda mungkin menghadapi:

| Masalah | Gejala Umum | Perbaikan Cepat |
|---------|-------------|-----------------|
| Kontras rendah | Output berantakan atau kosong | Terapkan filter contrast‑stretch sederhana menggunakan `System.Drawing` sebelum OCR. |
| Gambar diputar | Teks muncul miring | Gunakan `ocrEngine.ImageRotation = OcrRotation.Rotate90;` (atau 180/270) sebelum memanggil `RecognizeImage`. |
| Ukuran file besar | Pengenalan lambat, penggunaan memori tinggi | Ubah ukuran gambar menjadi maksimum 2000 px pada sisi terpanjang; kualitas OCR tetap tinggi. |

Berikut adalah helper ringkas yang mengubah ukuran dan meningkatkan gambar sebelum memberikannya ke mesin:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

static string PreprocessAndRead(string jpgPath)
{
    // Load the original image
    using var original = new Bitmap(jpgPath);

    // Resize while preserving aspect ratio (max 2000px)
    int maxDim = 2000;
    int newWidth, newHeight;
    if (original.Width > original.Height)
    {
        newWidth = maxDim;
        newHeight = original.Height * maxDim / original.Width;
    }
    else
    {
        newHeight = maxDim;
        newWidth = original.Width * maxDim / original.Height;
    }

    using var resized = new Bitmap(original, new Size(newWidth, newHeight));

    // Optional: increase contrast (simple linear stretch)
    var contrast = new ImageAttributes();
    float[][] matrix = {
        new float[] {1.2f, 0, 0, 0, 0},
        new float[] {0, 1.2f, 0, 0, 0},
        new float[] {0, 0, 1.2f, 0, 0},
        new float[] {0, 0, 0, 1, 0},
        new float[] {0, 0, 0, 0, 1}
    };
    contrast.SetColorMatrix(new ColorMatrix(matrix));

    using var graphics = Graphics.FromImage(resized);
    graphics.DrawImage(resized, new Rectangle(0, 0, newWidth, newHeight), 0, 0, newWidth, newHeight, GraphicsUnit.Pixel, contrast);

    // Save to a temporary file (Aspose OCR works with file paths)
    string tempPath = Path.GetTempFileName() + ".jpg";
    resized.Save(tempPath, ImageFormat.Jpeg);

    // Run OCR
    var engine = new OcrEngine(new OcrEngineSettings { OfflineResources = true });
    engine.Language = OcrLanguage.Russian;
    var res = engine.RecognizeImage(tempPath);
    File.Delete(tempPath); // clean up
    return res.Text;
}
```

Anda sekarang dapat memanggil `Console.WriteLine(PreprocessAndRead("YOUR_DIRECTORY/input.jpg"));` dan mendapatkan hasil yang lebih bersih.

## Contoh Lengkap yang Berfungsi – Semua Langkah dalam Satu File

Berikut adalah program *lengkap* yang dapat Anda salin‑tempel ke dalam `Program.cs`. Program ini mencakup catatan instalasi, konfigurasi bahasa, pra‑pemrosesan, dan penanganan error.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        string imagePath = "YOUR_DIRECTORY/input.jpg";

        try
        {

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}