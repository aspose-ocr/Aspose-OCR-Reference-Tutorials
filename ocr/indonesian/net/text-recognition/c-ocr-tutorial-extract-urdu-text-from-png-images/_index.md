---
category: general
date: 2026-03-21
description: 'c# ocr tutorial: Pelajari cara mengekstrak teks Urdu dari gambar PNG
  menggunakan OCR di C#. Termasuk kode langkah demi langkah, pengaturan bahasa, dan
  tips praktis.'
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: id
og_description: 'tutorial c# ocr: Pelajari cara mengekstrak teks Urdu dari gambar
  PNG menggunakan OCR di C#. Panduan lengkap dengan kode dan tips.'
og_title: tutorial OCR c# – Ekstrak Teks Urdu dari Gambar PNG
tags:
- OCR
- C#
- Urdu
- Image Processing
title: Tutorial OCR C# – Ekstrak Teks Urdu dari Gambar PNG
url: /id/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Ekstrak Teks Urdu dari Gambar PNG

Pernah membutuhkan **c# ocr tutorial** yang benar‑benar mengambil teks Urdu dari file PNG? Anda tidak sendirian. Dalam banyak proyek—pemrosesan faktur, pengarsipan dokumen, atau bahkan alat terjemahan cepat—Anda akan sampai pada titik di mana Anda harus mengenali data gambar teks, dan bahasa menjadi penting.  

Dalam panduan ini kami akan menelusuri solusi lengkap yang siap dijalankan untuk mengekstrak teks Urdu dari PNG menggunakan mesin OCR. Anda akan melihat mengapa setiap baris ada, cara menangani paket bahasa yang hilang, dan apa yang harus dilakukan jika gambar tidak sempurna. Pada akhir tutorial Anda akan cukup percaya diri untuk menyesuaikan kode bagi bahasa atau tipe file lain.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan pustaka OCR C# (tanpa sihir tersembunyi)  
- Langkah‑langkah tepat untuk **extract urdu text** dari file PNG  
- Mengapa mengonfigurasi bahasa ke Urdu penting dan bagaimana engine mengunduh data yang hilang secara otomatis  
- Cara memverifikasi output dan mengatasi masalah umum  

Tidak ada tautan dokumentasi eksternal yang diperlukan—semua yang Anda butuhkan ada di sini.

## Prerequisites (What You Need Before Starting)

| Persyaratan | Mengapa Penting |
|-------------|-----------------|
| .NET 6.0+ (or .NET Core 3.1) | API modern dan dukungan async |
| Visual Studio 2022 (or VS Code with C# extension) | IDE dengan IntelliSense membuat kode lebih jelas |
| An OCR library that exposes `OcrEngine` (e.g., **Microsoft.Windows.SDK.Contracts** or a third‑party NuGet) | Menyediakan metode `Language.Urdu` dan `Recognize` |
| A PNG image containing Urdu text (e.g., `urdu_invoice.png`) | Sumber untuk **recognize text image** operation |

Jika Anda belum memiliki paket OCR, jalankan satu baris berikut di Package Manager Console:

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

> **Pro tip:** SDK secara otomatis mengambil data bahasa pada penggunaan pertama, jadi Anda tidak perlu mengunduh paket bahasa Urdu secara manual.

## Langkah 1: Instal dan Referensikan Pustaka OCR

Sebelum kita dapat membuat engine, proyek harus mereferensikan paket OCR. Tambahkan direktif `using` berikut di bagian atas file Anda:

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

Namespace ini memberi kita akses ke `OcrEngine`, `Language`, dan utilitas pemuatan gambar. Jika Anda menggunakan pustaka yang berbeda, cari namespace serupa.

## Langkah 2: Buat Instance OcrEngine  

Sekarang kita benar‑benar memulai engine. Anggap engine sebagai otak yang akan menginterpretasikan pola piksel sebagai karakter.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**Mengapa ini penting:** `TryCreateFromLanguage` mengembalikan `null` jika data bahasa tidak ada, memberi kita kesempatan untuk gagal lebih awal alih‑alih crash di kemudian hari.

## Langkah 3: Muat Gambar PNG  

Engine OCR bekerja dengan objek `SoftwareBitmap`, bukan jalur file mentah. Helper berikut memuat PNG dari disk dan mengonversinya ke format yang diperlukan.

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**Kasus tepi:** Jika PNG berwarna, mengonversi ke grayscale (`Gray8`) sering meningkatkan pengenalan, terutama untuk skrip seperti Urdu yang memiliki diakritik halus.

## Langkah 4: Kenali Teks dari Gambar  

Berikut inti dari **c# ocr tutorial**—meminta engine membaca gambar.

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

Properti `OcrResult.Text` berisi string Unicode mentah. Karena kita telah mengatur bahasa ke Urdu sebelumnya, engine menerapkan aturan skrip yang tepat.

## Langkah 5: Output dan Verifikasi Teks yang Diekstrak  

Akhirnya, kita mencetak hasil ke konsol. Dalam aplikasi nyata Anda mungkin menyimpannya ke basis data atau mengirimnya ke layanan terjemahan.

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**Apa yang diharapkan:** Jika gambar jelas, Anda akan melihat sesuatu seperti:

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

Jika output terlihat berantakan, periksa kualitas gambar (kontras, noise) dan pertimbangkan pra‑pemrosesan (misalnya, binarisasi).

## Cara Mengekstrak Teks Urdu dari File PNG – Kendala Umum  

1. **Kontras rendah** – OCR kesulitan ketika warna latar depan dan latar belakang mirip. Gunakan alat pengedit gambar untuk meningkatkan kontras sebelum menjalankan kode.  
2. **DPI tidak tepat** – Memindai pada 300 dpi atau lebih tinggi memberi engine detail lebih banyak untuk diproses.  
3. **Paket bahasa hilang** – Panggilan pertama ke `TryCreateFromLanguage` mungkin memicu unduhan; pastikan mesin Anda terhubung ke internet.  

Menangani masalah‑masalah ini secara signifikan meningkatkan tingkat keberhasilan **recognize text image**.

## Recognize Text Image: Memperluas ke Format Lain  

Meskipun tutorial ini berfokus pada PNG, alur kerja yang sama berlaku untuk JPEG, BMP, atau TIFF—cukup ubah ekstensi file dan pastikan decoder mendukungnya. Baris kunci tetap `await ocrEngine.RecognizeAsync(bitmap);`.

## Tips untuk OCR dari File PNG – Kinerja dan Skalabilitas  

- **Pemrosesan batch:** Muat beberapa gambar ke dalam daftar dan jalankan `Task.WhenAll` untuk memparalelkan pengenalan.  
- **Caching engine:** Buat satu instance `OcrEngine` dan gunakan kembali pada setiap pemanggilan; membuatnya berulang‑ulang menambah beban.  
- **Manajemen memori:** Dispose objek `SoftwareBitmap` setelah selesai (`bitmap.Dispose()`) agar proses tetap ringan.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut seluruh program yang dapat Anda kompilasi dan jalankan. Termasuk semua pernyataan `using`, penanganan async, dan pengecekan error.

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**Output yang diharapkan:** Konsol mencetak karakter Urdu tepat yang ditemukan dalam gambar, mempertahankan urutan kanan‑ke‑kiri.

## Kesimpulan  

Anda baru saja menyelesaikan **c# ocr tutorial** yang menunjukkan cara **extract urdu text** dari PNG, mengonfigurasi bahasa, dan menangani hasil dengan aman. Langkah‑langkah—menginstal pustaka, membuat engine, memuat gambar, mengenali teks, dan menampilkannya—merupakan pola yang dapat dipakai ulang untuk skrip atau tipe file apa pun.  

Selanjutnya, coba eksperimen dengan **recognize text image** pada PDF multi‑halaman (konversi tiap halaman ke PNG terlebih dahulu) atau integrasikan API terjemahan untuk mengubah Urdu yang diekstrak menjadi bahasa Inggris secara otomatis. Langit adalah batasnya setelah Anda menguasai alur kerja inti ini.

Selamat coding, semoga hasil OCR Anda jernih!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}