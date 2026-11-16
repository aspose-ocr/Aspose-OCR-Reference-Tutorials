---
category: general
date: 2026-03-07
description: Pelajari cara menggunakan OCR di C# untuk mengekstrak teks dari file
  gambar. Panduan ini menunjukkan OCR offline, mengonversi gambar menjadi teks, dan
  memuat gambar untuk OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: id
og_description: Cara menggunakan OCR di C# untuk mengekstrak teks dari gambar secara
  offline. Kode langkah demi langkah, tips, dan penjelasan lengkap untuk mengubah
  gambar menjadi teks.
og_title: Cara Menggunakan OCR di C# – Panduan Offline Lengkap
tags:
- OCR
- C#
- Aspose
title: Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar Secara Offline
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar Secara Offline

Pernah bertanya-tanya **bagaimana cara menggunakan OCR** dalam proyek .NET tanpa mengirim data ke cloud? Anda tidak sendirian. Banyak pengembang perlu *mengekstrak teks dari gambar* pada workstation yang aman, dan mereka khawatir lalu lintas jaringan dapat mengungkap informasi sensitif.  

Kabar baiknya? Dengan Aspose.OCR Anda dapat mengenali teks dari PNG, JPEG, atau PDF sepenuhnya secara offline. Dalam tutorial ini kami akan menuntun Anda memuat gambar untuk OCR, mengonfigurasi mesin untuk mode offline, dan akhirnya **mengonversi gambar menjadi teks** dengan hanya beberapa baris C#.

Pada akhir panduan ini Anda akan dapat:

* Menginstal paket NuGet Aspose.OCR.  
* Menyiapkan mesin OCR untuk pemrosesan offline.  
* Memuat gambar untuk OCR dan mengekstrak konten teksnya.  

Tanpa layanan eksternal, tanpa kunci API—hanya kode C# murni yang berjalan di mesin Windows atau Linux mana pun.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* .NET 6.0 SDK atau yang lebih baru (kode ini juga bekerja dengan .NET Framework 4.7+).  
* Visual Studio 2022, VS Code, atau editor apa pun yang mendukung C#.  
* Salinan pustaka **Aspose.OCR** – Anda dapat mengambilnya dari NuGet (`Aspose.OCR`).  
* Folder sumber daya OCR (`Resources`) yang disertakan bersama pustaka (berisi file data bahasa).  
* Contoh gambar (misalnya `offline_test.png`) yang ditempatkan di direktori yang diketahui.

> **Pro tip:** Simpan folder resources di samping executable Anda; ini mempermudah konfigurasi `ResourcesPath`.

---

## Langkah 1: Instal Paket NuGet Aspose.OCR

Pertama, tambahkan pustaka ke proyek Anda. Buka terminal di folder proyek dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Atau, jika Anda lebih suka UI Visual Studio, klik kanan **Dependencies → Manage NuGet Packages**, cari *Aspose.OCR*, dan klik **Install**.

> Menginstal paket akan menarik semua binary yang diperlukan, sehingga Anda tidak memerlukan DLL tambahan.

---

## Langkah 2: Buat dan Konfigurasikan Mesin OCR (Cara Menggunakan OCR – Mode Offline)

Sekarang kita akan menginstansiasi mesin OCR dan memberitahunya untuk bekerja **offline**. Ini memastikan tidak ada lalu lintas jaringan selama proses pengenalan.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**Mengapa offline?**  
Ketika `EngineMode` diatur ke `Online`, mesin akan menghubungi cloud Aspose untuk mengunduh paket bahasa secara dinamis. Di lingkungan yang diatur (keuangan, kesehatan) lalu lintas tersebut sering dilarang. Dengan memaksa mode offline Anda menjamin semua proses tetap berada di mesin lokal.

---

## Langkah 3: Arahkan Mesin ke Folder Sumber Daya OCR

Mesin OCR membutuhkan data bahasa (model terlatih) untuk mengenali karakter. Beritahu mesin di mana file‑file tersebut berada:

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

Jika Anda tidak yakin di mana foldernya, temukan di direktori paket NuGet (`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`). Salin seluruh folder ke dalam proyek Anda untuk memudahkan penyebaran.

---

## Langkah 4: Muat Gambar untuk OCR (Load Image for OCR)

Anda dapat memberi mesin bitmap apa pun yang didukung. Di sini kami akan memuat PNG yang disimpan di disk:

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**Tip:** Jika Anda perlu memproses gambar dari stream (misalnya diunggah melalui API), gunakan `ImageStream.FromStream(yourStream)` sebagai gantinya.

---

## Langkah 5: Jalankan Proses Pengenalan dan Konversi Gambar ke Teks

Dengan semua hal sudah siap, aktifkan OCR. Metode `Recognize()` melakukan pekerjaan berat, dan teks yang diekstrak tersedia melalui properti `Text`.

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

---

## Langkah 6: Tampilkan Teks yang Diekstrak

Akhirnya, tampilkan hasilnya. Pada aplikasi console Anda cukup menulis ke console, tetapi pada web API Anda dapat mengembalikan string sebagai JSON.

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

Menjalankan program seharusnya mencetak konten teks dari `offline_test.png`. Misalnya, jika gambar berisi frasa *“Hello, World!”*, Anda akan melihat:

```
=== OCR Result ===
Hello, World!
```

---

## Contoh Lengkap yang Siap Dijalan

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke proyek console baru (`dotnet new console`) dan sesuaikan jalur agar cocok dengan lingkungan Anda.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Output yang diharapkan:** Console mencetak teks persis yang terdapat dalam file PNG. Jika gambar buram, hasilnya mungkin mengandung karakter yang salah dikenali—lihat bagian pemecahan masalah di bawah.

---

## Kesulitan Umum & Tips (Mengenali Teks dari PNG Secara Efisien)

| Masalah | Mengapa Terjadi | Cara Memperbaiki |
|---------|-----------------|------------------|
| **Output kosong** | `ResourcesPath` mengarah ke folder yang salah atau file bahasa tidak ada. | Pastikan folder berisi `eng.traineddata` (atau file bahasa lain) dan periksa kembali string path. |
| **Karakter sampah** | Resolusi gambar terlalu rendah atau gambar belum dibinarisasi. | Pralakukan pemrosesan gambar (tingkatkan DPI, terapkan `ImageProcessor` untuk menajamkan). |
| **Lag kinerja** | Gambar besar diproses dengan resolusi penuh. | Ubah ukuran gambar menjadi maksimal lebar 2000 px sebelum diberikan ke OCR. |
| **Format tidak didukung** | Menggunakan BMP dengan format piksel yang tidak biasa. | Konversi gambar ke PNG atau JPEG terlebih dahulu (`System.Drawing.Image.Save`). |

**Pro tip:** Jika Anda perlu mengenali beberapa bahasa, atur `ocrEngine.Settings.Language = Language.English | Language.French;` sebelum memanggil `Recognize()`.

---

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menggunakan kode ini di Linux?**  
Tentu saja. Aspose.OCR bersifat lintas‑platform; cukup pastikan pustaka native tersedia (sudah disertakan dalam paket NuGet).

**T: Bagaimana jika saya tidak memiliki folder Resources?**  
Anda dapat mengunduh paket bahasa gratis dari situs Aspose atau mengekstraknya dari paket NuGet (`.../aspose.ocr/<versi>/resources`).

**T: Apakah ada cara mendapatkan skor kepercayaan?**  
Ya. Setelah `Recognize()`, periksa `ocrEngine.RecognizedWords` – setiap kata memiliki properti `Confidence`.

---

## Kesimpulan

Kami telah membahas **cara menggunakan OCR** di C# untuk *mengekstrak teks dari gambar* secara sepenuhnya offline. Dengan menginstal Aspose.OCR, mengonfigurasi `EngineMode.Offline`, menunjuk ke resources, memuat gambar, dan memanggil `Recognize()`, Anda dapat dengan andal **mengonversi gambar menjadi teks** tanpa pernah menyentuh internet.  

Ambil kode di atas, ganti jalur gambar Anda, dan mulailah membangun fitur seperti PDF yang dapat dicari, otomatisasi entri data, atau alat aksesibilitas. Selanjutnya, Anda bisa menjelajahi **pengenalan teks dari PNG** secara massal, atau mengintegrasikan mesin ke API ASP.NET Core untuk menyajikan hasil OCR ke aplikasi front‑end.

Selamat coding, dan jangan ragu bereksperimen—OCR ternyata cukup toleran setelah mesin disiapkan dengan benar!

--- 

![Diagram yang menunjukkan alur kerja OCR offline – cara menggunakan OCR di lingkungan yang aman](https://example.com/ocr-workflow.png "diagram cara menggunakan OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}