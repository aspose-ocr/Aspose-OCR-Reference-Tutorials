---
category: general
date: 2026-01-13
description: tutorial c# ocr yang menunjukkan cara mengenali teks dari file PNG, mengekstrak
  teks dari gambar, dan menangani teks Rusia menggunakan Aspose.OCR.
draft: false
keywords:
- c# ocr tutorial
- recognize text from png
- how to extract text from image
- recognize russian text
- load image for ocr
language: id
og_description: 'c# ocr tutorial: Pelajari cara mengenali teks dari file PNG, mengekstrak
  teks dari gambar, dan memproses teks Rusia dengan Aspose.OCR.'
og_title: tutorial OCR c# – Mengenali Teks dari Gambar PNG
tags:
- OCR
- C#
- Aspose
title: 'Tutorial OCR C#: Mengenali Teks dari Gambar PNG'
url: /id/net/text-recognition/c-ocr-tutorial-recognize-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Mengenali Teks dari Gambar PNG

Pernah membutuhkan **c# ocr tutorial** yang dapat mengubah faktur yang dipindai menjadi teks yang dapat diedit hanya dalam beberapa baris kode? Anda tidak sendirian. Baik Anda sedang membangun alat otomatisasi penagihan atau hanya mencoba mengambil data dari tangkapan layar, mengenali teks dari gambar PNG adalah titik sakit yang umum. Dalam panduan ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan *cara mengekstrak teks dari gambar*, secara otomatis memuat modul bahasa Cyrillic, dan mencetak hasilnya ke konsol.

> **Hook cepat:** Seluruh solusi berada dalam satu metode `Main`, sehingga Anda dapat menyalin‑tempel, menekan F5, dan melihat karakter Rusia muncul secara instan.

Kami juga akan membahas beberapa skenario “what if”—seperti memuat gambar dari stream atau menangani paket bahasa yang hilang—sehingga Anda akan menyelesaikan tutorial ini dengan pemahaman yang menyeluruh.

## Apa yang Anda Butuhkan

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6.0 atau lebih baru (atau .NET Framework 4.7+) | Aspose.OCR mendukung keduanya, tetapi .NET 6 memberikan perbaikan runtime terbaru. |
| Visual Studio 2022 (atau IDE C# apa pun) | Memudahkan debugging dan manajemen paket NuGet. |
| Koneksi internet (hanya pada run pertama) | Modul bahasa Cyrillic diunduh secara otomatis pada pertama kali Anda meminta bahasa Rusia. |
| Gambar PNG dari faktur Rusia (atau PNG dengan banyak teks) | Kami akan menggunakan `russian_invoice.png` sebagai file demo. |

Jika Anda sudah memiliki proyek, Anda dapat melewati langkah pembuatan. Jika tidak, buka terminal dan jalankan:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Sekarang Anda memiliki proyek konsol bersih yang siap untuk **c# ocr tutorial**.

## Langkah 1: Instal Aspose.OCR via NuGet

Aspose.OCR adalah perpustakaan komersial, tetapi menawarkan percobaan gratis dengan fungsionalitas penuh. Tambahkan ke proyek Anda dengan:

```bash
dotnet add package Aspose.OCR
```

> **Tip pro:** Jika Anda berada di belakang proxy perusahaan, set variabel lingkungan `http_proxy` sebelum menjalankan perintah; jika tidak, pengunduhan paket mungkin gagal.

Paket ini menyertakan `Aspose.OCR.dll`, `Aspose.OCR.Common.dll`, dan sekumpulan kecil file data bahasa. Paket Cyrillic (digunakan untuk Rusia) tidak disertakan—itu diunduh sesuai permintaan, sehingga jejak awal tetap kecil.

## Langkah 2: Muat Gambar untuk OCR

Langkah **load image for ocr** ternyata sangat sederhana. Aspose.OCR mengabstraksi penanganan file di balik kelas `OcrImage`, yang dapat membaca dari jalur file, `Stream`, atau bahkan array byte. Berikut pola yang paling umum:

```csharp
using Aspose.OCR;

// ...

// Step 2: Load the PNG file you want to process.
// Replace the path with the actual location of your invoice image.
string imagePath = Path.Combine(Environment.CurrentDirectory, "russian_invoice.png");

// OcrImage.FromFile automatically detects the format (PNG, JPEG, etc.).
OcrImage invoiceImage = OcrImage.FromFile(imagePath);
```

Jika gambar Anda berada dalam BLOB basis data, Anda dapat mengganti pemanggilan `FromFile` dengan `FromStream(new MemoryStream(blobBytes))`. Perpustakaan akan memperlakukan kedua kasus secara identik.

## Langkah 3: Kenali Teks dari PNG

Sekarang masuk ke inti **c# ocr tutorial**—memanggil mesin OCR. Kelas `OcrEngine` ringan; Anda dapat menggunakan kembali satu instance untuk banyak gambar, atau membuat yang baru per permintaan jika menginginkan isolasi.

```csharp
// Step 3: Create the OCR engine.
using var ocrEngine = new OcrEngine();

// Recognize Russian text; the Cyrillic language pack is fetched automatically.
// If you wanted English, you’d pass OcrLanguage.English instead.
OcrResult ocrResult = ocrEngine.Recognize(invoiceImage, OcrLanguage.Russian);
```

Di balik layar, Aspose memeriksa apakah file data Cyrillic ada secara lokal. Jika tidak, ia mengunduhnya dari CDN Aspose, menyimpannya di folder cache (`%USERPROFILE%\.Aspose\OCR` di Windows), lalu melanjutkan pengenalan. Inilah mengapa run pertama dapat memakan beberapa detik—run selanjutnya instan.

### Bagaimana Jika Unduhan Gagal?

Gangguan jaringan dapat terjadi. Bungkus pemanggilan dalam blok try‑catch dan gunakan bahasa bawaan (mis., Inggris) atau tampilkan pesan error yang ramah:

```csharp
try
{
    OcrResult ocrResult = ocrEngine.Recognize(invoiceImage, OcrLanguage.Russian);
    // Use ocrResult...
}
catch (Aspose.OCR.Exceptions.OcrLicenseException ex)
{
    Console.WriteLine("Language pack download failed: " + ex.Message);
    // Optionally retry or switch language.
}
```

## Langkah 4: Ekstrak dan Tampilkan Hasil

Objek `OcrResult` menyimpan teks mentah, skor kepercayaan, dan bounding box untuk setiap kata. Untuk kebanyakan skenario sederhana, Anda hanya membutuhkan properti `Text`:

```csharp
// Step 4: Output the recognized text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

### Output yang Diharapkan

Jika `russian_invoice.png` berisi baris seperti `Сумма: 1 200,00 ₽`, konsol akan mencetak:

```
=== OCR Output ===
Сумма: 1 200,00 ₽
```

Perhatikan karakter Cyrillic yang benar dan spasi tak terputus yang digunakan dalam jumlah. Aspose.OCR mempertahankan Unicode persis seperti yang muncul di gambar.

## Langkah 5: Contoh Kerja Lengkap

Menggabungkan semuanya, berikut program **lengkap, mandiri** yang dapat Anda letakkan di `Program.cs`. Tanpa referensi eksternal, tanpa langkah tersembunyi.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class AutoDownloadDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance.
        using var ocrEngine = new OcrEngine();

        // 2️⃣ Load the PNG image you want to process.
        //    Update the path to point at your own file.
        string imagePath = Path.Combine(Environment.CurrentDirectory, "russian_invoice.png");
        OcrImage invoiceImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize the text, automatically fetching the Russian (Cyrillic) module.
        OcrResult ocrResult;
        try
        {
            ocrResult = ocrEngine.Recognize(invoiceImage, OcrLanguage.Russian);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"⚠️ OCR failed: {ex.Message}");
            return;
        }

        // 4️⃣ Display the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Jalankan:**  
```bash
dotnet run
```

Anda akan melihat teks Rusia yang diekstrak dicetak ke konsol. Jika paket bahasa belum di-cache, run pertama akan mengunduh file ~2 MB; run selanjutnya hampir instan.

## Variasi Umum & Kasus Tepi

| Skenario | Cara Menyesuaikan |
|----------|-------------------|
| Gambar adalah JPEG bukan PNG | Pemanggilan `OcrImage.FromFile` yang sama berfungsi; perpustakaan otomatis mendeteksi format. |
| Anda perlu memproses banyak gambar dalam batch | Gunakan kembali instance `OcrEngine` yang sama dalam loop `foreach`; hanya pemanggilan `Recognize` yang berubah. |
| Anda hanya menginginkan angka (mis., total faktur) | Setelah OCR, saring `ocrResult.Text` dengan ekspresi reguler seperti `\d[\d\s,]*\d`. |
| Menjalankan di Linux/macOS | Pastikan dependensi `libgdiplus` terpasang (`sudo apt-get install -y libgdiplus`). |
| Keterbatasan memori | Dispose setiap `OcrImage` setelah penggunaan: `invoiceImage.Dispose();` |

## Tips Pro untuk Pengalaman **c# ocr tutorial** yang Lancar

- **Cache paket bahasa secara manual** jika Anda memiliki banyak mesin di belakang firewall. Salin folder `%USERPROFILE%\.Aspose\OCR` ke setiap mesin target.
- **Sesuaikan mesin OCR** dengan mengubah `ocrEngine.Config` (mis., set `PageSegMode = PageSegMode.SingleLine` untuk kwitansi satu baris).
- **Catat kepercayaan**: `ocrResult.Confidence` memberikan skor 0‑1 per kata—gunakan untuk menandai hasil dengan kepercayaan rendah untuk tinjauan manual.
- **Kombinasikan dengan konversi PDF**: Aspose.PDF dapat merender halaman PDF ke PNG, yang kemudian Anda masukkan ke pipeline OCR yang sama.

## Kesimpulan

Anda baru saja menyelesaikan **c# ocr tutorial** yang menunjukkan cara **mengenali teks dari png** file, **cara mengekstrak teks dari gambar**, dan secara khusus **mengenali teks Rusia** menggunakan fitur unduh otomatis Aspose.OCR. Contoh ini memperlihatkan siklus hidup lengkap—dari memuat gambar, memanggil mesin, menangani pengambilan paket bahasa, hingga mencetak hasil.

Dari sini Anda dapat memperluas: mengintegrasikan output OCR ke basis data, mengirimkannya ke model pembelajaran mesin, atau membangun UI yang memungkinkan pengguna mengunggah faktur secara langsung. Blok bangunan sudah ada, jadi cobalah dengan kualitas gambar, bahasa, atau strategi pemrosesan batch yang berbeda.

Jika Anda menemui masalah—apakah itu DLL yang hilang, timeout jaringan saat mengambil modul Cyrillic, atau karakter tak terduga—kembali ke tabel “Variasi Umum & Kasus Tepi”. Dan tentu saja, dokumentasi Aspose (tertaut dalam komentar kode) adalah langkah selanjutnya yang solid untuk kustomisasi lebih dalam.

Selamat coding, semoga hasil OCR Anda selalu jernih!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}