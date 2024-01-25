---
title: Lakukan OCR pada Gambar dari URL dalam Pengenalan Gambar OCR
linktitle: Lakukan OCR pada Gambar dari URL dalam Pengenalan Gambar OCR
second_title: Aspose.OCR .NET API
description: Jelajahi integrasi OCR yang lancar dengan Aspose.OCR untuk .NET. Kenali teks dari gambar dengan presisi.
type: docs
weight: 10
url: /id/net/ocr-optimization/perform-ocr-on-image-from-url/
---
## Perkenalan

Di bidang Pengenalan Karakter Optik (OCR), Aspose.OCR untuk .NET menonjol sebagai alat canggih yang memberdayakan pengembang untuk mengekstrak konten teks dari gambar dengan presisi. Jika Anda ingin mengintegrasikan kemampuan OCR ke dalam aplikasi .NET dan melakukan pengenalan teks dengan mudah, panduan langkah demi langkah ini akan memandu Anda melalui proses melakukan OCR pada gambar dari URL.

## Prasyarat

Sebelum mempelajari tutorialnya, pastikan Anda memiliki prasyarat berikut:

-  Aspose.OCR untuk .NET: Pastikan Anda memiliki perpustakaan Aspose.OCR yang terintegrasi ke dalam proyek .NET Anda. Anda dapat mengunduhnya dari[halaman rilis](https://releases.aspose.com/ocr/net/).

- Lingkungan Pengembangan: Siapkan lingkungan pengembangan .NET yang berfungsi di mesin Anda.

## Impor Namespace

Dalam proyek .NET Anda, sertakan namespace yang diperlukan untuk mengakses fungsionalitas Aspose.OCR. Tambahkan cuplikan kode berikut ke proyek Anda:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Langkah 1: Siapkan Direktori Dokumen Anda

 Mulailah dengan menentukan direktori tempat dokumen Anda disimpan. Mengganti`"Your Document Directory"` dengan jalur sebenarnya ke dokumen Anda.

```csharp
string dataDir = "Your Document Directory";
```

## Langkah 2: Dapatkan Gambar untuk Pengakuan

Berikan URL gambar yang ingin Anda lakukan OCR. Pastikan gambar dapat diakses publik.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

## Langkah 3: Inisialisasi AsposeOcr

Buat instance kelas AsposeOcr untuk mengakses fungsionalitas OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

## Langkah 4: Kenali Gambar

Manfaatkan perpustakaan Aspose.OCR untuk mengenali teks dari URL gambar yang ditentukan. Sesuaikan pengaturan pengenalan berdasarkan kebutuhan Anda.

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

## Langkah 5: Hasil Cetak

Menampilkan hasil pengenalan, termasuk teks yang dikenali, area, dan peringatan apa pun.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

## Langkah 6: Jalankan dan Verifikasi

Jalankan aplikasi Anda, dan jika semuanya sudah diatur dengan benar, Anda akan melihat proses OCR dijalankan dengan sukses.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Kesimpulan

Dengan Aspose.OCR untuk .NET, mengintegrasikan kemampuan OCR ke dalam aplikasi .NET Anda menjadi pengalaman yang lancar. Tutorial ini telah memandu Anda melalui proses melakukan OCR pada gambar dari URL, memberi Anda landasan untuk memanfaatkan kekuatan pengenalan teks dalam proyek Anda.

## FAQ

### Q1: Apakah Aspose.OCR cocok untuk menangani berbagai bahasa?

A1: Ya, Aspose.OCR mendukung pengenalan teks dalam berbagai bahasa, menjadikannya serbaguna untuk aplikasi internasional.

### Q2: Dapatkah saya menggunakan Aspose.OCR untuk pengenalan teks satu baris dan multi-baris?

A2: Tentu saja! Aspose.OCR memberikan fleksibilitas untuk mengenali teks satu baris dan banyak baris, beradaptasi dengan kasus penggunaan spesifik Anda.

### Q3: Apakah ada opsi lisensi yang tersedia untuk Aspose.OCR?

 A3: Ya, Anda dapat menjelajahi opsi lisensi dan melakukan pembelian di[Asumsikan toko](https://purchase.aspose.com/buy).

### Q4: Apakah ada uji coba gratis yang tersedia untuk Aspose.OCR?

 A4: Ya, Anda dapat mencoba Aspose.OCR secara gratis dengan mengunjungi[halaman rilis](https://releases.aspose.com/).

### Q5: Di mana saya dapat menemukan dukungan atau diskusi komunitas terkait Aspose.OCR?

 A5: Kunjungi[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan dan keterlibatan dengan komunitas.