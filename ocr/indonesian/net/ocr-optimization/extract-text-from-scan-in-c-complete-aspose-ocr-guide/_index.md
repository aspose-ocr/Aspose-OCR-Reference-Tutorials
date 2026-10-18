---
category: general
date: 2026-02-19
description: Pelajari cara mengekstrak teks dari gambar hasil pemindaian dengan Aspose
  OCR dan melakukan pra‑pemrosesan gambar untuk OCR guna meningkatkan akurasi. Tutorial
  C# langkah demi langkah.
draft: false
keywords:
- extract text from scan
- preprocess image for ocr
language: id
og_description: Ekstrak teks dari pemindaian dengan cepat. Panduan ini menunjukkan
  cara memproses gambar untuk OCR dan mendapatkan hasil yang dapat diandalkan dengan
  Aspose OCR di C#.
og_title: Ekstrak Teks dari Pemindaian – Tutorial Lengkap C# Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Ekstrak Teks dari Pemindaian di C# – Panduan Lengkap Aspose OCR
url: /id/net/ocr-optimization/extract-text-from-scan-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Scan – Panduan Lengkap Aspose OCR

Pernahkah Anda **mengekstrak teks dari scan** file tetapi terus mendapatkan output yang berantakan? Anda tidak sendirian. Dalam banyak proyek dunia nyata—misalnya digitalisasi faktur atau pengarsipan dokumen lama—mendapatkan teks bersih dari gambar yang dipindai adalah rintangan pertama. Kabar baiknya? Dengan beberapa baris C# dan Aspose OCR Anda dapat mengubah JPEG yang berisik menjadi karakter yang dapat dibaca, dan sedikit pra‑pemrosesan membuat perbedaan antara “meh” dan “wow”.

Dalam tutorial ini kami akan membahas seluruh proses: menyiapkan mesin OCR, **pra‑pemrosesan gambar untuk OCR** guna meningkatkan kualitas, menjalankan pengenalan, dan akhirnya mencetak teks yang diekstrak. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang secara andal mengambil teks dari gambar scan apa pun yang Anda berikan.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

- **.NET 6+** (atau .NET Framework 4.7.2+) terpasang – API berfungsi dengan keduanya.
- Paket NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`) – ini satu‑satunya ketergantungan eksternal.
- Contoh gambar scan (misalnya `skewed_scan.jpg`) yang ditempatkan di folder yang dapat Anda referensikan.
- Editor kode atau IDE – Visual Studio, Rider, atau VS Code semuanya dapat digunakan.

Tidak ada pustaka lain yang diperlukan; opsi pra‑pemrosesan yang akan kami gunakan sudah terintegrasi dalam Aspose OCR.

## Langkah 1: Buat Proyek Konsol Baru

Pertama, buat aplikasi konsol baru agar Anda memiliki sandbox yang bersih.

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Itu saja—proyek Anda kini merujuk ke pustaka OCR. Buka `Program.cs` dan hapus baris `Hello World` default; kami akan menggantinya dengan kode kami sendiri.

## Langkah 2: Inisialisasi Mesin OCR – Inti dari Ekstraksi

Untuk **mengekstrak teks dari scan** Anda memerlukan instance `OcrEngine`. Menetapkan bahasa ke Inggris adalah kasus paling umum, tetapi Aspose mendukung puluhan bahasa jika Anda membutuhkannya.

```csharp
using Aspose.OCR;
using Aspose.OCR.Preprocessing;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine and tell it we’re dealing with English text
        var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };
```

Mengapa kita menginstansiasi mesin terlebih dahulu? Mesin menyimpan semua konfigurasi—bahasa, pra‑pemrosesan, dan cache internal—sehingga membuatnya di awal memastikan setiap panggilan berikutnya menggunakan pengaturan yang sama.

## Langkah 3: Pra‑pemrosesan Gambar untuk OCR – Tingkatkan Akurasi Sebelum Ekstraksi

Scan jarang sempurna. Mereka mungkin terputar, berisik, atau kontras rendah. Aspose OCR menawarkan tiga opsi pra‑pemrosesan yang sangat membantu dan secara dramatis meningkatkan hasil:

- **Deskew** – secara otomatis meluruskan halaman yang berputar.
- **Denoise** – menghaluskan bintik‑bintik dan grain.
- **Contrast** – mencerahkan karakter yang pudar.

```csharp
        // 2️⃣ Turn on preprocessing to clean up the image
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = DeskewAdvanced.Enable(),      // corrects rotation
            Denoise = DenoiseWavelet.Enable(),    // reduces noise
            Contrast = ContrastBoost.Enable()     // enhances contrast
        };
```

Anggap langkah ini sebagai memberi pemindai sedikit sentuhan kilau sebelum Anda menyerahkan foto ke mesin OCR. Melewatkannya seperti mencoba membaca kartu pos yang ternoda—mungkin, tapi menyebalkan.

## Langkah 4: Kenali Teks – Ekstraksi Sebenarnya

Sekarang kami memberikan gambar yang telah dibersihkan ke mesin. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya tempat `skewed_scan.jpg` Anda berada.

```csharp
        // 3️⃣ Run OCR on the preprocessed image
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/skewed_scan.jpg");
```

Metode `RecognizeImage` mengembalikan objek `OcrResult` yang berisi teks mentah, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti.

## Langkah 5: Tampilkan (atau Simpan) Teks yang Diekstrak

Akhirnya, mari lihat apa yang kami dapatkan. Dalam proyek nyata Anda mungkin menuliskannya ke basis data atau file; untuk saat ini kami hanya mencetaknya ke konsol.

```csharp
        // 4️⃣ Output the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Saat Anda menjalankan program (`dotnet run`) Anda akan melihat sesuatu seperti:

```
=== Extracted Text ===
Invoice #12345
Date: 01/02/2026
Total: $1,234.56
Thank you for your business!
```

Jika output terlihat berantakan, periksa kembali bahwa jalur gambar sudah benar dan opsi pra‑pemrosesan diaktifkan. Seringkali rotasi halus atau noise berat menjadi penyebabnya.

![ekstrak teks dari scan contoh](/images/ocr-example.png)

*Alt text: screenshot menunjukkan ekstrak teks dari scan menggunakan Aspose OCR dalam C#*

## Kesalahan Umum dan Cara Menghindarinya

- **Jalur file salah** – Jalur relatif bersifat relatif terhadap root proyek, bukan folder binary. Gunakan jalur absolut jika Anda tidak yakin.
- **Format gambar tidak didukung** – Aspose OCR bekerja dengan JPEG, PNG, BMP, TIFF. Jika Anda memiliki PDF, konversi dulu ke gambar.
- **Data bahasa hilang** – Untuk bahasa selain Inggris, Anda mungkin perlu mengunduh paket bahasa tambahan dari situs Aspose.
- **Pra‑pemrosesan berlebihan** – Menerapkan denoise dan peningkatan kontras pada gambar yang sudah bersih dapat menghilangkan karakter yang pudar. Uji dengan dan tanpa masing‑masing opsi.

Tips pro: Jika Anda hanya membutuhkan deskew (sebagian besar scan hanya berputar), Anda dapat mengabaikan dua opsi lainnya untuk menghemat beberapa milidetik.

## Memperluas Solusi – Bagaimana Jika Saya Membutuhkan Lebih?

### Mengekstrak Teks dari Banyak Scan

Bungkus kode pengenalan dalam loop `foreach` yang mengiterasi semua gambar dalam sebuah folder:

```csharp
string[] files = Directory.GetFiles(@"YOUR_DIRECTORY", "*.jpg");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(result.Text);
}
```

### Mendapatkan Skor Kepercayaan

Jika Anda perlu menyaring hasil dengan kepercayaan rendah:

```csharp
if (ocrResult.Confidence < 0.75)
{
    Console.WriteLine("Warning: Low confidence, consider manual review.");
}
```

### Menggunakan OCR dalam Web API

Ekspose logika ekstraksi melalui endpoint ASP.NET Core. Kode inti tetap sama; cukup injeksikan mesin sebagai layanan singleton.

## Ringkasan

Kami telah membahas semua yang Anda perlukan untuk **mengekstrak teks dari scan** gambar dengan Aspose OCR dalam C#. Mulai dari pembuatan proyek, kami:

1. Menginisialisasi mesin OCR dengan bahasa Inggris.
2. **Pra‑pemrosesan gambar untuk OCR** menggunakan deskew, denoise, dan peningkatan kontras.
3. Menjalankan pengenalan pada contoh JPEG.
4. Mencetak teks bersih ke konsol.

Dengan blok‑blok bangunan ini Anda kini dapat mengintegrasikan OCR ke dalam pemroses faktur, pengarsip dokumen, atau aplikasi apa pun yang perlu mengubah kertas menjadi data yang dapat dicari.

## Apa Selanjutnya?

- Bereksperimen dengan kombinasi pra‑pemrosesan lain (misalnya `Binarize` untuk dokumen hitam‑putih).
- Mencoba bahasa lain atau deteksi multi‑bahasa.
- Menggabungkan output OCR dengan Natural Language Processing untuk mengekstrak bidang kunci secara otomatis.

Jangan ragu meninggalkan komentar jika Anda mengalami kendala atau menemukan trik cerdas. Selamat coding, dan semoga scan Anda selalu jernih!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}