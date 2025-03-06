---
title: Dapatkan Persegi Panjang untuk Garis dalam Pengenalan Gambar OCR
linktitle: Dapatkan Persegi Panjang untuk Garis dalam Pengenalan Gambar OCR
second_title: Aspose.OCR .NET API
description: Jelajahi Aspose.OCR untuk .NET kunci Anda untuk pengenalan gambar OCR yang tepat. Bebaskan kekuatan ekstraksi teks dengan mudah.
weight: 10
url: /id/net/image-and-drawing-recognition/get-rectangles-for-lines/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Persegi Panjang untuk Garis dalam Pengenalan Gambar OCR

## Perkenalan

Selamat datang di dunia Aspose.OCR untuk .NET, alat canggih yang memungkinkan Anda memanfaatkan potensi Pengenalan Karakter Optik (OCR) dalam aplikasi .NET Anda. Baik Anda seorang pengembang berpengalaman atau penggemar yang penasaran, panduan ini akan memandu Anda melalui proses mendapatkan persegi panjang untuk garis dalam pengenalan gambar OCR menggunakan Aspose.OCR.

## Prasyarat

Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:

- Pengetahuan dasar tentang pengembangan C# dan .NET.
- Lingkungan pengembangan terintegrasi (IDE) seperti Visual Studio.
-  Aspose.OCR untuk perpustakaan .NET diinstal. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/ocr/net/).
- Contoh gambar yang berisi teks untuk pengenalan OCR.

## Impor Namespace

Pastikan Anda telah mengimpor namespace yang diperlukan ke proyek Anda. Tambahkan baris berikut ke bagian atas file C# Anda:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Sekarang, mari kita uraikan proses mendapatkan persegi panjang untuk garis dalam pengenalan gambar OCR menjadi langkah-langkah yang mudah diikuti.

## Langkah 1: Siapkan Direktori Dokumen Anda

```csharp
// MantanMulai:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

 Mengganti`"Your Document Directory"` dengan jalur sebenarnya ke direktori dokumen Anda.

## Langkah 2: Inisialisasi Aspose.OCR

```csharp
// MantanMulai:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

 Buat sebuah instance dari`AsposeOcr` kelas untuk mengakses fungsionalitas OCR.

## Langkah 3: Tentukan Jalur Gambar

```csharp
// MantanMulai:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Tentukan jalur lengkap ke gambar tempat Anda ingin melakukan OCR.

## Langkah 4: Kenali Gambar dan Dapatkan Persegi Panjang

```csharp
// MantanMulai:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

 Memanfaatkan`GetRectangles` metode untuk mengambil persegi panjang untuk garis pada gambar yang ditentukan.

## Langkah 5: Hasil Cetak

```csharp
// MantanMulai:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Cetak koordinat area yang terdeteksi ke konsol.

## Kesimpulan

Selamat! Anda telah berhasil memperoleh persegi panjang untuk garis dalam pengenalan gambar OCR menggunakan Aspose.OCR untuk .NET. Alat serbaguna ini membuka banyak kemungkinan untuk ekstraksi teks di aplikasi Anda.

## FAQ

### Q1: Dapatkah saya menggunakan Aspose.OCR untuk .NET dengan jenis gambar apa pun?

A1: Aspose.OCR mendukung berbagai format gambar, memastikan fleksibilitas dalam aplikasi OCR Anda.

### Q2: Seberapa akurat pengenalan OCR?

A2: Aspose.OCR memanfaatkan algoritme canggih untuk akurasi tinggi, sehingga cocok untuk berbagai skenario pengenalan teks.

### Q3: Apakah ada versi uji coba yang tersedia?

 A3: Ya, Anda dapat menjelajahi kemampuan Aspose.OCR untuk .NET dengan[uji coba gratis](https://releases.aspose.com/).

### Q4: Di mana saya dapat menemukan dokumentasi lengkap?

 A4: Lihat[dokumentasi](https://reference.aspose.com/ocr/net/) untuk informasi rinci dan pedoman penggunaan.

### Q5: Butuh bantuan atau punya pertanyaan spesifik?

 A5: Kunjungi[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan dan diskusi komunitas.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
