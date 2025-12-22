---
date: 2025-12-22
description: Pelajari cara mengenali teks dari gambar menggunakan Aspose.OCR untuk
  .NET, mengonversi gambar menjadi teks dengan pengaturan pengenalan OCR yang tepat.
linktitle: recognize text from image – Perform OCR on Image from URL
second_title: Aspose.OCR .NET API
title: Mengenali teks dari gambar – Lakukan OCR pada gambar dari URL
url: /id/net/ocr-optimization/perform-ocr-on-image-from-url/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar dari URL dalam Pengenalan Gambar OCR

## Pendahuluan

Dalam ranah Optical Character Recognition (OCR), Aspose.OCR untuk .NET memungkinkan Anda **recognize text from image** dengan presisi, memberi kekuatan kepada pengembang untuk mengekstrak konten dari gambar dengan mudah. Jika Anda ingin mengintegrasikan kemampuan OCR ke dalam aplikasi .NET Anda dan melakukan pengenalan teks dari sumber remote, panduan langkah‑demi‑langkah ini akan memandu Anda melalui proses melakukan OCR pada gambar dari sebuah URL.

## Jawaban Cepat
- **Apa yang dibahas dalam tutorial ini?** Mengenali teks dari gambar yang terletak pada URL publik menggunakan Aspose.OCR untuk .NET.  
- **Kata kunci utama yang ditargetkan?** *recognize text from image*  
- **Apakah saya memerlukan lisensi?** Tersedia versi percobaan, tetapi lisensi komersial diperlukan untuk penggunaan produksi.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Berapa lama implementasinya?** Biasanya kurang dari 10 menit untuk pengaturan dasar.

## Apa itu “recognize text from image”?
Mengenali teks dari gambar berarti mengubah representasi visual karakter menjadi teks yang dapat diedit dan dapat dicari. Proses ini sering disebut **convert image to text** atau **extract text from image**, dan mendukung skenario seperti digitalisasi dokumen, otomatisasi entri data, dan peningkatan aksesibilitas.

## Mengapa menggunakan Aspose.OCR untuk .NET?
- **Akurasi tinggi** dengan dukungan bahasa bawaan.  
- **Pengaturan pengenalan OCR yang halus** (mis., auto‑skew, deteksi area).  
- **API sederhana** yang bekerja dengan .NET Framework dan .NET Core.  
- **Tanpa dependensi eksternal** – semuanya berjalan secara lokal.

## Prasyarat

Sebelum menyelami tutorial, pastikan Anda memiliki prasyarat berikut:

- Aspose.OCR untuk .NET: Pastikan Anda telah mengintegrasikan pustaka Aspose.OCR ke dalam proyek .NET Anda. Anda dapat mengunduhnya dari [halaman rilis](https://releases.aspose.com/ocr/net/).

- Lingkungan Pengembangan: Miliki lingkungan pengembangan .NET yang berfungsi di mesin Anda.

## Impor Namespace

Di proyek .NET Anda, sertakan namespace yang diperlukan untuk mengakses fungsionalitas Aspose.OCR. Tambahkan cuplikan kode berikut ke proyek Anda:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Cara mengenali teks dari gambar menggunakan URL?

### Langkah 1: Siapkan Direktori Dokumen Anda

Mulailah dengan menentukan direktori tempat dokumen Anda disimpan. Ganti `"Your Document Directory"` dengan jalur sebenarnya ke dokumen Anda.

```csharp
string dataDir = "Your Document Directory";
```

### Langkah 2: Dapatkan Gambar untuk Pengenalan

Berikan URL gambar yang ingin Anda lakukan OCR. Pastikan gambar dapat diakses secara publik.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

### Langkah 3: Inisialisasi AsposeOcr

Buat instance dari kelas AsposeOcr untuk mengakses fungsionalitas OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

### Langkah 4: Kenali Gambar

Manfaatkan pustaka Aspose.OCR untuk mengenali teks dari URL gambar yang ditentukan. Sesuaikan pengaturan pengenalan sesuai kebutuhan Anda.

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

### Langkah 5: Cetak Hasil

Tampilkan hasil pengenalan, termasuk teks yang dikenali, area, dan peringatan apa pun.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

### Langkah 6: Jalankan dan Verifikasi

Jalankan aplikasi Anda, dan jika semuanya telah diatur dengan benar, Anda akan melihat proses OCR berhasil dijalankan.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Masalah Umum dan Solusinya

- **Gambar tidak dapat diakses secara publik** – Verifikasi URL berfungsi di browser. Jika gambar memerlukan autentikasi, unduh terlebih dahulu dan gunakan `RecognizeImageFromStream`.
- **Area pengenalan tidak tepat** – Sesuaikan nilai `Rectangle` atau setel `DetectAreas = false` agar mesin mendeteksi secara otomatis.
- **Bahasa tidak dikenali** – Pastikan paket bahasa yang sesuai terpasang atau setel `Language = "eng"` (atau kode ISO lain) dalam `RecognitionSettings`.

## Pertanyaan yang Sering Diajukan

### Q1: Apakah Aspose.OCR cocok untuk menangani banyak bahasa?
A1: Ya, Aspose.OCR mendukung pengenalan teks dalam berbagai bahasa, menjadikannya serbaguna untuk aplikasi internasional.

### Q2: Bisakah saya menggunakan Aspose.OCR untuk pengenalan teks satu baris maupun banyak baris?
A2: Tentu saja! Aspose.OCR menyediakan fleksibilitas untuk mengenali teks satu baris maupun banyak baris, menyesuaikan dengan kasus penggunaan Anda.

### Q3: Apakah ada opsi lisensi yang tersedia untuk Aspose.OCR?
A3: Ya, Anda dapat menjelajahi opsi lisensi dan melakukan pembelian di [Aspose store](https://purchase.aspose.com/buy).

### Q4: Apakah ada percobaan gratis untuk Aspose.OCR?
A4: Ya, Anda dapat mencoba Aspose.OCR secara gratis dengan mengunjungi [halaman rilis](https://releases.aspose.com/).

### Q5: Di mana saya dapat menemukan dukungan atau diskusi komunitas terkait Aspose.OCR?
A5: Kunjungi [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan dan berinteraksi dengan komunitas.

## Kesimpulan

Dengan Aspose.OCR untuk .NET, mengintegrasikan kemampuan OCR ke dalam aplikasi .NET Anda menjadi pengalaman yang mulus. Tutorial ini telah memandu Anda melalui proses **recognize text from image** menggunakan URL, memberikan dasar yang kuat untuk memanfaatkan ekstraksi teks dalam proyek Anda.

---

**Terakhir Diperbarui:** 2025-12-22  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}