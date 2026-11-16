---
category: general
date: 2026-02-28
description: Ekstrak teks dari gambar menggunakan Aspose.OCR tanpa internet. Pelajari
  cara mengenali teks dari PNG, membaca teks dari hasil pemindaian, mengonversi gambar
  menjadi teks, dan memuat gambar untuk OCR.
draft: false
keywords:
- extract text from image
- recognize text from png
- read text from scan
- convert image to text
- load image for OCR
language: id
og_description: Ekstrak teks dari gambar secara offline dengan Aspose.OCR. Tutorial
  ini menunjukkan cara mengenali teks dari PNG, membaca teks dari pemindaian, mengonversi
  gambar menjadi teks, dan memuat gambar untuk OCR.
og_title: Ekstrak Teks dari Gambar di C# – Panduan OCR Offline
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Ekstrak Teks dari Gambar di C# – Panduan Langkah-demi-Langkah OCR Offline
url: /id/net/text-recognition/extract-text-from-image-in-c-offline-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di C# – Panduan Langkah‑demi‑Langkah OCR Offline

Pernah membutuhkan untuk **extract text from image** tetapi aplikasi Anda tidak dapat mengandalkan koneksi internet? Mungkin Anda sedang membangun pemindai aman yang berjalan pada perangkat sandboxed, atau Anda hanya ingin menghindari lonjakan latensi. Dalam kedua kasus, kabar baiknya adalah Aspose.OCR memungkinkan Anda **recognize text from png** secara lengkap offline.  

Dalam tutorial ini kami akan menjelaskan contoh lengkap yang dapat dijalankan yang menunjukkan cara **read text from scan** file, **convert image to text**, dan **load image for OCR** menggunakan library Aspose.OCR. Pada akhir Anda akan memiliki aplikasi console mandiri yang mencetak teks yang diekstrak ke console—tanpa layanan cloud.

## Apa yang Anda Butuhkan

- **.NET 6.0** (atau versi .NET terbaru lainnya). Sintaks yang ditunjukkan bekerja dengan .NET 6+ tetapi konsep yang sama berlaku untuk .NET Framework 4.7+.
- **Aspose.OCR for .NET** paket NuGet. Instal dengan `dotnet add package Aspose.OCR`.
- Sebuah file gambar (png, jpg, bmp, dll.) yang berisi teks yang jelas dan terbaca. Untuk panduan ini kami akan menyebutnya `offline_test.png` dan menempatkannya di folder bernama `YOUR_DIRECTORY`.
- IDE favorit Anda (Visual Studio, VS Code, Rider—apa pun yang Anda suka).

> **Pro tip:** Simpan paket bahasa yang Anda butuhkan (Inggris dalam contoh) pada mesin yang sama dengan aplikasi; ini memastikan operasi offline yang sesungguhnya.

## Langkah 1 – Siapkan Proyek dan Instal Aspose.OCR

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
dotnet add package Aspose.OCR
```

> **Mengapa ini penting:** Menambahkan paket NuGet mengembalikan semua DLL yang diperlukan, sehingga Anda tidak akan mendapatkan error “missing reference” saat mengompilasi.

## Langkah 2 – Konfigurasikan Mesin OCR untuk Penggunaan Offline

Inti dari solusi ini adalah kelas `OcrEngine`. Dengan mengubah `OfflineMode` menjadi `true` Anda menjamin mesin tidak pernah melakukan panggilan jaringan. Anda juga menentukan paket bahasa yang berada secara lokal.

```csharp
using Aspose.OCR;
using System.Drawing;   // For Image.Load

// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    OfflineMode = true,               // Prevent any network calls
    Language = OcrLanguage.English    // Use the locally‑installed English pack
};
```

> **Penjelasan:** `OfflineMode` adalah perlindungan. Jika Anda lupa mengaturnya, Aspose dapat secara diam-diam menghubungi layanan cloudnya untuk mengunduh data bahasa yang hilang, yang mengalahkan tujuan pemindai offline.

## Langkah 3 – Muat Gambar yang Ingin Diproses

Memuat gambar cukup sederhana, tetapi perhatikan penggunaan `using var` yang memastikan bitmap dibuang secara otomatis.

```csharp
// Adjust the path to point at your image file
using var image = Image.Load(@"YOUR_DIRECTORY/offline_test.png");

// Quick sanity check – you can inspect image.Width / image.Height if needed
Console.WriteLine($"Loaded image with dimensions: {image.Width}x{image.Height}");
```

> **Kasus tepi:** Jika file tidak ditemukan, `Image.Load` melempar `FileNotFoundException`. Bungkus pemanggilan dalam blok try‑catch untuk kode produksi.

## Langkah 4 – Jalankan OCR dan Dapatkan Teks

Sekarang kita benar‑benar melakukan pengenalan. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi string yang diekstrak dan skor kepercayaan.

```csharp
// Perform OCR
var ocrResult = ocrEngine.Recognize(image);

// The Text property holds the plain‑text extraction
string extractedText = ocrResult.Text;

// Show the result
Console.WriteLine("\n--- OCR Output ---");
Console.WriteLine(extractedText);
```

> **Apa yang Anda lihat:** `ocrResult.Text` sudah berupa string bersih—tidak perlu menghapus baris baru kecuali logika downstream Anda memerlukannya.

## Langkah 5 – Contoh Kerja Lengkap

Menggabungkan semuanya, berikut adalah `Program.cs` lengkap yang dapat Anda salin‑tempel ke proyek Anda. Ia akan dikompilasi dan dijalankan apa adanya (hanya ganti jalur gambar).

```csharp
using Aspose.OCR;
using System.Drawing;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine for offline use
        var ocrEngine = new OcrEngine
        {
            OfflineMode = true,               // Prevent any network calls
            Language = OcrLanguage.English    // Use a locally‑available language pack
        };

        // Step 2: Load the image you want to process
        using var image = Image.Load(@"YOUR_DIRECTORY/offline_test.png");

        // Step 3: Run OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Display the extracted text
        System.Console.WriteLine("\n--- Extracted Text ---");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Output yang Diharapkan

Jika `offline_test.png` berisi kalimat “Hello, world!”, console akan mencetak:

```
--- Extracted Text ---
Hello, world!
```

Untuk dokumen yang lebih panjang Anda akan melihat paragraf lengkap, baris baru, dan tanda baca tetap terjaga sebagaimana mesin OCR menafsirkannya.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

### 1. *Can I recognize text from png files that have a colored background?*  
Ya. Aspose.OCR secara otomatis menerapkan langkah pra‑pemrosesan yang menormalkan kontras. Jika latar belakang terlalu berisik, pertimbangkan mengonversi gambar ke skala abu‑abu terlebih dahulu:

```csharp
image = image.ConvertToGrayscale();
```

### 2. *What if I need to read text from scan PDFs instead of PNG?*  
Ekstrak setiap halaman sebagai gambar (menggunakan perpustakaan PDF seperti Aspose.PDF) dan masukkan gambar‑gambar tersebut ke dalam pipeline OCR yang sama. Alur kerja tetap identik setelah Anda memiliki bitmap.

### 3. *How do I handle low‑confidence results?*  
`OcrResult` menyertakan properti `Confidence` per karakter. Anda dapat mengiterasi `ocrResult.Characters` dan menandai karakter apa pun dengan kepercayaan < 0.75 untuk ditinjau secara manual.

### 4. *Is the English language pack the only one that works offline?*  
Tidak. Paket bahasa apa pun yang Anda instal secara lokal (misalnya, `OcrLanguage.Spanish`) berfungsi dengan cara yang sama—cukup atur `Language = OcrLanguage.Spanish`.

### 5. *Can I batch‑process a folder of images?*  
Tentu saja. Bungkus logika pemuatan dan pengenalan dalam loop `foreach (var file in Directory.GetFiles(folder, "*.png"))`. Ingat untuk membuang setiap gambar setelah diproses.

## Tips Kinerja

- **Gunakan kembali instance `OcrEngine`** untuk beberapa gambar. Membuat mesin baru untuk setiap file menambah beban.
- **Ubah ukuran gambar besar** menjadi maksimum 2000 px pada sisi terpanjang; dimensi yang lebih besar tidak meningkatkan akurasi tetapi memperlambat pemrosesan.
- **Aktifkan multi‑threading** jika Anda memiliki banyak gambar—pastikan setiap thread memiliki `OcrEngine` masing‑masing atau lindungi yang dibagikan dengan lock.

## Gambaran Visual

![Diagram yang menunjukkan alur OCR offline – ekstrak teks dari gambar → muat gambar untuk OCR → kenali teks dari png → output teks](https://example.com/ocr-flow.png "Alur kerja ekstrak teks dari gambar")

*Ilustrasi ini menyoroti empat tahap utama yang dibahas dalam panduan ini.*

## Kesimpulan

Anda sekarang tahu cara **extract text from image** file secara lengkap offline menggunakan Aspose.OCR. Tutorial ini mencakup semua hal mulai dari menyiapkan proyek, mengkonfigurasi mesin untuk mode offline, memuat gambar, dan akhirnya **recognize text from png** serta **read text from scan** dokumen. Dengan kode sumber lengkap di tangan, Anda dapat dengan cepat menyesuaikan solusi untuk **convert image to text** dalam pekerjaan batch, mengintegrasikannya ke utilitas desktop, atau menyematkannya dalam layanan sisi‑server yang harus tetap on‑premises.

Apa selanjutnya? Cobalah mengganti paket bahasa Inggris dengan bahasa lain, bereksperimen dengan pra‑pemrosesan gambar (thresholding, deskew), atau masukkan output OCR ke dalam pipeline bahasa alami untuk analisis sentimen. Langit adalah batasnya ketika Anda menggabungkan OCR offline dengan alat .NET modern.

Selamat coding, dan semoga pemindaian Anda selalu jernih!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}