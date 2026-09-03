---
category: general
date: 2026-01-09
description: Mengenali teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  menonaktifkan unduhan otomatis, mengekstrak gambar teks Cina, dan mengatur bahasa
  OCR.
draft: false
keywords:
- recognize text from image
- disable auto download
- extract text image
- extract chinese text image
- set OCR language
language: id
og_description: Mengenali teks dari gambar menggunakan Aspose OCR di C#. Ikuti tutorial
  langkah demi langkah ini untuk menonaktifkan unduhan otomatis, mengekstrak gambar
  teks berbahasa Mandarin, dan mengatur bahasa OCR.
og_title: Mengenali teks dari gambar dengan Aspose OCR – Panduan Lengkap C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Mengenali teks dari gambar dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar dengan Aspose OCR – Panduan Lengkap C#

Pernah perlu **mengenali teks dari gambar** tetapi terhambat oleh detail konfigurasi? Anda tidak sendirian. Banyak pengembang menemui kendala ketika mesin OCR mencoba mengunduh paket bahasa saat runtime, atau ketika mereka tidak dapat mengekstrak karakter Mandarin dari foto tanda.

Dalam tutorial ini kami akan membimbing Anda melalui solusi praktis yang menunjukkan cara **menonaktifkan unduhan otomatis**, **mengekstrak teks gambar**, **mengekstrak teks gambar Mandarin**, dan **mengatur bahasa OCR**—semua dengan Aspose OCR untuk .NET. Pada akhir tutorial Anda akan memiliki satu program yang dapat dijalankan dan mencetak teks yang dikenali langsung ke konsol.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mereferensikan paket NuGet Aspose.OCR.  
- Mengapa mematikan unduhan sumber daya otomatis penting untuk lingkungan offline atau yang aman.  
- Langkah‑langkah tepat untuk menunjuk mesin ke folder paket bahasa lokal.  
- Cara memilih bahasa yang tepat (Chinese Simplified) sebelum memproses gambar.  
- Memverifikasi output dan memecahkan masalah umum.

Tidak diperlukan pengalaman sebelumnya dengan Aspose; cukup dengan setup C# dasar dan file gambar yang ingin Anda baca.

## Prasyarat

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6.0 atau lebih baru (atau .NET Framework 4.7+) | Aspose.OCR mendukung runtime tersebut. |
| Visual Studio 2022 (atau IDE apa pun yang Anda suka) | Untuk memudahkan pembuatan proyek dan debugging. |
| File gambar yang berisi teks Mandarin (misalnya `chinese‑sign.jpg`) | Untuk mendemonstrasikan **mengekstrak teks gambar Mandarin**. |
| Salinan lokal paket bahasa Aspose OCR (diunduh sekali dari portal Aspose) | Diperlukan karena kami akan **menonaktifkan unduhan otomatis**. |

Pastikan file ZIP paket bahasa berada di folder yang dapat Anda referensikan, misalnya `C:\MyOCR\Resources`.

## Langkah 1: Mengenali teks dari gambar – Konfigurasikan Mesin OCR

Hal pertama yang harus dilakukan: kita memerlukan objek `OcrEngineSettings` yang memberi tahu Aspose di mana mencari sumber daya. Ini adalah fondasi untuk setiap operasi **mengekstrak teks gambar**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 1: Configure OCR engine settings
var ocrSettings = new OcrEngineSettings
{
    // Folder that contains language pack .zip files
    ResourceFolder = @"C:\MyOCR\Resources",

    // Turn off the built‑in downloader – we want total control
    AutoDownloadResources = false
};
```

Mengapa mengatur `AutoDownloadResources` ke `false`? Pada lingkungan produksi Anda sering berada di belakang firewall, atau Anda memang tidak ingin aplikasi mengakses internet saat runtime. Menonaktifkan fitur ini menjamin mesin hanya menggunakan file yang Anda tempatkan di `ResourceFolder`, yang juga mempercepat inisialisasi.

## Langkah 2: Buat mesin OCR dengan pengaturan yang telah ditentukan

Setelah pengaturan siap, kita menginstansiasi mesin. Langkah ini adalah tempat kemampuan **mengatur bahasa OCR** akan berperan nantinya.

```csharp
// Step 2: Create the OCR engine using the settings above
var ocrEngine = new OcrEngine(ocrSettings);
```

Objek `OcrEngine` ringan; ia tidak benar‑benar memuat data bahasa apa pun sampai Anda menetapkan bahasa. Pemuatan malas inilah yang memungkinkan Anda membuat mesin meskipun folder sumber daya kosong—tidak ada yang akan rusak sampai Anda mencoba **mengekstrak teks gambar Mandarin**.

## Langkah 3: Atur bahasa OCR – Pilih Chinese Simplified

Aspose mendukung puluhan bahasa, masing‑masing dikemas dalam file ZIP. Karena gambar contoh kami berisi karakter Mandarin Sederhana, kami secara eksplisit menetapkan bahasa sebelum pengenalan.

```csharp
// Step 3: Select the language for recognition (must be available locally)
ocrEngine.Language = OcrLanguage.ChineseSimplified;
```

Jika Anda melewatkan langkah ini, mesin akan default ke bahasa Inggris dan Anda akan mendapatkan output yang berantakan. Juga, perhatikan bahwa nama bahasa harus cocok dengan nama file ZIP di dalam `ResourceFolder`. Misalnya, `ChineseSimplified.zip` harus ada.

## Langkah 4: Ekstrak teks dari gambar target

Dengan mesin yang telah dikonfigurasi dan bahasa yang telah ditetapkan, akhirnya kita **mengenali teks dari gambar**. Metode ini mengembalikan string biasa yang dapat Anda log, simpan, atau kirim ke sistem lain.

```csharp
// Step 4: Recognize text from the target image
string recognizedText = ocrEngine.RecognizeImage(@"C:\MyOCR\chinese-sign.jpg");

// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Pemanggilan `RecognizeImage` melakukan semua pekerjaan berat: pra‑pemrosesan, segmentasi, pencocokan karakter, dan akhirnya merakit hasil. Jika gambar jelas dan paket bahasa tepat, Anda akan melihat karakter Mandarin tercetak di konsol.

> **Tip:** Jika Anda hanya perlu mengekstrak bagian tertentu dari gambar (misalnya wilayah spesifik), gunakan overload `RecognizeImage(string, Rectangle)` untuk memberikan kotak pemotongan.

## Contoh Program Lengkap

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru. Ia mencakup pernyataan `using`, pengaturan, pemilihan bahasa, dan output akhir. Simpan sebagai `Program.cs`, pulihkan paket NuGet, dan jalankan.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Configure OCR engine – point to local resources
        // ------------------------------------------------------------
        var ocrSettings = new OcrEngineSettings
        {
            ResourceFolder = @"C:\MyOCR\Resources", // <-- your local folder
            AutoDownloadResources = false           // <-- we disable auto download
        };

        // ------------------------------------------------------------
        // 2️⃣ Create the engine with those settings
        // ------------------------------------------------------------
        var ocrEngine = new OcrEngine(ocrSettings);

        // ------------------------------------------------------------
        // 3️⃣ Set OCR language – we want Chinese Simplified
        // ------------------------------------------------------------
        ocrEngine.Language = OcrLanguage.ChineseSimplified;

        // ------------------------------------------------------------
        // 4️⃣ Recognize text from the image (extract Chinese text image)
        // ------------------------------------------------------------
        string imagePath = @"C:\MyOCR\chinese-sign.jpg";
        string recognizedText = ocrEngine.RecognizeImage(imagePath);

        // ------------------------------------------------------------
        // 5️⃣ Show the result (extract text image)
        // ------------------------------------------------------------
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### Output yang Diharapkan

Jika `chinese‑sign.jpg` berisi frasa “欢迎光临”, konsol akan menampilkan sesuatu seperti:

```
=== Recognized Text ===
欢迎光临
```

Pemformatan tepatnya dapat bervariasi tergantung pada kualitas gambar, tetapi karakter harus dapat dibaca.

## Kesalahan Umum & Tips Pro

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| **String kosong dikembalikan** | Paket bahasa tidak ditemukan atau `AutoDownloadResources` masih mencoba mengunduhnya | Verifikasi jalur `ResourceFolder` dan pastikan `ChineseSimplified.zip` ada. |
| **Karakter sampah** | Gambar blur atau kontras rendah | Lakukan pra‑pemrosesan gambar (tingkatkan kontras, binarisasi) sebelum mengirim ke `RecognizeImage`. |
| **Exception: `FileNotFoundException`** | Jalur gambar salah | Gunakan jalur absolut atau letakkan gambar di direktori output proyek dan referensikan dengan `Path.Combine(Directory.GetCurrentDirectory(), "chinese‑sign.jpg")`. |
| **Lag kinerja** | Dimensi gambar terlalu besar | Ubah ukuran gambar ke lebar yang wajar (misalnya 1024 px) sebelum pengenalan. |

**Tip pro:** Simpan paket bahasa dalam folder yang dikontrol versi. Saat Anda memperbarui Aspose.OCR, paket baru mungkin memiliki konvensi penamaan yang berbeda, yang dapat secara diam‑diam mematahkan strategi **menonaktifkan unduhan otomatis** Anda.

## Memperluas Contoh

Setelah Anda dapat **mengenali teks dari gambar**, Anda mungkin ingin:

- **Memproses batch** folder gambar (loop melalui file, panggil `RecognizeImage` setiap kali).  
- **Mengekspor** hasil ke file CSV atau JSON untuk analitik lanjutan.  
- **Menggabungkan** OCR dengan API terjemahan untuk mengubah tanda Mandarin menjadi bahasa Inggris secara langsung.  

Semua skenario ini menggunakan langkah inti yang sama: konfigurasi sekali, atur bahasa, dan panggil `RecognizeImage`. Desain modular menjaga kode tetap bersih dan mudah dipelihara.

## Kesimpulan

Anda baru saja mempelajari cara **mengenali teks dari gambar** menggunakan Aspose OCR dalam C#. Dengan secara eksplisit **menonaktifkan unduhan otomatis**, menunjuk mesin ke folder sumber daya lokal, dan **mengatur bahasa OCR** ke Chinese Simplified, Anda dapat secara andal **mengekstrak teks gambar Mandarin** serta bahasa lain yang Anda sediakan.  

Kode lengkap yang dapat dijalankan di atas menunjukkan alur kerja praktis yang dapat Anda sisipkan ke dalam proyek nyata. Dari sini, coba bereksperimen dengan kualitas gambar yang berbeda, tambahkan penanganan error, atau integrasikan output ke sistem yang lebih besar. Kemungkinannya hampir tak terbatas.

Punya pertanyaan tentang bahasa lain, optimasi performa, atau deployment ke cloud? Silakan tinggalkan komentar—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}